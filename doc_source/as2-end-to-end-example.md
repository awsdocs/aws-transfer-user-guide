# Enable your server endpoint for AS2<a name="as2-end-to-end-example"></a>

This topic walks through how to set up an Applicability Statement 2 \(AS2\) configuration with AWS Transfer Family\. After you complete the steps described here, you will have an AS2\-enabled server that's ready for accepting AS2 messages from a sample trading partner, and a connector that can be used to send AS2 messages to the sample trading partner\.

1. Create certificates for yourself and your trading partner\. You can skip this section if you have existing certificates that you can use\.

   This process is described in [Step 1: Create certificates for AS2](#as2-create-certs)\.

1. Create an AWS Transfer Family server that uses the AS2 protocol\. Optionally, you can add an Elastic IP address to the server to make it internet\-facing\.

   This process is described in [Step 2: Create a Transfer Family server that uses the AS2 protocol](#as2-example-server)\.

1. Import the certificates that you created in step 1\.

   This process is described in [Step 3: Import certificates as Transfer Family certificate resources](#as2-import-certs-example)\.

1. Create a local profile and a partner profile to set up your trading partners\.

   This process is described in [Step 4: Create profiles for you and your trading partner](#as2-create-profiles-example)\.

1. Create an agreement between you and your trading partner\.

   This process is described in [Step 5: Create an agreement between you and your partner](#as2-create-agreement-example)\.

1. Create a connector between you and your trading partner\.

   This process is described in [Step 6: Create a connector between you and your partner](#as2-create-connector-example)\.

1. Test an AS2 file exchange\.

   This process is described in [Step 7: Test exchanging files over AS2 by using Transfer Family](#as2-test-config)\.

After you complete these steps, you can do the following: 
+ Send files to a remote AS2\-enabled partner server with the Transfer Family `start-file-transfer` AWS Command Line Interface \(AWS CLI\) command\.
+ Receive files from a remote AS2\-enabled partner server on port 5080 through your virtual private cloud \(VPC\) endpoint\.



## Step 1: Create certificates for AS2<a name="as2-create-certs"></a>

Both parties in an AS2 exchange need X\.509 certificates\. You can create these certificates in any way that you like\. This topic describes how to use [OpenSSL](https://www.openssl.org/) from the command line to create a root certificate, and then sign subordinate certificates\. Both parties must generate their own certificates\. 

To transfer files with a partner, take note of the following:
+ You can attach certificates to profiles\. The certificates contain public or private keys\.
+ Your trading partner sends you their public keys, and you send them yours\.
+ Your trading partner encrypts messages with your public key and signs them with their private key\. Conversely, you encrypt messages with your partner's public key and sign them with your private key\.
**Note**  
If you prefer to manage keys with a GUI, [Portecle](http://portecle.sourceforge.net/) is one option that you can use\.

**To generate example certificates**
**Important**  
**Do not send your partner your private keys\.** In this example, you generate a set of self\-signed public and private keys for one party\. If you are going to act as both trading partners for testing purposes, you can repeat these instructions to generate two sets of keys: one for each trading partner\. In this case, you do not need to generate two root certificate authorities \(CAs\)\.

1. Run the following command to generate an RSA private key with a 2048\-bit\-long modulus\.

   ```
   /usr/bin/openssl genrsa -out root-ca-key.pem 2048
   ```

1. Run the following command to create a self\-signed certificate with your `root-ca-key.pem` file\.

   ```
   /usr/bin/openssl req \
   -x509 -new -nodes -sha256 \
   -days 1825 \
   -subj "/C=US/ST=MA/L=Boston/O=TransferFamilyCustomer/OU=IT-dept/CN=ROOTCA" \
   -key root-ca-key.pem \
   -out root-ca.pem
   ```

   The `-subj` argument consists of the following values\.

     
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transfer/latest/userguide/as2-end-to-end-example.html)

1. Create a signing key and an encryption key for your local profile\.

   ```
   /usr/bin/openssl genrsa -out signing-key.pem 2048
   /usr/bin/openssl genrsa -out encryption-key.pem 2048
   ```
**Note**  
Some AS2\-enabled servers, such as OpenAS2, require that you use the same certificate for both signing and encryption\. In this case, you can import the same private key and certificate for both purposes\. To do so, run this command instead of the two previous commands:  

   ```
   /usr/bin/openssl genrsa -out signing-and-encryption-key.pem 2048
   ```

1. Run the following commands to create Certificate Signing Requests \(CSRs\) for the root key to sign\.

   ```
   /usr/bin/openssl req -new -key signing-key.pem -subj \
   "/C=US/ST=MA/L=Boston/O=TransferFamilyCustomer/OU=IT-dept/CN=Signer" -out signing-key-csr.pem
   ```

   ```
   /usr/bin/openssl req -new -key encryption-key.pem -subj \
   "/C=US/ST=MA/L=Boston/O=TransferFamilyCustomer/OU=IT-dept/CN=Encrypter" -out encryption-key-csr.pem
   ```

1. Next, you must create a `signing-cert.conf` file and an `encryption-cert.conf` file\.
   + Use a text editor to create the `signing-cert.conf` file with the following contents:

     ```
     authorityKeyIdentifier=keyid,issuer
     keyUsage = digitalSignature, nonRepudiation
     ```
   + Use a text editor to create the `encryption-cert.conf` file with the following contents:

     ```
     authorityKeyIdentifier=keyid,issuer
     keyUsage = dataEncipherment
     ```

1. Finally, you create the signed certificates by running the following commands\.

   ```
   /usr/bin/openssl x509 -req -sha256 -CAcreateserial -days 1825 -in signing-key-csr.pem -out signing-cert.pem -CA \
   root-ca.pem -CAkey root-ca-key.pem -extfile signing-cert.conf
   ```

   ```
   /usr/bin/openssl x509 -req -sha256 -CAcreateserial -days 1825 -in encryption-key-csr.pem -out encryption-cert.pem \
   -CA root-ca.pem -CAkey root-ca-key.pem -extfile encryption-cert.conf
   ```

## Step 2: Create a Transfer Family server that uses the AS2 protocol<a name="as2-example-server"></a>

This procedure explains how to create an AS2\-enabled server by using the Transfer Family AWS CLI\. If you want to use the console instead, see [Create an AS2\-enabled server](create-b2b-server.md#create-server-as2)\.

Similar to how you create an SFTP or FTPS AWS Transfer Family server, you create an AS2\-enabled server by using the `--protocols AS2` parameter of the `create-server` AWS CLI command\. Currently, Transfer Family supports only VPC endpoint types and Amazon S3 storage with the AS2 protocol\. 

When you create your AS2\-enabled server for Transfer Family by using the `create-server` command, a VPC endpoint is automatically created for you\. This endpoint exposes TCP port 5080 so that it can accept AS2 messages\. 

If you want to expose your VPC endpoint publicly to the internet, you can associate Elastic IP addresses with your VPC endpoint\. 

To use these instructions, you need the following:
+ The ID of your VPC \(for example, **vpc\-abcdef01**\)\.
+ The IDs of your VPC subnets \(for example, **subnet\-abcdef01**, **subnet\-subnet\-abcdef01**, **subnet\-021345ab**\)\.
+ One or more IDs of the security groups that allow incoming traffic on TCP port 5080 from your trading partners \(for example, **sg\-1234567890abcdef0** and **sg\-abcdef01234567890**\)\.
+ \(Optional\) The Elastic IP addresses that you want to associate with your VPC endpoint\. 
+ If your trading partner is not connected to your VPC through a VPN, you need an internet gateway\. For more information, see [Connect to the internet using an internet gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) in the *Amazon VPC User Guide*\.

**Create an AS2\-enabled server**

1. Run the following command\. Replace each `user input placeholder` with your own information\.

   ```
   aws transfer create-server --endpoint-type VPC \
   --endpoint-details VpcId=vpc-abcdef01,SubnetIds=subnet-abcdef01,subnet-abcdef01,subnet-
   021345ab,SecurityGroupIds=sg-abcdef01234567890,sg-1234567890abcdef0 --protocols AS2 \
   --protocol-details As2Transports=HTTP
   ```

1. \(Optional\) You can make the VPC endpoint public\. You can attach Elastic IP addresses to a Transfer Family server only through an `update-server` operation\. The following commands stop the server, update it with Elastic IP addresses, and then start it again\.

   ```
   aws transfer stop-server --server-id your-server-id
   ```

   ```
   aws transfer update-server --server-id your-server-id --endpoint-details \
   AddressAllocationIds=eipalloc-abcdef01234567890,eipalloc-1234567890abcdef0,eipalloc-abcd012345ccccccc
   ```

   ```
   aws transfer start-server --server-id your-server-id
   ```

   This `start-server` command automatically creates a DNS record for you that contains the public IP address for your server\. To give your trading partner access to the server, you provide them with the following information\. In this case, `your-region` refers to your AWS Region\. 

   `s-your-server-id.server.transfer.your-region.amazonaws.com`

   The full URL that you provide to your trading partner is as follows: 

   `http://s-your-server-id.server.transfer.your-region.amazonaws.com:5080`

1. Use the following commands to test whether your AS2\-enabled server is accessible, either through your VPC endpoint's private DNS address, or through your public endpoint \(if you associated an Elastic IP address to your endpoint\)\. 

   If your server is configured correctly, the connection will succeed, but you will receive an HTTP status code 400 \(Bad Request\) response because you aren't sending a valid AS2 message\.
   + For a public endpoint \(if you associated an Elastic IP address in the previous step\), run the following command, substituting your server ID and Region\.

     ```
     curl -vv -X POST http://s-your-server-id.transfer.your-region.amazonaws.com:5080
     ```
   + If you are connecting within your VPC, look up your VPC endpoint's private DNS name by running the following commands\.

     ```
     aws transfer describe-server --server-id s-your-server-id
     ```

     This `describe-server` command returns your VPC endpoint ID in the `VpcEndpointId` parameter\. Use this value to run the following command\.

     ```
     aws ec2 describe-vpc-endpoints --vpc-endpoint-ids vpce-your-vpc-endpoint-id
     ```

     This `describe-vpc-endpoints` command returns a `DNSEntries` array, with several `DnsName` parameters\. Use the Regional DNS name \(the one that does not include the Availability Zone\) in the following command\.

     ```
     curl -vv -X POST http://vpce-your-vpce.vpce-svc-your-vpce-svc.your-region.vpce.amazonaws.com:5080
     ```

     For example, the following command shows sample values for the placeholders in the previous command\.

     ```
     curl -vv -X POST http://vpce-0123456789abcdefg-fghij123.vpce-svc-11111aaaa2222bbbb.us-east-1.vpce.amazonaws.com:5080
     ```

1. \(Optional\) Configure a logging role\. Transfer Family logs the status of messages sent and received in a structured JSON format to Amazon CloudWatch logs\. To provide Transfer Family with access to the CloudWatch logs in your account, you must configure a logging role on your server\. 

   Create an AWS Identity and Access Management \(IAM\) role that trusts `transfer.amazonaws.com`, and attach the `AWSTransferLoggingAccess` managed policy\. For details, see [Create an IAM role and policy](requirements-roles.md)\. Note the Amazon Resource Name \(ARN\) of the IAM role that you just created, and associate it with the server by running the following `update-server` command:

   ```
   aws transfer update-server --server-id your-server-id --logging-role arn:aws:iam::your-account-id:role/logging-role-name
   ```
**Note**  
Even though the logging role is optional, we highly recommend setting it up so that you can see the status of your messages and troubleshoot configuration issues\.

## Step 3: Import certificates as Transfer Family certificate resources<a name="as2-import-certs-example"></a>

This procedure explains how to import certificates by using the AWS CLI\. If you want to use the Transfer Family console instead, see [Import AS2 certificates](create-b2b-server.md#configure-as2-certificate)\.

To import the signing and encryption certificates that you created in step 1, run the following `import-certificate` commands\. If you're using the same certificate for encryption and signing, import the same certificate twice \(once with the `SIGNING` usage and again with the `ENCRYPTION` usage\)\.

```
aws transfer import-certificate --usage SIGNING --certificate file://signing-cert.pem \
            --private-key file://signing-key.pem --certificate-chain file://root-ca.pem
```

This command returns your signing `CertificateId`\. In the next section, this certificate ID is referred to as `my-signing-cert-id`\.

```
aws transfer import-certificate --usage ENCRYPTION --certificate file://encryption-cert.pem \
            --private-key file://encryption-key.pem --certificate-chain file://root-ca.pem
```

This command returns your encryption `CertificateId`\. In the next section, this certificate ID is referred to as `my-encrypt-cert-id`\.

Next, import your partner's encryption and signing certificates by running the following commands\.

```
aws transfer import-certificate --usage ENCRYPTION --certificate file://partner-encryption-cert.pem \
--certificate-chain file://partner-root-ca.pem
```

This command returns your partner's encryption `CertificateId`\. In the next section, this certificate ID is referred to as `partner-encrypt-cert-id`\.

```
aws transfer import-certificate --usage SIGNING --certificate file://partner-signing-cert.pem \
--certificate-chain file://partner-root-ca.pem
```

This command returns your partner's signing `CertificateId`\. In the next section, this certificate ID is referred to as `partner-signing-cert-id`\.

## Step 4: Create profiles for you and your trading partner<a name="as2-create-profiles-example"></a>

This procedure explains how to create AS2 profiles by using AWS CLI\. If you want to use the Transfer Family console instead, see [Create AS2 profiles](create-b2b-server.md#configure-as2-profile)\.

Create your local AS2 profile by running the following command\. This command references the certificates that contain your public and private keys\.

```
aws transfer create-profile --as2-id MYCORP --profile-type LOCAL --certificate-ids \
my-signing-cert-id my-encrypt-cert-id
```

This command returns your profile ID\. In the next section, this ID is referred to as `my-profile-id`\.

Now create the partner profile by running the following command\. This command uses only your partner's public key certificates\. To use this command, replace the `user input placeholders` with your own information; for example, your partner's AS2 name and certificate IDs\.

```
aws transfer create-profile --as2-id PARTNER-COMPANY --profile-type PARTNER --certificate-ids \
partner-signing-cert-id partner-encrypt-cert-id
```

This command returns your partner's profile ID\. In the next section, this ID is referred to as `partner-profile-id`\.

**Note**  
In the previous commands, replace *MYCORP* with the name of your organization, and *PARTNER\-COMPANY* with the name of your trading partner's organization\.

## Step 5: Create an agreement between you and your partner<a name="as2-create-agreement-example"></a>

This procedure explains how to create AS2 agreements by using the AWS CLI\. If you want to use the Transfer Family console instead, see [Create AS2 agreements](create-b2b-server.md#as2-agreements)\.

Agreements bring together the two profiles \(local and partner\), their certificates, and a server configuration that allows inbound AS2 transfers between two parties\. You can list your items by running the following commands\.

```
aws transfer list-profiles --profile-type LOCAL
aws transfer list-profiles --profile-type PARTNER
aws transfer list-servers
```

This step requires an Amazon S3 bucket and IAM role with read/write access to and from the bucket\. The instructions for creating this role are the same as for the Transfer Family SFTP, FTP, and FTPS protocols and are available in [Create an IAM role and policy](requirements-roles.md)\. 

To create an agreement, you need the following items:
+ The Amazon S3 bucket name \(and object prefix, if specified\)
+ The ARN of the IAM role with access to the bucket
+ Your Transfer Family server ID
+ Your profile ID and your partner's profile ID

Create the agreement by running the following command\.

```
aws transfer create-agreement --description "ExampleAgreementName" --server-id your-server-id \
--local-profile-id your-profile-id --partner-profile-id your-partner-profile-id --base-directory /DOC-EXAMPLE-BUCKET/AS2-inbox \
--access-role arn:aws:iam::111111111111:role/TransferAS2AccessRole
```

If successful, this command returns the ID for the agreement\. You can then view the details of the agreement with the following command\.

```
aws transfer describe-agreement --agreement-id agreement-id --server-id your-server-id
```

## Step 6: Create a connector between you and your partner<a name="as2-create-connector-example"></a>

This procedure explains how to create AS2 connectors by using the AWS CLI\. If you want to use the Transfer Family console instead, see [Create AS2 connectors](create-b2b-server.md#configure-as2-connector)\.

You can use the `StartFileTransfer` API operation to send files that are stored in Amazon S3 to your trading partner's AS2 endpoint by using a connector\. You can find the profiles that you created earlier by running the following command\.

```
aws transfer list-profiles
```

When you create the connector, you must provide your partner's AS2 server URL\. Copy the following text to a file named `testAS2Config.json`\.

```
{
"LocalProfileId": "your-profile-id",
"PartnerProfileId": "partner-profile-id",
"MdnResponse": "SYNC",
"Compression": "ZLIB",
"EncryptionAlgorithm": "AES256_CBC",
"SigningAlgorithm": "SHA256",
"MdnSigningAlgorithm": "DEFAULT",
"MessageSubject": "Your Message Subject"
}
```

Then run the following command to create the connector\.

```
aws transfer create-connector --url "http://partner-as2-server-url" \
--access-role your-IAM-role-for-bucket-access \
--logging-role arn:aws:iam::your-account-id:role/service-role/AWSTransferLoggingAccess \
--as2-config file:///path/to/testAs2Config.json
```

## Step 7: Test exchanging files over AS2 by using Transfer Family<a name="as2-test-config"></a>

### Receive a file from your trading partner<a name="as2-receive-file"></a>

If you associated a public Elastic IP address with your VPC endpoint, Transfer Family automatically created a DNS name that contains your public IP address\. The subdomain is your AWS Transfer Family server ID \(of the format `s-1234567890abcdef0`\)\. Provide your server URL to your trading partner in the following format\.

```
http://s-1234567890abcdef0.transfer.us-east-1.amazonaws.com:5080
```

If you didn't associate a public Elastic IP address with your VPC endpoint, look up the hostname of the VPC endpoint that can accept AS2 messages over HTTP POST from your trading partners on port 5080\. To retrieve the VPC endpoint details, use the following command\.

```
aws transfer describe-server --server-id s-1234567890abcdef0
```

For example, assume the preceding command returns a VPC endpoint ID of `vpce-1234abcd5678efghi`\. Then, you would use the following command to retrieve the DNS names\.

```
aws ec2 describe-vpc-endpoints --vpc-endpoint-ids vpce-1234abcd5678efghi
```

This command returns all the details for the VPC endpoint that you need to run the following command\.

The DNS name is listed in the `DnsEntries` array\. Your trading partner must be within your VPC to access your VPC endpoint \(for example through AWS PrivateLink or a VPN\)\. Provide your VPC endpoint URL to your partner in the following format\.

```
http://vpce-your-vpce-id.vpce-svc-your-vpce-svc-id.your-region.vpce.amazonaws.com:5080
```

For example, the following URL shows sample values for the placeholders in the previous commands\.

```
http://vpce-0123456789abcdefg-fghij123.vpce-svc-11111aaaa2222bbbb.us-east-1.vpce.amazonaws.com:5080 
```

### Send a file to your trading partner<a name="as2-send-file"></a>

You can use Transfer Family to send files by referencing the connector ID and the paths to the files in the following command\.

```
aws transfer start-file-transfer --connector-id c-1234567890abcdef0 \
--send-file-paths "DOC-EXAMPLE-BUCKET/myfile1" "DOC-EXAMPLE-BUCKET/myfile2"
```

**Note**  
To find details for your connectors, run the command `aws transfer list-connectors`\. This command returns the connector ID, URL, and ARN for your connectors\. Then, you can run the command `aws transfer describe-connector --connector-id your-connector-id`, with the ID that you want to use\. This command returns all of the details for `your-connector-id`\.

Successful transfers are stored at the location specified in the `SendFilePaths` parameter of the `StartFileTransferRequest` API operation\. For example, if you ran the previous command, files are transferred to `DOC-EXAMPLE-BUCKET/myfile1` and `DOC-EXAMPLE-BUCKET/myfile2`\. If you configured a logging role when you created the connector, you can also check your CloudWatch logs for the status of the AS2 message\.
# AS2 configurations, limits, and error messages<a name="as2-config-etc"></a>

This section describes the supported configurations for transfers that use the Applicability Statement 2 \(AS2\) protocol, including the accepted ciphers and digests\. This section also describes the limits and known issues for AS2 transfers\. The various error codes that you might receive from AS2 file transfers are also provided\. 

## AS2 supported configurations<a name="as2-supported-configurations"></a>

**Signing, encryption, compression, MDN**

For both inbound and outbound transfers, the following items are either required or optional:
+ **Encryption** – Required \(for HTTP transport, which is the only transport method currently supported\)
+ **Signing** – Optional
+ **Compression** – Optional \(the only currently supported compression algorithm is ZLIB\)
+ **Message Disposition Notice \(MDN\)** – Optional

**Ciphers**

The following ciphers are supported:
+ **Inbound transfers** – AES128\_CBC, AES192\_CBC, AES256\_CBC, 3DES \(for backward compatibility only\)
+ **Outbound transfers** – AES128\_CBC, AES192\_CBC, AES256\_CBC

**Digests**

The following digests are supported:
+ **Inbound signing and MDN** – SHA1, SHA256, SHA384, SHA512
+ **Outbound signing and MDN** – SHA1, SHA256, SHA384, SHA512

**MDN**

For MDN responses, certain types are supported, as follows: 
+ **Inbound transfers** – Synchronous and asynchronous
+ **Outbound transfers** – Synchronous only
+ **Simple Mail Transfer Protocol \(SMTP\) \(email MDN\)** – Not supported

**Transports**
+ **Inbound transfers** – HTTP is the only currently supported transport, and you must specify it explicitly\.
**Note**  
If you need to use HTTPS for inbound transfers, you can terminate TLS on an Application Load Balancer or a Network Load Balancer\. For more information, see [TlsSessionResumptionMode](https://docs.aws.amazon.com/transfer/latest/userguide/API_ProtocolDetails.html#TransferFamily-Type-ProtocolDetails-TlsSessionResumptionMode)\.
+ **Outbound transfers** – If you use HTTP, you must also specify an encryption algorithm\. If you specify HTTPS, you should specify **NONE** for your encryption algorithm\.

## Set the AS2 endpoint to port 443 \(HTTPS\)<a name="as2-https-inbound"></a>

 AWS Transfer Family AS2 servers currently only provide HTTP transport over port 5080\. However, you can terminate TLS on a load balancer in front of your Transfer Family server VPC endpoint using a port and certificate of your choosing\. This allows you to have incoming AS2 messages use HTTPS\.

**Prerequisites**
+ The VPC must be in the same AWS Region as your Transfer Family server\.
+ The subnets of your VPC need to be within Availability Zones in which you want to use your server\.
**Note**  
Each Transfer Family server can support up to three Availability Zones\.
+ Allocate up to three Elastic IP addresses in the same region as your server\. Or, you can choose to bring your own IP address range \(BYOIP\)\.
**Note**  
The number of Elastic IP addresses must match the number of Availability Zones that you use with your server endpoints\.

**Configure your Network Load Balancer**

Set up an internet\-facing network load balancer \(NLB\) in your VPC\. <a name="create-nlb-AS2"></a>

**Create a Network Load Balancer and define the VPC endpoint of the server as the load balancer's target**

1. Open the Amazon Elastic Compute Cloud console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation pane, choose **Load Balancers** and then choose **Create Load Balancer**\.

1. Under **Network Load Balancer**, choose **Create**\.

1. In the **Basic configuration** section, enter the following information:
   + For **Name**, enter a descriptive name for the load balancer\.
   + For **Scheme**, select **internet\-facing**\.
   + For the **IPv4 address** of each subnet, select one of the Elastic IP addresses that you allocated\.

1. In the **Network mapping** section, enter the following information:
   + For **VPC**, select the Amazon VPC that you created\.
   + Under **Mappings**, select the Availability Zones associated with the public subnets that are available in the same VPC you use with your server endpoints\.
   + For the **IPv4 address** of each subnet, select one of the Elastic IP addresses that you allocated\.

1. In the **Listeners and routing** section, enter the following information:
   + For **Protocol**, select **TLS**\.
   + For **Port**, enter **5080**\.
   + For **Default action**, select **Create target group**\. For the details to create a new target group, see [Create a target group](#create-target-group)\.

   After you create a target group, enter its name into the **Default action** field\.

1. In the **Secure listener settings** section, select your certificate in the **Default SSL/TLS certificate** area\.

1. Select **Create load balancer** to create your NLB\.

1. Optionally, turn on access logs for the Network Load balancer to maintain a full audit trail, as described in [Access logs for your Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-access-logs.html)\.

   We recommend this step because the TLS connection is terminated at the NLB, so the source IP address reflected in your Transfer Family AS2 CloudWatch log groups is the NLB's private IP address, rather than your trading partner's external IP address\.

After you set up the load balancer, clients communicate to the load balancer over the custom port listener\. Then, the load balancer communicates to the server over port 5080\.

**Create a target group**<a name="create-target-group"></a>

**Create a target group**

1. After you select **Create target group** in the previous procedure, you are taken to the **Specify group details** for a new target group\.

1.  In the **Basic configuration** section, enter the following information\.
   + For **Choose a target type**, select **IP addresses**\.
   + For **Target group name**, enter a name for the target group\.
   + For **Protocol**, select **TLS**\. 
   + For **Port**, enter **5080**\. 
   + For **IP address** type, select **IPv4**\.
   + For **VPC**, select the Amazon VPC that you created for your Transfer Family AS2 server\.

1. <a name="vpc-register-targets"></a>In the **Health checks** section, select **TCP** for the **Health check protocol**\.

1. <a name="vpc-add-to-list"></a>Select **Next**\.

1. In the **Register targets** page, enter the following information:
   + For **Network**, confirm that the Amazon VPC that you created for your Transfer Family AS2 server is selected\.
   + For **IPv4 address**, enter the private IPv4 address of your Transfer Family AS2 server's endpoints\.

      If you have more than one endpoint for your server, select **Add IPv4 address** to add another row for entering another IPv4 address\. Repeat this process until you've entered the private IP addresses for all of your server's endpoints\.
   + Ensure **Ports** is set to **5080**\.
   + Select **Include as pending below** to add your entries to the **Review targets** section\.

1. In the **Review targets** section, review your IP targets\.

1. Select **Create target group**, then go back to the procedure for creating your NLB and enter the new target group where indicated\.

**Test access to the server from an Elastic IP address**

Connect to the server over the custom port using an Elastic IP address or the DNS name of the Network Load Balancer\.

**Important**  
Manage access to your server from client IP addresses using the [network access control lists \(network ACLs\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) for the subnets configured on the load balancer\. Network ACL permissions are set at the subnet level, so the rules apply to all resources using the subnet\. You can't control access from client IP addresses using security groups because the load balancer's target type is set to IP instead of Instance\. This means that the load balancer doesn't preserve source IP addresses\. If the [Network Load Balancer's health checks](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/target-group-health-checks.html) fail, this means the load balancer can't connect to the server endpoint\. To troubleshoot this, check the following:  
Confirm that the server [endpoint's associated security group](https://aws.amazon.com/premiumsupport/knowledge-center/sftp-enable-elastic-ip-custom-port/) allows inbound connections from the subnets configured on the load balancer\. The load balancer must be able to connect to the server endpoint over port 5080\.
Confirm that the server's **State** is **Online**\.

## AS2 limits and limitations<a name="as2-limits-issues"></a>

**Limits**

The following limits are in place for AS2 file transfers\.


**AS2 limits**  

| Name | Default | Adjustable | 
| --- | --- | --- | 
| Inbound AS2 requests per second per server | 25 | Yes | 
| Inbound AS2 requests in progress per server | 100 | Yes | 
| Maximum number of file transfer requests per second per connector | 3 | Yes | 
| Maximum number of files per file transfer request | 10 | No | 
| Outbound AS2 requests in progress per connector | 100 | Yes | 
| Maximum file size \(compressed or uncompressed\) | 50 MB | Yes | 
| Inactivity timeout | 350 seconds | No | 
| Maximum number of partner profiles per account | 1000 \(up to 10 certificates per partner profile: not adjustable\) | Yes | 
| Maximum number of certificates per account | 1000 | Yes | 
| Maximum number of connectors per account | 100 | Yes | 
| Maximum number of agreements per server | 100 | Yes | 

**Known limitations**
+ Server\-side TCP keep\-alive is not supported\. The connection times out after 350 seconds of inactivity unless the client sends keep\-alive packets\.
+ For an active agreement to be accepted by the service and appear in Amazon CloudWatch logs, messages must contain valid AS2 headers\.
+ The server that's receiving messages from AWS Transfer Family for AS2 must support the Cryptographic Message Syntax \(CMS\) algorithm protection attribute for validating message signatures, as defined in [RFC 6211](https://datatracker.ietf.org/doc/html/rfc6211)\. This attribute is not supported in some older IBM Sterling products\.
+ Duplicate message IDs result in a processed/Warning: duplicate\-document message\.
+ When sending AS2 messages or asynchronous MDNs to a trading partner's HTTPS endpoint, the messages or MDNs must use a valid SSL certificate signed by a certificate authority \(CA\) that's trusted by AWS Transfer Family\. \(For a list of trusted CAs, see [https://www\.amazontrust\.com/repository/](https://www.amazontrust.com/repository/)\.\) Self\-signed certificates are not currently supported\. 
+ The endpoint must support the TLS version 1\.2 protocol and a cryptographic algorithm that's permitted by the security policy \(as described in [Working with security policies](security-policies.md)\)\.
+ Mutual TLS \(mTLS\) is not currently supported\.
+ Multiple attachments and certificate exchange messaging \(CEM\) from AS2 version 1\.2 is not currently supported\.
+ Basic authentication is not currently supported\.

## AS2 error codes<a name="as2-error-codes"></a>


**AS2 error codes**  

| Code | Error | Description | 
| --- | --- | --- | 
| DECRYPT\_FAILED | Failed to decrypt message message\-ID\. Ensure that the partner has the correct public encryption key\. | Decryption failed\. Confirm that the partner sent a payload by using a valid certificate and that encryption was performed by using a valid encryption algorithm\. | 
| ERROR\_DECRYPT\_UNSUPPORTED\_ENCRYPTION\_ALG | SMIME Payload Decryption requested using unsupported algorithm with ID: encryption\-ID\. | The remote sender has sent an AS2 payload with an unsupported encryption algorithm\. The sender must choose an encryption algorithm that's supported by AWS Transfer Family\. | 
| DECRYPT\_FAILED\_INVALID\_SMIME\_FORMAT | Unable to parse enveloped mimePart\. | MIME payload is either corrupt or in an unsupported SMIME format\. The sender should make sure that the format they're using is supported, and then resend the payload\. | 
| DECRYPT\_FAILED\_NO\_DECRYPTION\_KEY\_FOUND | No matching decryption key found\. | The partner profile did not have a certificate assigned that matched the message, or the certificates that matched the message are now expired or no longer valid\. You must update the partner profile and ensure that it contains a valid certificate\. | 
| ENCRYPTION\_FAILED | Failed to encrypt file file\-name\. | The file to be sent is not available for encryption\. Verify that the file is in its expected AS2 location and that AWS Transfer Family has permission to read the file\. | 
| VERIFICATION\_FAILED | Signature verification failed for AS2 message message\-ID or a MIC code did not match\. | Check that the sender's signing certificate matches the signing certificates for the remote profile\. Also check that the MIC algorithms are compatible with AWS Transfer Family\. | 
| SIGNING\_FAILED | Failed to sign file\. | The file to be sent is not available for signing, or signing could not be performed\. Verify that the file is in its expected AS2 location and that AWS Transfer Family has permission to read the file\. | 
| DECOMPRESSION\_FAILED | Failed to decompress message\. | Either the file sent is corrupt, or the compression algorithm is not valid\. Resend the message and verify that ZLIB compression is used, or resend the message without compression enabled\. | 
| AGREEMENT\_NOT\_FOUND | Agreement was not found\. | Either the agreement was not found, or the agreement is associated with an inactive profile\. Update the agreement within the Transfer Family server to include active profiles\. | 
| CONNECTOR\_NOT\_FOUND | Connector or related configuration was not found\. | Either the connector was not found, or the connector is associated with an inactive profile\. Update the connector to include active profiles\. | 
| INSUFFICENT\_MESSAGE\_SECURITY\_UNENCRYPTED | Encryption is required\. | The partner sent an unencrypted message to Transfer Family, which is not supported\. The sender must use an encrypted payload\. | 
| DUPLICATE\_MESSAGE | Duplicate or double processed step\. | The payload has a duplicate processing step\. For example, there are two encryption steps\. Resend the message with a single step for signing, compression, and encryption\. | 
| INVALID\_REQUEST | There is a problem with a message header\. | Check the as2\-from and as2\-to fields\. Make sure that the original message ID is accurate for the MDN format\. Also make sure that the message ID format is not missing any AS2 headers\. | 
| UNABLE\_TO\_RESOLVE\_HOSTNAME | Unable to resolve hostname hostname\.  | The Transfer Family server could not resolve the partner's hostname by using a public DNS server\. Check that the configured host is registered and that the DNS record has had time to publish\. | 
| HTTP\_ERROR\_RESPONSE\_FROM\_PARTNER |  *partner\-URL* returned status 400 for message with ID=*message\-id*\.  | Communicating with the partner's AS2 server returned an unexpected HTTP response code\. The partner might be able to provide more diagnostics from their AS2 server logs\. | 
| INVALID\_ENDPOINT\_PROTOCOL | Only HTTP and HTTPS are supported\. | You must specify HTTP or HTTPS as the protocol in your AS2 connector configuration\. | 
| UNABLE\_RESOLVE\_HOST\_TO\_IP\_ADDRESS | Unable to resolve hostname to IP addresses\. | Transfer Family is unable to perform DNS to IP address resolution on the public DNS server that is configured in the AS2 connector\. Update the connector to point to a valid partner URL\. | 
| UNABLE\_TO\_CONNECT\_TO\_REMOTE\_HOST\_OR\_IP | Connection to endpoint timed out\. | Transfer Family cannot establish a socket connection to the configured partner's AS2 server\. Check that the partner's AS2 server is available at the configured IP address\. | 
| SEND\_FILE\_NOT\_FOUND | File path file\-path not found\. | Transfer Family can't locate the file in the send file operation\. Check that the configured home directory and path are valid and that Transfer Family has read permissions for the file\. | 
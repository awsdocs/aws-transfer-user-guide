# CreateServer<a name="API_CreateServer"></a>

Instantiates an auto\-scaling virtual server based on the selected file transfer protocol in AWS\. When you make updates to your file transfer protocol\-enabled server or when you work with users, use the service\-generated `ServerId` property that is assigned to the newly created server\.

## Request Syntax<a name="API_CreateServer_RequestSyntax"></a>

```
{
   "Certificate": "string",
   "Domain": "string",
   "EndpointDetails": { 
      "AddressAllocationIds": [ "string" ],
      "SecurityGroupIds": [ "string" ],
      "SubnetIds": [ "string" ],
      "VpcEndpointId": "string",
      "VpcId": "string"
   },
   "EndpointType": "string",
   "HostKey": "string",
   "IdentityProviderDetails": { 
      "DirectoryId": "string",
      "Function": "string",
      "InvocationRole": "string",
      "Url": "string"
   },
   "IdentityProviderType": "string",
   "LoggingRole": "string",
   "PostAuthenticationLoginBanner": "string",
   "PreAuthenticationLoginBanner": "string",
   "ProtocolDetails": { 
      "As2Transports": [ "string" ],
      "PassiveIp": "string",
      "SetStatOption": "string",
      "TlsSessionResumptionMode": "string"
   },
   "Protocols": [ "string" ],
   "SecurityPolicyName": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "WorkflowDetails": { 
      "OnPartialUpload": [ 
         { 
            "ExecutionRole": "string",
            "WorkflowId": "string"
         }
      ],
      "OnUpload": [ 
         { 
            "ExecutionRole": "string",
            "WorkflowId": "string"
         }
      ]
   }
}
```

## Request Parameters<a name="API_CreateServer_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Certificate](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-Certificate"></a>
The Amazon Resource Name \(ARN\) of the AWS Certificate Manager \(ACM\) certificate\. Required when `Protocols` is set to `FTPS`\.  
To request a new public certificate, see [Request a public certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html) in the * AWS Certificate Manager User Guide*\.  
To import an existing certificate into ACM, see [Importing certificates into ACM](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html) in the * AWS Certificate Manager User Guide*\.  
To request a private certificate to use FTPS through private IP addresses, see [Request a private certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-private.html) in the * AWS Certificate Manager User Guide*\.  
Certificates with the following cryptographic algorithms and key sizes are supported:  
+ 2048\-bit RSA \(RSA\_2048\)
+ 4096\-bit RSA \(RSA\_4096\)
+ Elliptic Prime Curve 256 bit \(EC\_prime256v1\)
+ Elliptic Prime Curve 384 bit \(EC\_secp384r1\)
+ Elliptic Prime Curve 521 bit \(EC\_secp521r1\)
The certificate must be a valid SSL/TLS X\.509 version 3 certificate with FQDN or IP address specified and information about the issuer\.
Type: String  
Length Constraints: Maximum length of 1600\.  
Required: No

 ** [Domain](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-Domain"></a>
The domain of the storage system that is used for file transfers\. There are two domains available: Amazon Simple Storage Service \(Amazon S3\) and Amazon Elastic File System \(Amazon EFS\)\. The default value is S3\.  
After the server is created, the domain cannot be changed\.
Type: String  
Valid Values:` S3 | EFS`   
Required: No

 ** [EndpointDetails](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-EndpointDetails"></a>
The virtual private cloud \(VPC\) endpoint settings that are configured for your server\. When you host your endpoint within your VPC, you can make your endpoint accessible only to resources within your VPC, or you can attach Elastic IP addresses and make your endpoint accessible to clients over the internet\. Your VPC's default security groups are automatically assigned to your endpoint\.  
Type: [EndpointDetails](API_EndpointDetails.md) object  
Required: No

 ** [EndpointType](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-EndpointType"></a>
The type of endpoint that you want your server to use\. You can choose to make your server's endpoint publicly accessible \(PUBLIC\) or host it inside your VPC\. With an endpoint that is hosted in a VPC, you can restrict access to your server and resources only within your VPC or choose to make it internet facing by attaching Elastic IP addresses directly to it\.  
 After May 19, 2021, you won't be able to create a server using `EndpointType=VPC_ENDPOINT` in your AWS account if your account hasn't already done so before May 19, 2021\. If you have already created servers with `EndpointType=VPC_ENDPOINT` in your AWS account on or before May 19, 2021, you will not be affected\. After this date, use `EndpointType`=`VPC`\.  
For more information, see [Discontinuing the use of VPC\_ENDPOINTYou can change the endpoint type for your server using the Transfer Family console, AWS CLI, API, SDKs, or AWS CloudFormation\. To change your server’s endpoint type, see [Updating the AWS Transfer Family server endpoint type from VPC\_ENDPOINT to VPC](update-endpoint-type-vpc.md)\.](create-server-in-vpc.md#deprecate-vpc-endpoint)\.  
It is recommended that you use `VPC` as the `EndpointType`\. With this endpoint type, you have the option to directly associate up to three Elastic IPv4 addresses \(BYO IP included\) with your server's endpoint and use VPC security groups to restrict traffic by the client's public IP address\. This is not possible with `EndpointType` set to `VPC_ENDPOINT`\.
Type: String  
Valid Values:` PUBLIC | VPC | VPC_ENDPOINT`   
Required: No

 ** [HostKey](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-HostKey"></a>
The RSA, ECDSA, or ED25519 private key to use for your SFTP\-enabled server\. You can add multiple host keys, in case you want to rotate keys, or have a set of active keys that use different algorithms\.  
Use the following command to generate an RSA 2048 bit key with no passphrase:  
 `ssh-keygen -t rsa -b 2048 -N "" -m PEM -f my-new-server-key`\.  
Use a minimum value of 2048 for the `-b` option\. You can create a stronger key by using 3072 or 4096\.  
Use the following command to generate an ECDSA 256 bit key with no passphrase:  
 `ssh-keygen -t ecdsa -b 256 -N "" -m PEM -f my-new-server-key`\.  
Valid values for the `-b` option for ECDSA are 256, 384, and 521\.  
Use the following command to generate an ED25519 key with no passphrase:  
 `ssh-keygen -t ed25519 -N "" -f my-new-server-key`\.  
For all of these commands, you can replace *my\-new\-server\-key* with a string of your choice\.  
If you aren't planning to migrate existing users from an existing SFTP\-enabled server to a new server, don't update the host key\. Accidentally changing a server's host key can be disruptive\.
For more information, see [Update host keys for your SFTP\-enabled server](https://docs.aws.amazon.com/transfer/latest/userguide/edit-server-config.html#configuring-servers-change-host-key) in the * AWS Transfer Family User Guide*\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Required: No

 ** [IdentityProviderDetails](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-IdentityProviderDetails"></a>
Required when `IdentityProviderType` is set to `AWS_DIRECTORY_SERVICE` or `API_GATEWAY`\. Accepts an array containing all of the information required to use a directory in `AWS_DIRECTORY_SERVICE` or invoke a customer\-supplied authentication API, including the API Gateway URL\. Not required when `IdentityProviderType` is set to `SERVICE_MANAGED`\.  
Type: [IdentityProviderDetails](API_IdentityProviderDetails.md) object  
Required: No

 ** [IdentityProviderType](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-IdentityProviderType"></a>
The mode of authentication for a server\. The default value is `SERVICE_MANAGED`, which allows you to store and access user credentials within the AWS Transfer Family service\.  
Use `AWS_DIRECTORY_SERVICE` to provide access to Active Directory groups in AWS Directory Service for Microsoft Active Directory or Microsoft Active Directory in your on\-premises environment or in AWS using AD Connector\. This option also requires you to provide a Directory ID by using the `IdentityProviderDetails` parameter\.  
Use the `API_GATEWAY` value to integrate with an identity provider of your choosing\. The `API_GATEWAY` setting requires you to provide an Amazon API Gateway endpoint URL to call for authentication by using the `IdentityProviderDetails` parameter\.  
Use the `AWS_LAMBDA` value to directly use an AWS Lambda function as your identity provider\. If you choose this value, you must specify the ARN for the Lambda function in the `Function` parameter or the `IdentityProviderDetails` data type\.  
Type: String  
Valid Values:` SERVICE_MANAGED | API_GATEWAY | AWS_DIRECTORY_SERVICE | AWS_LAMBDA`   
Required: No

 ** [LoggingRole](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a server to turn on Amazon CloudWatch logging for Amazon S3 or Amazon EFSevents\. When set, you can view user activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** [PostAuthenticationLoginBanner](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-PostAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed after the user authenticates\.  
The SFTP protocol does not support post\-authentication display banners\.
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** [PreAuthenticationLoginBanner](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-PreAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed before the user authenticates\. For example, the following banner displays details about using the system:  
 `This system is for the use of authorized users only. Individuals using this computer system without authority, or in excess of their authority, are subject to having all of their activities on this system monitored and recorded by system personnel.`   
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** [ProtocolDetails](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-ProtocolDetails"></a>
The protocol settings that are configured for your server\.  
+  To indicate passive mode \(for FTP and FTPS protocols\), use the `PassiveIp` parameter\. Enter a single dotted\-quad IPv4 address, such as the external IP address of a firewall, router, or load balancer\. 
+ To ignore the error that is generated when the client attempts to use the `SETSTAT` command on a file that you are uploading to an Amazon S3 bucket, use the `SetStatOption` parameter\. To have the AWS Transfer Family server ignore the `SETSTAT` command and upload files without needing to make any changes to your SFTP client, set the value to `ENABLE_NO_OP`\. If you set the `SetStatOption` parameter to `ENABLE_NO_OP`, Transfer Family generates a log entry to Amazon CloudWatch Logs, so that you can determine when the client is making a `SETSTAT` call\.
+ To determine whether your AWS Transfer Family server resumes recent, negotiated sessions through a unique session ID, use the `TlsSessionResumptionMode` parameter\.
+  `As2Transports` indicates the transport method for the AS2 messages\. Currently, only HTTP is supported\.
Type: [ProtocolDetails](API_ProtocolDetails.md) object  
Required: No

 ** [Protocols](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-Protocols"></a>
Specifies the file transfer protocol or protocols over which your file transfer protocol client can connect to your server's endpoint\. The available protocols are:  
+  `SFTP` \(Secure Shell \(SSH\) File Transfer Protocol\): File transfer over SSH
+  `FTPS` \(File Transfer Protocol Secure\): File transfer with TLS encryption
+  `FTP` \(File Transfer Protocol\): Unencrypted file transfer
+  `AS2` \(Applicability Statement 2\): used for transporting structured business\-to\-business data
+ If you select `FTPS`, you must choose a certificate stored in AWS Certificate Manager \(ACM\) which is used to identify your server when clients connect to it over FTPS\.
+ If `Protocol` includes either `FTP` or `FTPS`, then the `EndpointType` must be `VPC` and the `IdentityProviderType` must be either `AWS_DIRECTORY_SERVICE`, `AWS_LAMBDA`, or `API_GATEWAY`\.
+ If `Protocol` includes `FTP`, then `AddressAllocationIds` cannot be associated\.
+ If `Protocol` is set only to `SFTP`, the `EndpointType` can be set to `PUBLIC` and the `IdentityProviderType` can be set any of the supported identity types: `SERVICE_MANAGED`, `AWS_DIRECTORY_SERVICE`, `AWS_LAMBDA`, or `API_GATEWAY`\.
+ If `Protocol` includes `AS2`, then the `EndpointType` must be `VPC`, and domain must be Amazon S3\.
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Valid Values:` SFTP | FTP | FTPS | AS2`   
Required: No

 ** [SecurityPolicyName](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-SecurityPolicyName"></a>
Specifies the name of the security policy that is attached to the server\.  
Type: String  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+`   
Required: No

 ** [Tags](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-Tags"></a>
Key\-value pairs that can be used to group and search for servers\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** [WorkflowDetails](#API_CreateServer_RequestSyntax) **   <a name="TransferFamily-CreateServer-request-WorkflowDetails"></a>
Specifies the workflow ID for the workflow to assign and the execution role that's used for executing the workflow\.  
In addition to a workflow to execute when a file is uploaded completely, `WorkflowDetails` can also contain a workflow ID \(and execution role\) for a workflow to execute on partial upload\. A partial upload occurs when a file is open when the session disconnects\.  
Type: [WorkflowDetails](API_WorkflowDetails.md) object  
Required: No

## Response Syntax<a name="API_CreateServer_ResponseSyntax"></a>

```
{
   "ServerId": "string"
}
```

## Response Elements<a name="API_CreateServer_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ServerId](#API_CreateServer_ResponseSyntax) **   <a name="TransferFamily-CreateServer-response-ServerId"></a>
The service\-assigned identifier of the server that is created\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_CreateServer_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You do not have sufficient access to perform this action\.  
HTTP Status Code: 400

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceExistsException **   
The requested resource does not exist\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

 ** ThrottlingException **   
The request was denied due to request throttling\.  
HTTP Status Code: 400

## Examples<a name="API_CreateServer_Examples"></a>

### Example<a name="API_CreateServer_Example_1"></a>

The following example creates a new server using a `VPC_ENDPOINT`\.

#### Sample Request<a name="API_CreateServer_Example_1_Request"></a>

```
{     
   "EndpointType": "VPC",
   "EndpointDetails":...,
   "HostKey": "Your RSA private key",
   "IdentityProviderDetails": "IdentityProvider",
   "IdentityProviderType": "SERVICE_MANAGED",
   "LoggingRole": "CloudWatchLoggingRole",
   "Tags": [ 
      { 
         "Key": "Name",
         "Value": "MyServer"
      }
   ]
}
```

### Example<a name="API_CreateServer_Example_2"></a>

This is a sample response for this API call\.

#### Sample Response<a name="API_CreateServer_Example_2_Response"></a>

```
{
   "ServerId": "s-01234567890abcdef"
}
```

## See Also<a name="API_CreateServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateServer) 
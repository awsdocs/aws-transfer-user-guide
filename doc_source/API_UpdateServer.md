# UpdateServer<a name="API_UpdateServer"></a>

Updates the file transfer protocol\-enabled server's properties after that server has been created\.

The `UpdateServer` call returns the `ServerId` of the server you updated\.

## Request Syntax<a name="API_UpdateServer_RequestSyntax"></a>

```
{
   "Certificate": "string",
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
   "ServerId": "string",
   "WorkflowDetails": { 
      "OnUpload": [ 
         { 
            "ExecutionRole": "string",
            "WorkflowId": "string"
         }
      ]
   }
}
```

## Request Parameters<a name="API_UpdateServer_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Certificate](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-Certificate"></a>
The Amazon Resource Name \(ARN\) of the AWSCertificate Manager \(ACM\) certificate\. Required when `Protocols` is set to `FTPS`\.  
To request a new public certificate, see [Request a public certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html) in the * AWSCertificate Manager User Guide*\.  
To import an existing certificate into ACM, see [Importing certificates into ACM](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html) in the * AWSCertificate Manager User Guide*\.  
To request a private certificate to use FTPS through private IP addresses, see [Request a private certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-private.html) in the * AWSCertificate Manager User Guide*\.  
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

 ** [EndpointDetails](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-EndpointDetails"></a>
The virtual private cloud \(VPC\) endpoint settings that are configured for your server\. When you host your endpoint within your VPC, you can make your endpoint accessible only to resources within your VPC, or you can attach Elastic IP addresses and make your endpoint accessible to clients over the internet\. Your VPC's default security groups are automatically assigned to your endpoint\.  
Type: [EndpointDetails](API_EndpointDetails.md) object  
Required: No

 ** [EndpointType](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-EndpointType"></a>
The type of endpoint that you want your server to use\. You can choose to make your server's endpoint publicly accessible \(PUBLIC\) or host it inside your VPC\. With an endpoint that is hosted in a VPC, you can restrict access to your server and resources only within your VPC or choose to make it internet facing by attaching Elastic IP addresses directly to it\.  
 After May 19, 2021, you won't be able to create a server using `EndpointType=VPC_ENDPOINT` in your AWSaccount if your account hasn't already done so before May 19, 2021\. If you have already created servers with `EndpointType=VPC_ENDPOINT` in your AWSaccount on or before May 19, 2021, you will not be affected\. After this date, use `EndpointType`=`VPC`\.  
For more information, see [Discontinuing the use of VPC\_ENDPOINTYou can change the endpoint type for your server using the Transfer Family console, AWS CLI, API, SDKs, or AWS CloudFormation\. To change your server’s endpoint type, see [Updating the AWS Transfer Family server endpoint type from VPC\_ENDPOINT to VPC](update-endpoint-type-vpc.md)\.](create-server-in-vpc.md#deprecate-vpc-endpoint)\.  
It is recommended that you use `VPC` as the `EndpointType`\. With this endpoint type, you have the option to directly associate up to three Elastic IPv4 addresses \(BYO IP included\) with your server's endpoint and use VPC security groups to restrict traffic by the client's public IP address\. This is not possible with `EndpointType` set to `VPC_ENDPOINT`\.
Type: String  
Valid Values:` PUBLIC | VPC | VPC_ENDPOINT`   
Required: No

 ** [HostKey](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-HostKey"></a>
The RSA, ECDSA, or ED25519 private key to use for your server\.  
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
For more information, see [Change the host key for your SFTP\-enabled server](https://docs.aws.amazon.com/transfer/latest/userguide/edit-server-config.html#configuring-servers-change-host-key) in the * AWS Transfer Family User Guide*\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Required: No

 ** [IdentityProviderDetails](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-IdentityProviderDetails"></a>
An array containing all of the information required to call a customer's authentication API method\.  
Type: [IdentityProviderDetails](API_IdentityProviderDetails.md) object  
Required: No

 ** [LoggingRole](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a server to turn on Amazon CloudWatch logging for Amazon S3 or Amazon EFSevents\. When set, you can view user activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Pattern: `^$|arn:.*role/.*`   
Required: No

 ** [PostAuthenticationLoginBanner](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-PostAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed after the user authenticates\.  
The SFTP protocol does not support post\-authentication display banners\.
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** [PreAuthenticationLoginBanner](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-PreAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed before the user authenticates\. For example, the following banner displays details about using the system:  
 `This system is for the use of authorized users only. Individuals using this computer system without authority, or in excess of their authority, are subject to having all of their activities on this system monitored and recorded by system personnel.`   
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** [ProtocolDetails](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-ProtocolDetails"></a>
The protocol settings that are configured for your server\.  
+  To indicate passive mode \(for FTP and FTPS protocols\), use the `PassiveIp` parameter\. Enter a single dotted\-quad IPv4 address, such as the external IP address of a firewall, router, or load balancer\. 
+ To ignore the error that is generated when the client attempts to use the `SETSTAT` command on a file that you are uploading to an Amazon S3 bucket, use the `SetStatOption` parameter\. To have the AWS Transfer Family server ignore the `SETSTAT` command and upload files without needing to make any changes to your SFTP client, set the value to `ENABLE_NO_OP`\. If you set the `SetStatOption` parameter to `ENABLE_NO_OP`, Transfer Family generates a log entry to Amazon CloudWatch Logs, so that you can determine when the client is making a `SETSTAT` call\.
+ To determine whether your AWS Transfer Family server resumes recent, negotiated sessions through a unique session ID, use the `TlsSessionResumptionMode` parameter\.
+  `As2Transports` indicates the transport method for the AS2 messages\. Currently, only HTTP is supported\.
Type: [ProtocolDetails](API_ProtocolDetails.md) object  
Required: No

 ** [Protocols](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-Protocols"></a>
Specifies the file transfer protocol or protocols over which your file transfer protocol client can connect to your server's endpoint\. The available protocols are:  
+  `SFTP` \(Secure Shell \(SSH\) File Transfer Protocol\): File transfer over SSH
+  `FTPS` \(File Transfer Protocol Secure\): File transfer with TLS encryption
+  `FTP` \(File Transfer Protocol\): Unencrypted file transfer
+  `AS2` \(Applicability Statement 2\): used for transporting structured business\-to\-business data
+ If you select `FTPS`, you must choose a certificate stored in AWS Certificate Manager \(ACM\) which is used to identify your server when clients connect to it over FTPS\.
+ If `Protocol` includes either `FTP` or `FTPS`, then the `EndpointType` must be `VPC` and the `IdentityProviderType` must be `AWS_DIRECTORY_SERVICE` or `API_GATEWAY`\.
+ If `Protocol` includes `FTP`, then `AddressAllocationIds` cannot be associated\.
+ If `Protocol` is set only to `SFTP`, the `EndpointType` can be set to `PUBLIC` and the `IdentityProviderType` can be set to `SERVICE_MANAGED`\.
+ If `Protocol` includes `AS2`, then the `EndpointType` must be `VPC`, and domain must be Amazon S3\.
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Valid Values:` SFTP | FTP | FTPS | AS2`   
Required: No

 ** [SecurityPolicyName](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-SecurityPolicyName"></a>
Specifies the name of the security policy that is attached to the server\.  
Type: String  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+`   
Required: No

 ** [ServerId](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-ServerId"></a>
A system\-assigned unique identifier for a server instance that the user account is assigned to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [WorkflowDetails](#API_UpdateServer_RequestSyntax) **   <a name="TransferFamily-UpdateServer-request-WorkflowDetails"></a>
Specifies the workflow ID for the workflow to assign and the execution role that's used for executing the workflow\.  
To remove an associated workflow from a server, you can provide an empty `OnUpload` object, as in the following example\.  
 `aws transfer update-server --server-id s-01234567890abcdef --workflow-details '{"OnUpload":[]}'`   
Type: [WorkflowDetails](API_WorkflowDetails.md) object  
Required: No

## Response Syntax<a name="API_UpdateServer_ResponseSyntax"></a>

```
{
   "ServerId": "string"
}
```

## Response Elements<a name="API_UpdateServer_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ServerId](#API_UpdateServer_ResponseSyntax) **   <a name="TransferFamily-UpdateServer-response-ServerId"></a>
A system\-assigned unique identifier for a server that the user account is assigned to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_UpdateServer_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You do not have sufficient access to perform this action\.  
HTTP Status Code: 400

 ** ConflictException **   
This exception is thrown when the `UpdateServer` is called for a file transfer protocol\-enabled server that has VPC as the endpoint type and the server's `VpcEndpointID` is not in the available state\.  
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

## Examples<a name="API_UpdateServer_Examples"></a>

### Example<a name="API_UpdateServer_Example_1"></a>

The following example updates the role of a server\.

#### Sample Request<a name="API_UpdateServer_Example_1_Request"></a>

```
{
   "EndpointDetails": { 
   "VpcEndpointId": "vpce-01234f056f3g13",
   "LoggingRole": "CloudWatchS3Events",
   "ServerId": "s-01234567890abcdef"
   }
}
```

### Example<a name="API_UpdateServer_Example_2"></a>

The following example removes any associated workflows from the server\.

#### Sample Request<a name="API_UpdateServer_Example_2_Request"></a>

```
aws transfer update-server --server-id s-01234567890abcdef --workflow-details '{"OnUpload":[]}'
```

### Example<a name="API_UpdateServer_Example_3"></a>

This is a sample response for this API call\.

#### Sample Response<a name="API_UpdateServer_Example_3_Response"></a>

```
{
   "ServerId": "s-01234567890abcdef"
}
```

## See Also<a name="API_UpdateServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/UpdateServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UpdateServer) 
# DescribedServer<a name="API_DescribedServer"></a>

Describes the properties of a file transfer protocol\-enabled server that was specified\.

## Contents<a name="API_DescribedServer_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-DescribedServer-Arn"></a>
Specifies the unique Amazon Resource Name \(ARN\) of the server\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** Certificate **   <a name="TransferFamily-Type-DescribedServer-Certificate"></a>
Specifies the ARN of the AWSCertificate Manager \(ACM\) certificate\. Required when `Protocols` is set to `FTPS`\.  
Type: String  
Length Constraints: Maximum length of 1600\.  
Required: No

 ** Domain **   <a name="TransferFamily-Type-DescribedServer-Domain"></a>
Specifies the domain of the storage system that is used for file transfers\.  
Type: String  
Valid Values:` S3 | EFS`   
Required: No

 ** EndpointDetails **   <a name="TransferFamily-Type-DescribedServer-EndpointDetails"></a>
The virtual private cloud \(VPC\) endpoint settings that are configured for your server\. When you host your endpoint within your VPC, you can make your endpoint accessible only to resources within your VPC, or you can attach Elastic IP addresses and make your endpoint accessible to clients over the internet\. Your VPC's default security groups are automatically assigned to your endpoint\.  
Type: [EndpointDetails](API_EndpointDetails.md) object  
Required: No

 ** EndpointType **   <a name="TransferFamily-Type-DescribedServer-EndpointType"></a>
Defines the type of endpoint that your server is connected to\. If your server is connected to a VPC endpoint, your server isn't accessible over the public internet\.  
Type: String  
Valid Values:` PUBLIC | VPC | VPC_ENDPOINT`   
Required: No

 ** HostKeyFingerprint **   <a name="TransferFamily-Type-DescribedServer-HostKeyFingerprint"></a>
Specifies the Base64\-encoded SHA256 fingerprint of the server's host key\. This value is equivalent to the output of the `ssh-keygen -l -f my-new-server-key` command\.  
Type: String  
Required: No

 ** IdentityProviderDetails **   <a name="TransferFamily-Type-DescribedServer-IdentityProviderDetails"></a>
Specifies information to call a customer\-supplied authentication API\. This field is not populated when the `IdentityProviderType` of a server is `AWS_DIRECTORY_SERVICE` or `SERVICE_MANAGED`\.  
Type: [IdentityProviderDetails](API_IdentityProviderDetails.md) object  
Required: No

 ** IdentityProviderType **   <a name="TransferFamily-Type-DescribedServer-IdentityProviderType"></a>
The mode of authentication for a server\. The default value is `SERVICE_MANAGED`, which allows you to store and access user credentials within the AWS Transfer Family service\.  
Use `AWS_DIRECTORY_SERVICE` to provide access to Active Directory groups in AWS Directory Service for Microsoft Active Directory or Microsoft Active Directory in your on\-premises environment or in AWS using AD Connector\. This option also requires you to provide a Directory ID by using the `IdentityProviderDetails` parameter\.  
Use the `API_GATEWAY` value to integrate with an identity provider of your choosing\. The `API_GATEWAY` setting requires you to provide an Amazon API Gateway endpoint URL to call for authentication by using the `IdentityProviderDetails` parameter\.  
Use the `AWS_LAMBDA` value to directly use an AWS Lambda function as your identity provider\. If you choose this value, you must specify the ARN for the Lambda function in the `Function` parameter or the `IdentityProviderDetails` data type\.  
Type: String  
Valid Values:` SERVICE_MANAGED | API_GATEWAY | AWS_DIRECTORY_SERVICE | AWS_LAMBDA`   
Required: No

 ** LoggingRole **   <a name="TransferFamily-Type-DescribedServer-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a server to turn on Amazon CloudWatch logging for Amazon S3 or Amazon EFSevents\. When set, you can view user activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** PostAuthenticationLoginBanner **   <a name="TransferFamily-Type-DescribedServer-PostAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed after the user authenticates\.  
The SFTP protocol does not support post\-authentication display banners\.
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** PreAuthenticationLoginBanner **   <a name="TransferFamily-Type-DescribedServer-PreAuthenticationLoginBanner"></a>
Specifies a string to display when users connect to a server\. This string is displayed before the user authenticates\. For example, the following banner displays details about using the system:  
 `This system is for the use of authorized users only. Individuals using this computer system without authority, or in excess of their authority, are subject to having all of their activities on this system monitored and recorded by system personnel.`   
Type: String  
Length Constraints: Maximum length of 512\.  
Pattern: `[\x09-\x0D\x20-\x7E]*`   
Required: No

 ** ProtocolDetails **   <a name="TransferFamily-Type-DescribedServer-ProtocolDetails"></a>
The protocol settings that are configured for your server\.  
+  To indicate passive mode \(for FTP and FTPS protocols\), use the `PassiveIp` parameter\. Enter a single dotted\-quad IPv4 address, such as the external IP address of a firewall, router, or load balancer\. 
+ To ignore the error that is generated when the client attempts to use the `SETSTAT` command on a file that you are uploading to an Amazon S3 bucket, use the `SetStatOption` parameter\. To have the AWS Transfer Family server ignore the `SETSTAT` command and upload files without needing to make any changes to your SFTP client, set the value to `ENABLE_NO_OP`\. If you set the `SetStatOption` parameter to `ENABLE_NO_OP`, Transfer Family generates a log entry to Amazon CloudWatch Logs, so that you can determine when the client is making a `SETSTAT` call\.
+ To determine whether your AWS Transfer Family server resumes recent, negotiated sessions through a unique session ID, use the `TlsSessionResumptionMode` parameter\.
+  `As2Transports` indicates the transport method for the AS2 messages\. Currently, only HTTP is supported\.
Type: [ProtocolDetails](API_ProtocolDetails.md) object  
Required: No

 ** Protocols **   <a name="TransferFamily-Type-DescribedServer-Protocols"></a>
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

 ** SecurityPolicyName **   <a name="TransferFamily-Type-DescribedServer-SecurityPolicyName"></a>
Specifies the name of the security policy that is attached to the server\.  
Type: String  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+`   
Required: No

 ** ServerId **   <a name="TransferFamily-Type-DescribedServer-ServerId"></a>
Specifies the unique system\-assigned identifier for a server that you instantiate\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: No

 ** State **   <a name="TransferFamily-Type-DescribedServer-State"></a>
The condition of the server that was described\. A value of `ONLINE` indicates that the server can accept jobs and transfer files\. A `State` value of `OFFLINE` means that the server cannot perform file transfer operations\.  
The states of `STARTING` and `STOPPING` indicate that the server is in an intermediate state, either not fully able to respond, or not fully offline\. The values of `START_FAILED` or `STOP_FAILED` can indicate an error condition\.  
Type: String  
Valid Values:` OFFLINE | ONLINE | STARTING | STOPPING | START_FAILED | STOP_FAILED`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedServer-Tags"></a>
Specifies the key\-value pairs that you can use to search for and group servers that were assigned to the server that was described\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** UserCount **   <a name="TransferFamily-Type-DescribedServer-UserCount"></a>
Specifies the number of users that are assigned to a server you specified with the `ServerId`\.  
Type: Integer  
Required: No

 ** WorkflowDetails **   <a name="TransferFamily-Type-DescribedServer-WorkflowDetails"></a>
Specifies the workflow ID for the workflow to assign and the execution role that's used for executing the workflow\.  
Type: [WorkflowDetails](API_WorkflowDetails.md) object  
Required: No

## See Also<a name="API_DescribedServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedServer) 
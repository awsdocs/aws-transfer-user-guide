# ListedServer<a name="API_ListedServer"></a>

Returns properties of a file transfer protocol\-enabled server that was specified\.

## Contents<a name="API_ListedServer_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-ListedServer-Arn"></a>
Specifies the unique Amazon Resource Name \(ARN\) for a server to be listed\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** Domain **   <a name="TransferFamily-Type-ListedServer-Domain"></a>
Specifies the domain of the storage system that is used for file transfers\.  
Type: String  
Valid Values:` S3 | EFS`   
Required: No

 ** EndpointType **   <a name="TransferFamily-Type-ListedServer-EndpointType"></a>
Specifies the type of VPC endpoint that your server is connected to\. If your server is connected to a VPC endpoint, your server isn't accessible over the public internet\.  
Type: String  
Valid Values:` PUBLIC | VPC | VPC_ENDPOINT`   
Required: No

 ** IdentityProviderType **   <a name="TransferFamily-Type-ListedServer-IdentityProviderType"></a>
The mode of authentication for a server\. The default value is `SERVICE_MANAGED`, which allows you to store and access user credentials within the AWS Transfer Family service\.  
Use `AWS_DIRECTORY_SERVICE` to provide access to Active Directory groups in AWS Directory Service for Microsoft Active Directory or Microsoft Active Directory in your on\-premises environment or in AWS using AD Connector\. This option also requires you to provide a Directory ID by using the `IdentityProviderDetails` parameter\.  
Use the `API_GATEWAY` value to integrate with an identity provider of your choosing\. The `API_GATEWAY` setting requires you to provide an Amazon API Gateway endpoint URL to call for authentication by using the `IdentityProviderDetails` parameter\.  
Use the `AWS_LAMBDA` value to directly use an AWS Lambda function as your identity provider\. If you choose this value, you must specify the ARN for the Lambda function in the `Function` parameter or the `IdentityProviderDetails` data type\.  
Type: String  
Valid Values:` SERVICE_MANAGED | API_GATEWAY | AWS_DIRECTORY_SERVICE | AWS_LAMBDA`   
Required: No

 ** LoggingRole **   <a name="TransferFamily-Type-ListedServer-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a server to turn on Amazon CloudWatch logging for Amazon S3 or Amazon EFSevents\. When set, you can view user activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** ServerId **   <a name="TransferFamily-Type-ListedServer-ServerId"></a>
Specifies the unique system assigned identifier for the servers that were listed\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: No

 ** State **   <a name="TransferFamily-Type-ListedServer-State"></a>
The condition of the server that was described\. A value of `ONLINE` indicates that the server can accept jobs and transfer files\. A `State` value of `OFFLINE` means that the server cannot perform file transfer operations\.  
The states of `STARTING` and `STOPPING` indicate that the server is in an intermediate state, either not fully able to respond, or not fully offline\. The values of `START_FAILED` or `STOP_FAILED` can indicate an error condition\.  
Type: String  
Valid Values:` OFFLINE | ONLINE | STARTING | STOPPING | START_FAILED | STOP_FAILED`   
Required: No

 ** UserCount **   <a name="TransferFamily-Type-ListedServer-UserCount"></a>
Specifies the number of users that are assigned to a server you specified with the `ServerId`\.  
Type: Integer  
Required: No

## See Also<a name="API_ListedServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedServer) 
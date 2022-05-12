# LoggingConfiguration<a name="API_LoggingConfiguration"></a>

Consists of the logging role and the log group name\.

## Contents<a name="API_LoggingConfiguration_Contents"></a>

 ** LoggingRole **   <a name="TransferFamily-Type-LoggingConfiguration-LoggingRole"></a>
Specifies the Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a server to turn on Amazon CloudWatch logging for Amazon S3 or Amazon EFS events\. When set, user activity can be viewed in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** LogGroupName **   <a name="TransferFamily-Type-LoggingConfiguration-LogGroupName"></a>
The name of the CloudWatch logging group for the AWS Transfer server to which this workflow belongs\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 512\.  
Pattern: `[\.\-_/#A-Za-z0-9]*`   
Required: No

## See Also<a name="API_LoggingConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/LoggingConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/LoggingConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/LoggingConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/LoggingConfiguration) 
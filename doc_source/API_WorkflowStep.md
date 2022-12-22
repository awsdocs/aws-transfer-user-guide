# WorkflowStep<a name="API_WorkflowStep"></a>

The basic building block of a workflow\.

## Contents<a name="API_WorkflowStep_Contents"></a>

 ** CopyStepDetails **   <a name="TransferFamily-Type-WorkflowStep-CopyStepDetails"></a>
Details for a step that performs a file copy\.  
 Consists of the following values:   
+ A description
+ An Amazon S3 location for the destination of the file copy\.
+ A flag that indicates whether to overwrite an existing file of the same name\. The default is `FALSE`\.
Type: [CopyStepDetails](API_CopyStepDetails.md) object  
Required: No

 ** CustomStepDetails **   <a name="TransferFamily-Type-WorkflowStep-CustomStepDetails"></a>
Details for a step that invokes an AWS Lambda function\.  
Consists of the Lambda function's name, target, and timeout \(in seconds\)\.   
Type: [CustomStepDetails](API_CustomStepDetails.md) object  
Required: No

 ** DecryptStepDetails **   <a name="TransferFamily-Type-WorkflowStep-DecryptStepDetails"></a>
Details for a step that decrypts an encrypted file\.  
Consists of the following values:  
+ A descriptive name
+ An Amazon S3 or Amazon Elastic File System \(Amazon EFS\) location for the source file to decrypt\.
+ An S3 or Amazon EFS location for the destination of the file decryption\.
+ A flag that indicates whether to overwrite an existing file of the same name\. The default is `FALSE`\.
+ The type of encryption that's used\. Currently, only PGP encryption is supported\.
Type: [DecryptStepDetails](API_DecryptStepDetails.md) object  
Required: No

 ** DeleteStepDetails **   <a name="TransferFamily-Type-WorkflowStep-DeleteStepDetails"></a>
Details for a step that deletes the file\.  
Type: [DeleteStepDetails](API_DeleteStepDetails.md) object  
Required: No

 ** TagStepDetails **   <a name="TransferFamily-Type-WorkflowStep-TagStepDetails"></a>
Details for a step that creates one or more tags\.  
You specify one or more tags\. Each tag contains a key\-value pair\.  
Type: [TagStepDetails](API_TagStepDetails.md) object  
Required: No

 ** Type **   <a name="TransferFamily-Type-WorkflowStep-Type"></a>
 Currently, the following step types are supported\.   
+  ** `COPY` ** \- Copy the file to another location\.
+  ** `CUSTOM` ** \- Perform a custom step with an AWS Lambda function target\.
+  ** `DECRYPT` ** \- Decrypt a file that was encrypted before it was uploaded\.
+  ** `DELETE` ** \- Delete the file\.
+  ** `TAG` ** \- Add a tag to the file\.
Type: String  
Valid Values:` COPY | CUSTOM | TAG | DELETE | DECRYPT`   
Required: No

## See Also<a name="API_WorkflowStep_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/WorkflowStep) 
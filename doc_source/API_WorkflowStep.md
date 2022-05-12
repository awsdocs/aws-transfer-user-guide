# WorkflowStep<a name="API_WorkflowStep"></a>

The basic building block of a workflow\.

## Contents<a name="API_WorkflowStep_Contents"></a>

 ** CopyStepDetails **   <a name="TransferFamily-Type-WorkflowStep-CopyStepDetails"></a>
Details for a step that performs a file copy\.  
 Consists of the following values:   
+ A description
+ An S3 location for the destination of the file copy\.
+ A flag that indicates whether or not to overwrite an existing file of the same name\. The default is `FALSE`\.
Type: [CopyStepDetails](API_CopyStepDetails.md) object  
Required: No

 ** CustomStepDetails **   <a name="TransferFamily-Type-WorkflowStep-CustomStepDetails"></a>
Details for a step that invokes a lambda function\.  
 Consists of the lambda function name, target, and timeout \(in seconds\)\.   
Type: [CustomStepDetails](API_CustomStepDetails.md) object  
Required: No

 ** DeleteStepDetails **   <a name="TransferFamily-Type-WorkflowStep-DeleteStepDetails"></a>
Details for a step that deletes the file\.  
Type: [DeleteStepDetails](API_DeleteStepDetails.md) object  
Required: No

 ** TagStepDetails **   <a name="TransferFamily-Type-WorkflowStep-TagStepDetails"></a>
Details for a step that creates one or more tags\.  
You specify one or more tags: each tag contains a key/value pair\.  
Type: [TagStepDetails](API_TagStepDetails.md) object  
Required: No

 ** Type **   <a name="TransferFamily-Type-WorkflowStep-Type"></a>
 Currently, the following step types are supported\.   
+  *COPY*: copy the file to another location
+  *CUSTOM*: custom step with a lambda target
+  *DELETE*: delete the file
+  *TAG*: add a tag to the file
Type: String  
Valid Values:` COPY | CUSTOM | TAG | DELETE`   
Required: No

## See Also<a name="API_WorkflowStep_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/WorkflowStep) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/WorkflowStep) 
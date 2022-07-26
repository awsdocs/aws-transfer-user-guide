# ExecutionStepResult<a name="API_ExecutionStepResult"></a>

Specifies the following details for the step: error \(if any\), outputs \(if any\), and the step type\.

## Contents<a name="API_ExecutionStepResult_Contents"></a>

 ** Error **   <a name="TransferFamily-Type-ExecutionStepResult-Error"></a>
Specifies the details for an error, if it occurred during execution of the specified workflow step\.  
Type: [ExecutionError](API_ExecutionError.md) object  
Required: No

 ** Outputs **   <a name="TransferFamily-Type-ExecutionStepResult-Outputs"></a>
The values for the key/value pair applied as a tag to the file\. Only applicable if the step type is `TAG`\.  
Type: String  
Length Constraints: Maximum length of 65536\.  
Required: No

 ** StepType **   <a name="TransferFamily-Type-ExecutionStepResult-StepType"></a>
One of the available step types\.  
+  *COPY*: Copy the file to another location\.
+  *CUSTOM*: Perform a custom step with an AWS Lambda function target\.
+  *DELETE*: Delete the file\.
+  *TAG*: Add a tag to the file\.
Type: String  
Valid Values:` COPY | CUSTOM | TAG | DELETE`   
Required: No

## See Also<a name="API_ExecutionStepResult_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ExecutionStepResult) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ExecutionStepResult) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ExecutionStepResult) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ExecutionStepResult) 
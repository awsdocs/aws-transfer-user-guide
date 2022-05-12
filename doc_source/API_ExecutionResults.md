# ExecutionResults<a name="API_ExecutionResults"></a>

Specifies the steps in the workflow, as well as the steps to execute in case of any errors during workflow execution\.

## Contents<a name="API_ExecutionResults_Contents"></a>

 ** OnExceptionSteps **   <a name="TransferFamily-Type-ExecutionResults-OnExceptionSteps"></a>
Specifies the steps \(actions\) to take if errors are encountered during execution of the workflow\.  
Type: Array of [ExecutionStepResult](API_ExecutionStepResult.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** Steps **   <a name="TransferFamily-Type-ExecutionResults-Steps"></a>
Specifies the details for the steps that are in the specified workflow\.  
Type: Array of [ExecutionStepResult](API_ExecutionStepResult.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## See Also<a name="API_ExecutionResults_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ExecutionResults) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ExecutionResults) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ExecutionResults) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ExecutionResults) 
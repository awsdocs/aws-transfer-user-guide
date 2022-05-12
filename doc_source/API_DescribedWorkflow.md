# DescribedWorkflow<a name="API_DescribedWorkflow"></a>

Describes the properties of the specified workflow

## Contents<a name="API_DescribedWorkflow_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-DescribedWorkflow-Arn"></a>
Specifies the unique Amazon Resource Name \(ARN\) for the workflow\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** Description **   <a name="TransferFamily-Type-DescribedWorkflow-Description"></a>
Specifies the text description for the workflow\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[\w- ]*$`   
Required: No

 ** OnExceptionSteps **   <a name="TransferFamily-Type-DescribedWorkflow-OnExceptionSteps"></a>
Specifies the steps \(actions\) to take if errors are encountered during execution of the workflow\.  
Type: Array of [WorkflowStep](API_WorkflowStep.md) objects  
Array Members: Maximum number of 8 items\.  
Required: No

 ** Steps **   <a name="TransferFamily-Type-DescribedWorkflow-Steps"></a>
Specifies the details for the steps that are in the specified workflow\.  
Type: Array of [WorkflowStep](API_WorkflowStep.md) objects  
Array Members: Maximum number of 8 items\.  
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedWorkflow-Tags"></a>
Key\-value pairs that can be used to group and search for workflows\. Tags are metadata attached to workflows for any purpose\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** WorkflowId **   <a name="TransferFamily-Type-DescribedWorkflow-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: No

## See Also<a name="API_DescribedWorkflow_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedWorkflow) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedWorkflow) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedWorkflow) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedWorkflow) 
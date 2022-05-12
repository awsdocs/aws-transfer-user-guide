# ListedWorkflow<a name="API_ListedWorkflow"></a>

Contains the ID, text description, and Amazon Resource Name \(ARN\) for the workflow\.

## Contents<a name="API_ListedWorkflow_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-ListedWorkflow-Arn"></a>
Specifies the unique Amazon Resource Name \(ARN\) for the workflow\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: No

 ** Description **   <a name="TransferFamily-Type-ListedWorkflow-Description"></a>
Specifies the text description for the workflow\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[\w- ]*$`   
Required: No

 ** WorkflowId **   <a name="TransferFamily-Type-ListedWorkflow-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: No

## See Also<a name="API_ListedWorkflow_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedWorkflow) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedWorkflow) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedWorkflow) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedWorkflow) 
# WorkflowDetail<a name="API_WorkflowDetail"></a>

Specifies the workflow ID for the workflow to assign and the execution role that's used for executing the workflow\.

In addition to a workflow to execute when a file is uploaded completely, `WorkflowDetails` can also contain a workflow ID \(and execution role\) for a workflow to execute on partial upload\. A partial upload occurs when a file is open when the session disconnects\.

## Contents<a name="API_WorkflowDetail_Contents"></a>

 ** ExecutionRole **   <a name="TransferFamily-Type-WorkflowDetail-ExecutionRole"></a>
Includes the necessary permissions for S3, EFS, and Lambda operations that Transfer can assume, so that all workflow steps can operate on the required resources  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: Yes

 ** WorkflowId **   <a name="TransferFamily-Type-WorkflowDetail-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: Yes

## See Also<a name="API_WorkflowDetail_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/WorkflowDetail) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/WorkflowDetail) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/WorkflowDetail) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/WorkflowDetail) 
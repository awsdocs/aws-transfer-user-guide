# WorkflowDetails<a name="API_WorkflowDetails"></a>

Container for the `WorkflowDetail` data type\. It is used by actions that trigger a workflow to begin execution\.

## Contents<a name="API_WorkflowDetails_Contents"></a>

 ** OnPartialUpload **   <a name="TransferFamily-Type-WorkflowDetails-OnPartialUpload"></a>
A trigger that starts a workflow if a file is only partially uploaded\. You can attach a workflow to a server that executes whenever there is a partial upload\.  
A *partial upload* occurs when a file is open when the session disconnects\.  
Type: Array of [WorkflowDetail](API_WorkflowDetail.md) objects  
Array Members: Maximum number of 1 item\.  
Required: No

 ** OnUpload **   <a name="TransferFamily-Type-WorkflowDetails-OnUpload"></a>
A trigger that starts a workflow: the workflow begins to execute after a file is uploaded\.  
To remove an associated workflow from a server, you can provide an empty `OnUpload` object, as in the following example\.  
 `aws transfer update-server --server-id s-01234567890abcdef --workflow-details '{"OnUpload":[]}'`   
Type: Array of [WorkflowDetail](API_WorkflowDetail.md) objects  
Array Members: Maximum number of 1 item\.  
Required: No

## See Also<a name="API_WorkflowDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/WorkflowDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/WorkflowDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/WorkflowDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/WorkflowDetails) 
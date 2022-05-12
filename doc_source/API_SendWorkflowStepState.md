# SendWorkflowStepState<a name="API_SendWorkflowStepState"></a>

Sends a callback for asynchronous custom steps\.

 The `ExecutionId`, `WorkflowId`, and `Token` are passed to the target resource during execution of a custom step of a workflow\. You must include those with their callback as well as providing a status\. 

## Request Syntax<a name="API_SendWorkflowStepState_RequestSyntax"></a>

```
{
   "ExecutionId": "string",
   "Status": "string",
   "Token": "string",
   "WorkflowId": "string"
}
```

## Request Parameters<a name="API_SendWorkflowStepState_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ExecutionId](#API_SendWorkflowStepState_RequestSyntax) **   <a name="TransferFamily-SendWorkflowStepState-request-ExecutionId"></a>
A unique identifier for the execution of a workflow\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$`   
Required: Yes

 ** [Status](#API_SendWorkflowStepState_RequestSyntax) **   <a name="TransferFamily-SendWorkflowStepState-request-Status"></a>
Indicates whether the specified step succeeded or failed\.  
Type: String  
Valid Values:` SUCCESS | FAILURE`   
Required: Yes

 ** [Token](#API_SendWorkflowStepState_RequestSyntax) **   <a name="TransferFamily-SendWorkflowStepState-request-Token"></a>
Used to distinguish between multiple callbacks for multiple Lambda steps within the same execution\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\w+`   
Required: Yes

 ** [WorkflowId](#API_SendWorkflowStepState_RequestSyntax) **   <a name="TransferFamily-SendWorkflowStepState-request-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: Yes

## Response Elements<a name="API_SendWorkflowStepState_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_SendWorkflowStepState_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You do not have sufficient access to perform this action\.  
HTTP Status Code: 400

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

 ** ThrottlingException **   
The request was denied due to request throttling\.  
 HTTP Status Code: 400  
HTTP Status Code: 400

## See Also<a name="API_SendWorkflowStepState_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/SendWorkflowStepState) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/SendWorkflowStepState) 
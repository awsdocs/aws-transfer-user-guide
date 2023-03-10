# ListWorkflows<a name="API_ListWorkflows"></a>

Lists all workflows associated with your AWS account for your current region\.

## Request Syntax<a name="API_ListWorkflows_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListWorkflows_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListWorkflows_RequestSyntax) **   <a name="TransferFamily-ListWorkflows-request-MaxResults"></a>
Specifies the maximum number of workflows to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListWorkflows_RequestSyntax) **   <a name="TransferFamily-ListWorkflows-request-NextToken"></a>
 `ListWorkflows` returns the `NextToken` parameter in the output\. You can then pass the `NextToken` parameter in a subsequent command to continue listing additional workflows\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

## Response Syntax<a name="API_ListWorkflows_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Workflows": [ 
      { 
         "Arn": "string",
         "Description": "string",
         "WorkflowId": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListWorkflows_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListWorkflows_ResponseSyntax) **   <a name="TransferFamily-ListWorkflows-response-NextToken"></a>
 `ListWorkflows` returns the `NextToken` parameter in the output\. You can then pass the `NextToken` parameter in a subsequent command to continue listing additional workflows\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [Workflows](#API_ListWorkflows_ResponseSyntax) **   <a name="TransferFamily-ListWorkflows-response-Workflows"></a>
Returns the `Arn`, `WorkflowId`, and `Description` for each workflow\.  
Type: Array of [ListedWorkflow](API_ListedWorkflow.md) objects

## Errors<a name="API_ListWorkflows_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidNextTokenException **   
The `NextToken` parameter that was passed is invalid\.  
HTTP Status Code: 400

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_ListWorkflows_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListWorkflows) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListWorkflows) 
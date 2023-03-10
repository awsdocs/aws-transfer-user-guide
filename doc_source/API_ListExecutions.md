# ListExecutions<a name="API_ListExecutions"></a>

Lists all in\-progress executions for the specified workflow\.

**Note**  
If the specified workflow ID cannot be found, `ListExecutions` returns a `ResourceNotFound` exception\.

## Request Syntax<a name="API_ListExecutions_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "WorkflowId": "string"
}
```

## Request Parameters<a name="API_ListExecutions_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListExecutions_RequestSyntax) **   <a name="TransferFamily-ListExecutions-request-MaxResults"></a>
Specifies the maximum number of executions to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListExecutions_RequestSyntax) **   <a name="TransferFamily-ListExecutions-request-NextToken"></a>
 `ListExecutions` returns the `NextToken` parameter in the output\. You can then pass the `NextToken` parameter in a subsequent command to continue listing additional executions\.  
 This is useful for pagination, for instance\. If you have 100 executions for a workflow, you might only want to list first 10\. If so, call the API by specifying the `max-results`:   
 `aws transfer list-executions --max-results 10`   
 This returns details for the first 10 executions, as well as the pointer \(`NextToken`\) to the eleventh execution\. You can now call the API again, supplying the `NextToken` value you received:   
 `aws transfer list-executions --max-results 10 --next-token $somePointerReturnedFromPreviousListResult`   
 This call returns the next 10 executions, the 11th through the 20th\. You can then repeat the call until the details for all 100 executions have been returned\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [WorkflowId](#API_ListExecutions_RequestSyntax) **   <a name="TransferFamily-ListExecutions-request-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: Yes

## Response Syntax<a name="API_ListExecutions_ResponseSyntax"></a>

```
{
   "Executions": [ 
      { 
         "ExecutionId": "string",
         "InitialFileLocation": { 
            "EfsFileLocation": { 
               "FileSystemId": "string",
               "Path": "string"
            },
            "S3FileLocation": { 
               "Bucket": "string",
               "Etag": "string",
               "Key": "string",
               "VersionId": "string"
            }
         },
         "ServiceMetadata": { 
            "UserDetails": { 
               "ServerId": "string",
               "SessionId": "string",
               "UserName": "string"
            }
         },
         "Status": "string"
      }
   ],
   "NextToken": "string",
   "WorkflowId": "string"
}
```

## Response Elements<a name="API_ListExecutions_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Executions](#API_ListExecutions_ResponseSyntax) **   <a name="TransferFamily-ListExecutions-response-Executions"></a>
Returns the details for each execution, in a `ListedExecution` array\.  
Type: Array of [ListedExecution](API_ListedExecution.md) objects

 ** [NextToken](#API_ListExecutions_ResponseSyntax) **   <a name="TransferFamily-ListExecutions-response-NextToken"></a>
 `ListExecutions` returns the `NextToken` parameter in the output\. You can then pass the `NextToken` parameter in a subsequent command to continue listing additional executions\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [WorkflowId](#API_ListExecutions_ResponseSyntax) **   <a name="TransferFamily-ListExecutions-response-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$` 

## Errors<a name="API_ListExecutions_Errors"></a>

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

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_ListExecutions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListExecutions) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListExecutions) 
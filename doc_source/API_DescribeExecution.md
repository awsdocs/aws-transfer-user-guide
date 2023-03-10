# DescribeExecution<a name="API_DescribeExecution"></a>

You can use `DescribeExecution` to check the details of the execution of the specified workflow\.

**Note**  
This API call only returns details for in\-progress workflows\.  
 If you provide an ID for an execution that is not in progress, or if the execution doesn't match the specified workflow ID, you receive a `ResourceNotFound` exception\.

## Request Syntax<a name="API_DescribeExecution_RequestSyntax"></a>

```
{
   "ExecutionId": "string",
   "WorkflowId": "string"
}
```

## Request Parameters<a name="API_DescribeExecution_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ExecutionId](#API_DescribeExecution_RequestSyntax) **   <a name="TransferFamily-DescribeExecution-request-ExecutionId"></a>
A unique identifier for the execution of a workflow\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$`   
Required: Yes

 ** [WorkflowId](#API_DescribeExecution_RequestSyntax) **   <a name="TransferFamily-DescribeExecution-request-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: Yes

## Response Syntax<a name="API_DescribeExecution_ResponseSyntax"></a>

```
{
   "Execution": { 
      "ExecutionId": "string",
      "ExecutionRole": "string",
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
      "LoggingConfiguration": { 
         "LoggingRole": "string",
         "LogGroupName": "string"
      },
      "PosixProfile": { 
         "Gid": number,
         "SecondaryGids": [ number ],
         "Uid": number
      },
      "Results": { 
         "OnExceptionSteps": [ 
            { 
               "Error": { 
                  "Message": "string",
                  "Type": "string"
               },
               "Outputs": "string",
               "StepType": "string"
            }
         ],
         "Steps": [ 
            { 
               "Error": { 
                  "Message": "string",
                  "Type": "string"
               },
               "Outputs": "string",
               "StepType": "string"
            }
         ]
      },
      "ServiceMetadata": { 
         "UserDetails": { 
            "ServerId": "string",
            "SessionId": "string",
            "UserName": "string"
         }
      },
      "Status": "string"
   },
   "WorkflowId": "string"
}
```

## Response Elements<a name="API_DescribeExecution_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Execution](#API_DescribeExecution_ResponseSyntax) **   <a name="TransferFamily-DescribeExecution-response-Execution"></a>
The structure that contains the details of the workflow' execution\.  
Type: [DescribedExecution](API_DescribedExecution.md) object

 ** [WorkflowId](#API_DescribeExecution_ResponseSyntax) **   <a name="TransferFamily-DescribeExecution-response-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$` 

## Errors<a name="API_DescribeExecution_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

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

## See Also<a name="API_DescribeExecution_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeExecution) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeExecution) 
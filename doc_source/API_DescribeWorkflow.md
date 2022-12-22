# DescribeWorkflow<a name="API_DescribeWorkflow"></a>

Describes the specified workflow\.

## Request Syntax<a name="API_DescribeWorkflow_RequestSyntax"></a>

```
{
   "WorkflowId": "string"
}
```

## Request Parameters<a name="API_DescribeWorkflow_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [WorkflowId](#API_DescribeWorkflow_RequestSyntax) **   <a name="TransferFamily-DescribeWorkflow-request-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$`   
Required: Yes

## Response Syntax<a name="API_DescribeWorkflow_ResponseSyntax"></a>

```
{
   "Workflow": { 
      "Arn": "string",
      "Description": "string",
      "OnExceptionSteps": [ 
         { 
            "CopyStepDetails": { 
               "DestinationFileLocation": { 
                  "EfsFileLocation": { 
                     "FileSystemId": "string",
                     "Path": "string"
                  },
                  "S3FileLocation": { 
                     "Bucket": "string",
                     "Key": "string"
                  }
               },
               "Name": "string",
               "OverwriteExisting": "string",
               "SourceFileLocation": "string"
            },
            "CustomStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string",
               "Target": "string",
               "TimeoutSeconds": number
            },
            "DecryptStepDetails": { 
               "DestinationFileLocation": { 
                  "EfsFileLocation": { 
                     "FileSystemId": "string",
                     "Path": "string"
                  },
                  "S3FileLocation": { 
                     "Bucket": "string",
                     "Key": "string"
                  }
               },
               "Name": "string",
               "OverwriteExisting": "string",
               "SourceFileLocation": "string",
               "Type": "string"
            },
            "DeleteStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string"
            },
            "TagStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string",
               "Tags": [ 
                  { 
                     "Key": "string",
                     "Value": "string"
                  }
               ]
            },
            "Type": "string"
         }
      ],
      "Steps": [ 
         { 
            "CopyStepDetails": { 
               "DestinationFileLocation": { 
                  "EfsFileLocation": { 
                     "FileSystemId": "string",
                     "Path": "string"
                  },
                  "S3FileLocation": { 
                     "Bucket": "string",
                     "Key": "string"
                  }
               },
               "Name": "string",
               "OverwriteExisting": "string",
               "SourceFileLocation": "string"
            },
            "CustomStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string",
               "Target": "string",
               "TimeoutSeconds": number
            },
            "DecryptStepDetails": { 
               "DestinationFileLocation": { 
                  "EfsFileLocation": { 
                     "FileSystemId": "string",
                     "Path": "string"
                  },
                  "S3FileLocation": { 
                     "Bucket": "string",
                     "Key": "string"
                  }
               },
               "Name": "string",
               "OverwriteExisting": "string",
               "SourceFileLocation": "string",
               "Type": "string"
            },
            "DeleteStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string"
            },
            "TagStepDetails": { 
               "Name": "string",
               "SourceFileLocation": "string",
               "Tags": [ 
                  { 
                     "Key": "string",
                     "Value": "string"
                  }
               ]
            },
            "Type": "string"
         }
      ],
      "Tags": [ 
         { 
            "Key": "string",
            "Value": "string"
         }
      ],
      "WorkflowId": "string"
   }
}
```

## Response Elements<a name="API_DescribeWorkflow_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Workflow](#API_DescribeWorkflow_ResponseSyntax) **   <a name="TransferFamily-DescribeWorkflow-response-Workflow"></a>
The structure that contains the details of the workflow\.  
Type: [DescribedWorkflow](API_DescribedWorkflow.md) object

## Errors<a name="API_DescribeWorkflow_Errors"></a>

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

## See Also<a name="API_DescribeWorkflow_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeWorkflow) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeWorkflow) 
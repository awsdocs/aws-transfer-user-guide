# CreateWorkflow<a name="API_CreateWorkflow"></a>

 Allows you to create a workflow with specified steps and step details the workflow invokes after file transfer completes\. After creating a workflow, you can associate the workflow created with any transfer servers by specifying the `workflow-details` field in `CreateServer` and `UpdateServer` operations\. 

## Request Syntax<a name="API_CreateWorkflow_RequestSyntax"></a>

```
{
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
   ]
}
```

## Request Parameters<a name="API_CreateWorkflow_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Description](#API_CreateWorkflow_RequestSyntax) **   <a name="TransferFamily-CreateWorkflow-request-Description"></a>
A textual description for the workflow\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[\w- ]*$`   
Required: No

 ** [OnExceptionSteps](#API_CreateWorkflow_RequestSyntax) **   <a name="TransferFamily-CreateWorkflow-request-OnExceptionSteps"></a>
Specifies the steps \(actions\) to take if errors are encountered during execution of the workflow\.  
For custom steps, the lambda function needs to send `FAILURE` to the call back API to kick off the exception steps\. Additionally, if the lambda does not send `SUCCESS` before it times out, the exception steps are executed\.
Type: Array of [WorkflowStep](API_WorkflowStep.md) objects  
Array Members: Maximum number of 8 items\.  
Required: No

 ** [Steps](#API_CreateWorkflow_RequestSyntax) **   <a name="TransferFamily-CreateWorkflow-request-Steps"></a>
Specifies the details for the steps that are in the specified workflow\.  
 The `TYPE` specifies which of the following actions is being taken for this step\.   
+  ** `COPY` ** \- Copy the file to another location\.
+  ** `CUSTOM` ** \- Perform a custom step with an AWS Lambda function target\.
+  ** `DECRYPT` ** \- Decrypt a file that was encrypted before it was uploaded\.
+  ** `DELETE` ** \- Delete the file\.
+  ** `TAG` ** \- Add a tag to the file\.
 Currently, copying and tagging are supported only on S3\. 
 For file location, you specify either the Amazon S3 bucket and key, or the Amazon EFS file system ID and path\.   
Type: Array of [WorkflowStep](API_WorkflowStep.md) objects  
Array Members: Maximum number of 8 items\.  
Required: Yes

 ** [Tags](#API_CreateWorkflow_RequestSyntax) **   <a name="TransferFamily-CreateWorkflow-request-Tags"></a>
Key\-value pairs that can be used to group and search for workflows\. Tags are metadata attached to workflows for any purpose\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateWorkflow_ResponseSyntax"></a>

```
{
   "WorkflowId": "string"
}
```

## Response Elements<a name="API_CreateWorkflow_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [WorkflowId](#API_CreateWorkflow_ResponseSyntax) **   <a name="TransferFamily-CreateWorkflow-response-WorkflowId"></a>
A unique identifier for the workflow\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^w-([a-z0-9]{17})$` 

## Errors<a name="API_CreateWorkflow_Errors"></a>

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

 ** ResourceExistsException **   
The requested resource does not exist\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

 ** ThrottlingException **   
The request was denied due to request throttling\.  
HTTP Status Code: 400

## Examples<a name="API_CreateWorkflow_Examples"></a>

### Example<a name="API_CreateWorkflow_Example_1"></a>

You can save workflow step information into a text file, and then use that file to create a workflow, as in the following example\. The following example assumes you have saved your workflow steps into ` example-file.json ` \(in the same folder from where you run the command\), and that you wish to create the workflow in the N\. Virginia \(us\-east\-1\) region\. 

#### <a name="w225ab1c52c14c26c15b3b5"></a>

```
aws transfer create-workflow --description "example workflow from a file" --steps file://example-file.json --region us-east-1
```

## See Also<a name="API_CreateWorkflow_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateWorkflow) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateWorkflow) 
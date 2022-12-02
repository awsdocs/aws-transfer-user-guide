# Use custom file\-processing steps<a name="custom-step-details"></a>

By using a custom file\-processing step, you can Bring Your Own file\-processing logic using AWS Lambda\. Upon file arrival, a Transfer Family server invokes a Lambda function that contains custom file\-processing logic, such as encrypting files, scanning for malware, or checking for incorrect file types\. In the following example, the target AWS Lambda function is used to process the output file from the previous step\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-custom.png)

**Note**  
For an example Lambda function, see [Example Lambda function for a custom workflow step](#example-workflow-lambda)

With a custom workflow step, you must configure the Lambda function to call the [SendWorkflowStepState](https://docs.aws.amazon.com/transfer/latest/userguide/API_SendWorkflowStepState.html) API operation\. `SendWorkflowStepState` notifies the workflow execution that the step was completed with either a success or a failure status\. The status of the `SendWorkflowStepState` API operation is used to either invoke an exception handler step or a nominal step in the linear sequence based on the outcome of the Lambda function\. 

If the Lambda function fails or times out, the step fails, and you see `StepErrored` in your CloudWatch logs\. If the Lambda function is part of the nominal step and the function responds to `SendWorkflowStepState` with `Status="FAILURE"` or times out, the flow continues with the exception handler steps\. In this case, the workflow does not continue to execute the remaining \(if any\) nominal steps\. For more details, see [Exception handling for a workflow](exception-workflow.md)\.

When you call the `SendWorkflowStepState` API operation, you must send the following parameters:

```
{
    "ExecutionId": "string",
    "Status": "string",
    "Token": "string",
    "WorkflowId": "string"
}
```

You can extract the `ExecutionId`, `Token`, and `WorkflowId` from the input event that is passed when the Lambda function executes \(examples are shown in the following sections\)\. The `Status` value can be either `SUCCESS` or `FAILURE`\. 

To be able to call the `SendWorkflowStepState` API operation from your Lambda function, you must use the latest version of the AWS SDK\.

## Using multiple Lambda functions consecutively<a name="multiple-lambdas"></a>

When you use multiple custom steps one after the other, the **File location** option works slightly differently than if you only use a single custom step\. Transfer Family doesn't support passing the Lambda\-processed file back to use as the next step's input\. So, if you have multiple custom steps all configured to use the `previous.file` option, they all use the same file location \(the input file location for the first custom step\)\.

**Note**  
If you have a pre\-defined step \(tag, copy, or delete\) after a custom step, and if the pre\-defined step is configured to use the `previous.file` setting, the pre\-defined step uses the same input file used by the custom step\. The processed file from the custom step is not passed to the pre\-defined step\. 

## Accessing a file after custom processing<a name="process-uploaded-file"></a>

If you are using Amazon S3 as your storage, and if your workflow includes a custom step that performs actions on the originally uploaded file, subsequent steps cannot access that file\. That is, any step after the custom step cannot reference the updated file from the custom step output\. For example, If you configure the `sourceFileLocation` for the step after custom step to be `${original.file}`, the step uses the original file location from when the server uploaded the file to storage\. And if you are using `${previous.file}` for that step, it will reuse the file location that custom step used as input\.

**Procedure that causes an error**

1. Step 1: upload file **example\-file**\.

1. Step 2: invoke a Lambda that changes **example\-file** in some way\.

1. Step 3: attempt to perform further processing on the updated version of **example\-file**\.

Step 3 causes an error\. For example, if step 3 is an attempt to copy the updated **example\-file**, you receive the following error:

```
{
    "type": "StepErrored",
    "details": {
        "errorType": "NOT_FOUND",
        "errorMessage": "ETag constraint not met (Service: null; Status Code: 412; Error Code: null; Request ID: null; S3 Extended Request ID: null; Proxy: null)",
        "stepType": "COPY",
        "stepName": "CopyFile"
    },
```

This error occurs because the custom step modifies the entity tag \(ETag\) for **example\-file**, so that it doesn't match the original file\.

**Note**  
This is not an issue if you are using Amazon EFS, as Amazon EFS doesn't use entity tags to identify files\.

## Example events sent to AWS Lambda upon file upload<a name="example-workflow-lambdas"></a>

The following examples show the events that are sent to AWS Lambda when a file upload is complete\. One example uses a Transfer Family server where the domain is configured with Amazon S3 and one where the domain uses Amazon EFS\. 

------
#### [ Custom step Amazon S3 domain ]

```
{
    "token": "MzI0Nzc4ZDktMGRmMi00MjFhLTgxMjUtYWZmZmRmODNkYjc0",
    "serviceMetadata": {
        "executionDetails": {
            "workflowId": "w-1234567890example",
            "executionId": "abcd1234-aa11-bb22-cc33-abcdef123456"
        },
        "transferDetails": {
            "sessionId": "36688ff5d2deda8c",
            "userName": "myuser",
            "serverId": "s-example1234567890"
        }
    },
    "fileLocation": {
        "domain": "S3",
        "bucket": "DOC-EXAMPLE-BUCKET",
        "key": "path/to/mykey",
        "eTag": "d8e8fca2dc0f896fd7cb4cb0031ba249",
        "versionId": null
    }
}
```

------
#### [ Custom step Amazon EFS domain ]

```
{
    "token": "MTg0N2Y3N2UtNWI5Ny00ZmZlLTk5YTgtZTU3YzViYjllNmZm",
    "serviceMetadata": {
        "executionDetails": {
            "workflowId": "w-1234567890example",
            "executionId": "abcd1234-aa11-bb22-cc33-abcdef123456"
        },
        "transferDetails": {
            "sessionId": "36688ff5d2deda8c",
            "userName": "myuser",
            "serverId": "s-example1234567890"
        }
    },
    "fileLocation": {
        "domain": "EFS",
        "fileSystemId": "fs-1234567",
        "path": "/path/to/myfile"
    }
}
```

------

## Example Lambda function for a custom workflow step<a name="example-workflow-lambda"></a>

The following Lambda function extracts the information regarding the execution status, and then calls the [SendWorkflowStepState](https://docs.aws.amazon.com/transfer/latest/userguide/API_SendWorkflowStepState.html) API operation to return the status to the workflow for the step—`SUCCESS` or `FAILURE`\. Before your function calls the `SendWorkflowStepState` API operation, you can configure Lambda to take an action based on your workflow logic\. 

```
import json
import boto3

transfer = boto3.client('transfer')

def lambda_handler(event, context):
    print(json.dumps(event))

    # call the SendWorkflowStepState API to notify the workflow about the step's SUCCESS or FAILURE status
    response = transfer.send_workflow_step_state(
        WorkflowId=event['serviceMetadata']['executionDetails']['workflowId'],
        ExecutionId=event['serviceMetadata']['executionDetails']['executionId'],
        Token=event['token'],
        Status='SUCCESS|FAILURE'
    )

    print(json.dumps(response))

    return {
      'statusCode': 200,
      'body': json.dumps(response)
    }
```
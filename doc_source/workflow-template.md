# Create a workflow from a template<a name="workflow-template"></a>

You can deploy an AWS CloudFormation stack that creates a workflow and a server from a template\. This procedure contains an example that you can use to quickly deploy a workflow\.

**To create an AWS CloudFormation stack that creates an AWS Transfer Family workflow and server**

1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. Save the following code to a file\.

------
#### [ YAML ]

   ```
   AWSTemplateFormatVersion: 2010-09-09
   Resources:
     SFTPServer:
       Type: 'AWS::Transfer::Server'
       Properties:
         WorkflowDetails:
           OnUpload:
             - ExecutionRole: workflow-execution-role-arn
               WorkflowId: !GetAtt
                 - TransferWorkflow
                 - WorkflowId
     TransferWorkflow:
       Type: AWS::Transfer::Workflow
       Properties:
         Description: Transfer Family Workflows Blog
         Steps:
           - Type: COPY
             CopyStepDetails:
               Name: copyToUserKey
               DestinationFileLocation:
                 S3FileLocation:
                   Bucket: archived-records
                   Key: ${transfer:UserName}/
               OverwriteExisting: 'TRUE'
           - Type: TAG
             TagStepDetails:
               Name: tagFileForArchive
               Tags:
                 - Key: Archive
                   Value: yes
           - Type: CUSTOM
             CustomStepDetails:
               Name: transferExtract
               Target: arn:aws:lambda:region:account-id:function:function-name
               TimeoutSeconds: 60
           - Type: DELETE
             DeleteStepDetails:
               Name: DeleteInputFile
               SourceFileLocation: '${original.file}'
         Tags:
           - Key: Name
             Value: TransferFamilyWorkflows
   ```

------
#### [ JSON ]

   ```
   {
       "AWSTemplateFormatVersion": "2010-09-09",
       "Resources": {
           "SFTPServer": {
               "Type": "AWS::Transfer::Server",
               "Properties": {
                   "WorkflowDetails": {
                       "OnUpload": [
                           {
                               "ExecutionRole": "workflow-execution-role-arn",
                               "WorkflowId": {
                                   "Fn::GetAtt": [
                                       "TransferWorkflow",
                                       "WorkflowId"
                                   ]
                               }
                           }
                       ]
                   }
               }
           },
           "TransferWorkflow": {
               "Type": "AWS::Transfer::Workflow",
               "Properties": {
                   "Description": "Transfer Family Workflows Blog",
                   "Steps": [
                       {
                           "Type": "COPY",
                           "CopyStepDetails": {
                               "Name": "copyToUserKey",
                               "DestinationFileLocation": {
                                   "S3FileLocation": {
                                       "Bucket": "archived-records",
                                       "Key": "${transfer:UserName}/"
                                   }
                               },
                               "OverwriteExisting": "TRUE"
                           }
                       },
                       {
                           "Type": "TAG",
                           "TagStepDetails": {
                               "Name": "tagFileForArchive",
                               "Tags": [
                                   {
                                       "Key": "Archive",
                                       "Value": "yes"
                                   }
                               ]
                           }
                       },
                       {
                           "Type": "CUSTOM",
                           "CustomStepDetails": {
                               "Name": "transferExtract",
                               "Target": "arn:aws:lambda:region:account-id:function:function-name",
                               "TimeoutSeconds": 60
                           }
                       },
                       {
                           "Type": "DELETE",
                           "DeleteStepDetails": {
                               "Name": "DeleteInputFile",
                               "SourceFileLocation": "${original.file}"
                           }
                       }
                   ],
                   "Tags": [
                       {
                           "Key": "Name",
                           "Value": "TransferFamilyWorkflows"
                       }
                   ]
               }
           }
       }
   }
   ```

------

1. Replace the following items with your actual values\.
   + Replace *`workflow-execution-role-arn`* with the ARN for an actual workflow execution role\. For example, `arn:aws:transfer:us-east-2:111122223333:workflow/w-1234567890abcdef0`
   + Replace `arn:aws:lambda:region:account-id:function:function-name` with the ARN for your Lambda function\. For example, `arn:aws:lambda:us-east-2:123456789012:function:example-lambda-idp`\.

1. Follow the instructions for deploying an AWS CloudFormation stack from an existing template in [Selecting a stack template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-using-console-create-stack-template.html) in the *AWS CloudFormation User Guide*\.

After the stack has been deployed, you can view details about it in the **Outputs** tab in the CloudFormation console\. The template creates a new AWS Transfer Family SFTP server that users service\-managed users, and a new workflow, and associates the workflow with the new server\.
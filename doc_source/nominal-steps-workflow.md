# Use predefined steps<a name="nominal-steps-workflow"></a>

When you're creating a workflow, you can choose to add one of the following predefined steps discussed in this topic\. You can also choose to add your own custom file\-processing steps\. For more information, see [Use custom file\-processing steps](custom-step-details.md)\.

**Topics**
+ [Copy file](#copy-step-details)
+ [Tag file](#tag-step-details)
+ [Delete file](#delete-step-details)
+ [Example tag and delete workflow](#sourcefile-workflow)

## Copy file<a name="copy-step-details"></a>

A copy file step creates a copy of the uploaded file in a new Amazon S3 location\. Currently, you can use a copy file step only with Amazon S3\.

The following copy file step copies files into the `test` folder in the `file-test` destination bucket\. 

If the copy file step is not the first step of your workflow, you can specify the **File location**\. By specifying the file location, you can copy either the file that was used in the previous step or the original file that was uploaded\. You can use this feature to make multiple copies of the original file while keeping the source file intact for file archival and records retention\. For an example, see [Example tag and delete workflow](#sourcefile-workflow)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-copy.png)

### Provide the bucket and key details<a name="copy-provide-bucket"></a>

You must provide the bucket name and a key for the destination of the copy file step\. The key can be either a path name or a file name\. Whether the key is treated as a path name or a file name is determined by whether you end the key with the forward slash \(`/`\) character\.

If the final character is `/`, your file is copied to the folder, and its name does not change\. If the final character is alphanumeric, your uploaded file is renamed to the key value\. In this case, if a file with that name already exists, the existing file is overwritten with the new one\. 

For example, if your key value is `test/`, your uploaded files are copied to the `test` folder\. If your key value is `test/today`, every file you upload is copied to a file named `today` in the `test` folder, and each succeeding file overwrites the previous one\.

**Note**  
Amazon S3 supports buckets and objects, and there is no hierarchy\. However, you can use prefixes and delimiters in object key names to imply a hierarchy and organize your data in a way similar to folders\.

### Use a named variable in a copy file step<a name="named-variable-copy"></a>

In a copy file step, you can use a variable to dynamically copy your files into user\-specific folders\. Currently, you can use `${transfer:UserName}` as a variable to copy files to a destination location for the given user who's uploading files\.

In the following example, if the user `richard-roe` uploads a file, it gets copied into the `file-test2/richard-roe/processed/` folder\. If the user `mary-major` uploads a file, it gets copied into the `file-test2/mary-major/processed/` folder\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-copy-dynamic.png)

## Tag file<a name="tag-step-details"></a>

To tag incoming files for further downstream processing, use a tag step\. Enter the value of the tag that you would like to assign to the incoming files\. Currently, the tag operation is supported only if you are using Amazon S3 for your Transfer Family server storage\.

The following example tag step assigns `scan_outcome` and `clean` as the tag key and value, respectively\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-tag.png)

## Delete file<a name="delete-step-details"></a>

To delete a processed file from a previous workflow step or to delete the originally uploaded file, use a delete file step\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-delete.png)

## Example tag and delete workflow<a name="sourcefile-workflow"></a>

The following example illustrates a workflow that tags incoming files that need to be processed by a downstream application, such as a data analytics platform\. After tagging the incoming file, the workflow then deletes the originally uploaded file to save on storage costs\.

------
#### [ Console ]

**Example tag and move workflow**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Workflows**\.

1. On the **Workflows** page, choose **Create workflow**\.

1. On the **Create workflow** page, enter a description\. This description appears on the **Workflows** page\.

1. Add the first step \(copy\)\.

   1. In the **Nominal steps** section, choose **Add step**\.

   1. Choose **Copy file**, then choose **Next**\.

   1. Enter a step name, then select a destination bucket and a key prefix\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-copy-first-step.png)

   1. Choose **Next**, then review the details for the step\. 

   1. Choose **Create step** to add the step and continue\.

1. Add the second step \(tag\)\.

   1. In the **Nominal steps** section, choose **Add step**\.

   1. Choose **Tag file**, then choose **Next**\.

   1. Enter a step name\.

   1. For **File location**, select **Tag the file created from previous step**\.

   1. Enter a **Key** and **Value**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-tag.png)

   1. Choose **Next**, then review the details for the step\. 

   1. Choose **Create step** to add the step and continue\.

1. Add the third step \(delete\)\.

   1. In the **Nominal steps** section, choose **Add step**\.

   1. Choose **Delete file**, then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-step-delete.png)

   1. Enter a step name\.

   1. For **File location**, select **Delete the original source file**\.

   1. Choose **Next**, then review the details for the step\. 

   1. Choose **Create step** to add the step and continue\.

1. Review the workflow configuration, and then choose **Create workflow**\. 

------
#### [ CLI ]

**Example tag and move workflow**

1. Save the following code into a file; for example, `tagAndMoveWorkflow.json`\. Replace each *user input placeholder* with your own information\. 

   ```
   [
         {
             "Type": "COPY",
             "CopyStepDetails": {
                 "Name": "CopyStep",
                 "DestinationFileLocation": {
                     "S3FileLocation": {
                         "Bucket": "DOC-EXAMPLE-BUCKET",
                         "Key": "test/"
                     }
                 }
             }
         },
         {
             "Type": "TAG",
             "TagStepDetails": {
                 "Name": "TagStep",
                 "Tags": [
                     {
                         "Key": "name",
                         "Value": "demo"
                     }
                 ],
                 "SourceFileLocation": "${previous.file}"
             }
         },
   {
           "Type": "DELETE",
           "DeleteStepDetails":{
             "Name":"DeleteStep",
             "SourceFileLocation": "${original.file}"
           }
     }
   
   ]
   ```

   The first step copies the uploaded file to a new Amazon S3 location\. The second step adds a tag \(key\-value pair\) to the file \(`previous.file`\) that was copied to the new location\. And, finally, the third step deletes the original file \(`original.file`\)\.

1. Create a workflow from the saved file\. Replace each *user input placeholder* with your own information\.

   ```
   aws transfer create-workflow --description "short-description" --steps file://path-to-file --region region-ID
   ```

   For example: 

   ```
   aws transfer create-workflow --description "copy-tag-delete workflow" --steps file://tagAndMoveWorkflow.json --region us-east-1
   ```

1. Update an existing server\.
**Note**  
This step assumes you already have a Transfer Family server and you want to associate a workflow with it\. If not, see [Creating a server](create-server.md)\. Replace each *user input placeholder* with your own information\.

   ```
   aws transfer update-server --server-id server-ID --region region-ID 
     --workflow-details '{"OnUpload":[{ "WorkflowId": "workflow-ID","ExecutionRole": "execution-role-ARN"}]}'
   ```

   For example:

   ```
   aws transfer update-server --server-id s-1234567890abcdef0 --region us-east-2 
     --workflow-details '{"OnUpload":[{ "WorkflowId": "w-abcdef01234567890","ExecutionRole": "arn:aws:iam::111111111111:role/nikki-wolf-execution-role"}]}'
   ```

------
# Create a workflow<a name="create-workflow"></a>

You can create a managed workflow by using the AWS Management Console, as described in this topic\. To make the workflow creation process as easy as possible, contextual help panels are available for most of the sections in the console\.

A workflow has two kinds of steps:
+ **Nominal steps** – Nominal steps are file\-processing steps that you want to apply to incoming files\. If you select more than one nominal step, each step is processed in a linear sequence\.
+ **Exception\-handling steps** – Exception handlers are file\-processing steps that AWS Transfer Family executes in case any nominal steps fail or result in validation errors\.

**Create a workflow**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Workflows**\.

1. On the **Workflows** page, choose **Create workflow**\.

1. On the **Create workflow** page, enter a description\. This description appears on the **Workflows** page\.

1. In the **Nominal steps** section, choose **Add step**\. Add one or more steps\.

   1. Choose a step type from the available options\. For more information about the various step types, see [Use predefined steps](nominal-steps-workflow.md)\.

   1. Choose **Next**, then configure parameters for the step\. 

   1. Choose **Next**, then review the details for the step\. 

   1. Choose **Create step** to add the step and continue\.

   1. Continue adding steps as needed\. The maximum number of steps in a workflow is 8\.

   1. After you have added all of the necessary nominal steps, scroll down to the **Exception handlers – *optional*** section, and choose **Add step**\. 
**Note**  
So that you are informed of failures in real time, we recommend that you set up exception handlers and steps to execute when your workflow fails\.

1. To configure exception handlers, add steps in the same manner as described previously\. If a file causes any step to throw an exception, your exception handlers are invoked one by one\. 

1. \(Optional\) Scroll down to the **Tags** section, and add tags for your workflow\.

1. Review the configuration, and choose **Create workflow**\. 
**Important**  
After you've created a workflow, you can't edit it, so make sure to review the configuration carefully\.

## Use PGP decryption in your workflow<a name="configure-decryption"></a>

Transfer Family has built\-in support for Pretty Good Privacy \(PGP\) decryption\. You can use PGP decryption on files that are uploaded over SFTP, FTPS, or FTP to Amazon Simple Storage Service \(Amazon S3\) or Amazon Elastic File System \(Amazon EFS\)\. 

To use PGP decryption, you must create and store the PGP key pairs that will be used for decryption of your files\. Your users can then encrypt files by using these PGP keys before uploading the files to your Transfer Family server\. After you receive the encrypted files, you can decrypt those files in your workflow\.

**To use PGP decryption in your workflow**

1. Install a PGP key\-generation application\. For more information, see [Generate PGP keys](key-management.md#generate-pgp-keys)\.

1. Generate a PGP key pair, and provide a passphrase to protect your private key\.
**Important**  
When you create a secret to store your PGP key, you must provide the passphrase and private key for the PGP key pair\. Transfer Family uses this passphrase and private key to decrypt the file\. For details about managing your PGP keys, see [Manage PGP keys](key-management.md#manage-pgp-keys)\.

1. Export your private key and save it to a file\.

1. Store your PGP key in AWS Secrets Manager\. For details about storing your PGP keys in Secrets Manager, see [Manage PGP keys](key-management.md#manage-pgp-keys)\.

1. Encrypt a file by using your PGP key pair\. If you are using the command line, run the following command\. To use this command, replace `username@example.com` with the email address that you used to create the PGP key pair\. Replace `testfile.txt` with the name of the file that you want to encrypt\. 

   ```
   gpg -e -r username@example.com --openpgp testfile.txt
   ```

   
**Important**  
You must use the `--openpgp` flag in this command\. By default, `gpg` produces encrypted files that do not conform to the [OpenPGP RFC4880](https://www.rfc-editor.org/rfc/rfc4880) standard\. If you don't use this flag, Transfer Family will be unable to decrypt your files\.

1. Upload the encrypted file to your Transfer Family server\.

1. Configure a decryption step in your workflow\. For more information, see [Decrypt file](nominal-steps-workflow.md#decrypt-step-details)\.

## Configure and execute a workflow<a name="configure-workflow"></a>

**To configure Transfer Family to run a workflow on uploaded files**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**\. 
   + To add the workflow to an existing server, choose the server that you want to use for your workflow\. 
   + Alternatively, create a new server and add the workflow to it\. For more information, see [Creating a server](create-server.md)\.

1. On the details page for the server, scroll down to the **Additional details** section, and then choose **Edit**\. 
**Note**  
 By default, servers do not have any associated workflows\. You use the **Additional details** section to associate a workflow with the selected server\. 

1. On the **Edit additional details** page, in the **Managed workflows** section, select a workflow to be run on all uploads\.
**Note**  
If you do not already have a workflow, choose **Create a new Workflow** to create one\.

   1. Choose the workflow ID to use\. 

   1. Choose an execution role\. This is the role that Transfer Family assumes when executing the workflow's steps\. For more information, see [IAM policies for workflows](workflow-execution-role.md)\. Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-addtoserver.png)

**To execute a workflow**

To execute a workflow, you upload a file to a Transfer Family server that you configured with an associated workflow\.

**Note**  
If you remove a workflow from a server and replace it with a new one, you must wait approximately 10 minutes before executing the new workflow\. The Transfer Family server caches the workflow details, and it takes 10 minutes for the server to refresh its cache\.

**Example**  

```
# Execute a workflow
> sftp bob@s-1234567890abcdef0.server.transfer.us-east-1.amazonaws.com

Connected to s-1234567890abcdef0.server.transfer.us-east-1.amazonaws.com.
sftp> put doc1.pdf
Uploading doc1.pdf to /DOC-EXAMPLE-BUCKET/home/users/bob/doc1.pdf
doc1.pdf                                                                    100% 5013KB 601.0KB/s   00:08    
sftp> exit
>
```

After your file has been uploaded, the action defined is performed on your file\. For example, if your workflow contains a copy step, the file is copied to the location that you defined in that step\. You can use Amazon CloudWatch Logs to track the steps that executed and their execution status\.

## View workflow details<a name="view-details-workflow"></a>

You can view details about previously created workflows or to workflow executions\. To view these details, you can use the console or the AWS Command Line Interface \(AWS CLI\)\. 

------
#### [ Console ]

**View workflow details**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Workflows**\. 

1. On the **Workflows** page, choose a workflow\. 

   The workflow details page opens\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-overview.png)

------
#### [ CLI ]

To view the workflow details, use the `describe-workflow` CLI command, as shown in the following example\. Replace the workflow ID `w-1234567890abcdef0` with your own value\. For more information, see [ describe\-workflow](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transfer/describe-workflow.html) in the *AWS CLI Command Reference*\.

```
# View Workflow details
> aws transfer describe-workflow --workflow-id w-1234567890abcdef0
{
    "Workflow": {
        "Arn": "arn:aws:transfer:us-east-1:111122223333:workflow/w-1234567890abcdef0",
        "WorkflowId": "w-1234567890abcdef0",
        "Name": "Copy file to shared_files",
        "Steps": [
            {
                "Type": "COPY",
                "CopyStepDetails": {
                "Name": "Copy to shared",
                "FileLocation": {
                    "S3FileLocation": {
                        "Bucket": "DOC-EXAMPLE-BUCKET",
                        "Key": "home/shared_files/"
                    }
                }
                }
            }
        ],
        "OnException": {}
    }
}
```

------
# Tutorial: Setting up a managed workflow for decrypting a file<a name="workflow-decrypt-tutorial"></a>

This tutorial illustrates how to set up a managed workflow that contains a decrypt step,and then upload an encrypted file to an Amazon S3 bucket, and view the decrypted file in another Amazon S3 bucket\.

**Contents**
+ [Step 1: Configure an execution role](#create-example-execution-role)
+ [Step 2: Create a managed workflow](#create-example-workflow)
+ [Step 4: Create a PGP key pair](#create-example-pgp-key-pair)
+ [Step 5: Store the PGP private key in AWS Secrets Manager](#output-private-key-to-secrets)
+ [Step 6: Encrypt a file](#encrypt-example-file)
+ [Step 7: Run the workflow and view the results](#test-decrypt-workflow)

## Step 1: Configure an execution role<a name="create-example-execution-role"></a>

We need to create an IAM role that Transfer Family can use to launch a workflow\. The process of creating a role is described in [Create a user role](requirements-roles.md#role-create-procedure)\.

**Note**  
As part of creating an execution role, make sure to establish a trust relationship between the execution role and Transfer Family, as described in [To establish a trust relationship](requirements-roles.md#establish-trust-transfer)\.

The following role contains all the required permissions to successfully execute the workflow we will create in this tutorial\.

**Note**  
Not every workflow requires every permission listed in this example\. You can limit permissions based on the types of steps in your specific workflow\. The permissions needed for each predefined step type are described in [Use predefined steps](nominal-steps-workflow.md)\. The permissions needed for a custom step are described in [IAM permissions for a custom step](custom-step-details.md#custom-step-iam)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CopyRead",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectTagging"
            ],
            "Resource": "arn:aws:s3:::SOURCE-BUCKET-NAME/*"
        },
        {
            "Sid": "CopyWrite",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectTagging"
            ],
            "Resource": "arn:aws:s3:::DECRYPTED-FILES-BUCKET/*"
        },
        {
            "Sid": "CopyList",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": [
                "arn:aws:s3:::SOURCE-BUCKET-NAME",
                "arn:aws:s3:::DECRYPTED-FILES-BUCKET"
            ]
        },
        {
            "Sid": "Tag",
            "Effect": "Allow",
            "Action": [
                "s3:PutObjectTagging",
                "s3:PutObjectVersionTagging"
            ],
            "Resource": "arn:aws:s3:::DECRYPTED-FILES-BUCKET/*",
            "Condition": {
                "StringEquals": {
                    "s3:RequestObjectTag/Archive": "yes"
                }
            }
        },
        {
            "Sid": "HomeDirObjectAccess",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObjectVersion",
                "s3:DeleteObject",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::DECRYPTED-FILES-BUCKET/*"
        },
        {
            "Sid": "Delete",
            "Effect": "Allow",
             "Action": [
                "s3:DeleteObjectVersion",
                "s3:DeleteObject"
            ]
        },   
        {
            "Sid": "Decrypt",
            "Effect": "Allow",
            "Action": [
                "secretsmanager:GetSecretValue"
            ],
            "Resource": "arn:aws:secretsmanager:region:account-ID:secret:aws/transfer/*"
        }
    ]
}
```

## Step 2: Create a managed workflow<a name="create-example-workflow"></a>

 Now we need to create a workflow that contains a decrypt step\.

**To create a workflow that contains a decrypt step**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. Select **Workflows**, and select **Create workflow**\. 

1. Enter the following details:
   + Enter a description, for example **Decrypt workflow example**\.
   + In **Nominal steps**, select **Add step** and select **Next**\.

1. For step type, select **Decrypt file**\.

1. <a name="configure-destination-details"></a>On the **Configure parameters** screen, specify the following:
   + Enter a descriptive step name \(spaces are not allowed\), for example **decrypt\-step**\.
   + For the **Destination for decrypted files**, choose Amazon S3\.
   + For the **Destination bucket name**, choose the same Amazon S3 bucket we specified as *DESTINATION\-BUCKET\-NAME* in the IAM policy we created in Step 1\.
   + For the **Destination key prefix**, enter the name of the folder to store your decrypted files, for example, **DECRYPTED\-FILES\-BUCKET/**\.
**Note**  
Make sure to add a trailing slash \(**/**\)\.
   + For this tutorial, we are leaving **Overwrite existing** cleared\. This means if you try to decrypt a file with the identical name of an existing file, the workflow processing stops, and the new file is not processed\.

   Select **Next** to move onto the review screen\.

1. Note the details for the step, and when you are ready, select **Create step**\.

1. Our workflow only has the single decrypt step\. Select **Create workflow** to create the new workflow\.

Note the workflow ID for your new workflow\. For the tutorial, we are using `w-1234abcd5678efghi` as the example ID\. Next, you must attach the workflow to a server\. For the tutorial, we are attaching the workflow to an existing Transfer Family server\. Alternately, you can create a new server to use with your workflow\.

## Step 3: Add the workflow to a server and create a user<a name="add-workflow-to-server"></a>

Now that we have a workflow with a decrypt step, we must associate it with a Transfer Family server\. Also, we need to create a user that can SFTP into the server and trigger the workflow to run\.

**To configure a Transfer Family server to run a workflow**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**, and select a server from the list\.

1. On the details page for the server, scroll down to the **Additional details** section, and then choose **Edit**\. 

1. On the **Edit additional details** page, in the **Managed workflows** section, select your workflow, and select a corresponding execution role\.
   + In the **Workflow for complete file uploads** choose the workflow we created in [Step 2: Create a managed workflow](#create-example-workflow), **w\-1234abcd5678efghi**\.
   + In the **Managed workflows execution role** field, select the IAM role that we created in [Step 1: Configure an execution role](#create-example-execution-role)\.

1. Scroll to the bottom of the page and select **Save** to save your changes\.

Note the ID for the server that you are using: the name of the AWS Secrets Manager secret that you use to store your PGP keys is based on the server ID\.

**To add a user that can trigger the workflow**

1. Continuing from the previous procedure, you should be on the server details page for the server we are using for the decrypt workflow\.

1. Scroll down to the **Users** section, and select **Add user**\. 

1. For your new user, enter the following details:
   + For **Username**, enter **decrypt\-user**\.
   + For **Role**, choose a user role that can access your server\.
   + For **Home directory**, choose a bucket that the user can access\. For the tutorial, we are using *SOURCE\-BUCKET\-NAME*, but you need to replace this with an actual Amazon S3 bucket that you can access\.
   + For **SSH public keys**, paste in a public key that corresponds to a private key that you have\. For details, see [Generate SSH keys](key-management.md#sshkeygen)\.

1. Select **Add** to save your new user\.

Note the names of your Transfer Family users for this server: the secret is also based on the name of the user\. Note, however, that for simplicity, in the tutorial, we are using a default secret that can be used by any user of the server\.

## Step 4: Create a PGP key pair<a name="create-example-pgp-key-pair"></a>

Use one of the [Supported PGP clients](key-management.md#pgp-key-clients) to generate a PGP key pair\. This process is described in detail in [Generate PGP keys](key-management.md#generate-pgp-keys)\.

**To generate a PGP key pair**

1. For the tutorial, we used **gpg \(GnuPG\) 2\.0\.22**\. For this client, we run the following command, and provide an email address and a passphrase\. You can use any name or email address you like: just remember the values you use, because you need to enter them later in the tutorial\.

   ```
   gpg --gen-key
   ```

1. We now export the private key by running the following command, replacing *user@example\.com* with the email address you used when you generated the key:

   ```
   gpg --output workflow-tutorial-key.pgp --armor --export-secret-key user@example.com
   ```

   This exports the private key into the **workflow\-tutorial\-key\.pgp** file: you can name the output file anything you like\. You can also delete the private key file after you have added it to AWS Secrets Manager\.

## Step 5: Store the PGP private key in AWS Secrets Manager<a name="output-private-key-to-secrets"></a>

We need to store the private key to Secrets Manager, in a very specific way, so that the workflow can find it when it runs a decrypt step on an uploaded file\.

**To create store a PGP private key in Secrets Manager**

1. Sign in to the AWS Management Console and open the AWS Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. In the left navigation pane, choose **Secrets**\. 

1. On the **Secrets** page, choose **Store a new secret**\.

1. On the **Choose secret type** page, for **Secret type**, select **Other type of secret**\.

1. In the **Key/value pairs** section, choose the **Key/value** tab\.
   + **Key** – Enter **PGPPrivateKey**\.
   + **value** – Paste the text of your private key into the value field\.

1. Select **Add row** and in the **Key/value pairs** section, choose the **Key/value** tab\.
   + **Key** – Enter **PGPPassphrase**\.
   + **value** – Enter the passphrase you used when we generated our PGP key pair in [Step 4: Create a PGP key pair](#create-example-pgp-key-pair)\.

1. Choose **Next**\.

1. On the **Configure secret** page, enter a name and description for your secret\. For the tutorial, we are creating a default secret\. Assuming the server ID is `s-11112222333344445`, name the secret **aws/transfer/s\-11112222333344445/@pgp\-default**\. You can enter any text you like for the description\.
**Note**  
To create a secret for the user we created earlier, we would name the secret **aws/transfer/s\-11112222333344445/decrypt\-user**\.

1. Choose **Next** and accept the defaults on the **Configure rotation** page\. Then choose **Next**\.

1. On the **Review** page, choose **Store** to create and store the secret\.

For more complete details on adding your PGP private key to Secrets Manager, see [Use AWS Secrets Manager to store your PGP key](key-management.md#store-pgp-key-details)\.

## Step 6: Encrypt a file<a name="encrypt-example-file"></a>

Use the `gpg` program to encrypt a file for use in your workflow\. Run the following command to encrypt a file:

```
gpg -e -r marymajor@example.com --openpgp testfile.txt
```

Note the following:
+ For the `-r` argument, specify the email address that you used when you created the PGP key pair\.
+ You *must* use the `--openpgp` flag, so that the encrypted file conforms to the [OpenPGP RFC4880](https://www.rfc-editor.org/rfc/rfc4880) standard\. If you don't use this flag, Transfer Family will be unable to decrypt your file\.
+ The command creates a file named **testfile\.txt\.gpg** in the same location as **testfile\.txt**\.

## Step 7: Run the workflow and view the results<a name="test-decrypt-workflow"></a>

To run the workflow, we connect to the Transfer Family server with the user created in Step 3\. We then look in the Amazon S3 bucket that we specified in [Step 2\.5 configure destination parameters](#configure-destination-details) to see the decrypted file\.

**To run the decrypt workflow**

1. On a Linux or macOS device, open a command terminal\.

1. Run the following command, replacing `s-11112222333344445.server.transfer.us-east-2.amazonaws.com` with your actual endpoint, and `transfer-key` with your user's SSH private key:

   ```
   sftp -i transfer-key decrypt-user@your-endpoint
   ```

   For example, if the private key is stored in `~/.ssh/decrypt-user`, and your endpoint is `s-11112222333344445.server.transfer.us-east-2.amazonaws.com`, the command is as follows:

   ```
   sftp -i  ~/.ssh/decrypt-user decrypt-user@s-11112222333344445.server.transfer.us-east-2.amazonaws.com
   ```

1. Run `pwd`, which should return the following:

   ```
   Remote working directory: /SOURCE-BUCKET-NAME/decrypt-user
   ```

   Your directory reflects the name of your Amazon S3 bucket\.

1. Run the following command to upload the file and trigger the workflow to run:

   ```
   put testfile.txt.gpg
   ```

1. Remember that for the destination of the decrypted files, we specified *DECRYPTED\-FILES\-BUCKET/* when we created the workflow\. Now, we can navigate to that folder and list the contents\.

   ```
   cd ../DECRYPTED-FILES-BUCKET
   ls
   ```

   The `ls` command should list the `testfile.txt`\. You can download this file and verify that it is the same as the original file that you encrypted earlier\.
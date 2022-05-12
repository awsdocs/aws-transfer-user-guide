# Tutorial: Getting started with AWS Transfer Family<a name="getting-started"></a>

Use this tutorial to get started with AWS Transfer Family \(Transfer Family\)\. You'll learn how to create an SFTP\-enabled server with publicly accessible endpoint using Amazon S3 storage, add a user with service\-managed authentication, and transfer a file with Cyberduck\.

**Contents**
+ [Prerequisites](#getting-started-prerequisites)
+ [Step 1: Sign in to the AWS Transfer Family console](#getting-started-logging-in)
+ [Step 2: Create an SFTP\-enabled server](#getting-started-server)
+ [Step 3: Add a service managed user](#getting-started-user)
+ [Step 4: Transfer a file using a client](#getting-started-transfer-file)

## Prerequisites<a name="getting-started-prerequisites"></a>

Before you begin, be sure to complete the requirements in [Setting up](setting-up.md)\. As part of this setup, you create an Amazon Simple Storage Service \(Amazon S3\) bucket and an AWS Identity and Access Management \(IAM\) user role\.

**Note**  
The role you create needs permissions defined in **AmazonS3FullAccess**, **AWSTransferConsoleFullAccess**, and **IAMFullAccess** policies\.   
**AmazonS3FullAccess** grants permissions to setup and use an Amazon S3 bucket\.
**AWSTransferConsoleFullAccess** grants permissions for your SFTP user to create Transfer Family resources\.
**IAMFullAccess** grants permissions to create the roles and policies you need\. 

## Step 1: Sign in to the AWS Transfer Family console<a name="getting-started-logging-in"></a>

**To sign in to Transfer Family**

1. Sign in to the AWS Management Console and open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. For **Account ID or alias**, enter your account ID or alias\.

1. For **IAM user name**, enter the name of the user role that you created for Transfer Family\.

1. For **Password**, enter your AWS account password\.

1. Choose **Sign in**\.

## Step 2: Create an SFTP\-enabled server<a name="getting-started-server"></a>

Secure Shell \(SSH\) File Transfer Protocol \(SFTP\) is a network protocol used for secure transfer of data over the internet\. The protocol supports the full security and authentication functionality of SSH\. It is widely used to exchange data, including sensitive information between business partners in a variety of industries such as financial services, healthcare, retail, and advertising\.

**To create an SFTP\-enabled server**

1. Select **Servers** from the Navigation pane then choose **Create server**\.

1. In **Choose protocols**, select **SFTP**, and then choose **Next**\.

1. In **Choose an identity provider**, choose **Service managed** to store user identities and keys in Transfer Family, and then choose **Next**\.

1. In **Choose an endpoint**, do the following:

   1. For **Endpoint type**, choose the **Publicly accessible** endpoint type\.

   1. For **Custom hostname**, choose **None**\.

   1. Choose **Next**\.

1. In **Choose a domain**, choose **Amazon S3**\.

1. In **Configure additional details**, do the following:

   1. For **CloudWatch logging**, choose **Create a new role** to allow Transfer Family to automatically create the IAM role, as long as you have the right permissions to create a new role\. The IAM role that is created is called `AWSTransferLoggingAccess`\.

   1. For **Cryptographic algorithm options**, choose a security policy that contains the cryptographic algorithms enabled for use by your server\. The default security policy is `TransferSecurityPolicy-2020-06`\.

   1. Choose **Next**\.

1. In **Review and create**, choose **Create server**\. You are taken to the **Servers** page\.

It can take a couple of minutes before the status for your new server changes to **Online**\. At that point, your server can perform file operations, but you'll need to create a user first\.

## Step 3: Add a service managed user<a name="getting-started-user"></a>

**To add a user to the SFTP\-enabled server**

1. On the **Servers** page, select the check box of the server that you want to add a user to\.

1. Choose **Add user**\.

1. In the **User configuration** section, for **Username**, enter the user name\. This user name must be a minimum of 3 and a maximum of 100 characters\. You can use the following characters in the user name: a–z, A\-Z, 0–9, underscore '\_', hyphen '\-', period '\.', and at sign "@"\. The user name can't start with a hyphen, period, or at sign\.

1. For **Access**, choose the IAM role that you previously created that provides access to your Amazon S3 bucket\.

   You created this IAM role using the procedure in [Create an IAM role and policy](requirements-roles.md)\. That IAM role includes an IAM policy that provides access to your Amazon S3 bucket\. It also includes a trust relationship with the AWS Transfer Family service, defined in another IAM policy\.
**Note**  
The IAM role for the service managed user must contain the permissions to access the desired bucket\. Permissions to access the desired bucket are covered within **S3FullAccess** which grants administrator level permissions to S3 resources\.

1. For **Policy**, choose **None**\.

1. For **Home directory**, choose the Amazon S3 bucket to store the data to transfer using AWS Transfer Family\. Enter the path to the `home` directory where your user lands when they log in using their client\.

   If you leave this parameter blank, the `root` directory of your Amazon S3 bucket is used\. In this case, make sure that your IAM role provides access to this `root` directory\.
**Note**  
We recommend that you choose a directory path that contains the user name of the user, which enables you to effectively use a session policy\. The session policy limits user access in the Amazon S3 bucket to that user's `home` directory\.

1. For **Restricted**, select the check box so that your users can't access anything outside of that folder and can't see the Amazon S3 bucket or folder name\.
**Note**  
When assigning the user a home directory and restricting the user to that home directory, this should be sufficient enough to lock down the user's access to the designated folder\. Use a session policy when you need to apply further controls\.

1. For **SSH public key**, enter the public SSH key portion of the SSH key pair\.

   Your key is validated by the service before you can add your new user\.
**Important**  
The format of the SSH public key is `ssh-rsa <string>`\. For instructions on how to generate an SSH key pair, see [Generate SSH keys](key-management.md#sshkeygen)\.

1. \(Optional\) For **Key** and **Value**, enter one or more tags as key\-value pairs, and choose **Add tag**\.

1. Choose **Add** to add your new user to the server that you chose\.

   The new user appears in the **Users** section of the **Server details** page\.

## Step 4: Transfer a file using a client<a name="getting-started-transfer-file"></a>

You transfer files over the AWS Transfer Family service by specifying the transfer operation in a client\. AWS Transfer Family supports several clients\. For details, see [Transferring files using a client](transfer-file.md)

This section contains procedures for using Cyberduck and OpenSSH\.

**Topics**
+ [Use Cyberduck](#cyberduck)
+ [Use OpenSSH](#openssh)

### Use Cyberduck<a name="cyberduck"></a>

**To transfer files over AWS Transfer Family using Cyberduck**

1. Open the [Cyberduck](https://cyberduck.io/download/) client\.

1. Choose **Open Connection**\.

1. In the **Open Connection** dialog box, choose **SFTP \(SSH File Transfer Protocol\)**\.

1. For **Server**, enter your server endpoint\. The server endpoint is located on the **Server details** page, see [View server details](configuring-servers-view-info.md)\.

1. For **Port number**, enter **22** for SFTP\.

1. For **Username**, enter the name for the user that you created in [Managing users](create-user.md)\.

1. For **SSH Private Key**, choose or enter the SSH private key\.

1. Choose **Connect**\.

1. Perform your file transfer\.

   Depending on where your files are, do one of the following:
   + In your local directory \(the source\), choose the files that you want to transfer, and drag and drop them into the Amazon S3 directory \(the target\)\.
   + In the Amazon S3 directory \(the source\), choose the files that you want to transfer, and drag and drop them into your local directory \(the target\)\.

### Use OpenSSH<a name="openssh"></a>

Use the instructions that follow to transfer files from the command line using OpenSSH\.

**Note**  
This client works only with an SFTP\-enabled server\.

**To transfer files over AWS Transfer Family using the OpenSSH command line utility**

1. On Linux or Macintosh, open a command terminal\.

1. At the prompt, enter the following command: `% sftp -i transfer-key sftp_user@service_endpoint`

   In the preceding command, `sftp_user` is the user name and `transfer-key` is the SSH private key\. Here, `service_endpoint` is the server's endpoint as shown in the AWS Transfer Family console for the selected server\.

   An `sftp` prompt should appear\.

1. \(Optional\) To view the user's home directory, enter the following command at the `sftp` prompt: `sftp> pwd`

1. On the next line, enter the following text: `sftp> cd /mybucket/home/sftp_user`

   In this getting\-started exercise, this Amazon S3 bucket is the target of the file transfer\.

1. On the next line, enter the following command: `sftp> put filename.txt`

   The `put` command transfers the file into the Amazon S3 bucket\.

   A message like the following appears, indicating that the file transfer is in progress, or complete\.

   `Uploading filename.txt to /my-bucket/home/sftp_user/filename.txt`

   `some-file.txt 100% 127 0.1KB/s 00:00`
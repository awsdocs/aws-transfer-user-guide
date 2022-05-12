# Create an Amazon EFS file system<a name="requirements-efs"></a>

AWS Transfer Family accesses Amazon Elastic File System \(Amazon EFS\) to service your users' transfer requests\. So you must provide an Amazon EFS file system as part of setting up your file transfer protocol\-enabled server\. You can use an existing file system, or you can create a new one\.

The following sections in the *Amazon Elastic File System User Guide* provide more information\.
+ For information about creating a new Amazon EFS file system, see [Getting started with Amazon Elastic File System](https://docs.aws.amazon.com/efs/latest/ug/getting-started.html) in the *Amazon Elastic File System User Guide*\.
+ For prerequisites to use Amazon EFS with Transfer Family, see [Prerequisites for using AWS Transfer Family with Amazon Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/using-aws-transfer-integration.html#prerequisites-aws-transfer)\.
+ To configure your Amazon EFS to work with AWS Transfer Family, see [ Configuring your Amazon EFS to work with AWS Transfer Family](https://docs.aws.amazon.com/efs/latest/ug/using-aws-transfer-integration.html#config-efs-aws-transfer-int)\.
+ To set file and directory permissions, see [ Setting file and directory permissions for AWS Transfer Family users](https://docs.aws.amazon.com/efs/latest/ug/using-aws-transfer-integration.html#efs-access-aws-transfer)\.

**Note**  
When you use a Transfer Family server and an Amazon EFS file system, the server and the file system must be in the same AWS Region\.

The server and the file system don't need to be in the same account\. If the server and file system are not in the same account, the file system policy must give explicit permission to the user role\. For information about using Amazon EFS, see [Using AWS Transfer Family to access files in your Amazon EFS file system](https://docs.aws.amazon.com/efs/latest/ug/using-aws-transfer-integration.html) in the *Amazon Elastic File System User Guide*\.

For information about how to set up multiple accounts, see [Managing the AWS accounts in your organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html) in the *AWS Organizations User Guide*\.

When you set up your users, you assign them each an IAM role\. This role determines the level of access that they have to your Amazon EFS file system\.

## Amazon EFS file ownership<a name="efs-file-ownership"></a>

Amazon EFS uses the Portable Operating System Interface \(POSIX\) file permission model to represent file ownership\.

 In POSIX, users in the system are categorized into three distinct permission classes: When you allow a user to access files stored in an Amazon EFS file system using AWS Transfer Family, you must assign them a “POSIX profile\.” This profile is used to determine their access to files and directories in the Amazon EFS file system\. 
+ User \(u\): Owner of the file or directory\. Usually, the creator of a file or directory is also the owner\.
+ Group \(g\): Set of users that need identical access to files and directories that they share\.
+ Others \(o\): All other users that have access to the system except for the owner and group members\. This permission class is also referred to as "Public\."

 In the POSIX permission model, every file system object \(files, directories, symbolic links, named pipes, and sockets\) is associated with the previously mentioned three sets of permissions\. Amazon EFS objects have a Unix\-style mode associated with them\. This mode value defines the permissions for performing actions on that object\. 

 Additionally, on Unix\-style systems, users and groups are mapped to numeric identifiers, which Amazon EFS uses to represent file ownership\. For Amazon EFS, objects are owned by a single owner and a single group\. Amazon EFS uses the mapped numeric IDs to check permissions when a user attempts to access a file system object\.

## Set up Amazon EFS users for Transfer Family<a name="configure-efs-users-permissions"></a>

Before you set your Amazon EFS users, you can do either of the following:
+ You can create users and set up their home folders in Amazon EFS\. See [Configure Transfer Family users on Amazon EFS](#set-up-efs-home-folders) for details\.
+ If you are comfortable adding a root user, you can [Create an Amazon EFS root user](#create-root-user-efs)\.

### Configure Transfer Family users on Amazon EFS<a name="set-up-efs-home-folders"></a>

Transfer Family maps the users to the UID/GID and directories you specify\. If the UID/GID/directories do not already exist in EFS, then you should create them before assigning them in Transfer to a user\. The details for creating Amazon EFS users is described in [Working with users, groups, and permissions at the Network File System \(NFS\) Level](https://docs.aws.amazon.com/efs/latest/ug/accessing-fs-nfs-permissions.html) in the *Amazon Elastic File System User Guide*\.

**Steps to set up Amazon EFS users in Transfer Family**

1. Map the EFS UID and GID for your user in Transfer Family using the [https://docs.aws.amazon.com/transfer/latest/userguide/API_PosixProfile.html](https://docs.aws.amazon.com/transfer/latest/userguide/API_PosixProfile.html) fields\.

1. If you want the user to start in a specific folder upon login, you can specify the EFS directory under the [https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#TransferFamily-CreateUser-request-HomeDirectory](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#TransferFamily-CreateUser-request-HomeDirectory) field\.

You can automate the process, by using a CloudWatch rule and Lambda function\. For an example Lambda function that interacts with EFS, see [Using Amazon EFS for AWS Lambda in your serverless applications](http://aws.amazon.com/blogs/compute/using-amazon-efs-for-aws-lambda-in-your-serverless-applications)\.

### Create an Amazon EFS root user<a name="create-root-user-efs"></a>

If your organization is comfortable for you to enable root user access via SFTP/FTPS for the configuration of your users, you can create a user who's UID and GID are 0 \(root user\), then use that root user to create folders and assign POSIX ID owners for rest of the users\. The advantage of this option is that there is no need to mount the Amazon EFS file system\.

Perform the steps described in [Adding Amazon EFS service\-managed users](service-managed-users.md#add-efs-user), and for both the User ID and Group ID, enter 0 \(zero\)\.

## Supported Amazon EFS commands<a name="efs-commands"></a>

The following commands are supported for Amazon EFS for AWS Transfer Family\.
+ `cd`
+ `ls`/`dir`
+ `pwd`
+ `put`
+ `get`
+ `rename`
+ `chown`: Only root \(that is, users with uid=0\) can change ownership and permissions of files and directories\.
+ `chmod`: Only root can change ownership and permissions of files and directories\.
+ `chgrp`: Supported either for root or for the file's owner who can only change a file's group to be one of their secondary groups\.
+  `ln -s`/`symlink`
+ `mkdir`
+ `rm`/`delete`
+ `rmdir`
+ `chmtime`
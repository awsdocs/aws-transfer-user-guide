# Transferring files using a client<a name="transfer-file"></a>

You transfer files over the AWS Transfer Family service by specifying the transfer operation in a client\. AWS Transfer Family supports the following clients:
+ OpenSSH \(macOS and Linux\)
**Note**  
This client works only with servers that are enabled for Secure Shell \(SSH\) File Transfer Protocol \(SFTP\)\.
+ WinSCP \(Microsoft Windows only\)
+ Cyberduck \(Windows, macOS, and Linux\)
+ FileZilla \(Windows, macOS, and Linux\)

The following limitations apply to every client:
+ Amazon S3 and Amazon EFS \(due to the NFSv4 protocol\) require filenames to be in UTF\-8 encoding\. Using different encoding can lead to unexpected results\. For Amazon S3, see [Object key naming guidelines](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-keys.html#object-key-guidelines)\.
+ For File Transfer Protocol over SSL \(FTPS\), only Explicit mode is supported\. Implicit mode is not supported\.
+ For File Transfer Protocol \(FTP\) and FTPS, only Passive mode is supported\.
+ For FTP and FTPS, only STREAM mode is supported\.
+ For FTP and FTPS, only Image/Binary mode is supported\.
+ For FTP and FTPS, TLS \- PROT C \(unprotected\) TLS for the data connection is the default but PROT C is not supported in the AWS Transfer Family FTPS protocol\. So for FTPS, you need to issue PROT P for your data operation to be accepted\.
+ If you are using Amazon S3 for your server's storage, and if your client contains an option to use multiple connections for a single transfer, make sure to disable the option\. Otherwise, large file uploads can fail in unpredictable ways\. Note that if you are using Amazon EFS as your storage backend, EFS *does* support multiple connections for a single transfer\.

The following is a list of available commands for FTP and FTPS:


| Available commands | 
| --- | 
| ABOR | FEAT | MLST | PASS | RETR | STOR | 
| AUTH | LANG | MKD | PASV | RMD | STOU | 
| CDUP | LIST | MODE | PBSZ | RNFR | STRU | 
| CWD | MDTM | NLST | PROT | RNTO | SYST | 
| DELE | MFMT | NOOP | PWD | SIZE | TYPE | 
| EPSV | MLSD | OPTS | QUIT | STAT | USER | 

**Note**  
APPE is not supported\.

For SFTP, the following operations are currently not supported for users that are using the logical home directory on servers that are using Amazon Elastic File System \(Amazon EFS\)\.


| Unsupported SFTP commands | 
| --- | 
| SSH\_FXP\_READLINK | SSH\_FXP\_SYMLINK | SSH\_FXP\_STAT when the requested file is a symlink | SSH\_FXP\_REALPATH when the requested path contains any symlink components | 

**Generate public\-private key pair**  
 Before you can transfer a file, you must have a public\-private key pair available\. If you have not previously generated a key pair, see [Generate SSH keys](key-management.md#sshkeygen)\. 

**Topics**
+ [Avoid `setstat` errors](#avoid-set-stat)
+ [Use OpenSSH](#openssh)
+ [Use WinSCP](#winscp)
+ [Use Cyberduck](#cyberduck)
+ [Use FileZilla](#filezilla)
+ [Use a Perl client](#using-clients-with-perl-modules)
+ [Post upload processing](#post-processing-upload)

## Avoid `setstat` errors<a name="avoid-set-stat"></a>

Some SFTP file transfer clients can attempt to change the attributes of remote files, including timestamp and permissions, using commands, such as SETSTAT when uploading the file\. However, these commands are not compatible with object storage systems, such as Amazon S3\. Due to this incompatibility, file uploads from these clients can result in errors even when the file is otherwise successfully uploaded\.
+ When you call the `CreateServer` or `UpdateServer` API, use the `ProtocolDetails` option `SetStatOption` to ignore the error that is generated when the client attempts to use SETSTAT on a file you are uploading to an S3 bucket\.
+ Set the value to `ENABLE_NO_OP` to have the Transfer Family server ignore the SETSTAT command, and upload files without needing to make any changes to your SFTP client\.
+ Note that while the `SetStatOption` `ENABLE_NO_OP` setting ignores the error, it *does* generate a log entry in CloudWatch Logs, so you can determine when the client is making a SETSTAT call\.

 For the API details for this option, see [ProtocolDetails](https://docs.aws.amazon.com/transfer/latest/userguide/API_ProtocolDetails.html)\.

## Use OpenSSH<a name="openssh"></a>

Use the instructions that follow to transfer files from the command line using OpenSSH\.

**Note**  
This client works only with an SFTP\-enabled server\.

**To transfer files over AWS Transfer Family using the OpenSSH command line utility**

1. On Linux or macOS, open a command terminal\.

1. At the prompt, enter the following command: 

   `sftp -i transfer-key sftp_user@service_endpoint`

   In the preceding command, `sftp_user` is the user name and `transfer-key` is the SSH private key\. Here, `service_endpoint` is the server's endpoint as shown in the AWS Transfer Family console for the selected server\.

   An `sftp` prompt should appear\.

1.  \(Optional\) To view the user's home directory, enter the following command at the `sftp` prompt: 

   `pwd` 

1. To upload a file from your file system to the Transfer Family server, use the `put` command\. For example, to upload `hello.txt` \(assuming that file is in your current directory on your file system\), run the following command at the `sftp` prompt: 

   `put hello.txt` 

   A message similar to the following appears, indicating that the file transfer is in progress, or complete\.

   `Uploading hello.txt to /my-bucket/home/sftp_user/hello.txt`

   `hello.txt 100% 127 0.1KB/s 00:00`

**Note**  
After your server is created, it can take a few minutes for the server endpoint hostname to be resolvable by the DNS service in your environment\.

## Use WinSCP<a name="winscp"></a>

Use the instructions that follow to transfer files from the command line using WinSCP\.

**Note**  
 If you are using WinSCP 5\.19, you can directly connect to Amazon S3 using your AWS credentials and upload/download files\. For more details, see [Connecting to Amazon S3 service](https://winscp.net/eng/docs/guide_amazon_s3)\. 

**To transfer files over AWS Transfer Family using WinSCP**

1. Open the WinSCP client\.

1. In the **Login** dialog box, for **File protocol**, choose a protocol: **SFTP** or **FTP**\.

   If you chose FTP, for **Encryption**, choose one of the following:
   + **No encryption** for FTP
   + **TLS/SSL Explicit encryption** for FTPS

1. For **Host name**, enter your server endpoint\. The server endpoint is located on the **Server details** page, see [View server details](configuring-servers-view-info.md)\.

1. For **Port number**, enter the following:
   + **22** for SFTP
   + **21** for FTP/FTPS

1. For **User name**, enter the name for the user that you created for your specific identity provider\.
**Note**  
The user name should be one of the users you created or configured for your identity provider\. AWS Transfer Family provides the following identity providers:  
[Working with service\-managed users](service-managed-users.md)
[Using the AWS Directory Service identity provider](directory-services-users.md)
[Working with custom identity providers](custom-identity-provider-users.md)

1. Choose **Advanced** to open the **Advanced Site Settings** dialog box\. In the **SSH** section, choose **Authentication**\.

1. For **Private key file**, browse for and choose the SSH private key file from your file system\.
**Note**  
If WinSCP offers to convert your SSH private key to the PPK format, choose **OK**\.

1. Choose **OK** to return to the **Login** dialog box, and then choose **Save**\.

1. In the **Save session as site** dialog box, choose **OK** to complete your connection setup\.

1. In the **Login** dialog box, choose **Tools**, and then choose **Preferences**\.

1. In the **Preferences** dialog box, for **Transfer**, choose **Endurance**\.

   For the **Enable transfer resume/transfer to temporary filename for** option, choose **Disable**\.
**Note**  
If you leave this option enabled, it increases upload costs, substantially decreasing upload performance\. It also can lead to failures of large file uploads\.

1. For **Transfer**, choose **Background**, and clear the **Use multiple connections for single transfer** check box\.
**Note**  
If you leave this option selected, large file uploads can fail in unpredictable ways\. For example, orphaned multipart uploads that incur Amazon S3 charges can be created\. Silent data corruption can also occur\.

1. Perform your file transfer\.

   You can use drag\-and\-drop methods to copy files between the target and source windows\. You can use toolbar icons to upload, download, delete, edit, or modify the properties of files in WinSCP\.

**Note**  
This note does not apply if you are using Amazon EFS for storage\.  
Commands that attempt to change attributes of remote files, including timestamps, are not compatible with object storage systems such as Amazon S3\. Therefore, if you are using Amazon S3 for storage, be sure to disable WinSCP timestamp settings \(or use the `SetStatOption` as described in [Avoid `setstat` errors](#avoid-set-stat)\) before you perform file transfers\. To do so, in the **WinSCP Transfer settings** dialog box, disable the **Set permissions** upload option and the **Preserve timestamp** common option\.

## Use Cyberduck<a name="cyberduck"></a>

Use the instructions that follow to transfer files from the command line using Cyberduck\.

**To transfer files over AWS Transfer Family using Cyberduck**

1. Open the [Cyberduck](https://cyberduck.io/download/) client\.

1. Choose **Open Connection**\.

1. In the **Open Connection** dialog box, choose a protocol: **SFTP \(SSH File Transfer Protocol\)**, **FTP\-SSL \(Explicit AUTH TLS\)**, or **FTP \(File Transfer Protocol\)**\.

1. For **Server**, enter your server endpoint\. The server endpoint is located on the **Server details** page\. For more information, see [View server details](configuring-servers-view-info.md)\.

1. For **Port number**, enter the following:
   + **22** for SFTP
   + **21** for FTP/FTPS

1. For **Username**, enter the name for the user that you created in [Managing users](create-user.md)\.

1. If SFTP is selected, for **SSH Private Key**, choose or enter the SSH private key\.

1. Choose **Connect**\.

1. Perform your file transfer\.

   Depending on where your files are, do one of the following:
   + In your local directory \(the source\), choose the files that you want to transfer, and drag and drop them into the Amazon S3 directory \(the target\)\.
   + In the Amazon S3 directory \(the source\), choose the files that you want to transfer, and drag and drop them into your local directory \(the target\)\.

## Use FileZilla<a name="filezilla"></a>

Use the instructions that follow to transfer files using FileZilla\.

**To set up FileZilla for a file transfer**

1. Open the FileZilla client\.

1. Choose **File**, and then choose **Site Manager**\.

1. In the **Site Manager** dialog box, choose **New site**\.

1. On the **General** tab, for **Protocol**, choose a protocol: **SFTP** or **FTP**\.

   If you chose FTP, for **Encryption**, choose one of the following:
   + **Only use plain FTP \(insecure\)** – for FTP
   + **Use explicit FTP over TLS if available** – for FTPS

1. For **Host name**, enter the protocol that you are using, followed by your server endpoint\. The server endpoint is located on the **Server details** page\. For more information, see [View server details](configuring-servers-view-info.md)\.
   + If you are using SFTP, enter: `sftp://hostname`
   +  If you are using FTPS, enter: `ftps://hostname` 

   Make sure to replace *hostname* with your actual server endpoint\.

1. For **Port number**, enter the following:
   + **22** for SFTP
   + **21** for FTP/FTPS

1. If SFTP is selected, for **Logon Type**, choose **Key file**\.

   For **Key file**, choose or enter the SSH private key\.

1. For **User**, enter the name for the user that you created in [Managing users](create-user.md)\.

1. Choose **Connect**\.

1. Perform your file transfer\.
**Note**  
If you interrupt a file transfer in progress, AWS Transfer Family might write a partial object in your Amazon S3 bucket\. If you interrupt an upload, check that the file size in the Amazon S3 bucket matches the file size of the source object before continuing\.

## Use a Perl client<a name="using-clients-with-perl-modules"></a>

If you use the NET::SFTP::Foreign perl client, you must set the `queue_size` to `1`\. For example:

`my $sftp = Net::SFTP::Foreign->new('user@s-12345.server.transfer.us-east-2.amazonaws.com', queue_size => 1);`

**Note**  
 This workaround is needed for revisions of `Net::SFTP::Foreign` prior to [1\.92\.02](https://metacpan.org/changes/release/SALVA/Net-SFTP-Foreign-1.93#L12)\. 

## Post upload processing<a name="post-processing-upload"></a>

You can view post upload processing information including Amazon S3 object metadata and event notifications\.

**Topics**
+ [Amazon S3 object metadata](#post-processing-S3-object-metadata)
+ [Amazon S3 event notifications](#post-processing-S3-event-notifications)

### Amazon S3 object metadata<a name="post-processing-S3-object-metadata"></a>

As a part of your object's metadata you see a key called `x-amz-meta-user-agent` whose value is `AWSTransfer` and `x-amz-meta-user-agent-id` whose value is `username@server-id`\. The `username` is the Transfer Family user who uploaded the file and `server-id` is the server used for the upload\. This information can be accessed using the [HeadObject](https://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectHEAD.html) operation on the S3 object inside your Lambda function\.



### Amazon S3 event notifications<a name="post-processing-S3-event-notifications"></a>

When an object is uploaded to your S3 bucket using Transfer Family, `RoleSessionName` is contained in the Requester field in the [S3 event notification structure](https://docs.aws.amazon.com/AmazonS3/latest/dev/notification-content-structure.html) as `[AWS:Role Unique Identifier]/username.sessionid@server-id`\. For example, the following are the contents for a sample Requester field from an S3 access log for a file that was copied to the S3 bucket\.

`arn:aws:sts::AWS-Account-ID:assumed-role/IamRoleName/username.sessionid@server-id`

In the Requester field above, it shows the IAM Role called `IamRoleName`\. For more information about configuring S3 event notifications, see [Configuring Amazon S3 event notifications](https://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html) in the *Amazon Simple Storage Service Developer Guide*\. For more information about AWS Identity and Access Management \(IAM\) role unique identifiers, see [Unique identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-unique-ids) in the *AWS Identity and Access Management User Guide*\.
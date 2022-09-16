# How AWS Transfer Family works<a name="how-aws-transfer-works"></a>

AWS Transfer Family is a fully managed AWS service that you can use to transfer files into and out of Amazon Simple Storage Service \(Amazon S3\) storage or Amazon Elastic File System \(Amazon EFS\) file systems over the following protocols:
+ Secure Shell \(SSH\) File Transfer Protocol \(SFTP\): version 3
+ File Transfer Protocol Secure \(FTPS\)
+ File Transfer Protocol \(FTP\)
+ Applicability Statement 2 \(AS2\)

 AWS Transfer Family supports up to 3 Availability Zones and is backed by an auto scaling, redundant fleet for your connection and transfer requests\. For an example on how to build for higher redundancy and minimize network latency by using Latency\-based routing, see [Minimize network latency with your AWS Transfer for SFTP servers](http://aws.amazon.com/blogs/storage/minimize-network-latency-with-your-aws-transfer-for-sftp-servers/)\. 

 Transfer Family Managed File Transfer Workflows \(MFTW\) is a fully managed, serverless File Transfer Workflow service that makes it easy to set up, run, automate, and monitor processing of files uploaded using AWS Transfer Family\. Customers can use MFTW to automate various processing steps such as copying, tagging, scanning, filtering, compressing/decompressing, and encrypting/decrypting the data that is transferred using Transfer Family\. This provides end to end visibility for tracking and auditability\. For more details, see [AWS Transfer Family managed workflows](transfer-workflows.md)\. 

You can get started with AWS Transfer Family by creating a file transfer protocol\-enabled server and then assigning users to use the server\. To service your AWS Transfer Family users' transfer requests, you create an AWS Identity and Access Management \(IAM\) role to access your Amazon S3 bucket or Amazon Elastic File System\.

To use AWS Transfer Family, you take the following high\-level steps:

1. Create an Amazon S3 bucket or Amazon EFS file system\.

    For information about using Amazon S3, see [Create an Amazon S3 bucket](requirements-S3.md)\. For information about using Amazon Elastic File System, see [Create an Amazon EFS file system](requirements-efs.md)\.

1. Create an IAM role that contains two IAM policies:
   + An IAM policy that includes the permissions to enable AWS Transfer Family to access your Amazon S3 bucket or Amazon EFS file system\. This IAM policy determines what level of access you provide your AWS Transfer Family users\.
   + An IAM policy to establish a trust relationship with AWS Transfer Family\.

   For more information about creating IAM policies, see [Managing access controls](users-policies.md)\.

1. \(Optional\) If you have your own registered domain, associate your registered domain with the server\.

   You can route file transfer protocol traffic to your server endpoint from a domain, such as `example.com`, or from a subdomain, such as `ftps.accounting.example.com`\. For more information, see [Working with custom hostnames](requirements-dns.md)\.

1. Create a Transfer Family server and specify the identity provider type used by the service to authenticate your users\.

    For more information about creating Transfer Family servers, see [Creating a server](create-server.md)\. For more information about identity provider types, see [Working with custom identity providers](custom-identity-provider-users.md)\. 

1. If you are working with a server with a service\-managed identity provider, as opposed to a custom identity provider, add one or more users\.

1. Open a file transfer protocol client and configure the connection to use the endpoint hostname for the server that you want to use\. You can get this hostname from the AWS Transfer Family console\.

AWS Transfer Family supports any standard file transfer protocol client\. Some commonly used clients are the following:
+ [OpenSSH](https://www.openssh.com/) – A Macintosh and Linux command line utility\.
+ [WinSCP](https://winscp.net/eng/download.php) – A Windows\-only graphical client\.
+  [Cyberduck](https://cyberduck.io/) – A Linux, Macintosh, and Microsoft Windows graphical client\.
+ [FileZilla](https://filezilla-project.org/) – A Linux, Macintosh, and Windows graphical client\.
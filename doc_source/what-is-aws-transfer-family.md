# What is AWS Transfer Family?<a name="what-is-aws-transfer-family"></a>

AWS Transfer Family is a secure transfer service that enables you to transfer files into and out of AWS storage services\. 

AWS Transfer Family supports transferring data from or to the following AWS storage services\. 
+ Amazon Simple Storage Service \(Amazon S3\) storage\. For information about Amazon S3, see [Getting started with Amazon Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html)\.
+ Amazon Elastic File System \(Amazon EFS\) Network File System \(NFS\) file systems\. For information about Amazon EFS, see [What Is Amazon Elastic File System?](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)

AWS Transfer Family supports transferring data over the following protocols:
+ Secure Shell \(SSH\) File Transfer Protocol \(SFTP\): version 3
+ File Transfer Protocol Secure \(FTPS\)
+ File Transfer Protocol \(FTP\)
+ Applicability Statement 2 \(AS2\)

**Note**  
 For FTP and FTPS data connections, the port range that Transfer Family uses to establish the data channel is 8192–8200\. 

File transfer protocols are used in data exchange workflows across different industries such as financial services, healthcare, advertising, and retail, among others\. Transfer Family simplifies the migration of file transfer workflows to AWS\.

The following are some common use cases for using Transfer Family with Amazon S3:
+ Data lakes in AWS for uploads from third parties such as vendors and partners\.
+ Subscription\-based data distribution with your customers\.
+ Internal transfers within your organization\.

The following are some common use cases for using Transfer Family with Amazon EFS:
+ Data distribution
+ Supply chain
+ Content management
+ Web serving applications

The following are some common use cases for using Transfer Family with AS2: 
+ Workflows with compliance requirements that rely on having data protection and security features built into the protocol
+ Supply chain logistics
+ Payments workflows
+ Business\-to\-business \(B2B\) transactions
+ Integrations with enterprise resource planning \(ERP\) and customer relationship management \(CRM\) systems

With Transfer Family, you get access to a file transfer protocol\-enabled server in AWS without the need to run any server infrastructure\. You can use this service to migrate your file transfer\-based workflows to AWS while maintaining your end users' clients and configurations as is\. You first associate your hostname with the server endpoint, then add your users and provision them with the right level of access\. After you do this, your users' transfer requests are serviced directly out of your Transfer Family server endpoint\.

Transfer Family provides the following benefits:
+ A fully managed service that scales in real time to meet your needs\.
+ You don't need to modify your applications or run any file transfer protocol infrastructure\.
+ With your data in durable Amazon S3 storage, you can use native AWS services for processing, analytics, reporting, auditing, and archival functions\.
+ With Amazon EFS as your data store, you get a fully managed elastic file system for use with AWS Cloud services and on\-premises resources\. Amazon EFS is built to scale on demand to petabytes without disrupting applications, growing and shrinking automatically as you add and remove files\. This helps eliminate the need to provision and manage capacity to accommodate growth\.
+ A fully managed, serverless File Transfer Workflow service that makes it easy to set up, run, automate, and monitor processing of files uploaded using AWS Transfer Family\.
+ There are no upfront costs, and you pay only for the use of the service\.

In the following sections, you can find a description of the different features of Transfer Family, a getting started tutorial, detailed instructions on how to set up the different protocol enabled servers, how to use different types of identity providers, and the service's API reference\.

To get started with Transfer Family, see the following:
+ [How AWS Transfer Family works](how-aws-transfer-works.md)
+ [Setting up](setting-up.md)
+ [Tutorial: Getting started with AWS Transfer Family](getting-started.md)
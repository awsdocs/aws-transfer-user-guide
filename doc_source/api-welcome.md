# Welcome to the AWS Transfer Family API<a name="api-welcome"></a>

AWS Transfer Family is a secure transfer service that you can use to transfer files into and out of Amazon Simple Storage Service \(Amazon S3\) storage over the following protocols:
+ Secure Shell \(SSH\) File Transfer Protocol \(SFTP\)
+ File Transfer Protocol Secure \(FTPS\)
+ File Transfer Protocol \(FTP\)

File transfer protocols are used in data exchange workflows across different industries such as financial services, healthcare, advertising, and retail, among others\. AWS Transfer Family simplifies the migration of file transfer workflows to AWS\.

To use the AWS Transfer Family service, you instantiate a server in the AWS Region of your choice\. You can create the server, list available servers, and update and delete servers\. The server is the entity that requests file operations from AWS Transfer Family\. Servers have a number of important properties\. The server is a named instance as identified by a system assigned `ServerId` identifier\. You can optionally assign a hostname, or even a custom hostname to a server\. The service bills for any instantiated servers \(even ones `OFFLINE`\), and for the amount of data transferred\.

Users must be known to the server that requests file operations\. A user as identified by their user name is assigned to a server\. User names are used to authenticate requests\. A server can have only one authentication method: `AWS_DIRECTORY_SERVICE`, `SERVICE_MANAGED`, `AWS_LAMBDA`, or `API_GATEWAY`\.

You can use any of the following identity provider types to authenticate users:
+ For `SERVICE_MANAGED`, an SSH public key is stored with the user's properties on a server\. A user can have one or more SSH public keys on file for the `SERVICE_MANAGED` authentication method\. When a client requests a file operation for `SERVICE_MANAGED` method, the client provides the user name and SSH private key, which is authenticated, and access is provided\.
+ You can manage user authentication and access with your Microsoft Active Directory groups by selecting the `AWS_DIRECTORY_SERVICE` authentication method\.
+ You can connect to a custom identity provider by using AWS Lambda\. Choose the `AWS_LAMBDA` authentication method\.
+ You can also authenticate user requests using a custom authentication method that provides both user authentication and access\. This method relies on the Amazon API Gateway to use your API call from your identity provider to validate user requests\. This method is referred to as `API_GATEWAY` in API calls, and as **Custom** in the console\. You might use this custom method to authenticate users against a directory service, a database name/password pair, or some other mechanism\.

Users are assigned a policy with a trust relationship between themselves and an Amazon S3 bucket\. They might be able to access all or part of a bucket\. For a server to act on a user's behalf, the server must inherit the trust relationship from the user\. An AWS Identity and Access Management \(IAM\) role is created that contains the trust relationship, and that role is assigned an `AssumeRole` action\. The server then can perform file operations as if it were the user\.

Users who have a `home` directory property set will have that directory \(or folder\) act as the target and source of file operations\. When no `home` directory is set, the bucket's `root` directory becomes the landing directory\.

Servers, users, and roles are all identified by their Amazon Resource Name \(ARN\)\. You can assign tags, which are key\-value pairs, to entities with an ARN\. Tags are metadata that can be used to group or search for these entities\. One example where tags are useful is for accounting purposes\.

The following conventions are observed in AWS Transfer Family ID formats:
+ `ServerId` values take the form `s-01234567890abcdef`\.
+ `SshPublicKeyId` values take the form `key-01234567890abcdef`\.

Amazon Resource Name \(ARN\) formats take the following form:
+ For servers, ARNs take the form `arn:aws:transfer:region:account-id:server/server-id`\.

  An example of a server ARN is: `arn:aws:transfer:us-east-1:123456789012:server/s-01234567890abcdef`\.
+ For users, ARNs take the form `arn:aws:transfer:region:account-id:user/server-id/username`\.

  An example is `arn:aws:transfer:us-east-1:123456789012:user/s-01234567890abcdef/user1`\.

DNS entries \(endpoints\) in use are as follows:
+ API endpoints take the form `transfer.region.amazonaws.com`\.
+ Server endpoints take the form `server.transfer.region.amazonaws.com`\.

For a list of Transfer Family endpoints by AWS Region, see the [AWS Transfer Family endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*\.

This API interface reference for AWS Transfer Family contains documentation for a programming interface that you can use to manage AWS Transfer Family\. The reference structure is as follows:
+ For the alphabetical list of API actions, see [Actions](API_Operations.md)\.
+ For the alphabetical list of data types, see [Data Types](API_Types.md)\.
+ For a list of common query parameters, see [Common Parameters](CommonParameters.md)\.
+ For descriptions of the error codes, see [Common Errors](CommonErrors.md)\.
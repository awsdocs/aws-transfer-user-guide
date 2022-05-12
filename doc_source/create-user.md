# Managing users<a name="create-user"></a>

In the following sections, you can find information about how to add users using AWS Transfer Family, AWS Directory Service for Microsoft Active Directory or a custom identity provider\.

If you use a service\-managed identity type, you add users to your file transfer protocol enabled server\. When you do so, each user name must be unique on your server\.

As part of each user's properties, you also store that user's Secure Shell \(SSH\) public key\. Doing so is required for key based authentication, which this procedure uses\. The private key is stored locally on your user's computer\. When your user sends an authentication request to your server by using a client, your server first confirms that the user has access to the associated SSH private key\. The server then successfully authenticates the user\.

In addition, you specify a user's home directory, or landing directory, and assign an AWS Identity and Access Management \(IAM\) role to the user\. Optionally, you can provide a session policy to limit user access only to the home directory of your Amazon S3 bucket\.

**Amazon EFS vs\. Amazon S3**  
Characteristics of each storage option:
+ To limit access: Amazon S3 supports session policies; Amazon EFS supports POSIX user, group, and secondary group IDs
+  Both support public/private keys 
+  Both support home directories 
+  Both support logical directories 
**Note**  
 For Amazon S3, most of the support for logical directories is via API/CLI\. You can use the **Restricted** check box in the console to lock down a user to their home directory, but you cannot specify a virtual directory structure\. 

**Topics**
+ [Working with service\-managed users](service-managed-users.md)
+ [Using the AWS Directory Service identity provider](directory-services-users.md)
+ [Working with custom identity providers](custom-identity-provider-users.md)
+ [Tutorial: Setting up an Amazon API Gateway method as a custom identity provider](gateway-api-tutorial.md)
# ListedUser<a name="API_ListedUser"></a>

Returns properties of the user that you specify\.

## Contents<a name="API_ListedUser_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-ListedUser-Arn"></a>
Provides the unique Amazon Resource Name \(ARN\) for the user that you want to learn about\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** HomeDirectory **   <a name="TransferFamily-Type-ListedUser-HomeDirectory"></a>
The landing directory \(folder\) for a user when they log in to the server using the client\.  
A `HomeDirectory` example is `/bucket_name/home/mydirectory`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: No

 ** HomeDirectoryType **   <a name="TransferFamily-Type-ListedUser-HomeDirectoryType"></a>
The type of landing directory \(folder\) that you want your users' home directory to be when they log in to the server\. If you set it to `PATH`, the user will see the absolute Amazon S3 bucket or EFS paths as is in their file transfer protocol clients\. If you set it `LOGICAL`, you need to provide mappings in the `HomeDirectoryMappings` for how you want to make Amazon S3 or Amazon EFS paths visible to your users\.  
Type: String  
Valid Values:` PATH | LOGICAL`   
Required: No

 ** Role **   <a name="TransferFamily-Type-ListedUser-Role"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that controls your users' access to your Amazon S3 bucket or Amazon EFS file system\. The policies attached to this role determine the level of access that you want to provide your users when transferring files into and out of your Amazon S3 bucket or Amazon EFS file system\. The IAM role should also contain a trust relationship that allows the server to access your resources when servicing your users' transfer requests\.  
The IAM role that controls your users' access to your Amazon S3 bucket for servers with `Domain=S3`, or your EFS file system for servers with `Domain=EFS`\.   
The policies attached to this role determine the level of access you want to provide your users when transferring files into and out of your S3 buckets or EFS file systems\.
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** SshPublicKeyCount **   <a name="TransferFamily-Type-ListedUser-SshPublicKeyCount"></a>
Specifies the number of SSH public keys stored for the user you specified\.  
Type: Integer  
Required: No

 ** UserName **   <a name="TransferFamily-Type-ListedUser-UserName"></a>
Specifies the name of the user whose ARN was specified\. User names are used for authentication purposes\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: No

## See Also<a name="API_ListedUser_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedUser) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedUser) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedUser) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedUser) 
# DescribedAccess<a name="API_DescribedAccess"></a>

Describes the properties of the access that was specified\.

## Contents<a name="API_DescribedAccess_Contents"></a>

 ** ExternalId **   <a name="TransferFamily-Type-DescribedAccess-ExternalId"></a>
A unique identifier that is required to identify specific groups within your directory\. The users of the group that you associate have access to your Amazon S3 or Amazon EFS resources over the enabled protocols using AWS Transfer Family\. If you know the group name, you can view the SID values by running the following command using Windows PowerShell\.  
 `Get-ADGroup -Filter {samAccountName -like "YourGroupName*"} -Properties * | Select SamAccountName,ObjectSid`   
In that command, replace *YourGroupName* with the name of your Active Directory group\.  
The regex used to validate this parameter is a string of characters consisting of uppercase and lowercase alphanumeric characters with no spaces\. You can also include underscores or any of the following characters: =,\.@:/\-  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^S-1-[\d-]+$`   
Required: No

 ** HomeDirectory **   <a name="TransferFamily-Type-DescribedAccess-HomeDirectory"></a>
The landing directory \(folder\) for a user when they log in to the server using the client\.  
A `HomeDirectory` example is `/bucket_name/home/mydirectory`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: No

 ** HomeDirectoryMappings **   <a name="TransferFamily-Type-DescribedAccess-HomeDirectoryMappings"></a>
Logical directory mappings that specify what Amazon S3 or Amazon EFS paths and keys should be visible to your user and how you want to make them visible\. You must specify the `Entry` and `Target` pair, where `Entry` shows how the path is made visible and `Target` is the actual Amazon S3 or Amazon EFS path\. If you only specify a target, it is displayed as is\. You also must ensure that your AWS Identity and Access Management \(IAM\) role provides access to paths in `Target`\. This value can only be set when `HomeDirectoryType` is set to *LOGICAL*\.  
In most cases, you can use this value instead of the session policy to lock down the associated access to the designated home directory \("`chroot`"\)\. To do this, you can set `Entry` to '/' and set `Target` to the `HomeDirectory` parameter value\.  
Type: Array of [HomeDirectoryMapEntry](API_HomeDirectoryMapEntry.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** HomeDirectoryType **   <a name="TransferFamily-Type-DescribedAccess-HomeDirectoryType"></a>
The type of landing directory \(folder\) you want your users' home directory to be when they log into the server\. If you set it to `PATH`, the user will see the absolute Amazon S3 bucket or EFS paths as is in their file transfer protocol clients\. If you set it `LOGICAL`, you need to provide mappings in the `HomeDirectoryMappings` for how you want to make Amazon S3 or EFS paths visible to your users\.  
Type: String  
Valid Values:` PATH | LOGICAL`   
Required: No

 ** Policy **   <a name="TransferFamily-Type-DescribedAccess-Policy"></a>
A session policy for your user so that you can use the same IAM role across multiple users\. This policy scopes down user access to portions of their Amazon S3 bucket\. Variables that you can use inside this policy include `${Transfer:UserName}`, `${Transfer:HomeDirectory}`, and `${Transfer:HomeBucket}`\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Required: No

 ** PosixProfile **   <a name="TransferFamily-Type-DescribedAccess-PosixProfile"></a>
The full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary groups IDs \(`SecondaryGids`\), that controls your users' access to your Amazon EFS file systems\. The POSIX permissions that are set on files and directories in your file system determine the level of access your users get when transferring files into and out of your Amazon EFS file systems\.  
Type: [PosixProfile](API_PosixProfile.md) object  
Required: No

 ** Role **   <a name="TransferFamily-Type-DescribedAccess-Role"></a>
Specifies the Amazon Resource Name \(ARN\) of the IAM role that controls your users' access to your Amazon S3 bucket or EFS file system\. The policies attached to this role determine the level of access that you want to provide your users when transferring files into and out of your Amazon S3 bucket or EFS file system\. The IAM role should also contain a trust relationship that allows the server to access your resources when servicing your users' transfer requests\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

## See Also<a name="API_DescribedAccess_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedAccess) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedAccess) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedAccess) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedAccess) 
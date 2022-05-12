# PosixProfile<a name="API_PosixProfile"></a>

The full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary groups IDs \(`SecondaryGids`\), that controls your users' access to your Amazon EFS file systems\. The POSIX permissions that are set on files and directories in your file system determine the level of access your users get when transferring files into and out of your Amazon EFS file systems\.

## Contents<a name="API_PosixProfile_Contents"></a>

 ** Gid **   <a name="TransferFamily-Type-PosixProfile-Gid"></a>
The POSIX group ID used for all EFS operations by this user\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 4294967295\.  
Required: Yes

 ** SecondaryGids **   <a name="TransferFamily-Type-PosixProfile-SecondaryGids"></a>
The secondary POSIX group IDs used for all EFS operations by this user\.  
Type: Array of longs  
Array Members: Minimum number of 0 items\. Maximum number of 16 items\.  
Valid Range: Minimum value of 0\. Maximum value of 4294967295\.  
Required: No

 ** Uid **   <a name="TransferFamily-Type-PosixProfile-Uid"></a>
The POSIX user ID used for all EFS operations by this user\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 4294967295\.  
Required: Yes

## See Also<a name="API_PosixProfile_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/PosixProfile) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/PosixProfile) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/PosixProfile) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/PosixProfile) 
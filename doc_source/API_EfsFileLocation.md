# EfsFileLocation<a name="API_EfsFileLocation"></a>

Specifies the details for the file location for the file that's being used in the workflow\. Only applicable if you are using Amazon Elastic File Systems \(Amazon EFS\) for storage\.

 

## Contents<a name="API_EfsFileLocation_Contents"></a>

 ** FileSystemId **   <a name="TransferFamily-Type-EfsFileLocation-FileSystemId"></a>
The identifier of the file system, assigned by Amazon EFS\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^(arn:aws[-a-z]*:elasticfilesystem:[0-9a-z-:]+:(access-point/fsap|file-system/fs)-[0-9a-f]{8,40}|fs(ap)?-[0-9a-f]{8,40})$`   
Required: No

 ** Path **   <a name="TransferFamily-Type-EfsFileLocation-Path"></a>
The pathname for the folder being used by a workflow\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 65536\.  
Pattern: `^[^\x00]+$`   
Required: No

## See Also<a name="API_EfsFileLocation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/EfsFileLocation) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/EfsFileLocation) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/EfsFileLocation) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/EfsFileLocation) 
# S3FileLocation<a name="API_S3FileLocation"></a>

Specifies the details for the file location for the file that's being used in the workflow\. Only applicable if you are using S3 storage\.

## Contents<a name="API_S3FileLocation_Contents"></a>

 ** Bucket **   <a name="TransferFamily-Type-S3FileLocation-Bucket"></a>
Specifies the S3 bucket that contains the file being used\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 63\.  
Pattern: `^[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]$`   
Required: No

 ** Etag **   <a name="TransferFamily-Type-S3FileLocation-Etag"></a>
The entity tag is a hash of the object\. The ETag reflects changes only to the contents of an object, not its metadata\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 65536\.  
Pattern: `^.+$`   
Required: No

 ** Key **   <a name="TransferFamily-Type-S3FileLocation-Key"></a>
The name assigned to the file when it was created in Amazon S3\. You use the object key to retrieve the object\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `[\P{M}\p{M}]*`   
Required: No

 ** VersionId **   <a name="TransferFamily-Type-S3FileLocation-VersionId"></a>
Specifies the file version\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^.+$`   
Required: No

## See Also<a name="API_S3FileLocation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/S3FileLocation) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/S3FileLocation) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/S3FileLocation) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/S3FileLocation) 
# S3Tag<a name="API_S3Tag"></a>

Specifies the key\-value pair that are assigned to a file during the execution of a Tagging step\.

## Contents<a name="API_S3Tag_Contents"></a>

 ** Key **   <a name="TransferFamily-Type-S3Tag-Key"></a>
The name assigned to the tag that you create\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Pattern: `^([\p{L}\p{Z}\p{N}_.:/=+\-@]*)$`   
Required: Yes

 ** Value **   <a name="TransferFamily-Type-S3Tag-Value"></a>
The value that corresponds to the key\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^([\p{L}\p{Z}\p{N}_.:/=+\-@]*)$`   
Required: Yes

## See Also<a name="API_S3Tag_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/S3Tag) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/S3Tag) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/S3Tag) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/S3Tag) 
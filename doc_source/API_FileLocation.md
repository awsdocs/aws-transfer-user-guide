# FileLocation<a name="API_FileLocation"></a>

Specifies the Amazon S3 or EFS file details to be used in the step\.

## Contents<a name="API_FileLocation_Contents"></a>

 ** EfsFileLocation **   <a name="TransferFamily-Type-FileLocation-EfsFileLocation"></a>
Specifies the Amazon EFS ID and the path for the file being used\.  
Type: [EfsFileLocation](API_EfsFileLocation.md) object  
Required: No

 ** S3FileLocation **   <a name="TransferFamily-Type-FileLocation-S3FileLocation"></a>
Specifies the S3 details for the file being used, such as bucket, Etag, and so forth\.  
Type: [S3FileLocation](API_S3FileLocation.md) object  
Required: No

## See Also<a name="API_FileLocation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/FileLocation) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/FileLocation) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/FileLocation) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/FileLocation) 
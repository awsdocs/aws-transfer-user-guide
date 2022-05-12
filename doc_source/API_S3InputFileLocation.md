# S3InputFileLocation<a name="API_S3InputFileLocation"></a>

Specifies the customer input S3 file location\. If it is used inside `copyStepDetails.DestinationFileLocation`, it should be the S3 copy destination\.

 You need to provide the bucket and key\. The key can represent either a path or a file\. This is determined by whether or not you end the key value with the forward slash \(/\) character\. If the final character is "/", then your file is copied to the folder, and its name does not change\. If, rather, the final character is alphanumeric, your uploaded file is renamed to the path value\. In this case, if a file with that name already exists, it is overwritten\. 

For example, if your path is `shared-files/bob/`, your uploaded files are copied to the `shared-files/bob/`, folder\. If your path is `shared-files/today`, each uploaded file is copied to the `shared-files` folder and named `today`: each upload overwrites the previous version of the *bob* file\.

## Contents<a name="API_S3InputFileLocation_Contents"></a>

 ** Bucket **   <a name="TransferFamily-Type-S3InputFileLocation-Bucket"></a>
Specifies the S3 bucket for the customer input file\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 63\.  
Pattern: `^[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]$`   
Required: No

 ** Key **   <a name="TransferFamily-Type-S3InputFileLocation-Key"></a>
The name assigned to the file when it was created in S3\. You use the object key to retrieve the object\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `[\P{M}\p{M}]*`   
Required: No

## See Also<a name="API_S3InputFileLocation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/S3InputFileLocation) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/S3InputFileLocation) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/S3InputFileLocation) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/S3InputFileLocation) 
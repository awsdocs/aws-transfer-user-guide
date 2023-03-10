# CopyStepDetails<a name="API_CopyStepDetails"></a>

Each step type has its own `StepDetails` structure\.

## Contents<a name="API_CopyStepDetails_Contents"></a>

 ** DestinationFileLocation **   <a name="TransferFamily-Type-CopyStepDetails-DestinationFileLocation"></a>
Specifies the location for the file being copied\. Use `${Transfer:UserName}` or `${Transfer:UploadDate}` in this field to parametrize the destination prefix by username or uploaded date\.  
+ Set the value of `DestinationFileLocation` to `${Transfer:UserName}` to copy uploaded files to an Amazon S3 bucket that is prefixed with the name of the Transfer Family user that uploaded the file\.
+ Set the value of `DestinationFileLocation` to `${Transfer:UploadDate}` to copy uploaded files to an Amazon S3 bucket that is prefixed with the date of the upload\.
**Note**  
The system resolves `UploadDate` to a date format of *YYYY\-MM\-DD*, based on the date the file is uploaded in UTC\.
Type: [InputFileLocation](API_InputFileLocation.md) object  
Required: No

 ** Name **   <a name="TransferFamily-Type-CopyStepDetails-Name"></a>
The name of the step, used as an identifier\.  
Type: String  
Length Constraints: Maximum length of 30\.  
Pattern: `^[\w-]*$`   
Required: No

 ** OverwriteExisting **   <a name="TransferFamily-Type-CopyStepDetails-OverwriteExisting"></a>
A flag that indicates whether to overwrite an existing file of the same name\. The default is `FALSE`\.  
If the workflow is processing a file that has the same name as an existing file, the behavior is as follows:  
+ If `OverwriteExisting` is `TRUE`, the existing file is replaced with the file being processed\.
+ If `OverwriteExisting` is `FALSE`, nothing happens, and the workflow processing stops\.
Type: String  
Valid Values:` TRUE | FALSE`   
Required: No

 ** SourceFileLocation **   <a name="TransferFamily-Type-CopyStepDetails-SourceFileLocation"></a>
Specifies which file to use as input to the workflow step: either the output from the previous step, or the originally uploaded file for the workflow\.  
+ To use the previous file as the input, enter `${previous.file}`\. In this case, this workflow step uses the output file from the previous workflow step as input\. This is the default value\.
+ To use the originally uploaded file location as input for this step, enter `${original.file}`\.
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^\$\{(\w+.)+\w+\}$`   
Required: No

## See Also<a name="API_CopyStepDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CopyStepDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CopyStepDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CopyStepDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CopyStepDetails) 
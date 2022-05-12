# CopyStepDetails<a name="API_CopyStepDetails"></a>

Each step type has its own `StepDetails` structure\.

## Contents<a name="API_CopyStepDetails_Contents"></a>

 ** DestinationFileLocation **   <a name="TransferFamily-Type-CopyStepDetails-DestinationFileLocation"></a>
Specifies the location for the file being copied\. Only applicable for Copy type workflow steps\. Use `${Transfer:username}` in this field to parametrize the destination prefix by username\.  
Type: [InputFileLocation](API_InputFileLocation.md) object  
Required: No

 ** Name **   <a name="TransferFamily-Type-CopyStepDetails-Name"></a>
The name of the step, used as an identifier\.  
Type: String  
Length Constraints: Maximum length of 30\.  
Pattern: `^[\w-]*$`   
Required: No

 ** OverwriteExisting **   <a name="TransferFamily-Type-CopyStepDetails-OverwriteExisting"></a>
A flag that indicates whether or not to overwrite an existing file of the same name\. The default is `FALSE`\.  
Type: String  
Valid Values:` TRUE | FALSE`   
Required: No

 ** SourceFileLocation **   <a name="TransferFamily-Type-CopyStepDetails-SourceFileLocation"></a>
Specifies which file to use as input to the workflow step: either the output from the previous step, or the originally uploaded file for the workflow\.  
+ Enter `${previous.file}` to use the previous file as the input\. In this case, this workflow step uses the output file from the previous workflow step as input\. This is the default value\.
+ Enter `${original.file}` to use the originally\-uploaded file location as input for this step\.
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
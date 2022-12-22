# DecryptStepDetails<a name="API_DecryptStepDetails"></a>

Each step type has its own `StepDetails` structure\.

## Contents<a name="API_DecryptStepDetails_Contents"></a>

 ** DestinationFileLocation **   <a name="TransferFamily-Type-DecryptStepDetails-DestinationFileLocation"></a>
Specifies the location for the file that's being processed\.  
Type: [InputFileLocation](API_InputFileLocation.md) object  
Required: Yes

 ** Name **   <a name="TransferFamily-Type-DecryptStepDetails-Name"></a>
The name of the step, used as an identifier\.  
Type: String  
Length Constraints: Maximum length of 30\.  
Pattern: `^[\w-]*$`   
Required: No

 ** OverwriteExisting **   <a name="TransferFamily-Type-DecryptStepDetails-OverwriteExisting"></a>
A flag that indicates whether to overwrite an existing file of the same name\. The default is `FALSE`\.  
Type: String  
Valid Values:` TRUE | FALSE`   
Required: No

 ** SourceFileLocation **   <a name="TransferFamily-Type-DecryptStepDetails-SourceFileLocation"></a>
Specifies which file to use as input to the workflow step: either the output from the previous step, or the originally uploaded file for the workflow\.  
+ To use the previous file as the input, enter `${previous.file}`\. In this case, this workflow step uses the output file from the previous workflow step as input\. This is the default value\.
+ To use the originally uploaded file location as input for this step, enter `${original.file}`\.
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^\$\{(\w+.)+\w+\}$`   
Required: No

 ** Type **   <a name="TransferFamily-Type-DecryptStepDetails-Type"></a>
The type of encryption used\. Currently, this value must be `PGP`\.  
Type: String  
Valid Values:` PGP`   
Required: Yes

## See Also<a name="API_DecryptStepDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DecryptStepDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DecryptStepDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DecryptStepDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DecryptStepDetails) 
# TagStepDetails<a name="API_TagStepDetails"></a>

Each step type has its own `StepDetails` structure\.

The key/value pairs used to tag a file during the execution of a workflow step\.

## Contents<a name="API_TagStepDetails_Contents"></a>

 ** Name **   <a name="TransferFamily-Type-TagStepDetails-Name"></a>
The name of the step, used as an identifier\.  
Type: String  
Length Constraints: Maximum length of 30\.  
Pattern: `^[\w-]*$`   
Required: No

 ** SourceFileLocation **   <a name="TransferFamily-Type-TagStepDetails-SourceFileLocation"></a>
Specifies which file to use as input to the workflow step: either the output from the previous step, or the originally uploaded file for the workflow\.  
+ To use the previous file as the input, enter `${previous.file}`\. In this case, this workflow step uses the output file from the previous workflow step as input\. This is the default value\.
+ To use the originally uploaded file location as input for this step, enter `${original.file}`\.
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^\$\{(\w+.)+\w+\}$`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-TagStepDetails-Tags"></a>
Array that contains from 1 to 10 key/value pairs\.  
Type: Array of [S3Tag](API_S3Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 10 items\.  
Required: No

## See Also<a name="API_TagStepDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/TagStepDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/TagStepDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/TagStepDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/TagStepDetails) 
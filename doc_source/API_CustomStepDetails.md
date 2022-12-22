# CustomStepDetails<a name="API_CustomStepDetails"></a>

Each step type has its own `StepDetails` structure\.

## Contents<a name="API_CustomStepDetails_Contents"></a>

 ** Name **   <a name="TransferFamily-Type-CustomStepDetails-Name"></a>
The name of the step, used as an identifier\.  
Type: String  
Length Constraints: Maximum length of 30\.  
Pattern: `^[\w-]*$`   
Required: No

 ** SourceFileLocation **   <a name="TransferFamily-Type-CustomStepDetails-SourceFileLocation"></a>
Specifies which file to use as input to the workflow step: either the output from the previous step, or the originally uploaded file for the workflow\.  
+ To use the previous file as the input, enter `${previous.file}`\. In this case, this workflow step uses the output file from the previous workflow step as input\. This is the default value\.
+ To use the originally uploaded file location as input for this step, enter `${original.file}`\.
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^\$\{(\w+.)+\w+\}$`   
Required: No

 ** Target **   <a name="TransferFamily-Type-CustomStepDetails-Target"></a>
The ARN for the lambda function that is being called\.  
Type: String  
Length Constraints: Maximum length of 170\.  
Pattern: `arn:[a-z-]+:lambda:.*$`   
Required: No

 ** TimeoutSeconds **   <a name="TransferFamily-Type-CustomStepDetails-TimeoutSeconds"></a>
Timeout, in seconds, for the step\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1800\.  
Required: No

## See Also<a name="API_CustomStepDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CustomStepDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CustomStepDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CustomStepDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CustomStepDetails) 
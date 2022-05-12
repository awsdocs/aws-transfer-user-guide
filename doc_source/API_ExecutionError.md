# ExecutionError<a name="API_ExecutionError"></a>

Specifies the error message and type, for an error that occurs during the execution of the workflow\.

## Contents<a name="API_ExecutionError_Contents"></a>

 ** Message **   <a name="TransferFamily-Type-ExecutionError-Message"></a>
Specifies the descriptive message that corresponds to the `ErrorType`\.  
Type: String  
Required: Yes

 ** Type **   <a name="TransferFamily-Type-ExecutionError-Type"></a>
Specifies the error type\.  
+  `ALREADY_EXISTS`: occurs for a copy step, if the overwrite option is not selected and a file with the same name already exists in the target location\.
+  `BAD_REQUEST`: a general bad request: for example, a step that attempts to tag an EFS file returns `BAD_REQUEST`, as only S3 files can be tagged\.
+  `CUSTOM_STEP_FAILED`: occurs when the custom step provided a callback that indicates failure\.
+  `INTERNAL_SERVER_ERROR`: a catch\-all error that can occur for a variety of reasons\.
+  `NOT_FOUND`: occurs when a requested entity, for example a source file for a copy step, does not exist\.
+  `PERMISSION_DENIED`: occurs if your policy does not contain the correct permissions to complete one or more of the steps in the workflow\.
+  `TIMEOUT`: occurs when the execution times out\.
**Note**  
 You can set the `TimeoutSeconds` for a custom step, anywhere from 1 second to 1800 seconds \(30 minutes\)\. 
+  `THROTTLED`: occurs if you exceed the new execution refill rate of one workflow per second\.
Type: String  
Valid Values:` PERMISSION_DENIED`   
Required: Yes

## See Also<a name="API_ExecutionError_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ExecutionError) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ExecutionError) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ExecutionError) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ExecutionError) 
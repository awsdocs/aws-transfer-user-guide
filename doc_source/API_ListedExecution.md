# ListedExecution<a name="API_ListedExecution"></a>

Returns properties of the execution that is specified\.

## Contents<a name="API_ListedExecution_Contents"></a>

 ** ExecutionId **   <a name="TransferFamily-Type-ListedExecution-ExecutionId"></a>
A unique identifier for the execution of a workflow\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$`   
Required: No

 ** InitialFileLocation **   <a name="TransferFamily-Type-ListedExecution-InitialFileLocation"></a>
A structure that describes the Amazon S3 or EFS file location\. This is the file location when the execution begins: if the file is being copied, this is the initial \(as opposed to destination\) file location\.  
Type: [FileLocation](API_FileLocation.md) object  
Required: No

 ** ServiceMetadata **   <a name="TransferFamily-Type-ListedExecution-ServiceMetadata"></a>
A container object for the session details that are associated with a workflow\.  
Type: [ServiceMetadata](API_ServiceMetadata.md) object  
Required: No

 ** Status **   <a name="TransferFamily-Type-ListedExecution-Status"></a>
The status is one of the execution\. Can be in progress, completed, exception encountered, or handling the exception\.  
Type: String  
Valid Values:` IN_PROGRESS | COMPLETED | EXCEPTION | HANDLING_EXCEPTION`   
Required: No

## See Also<a name="API_ListedExecution_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedExecution) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedExecution) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedExecution) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedExecution) 
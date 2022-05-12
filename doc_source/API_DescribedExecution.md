# DescribedExecution<a name="API_DescribedExecution"></a>

The details for an execution object\.

## Contents<a name="API_DescribedExecution_Contents"></a>

 ** ExecutionId **   <a name="TransferFamily-Type-DescribedExecution-ExecutionId"></a>
A unique identifier for the execution of a workflow\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[0-9a-fA-F]{8}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{4}\-[0-9a-fA-F]{12}$`   
Required: No

 ** ExecutionRole **   <a name="TransferFamily-Type-DescribedExecution-ExecutionRole"></a>
The IAM role associated with the execution\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** InitialFileLocation **   <a name="TransferFamily-Type-DescribedExecution-InitialFileLocation"></a>
A structure that describes the Amazon S3 or EFS file location\. This is the file location when the execution begins: if the file is being copied, this is the initial \(as opposed to destination\) file location\.  
Type: [FileLocation](API_FileLocation.md) object  
Required: No

 ** LoggingConfiguration **   <a name="TransferFamily-Type-DescribedExecution-LoggingConfiguration"></a>
The IAM logging role associated with the execution\.  
Type: [LoggingConfiguration](API_LoggingConfiguration.md) object  
Required: No

 ** PosixProfile **   <a name="TransferFamily-Type-DescribedExecution-PosixProfile"></a>
The full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary groups IDs \(`SecondaryGids`\), that controls your users' access to your Amazon EFS file systems\. The POSIX permissions that are set on files and directories in your file system determine the level of access your users get when transferring files into and out of your Amazon EFS file systems\.  
Type: [PosixProfile](API_PosixProfile.md) object  
Required: No

 ** Results **   <a name="TransferFamily-Type-DescribedExecution-Results"></a>
A structure that describes the execution results\. This includes a list of the steps along with the details of each step, error type and message \(if any\), and the `OnExceptionSteps` structure\.  
Type: [ExecutionResults](API_ExecutionResults.md) object  
Required: No

 ** ServiceMetadata **   <a name="TransferFamily-Type-DescribedExecution-ServiceMetadata"></a>
A container object for the session details associated with a workflow\.  
Type: [ServiceMetadata](API_ServiceMetadata.md) object  
Required: No

 ** Status **   <a name="TransferFamily-Type-DescribedExecution-Status"></a>
The status is one of the execution\. Can be in progress, completed, exception encountered, or handling the exception\.   
Type: String  
Valid Values:` IN_PROGRESS | COMPLETED | EXCEPTION | HANDLING_EXCEPTION`   
Required: No

## See Also<a name="API_DescribedExecution_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedExecution) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedExecution) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedExecution) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedExecution) 
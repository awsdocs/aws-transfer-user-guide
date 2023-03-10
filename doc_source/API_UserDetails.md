# UserDetails<a name="API_UserDetails"></a>

Specifies the user name, server ID, and session ID for a workflow\.

## Contents<a name="API_UserDetails_Contents"></a>

 ** ServerId **   <a name="TransferFamily-Type-UserDetails-ServerId"></a>
The system\-assigned unique identifier for a Transfer server instance\.   
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** SessionId **   <a name="TransferFamily-Type-UserDetails-SessionId"></a>
The system\-assigned unique identifier for a session that corresponds to the workflow\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 32\.  
Pattern: `^[\w-]*$`   
Required: No

 ** UserName **   <a name="TransferFamily-Type-UserDetails-UserName"></a>
A unique string that identifies a Transfer Family user associated with a server\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

## See Also<a name="API_UserDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UserDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UserDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UserDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UserDetails) 
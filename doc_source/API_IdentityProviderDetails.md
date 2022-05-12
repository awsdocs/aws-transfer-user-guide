# IdentityProviderDetails<a name="API_IdentityProviderDetails"></a>

Returns information related to the type of user authentication that is in use for a file transfer protocol\-enabled server's users\. A server can have only one method of authentication\.

## Contents<a name="API_IdentityProviderDetails_Contents"></a>

 ** DirectoryId **   <a name="TransferFamily-Type-IdentityProviderDetails-DirectoryId"></a>
The identifier of the AWS Directory Service directory that you want to stop sharing\.  
Type: String  
Length Constraints: Fixed length of 12\.  
Pattern: `^d-[0-9a-f]{10}$`   
Required: No

 ** Function **   <a name="TransferFamily-Type-IdentityProviderDetails-Function"></a>
The ARN for a lambda function to use for the Identity provider\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 170\.  
Pattern: `^arn:[a-z-]+:lambda:.*$`   
Required: No

 ** InvocationRole **   <a name="TransferFamily-Type-IdentityProviderDetails-InvocationRole"></a>
Provides the type of `InvocationRole` used to authenticate the user account\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** Url **   <a name="TransferFamily-Type-IdentityProviderDetails-Url"></a>
Provides the location of the service endpoint used to authenticate users\.  
Type: String  
Length Constraints: Maximum length of 255\.  
Required: No

## See Also<a name="API_IdentityProviderDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/IdentityProviderDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/IdentityProviderDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/IdentityProviderDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/IdentityProviderDetails) 
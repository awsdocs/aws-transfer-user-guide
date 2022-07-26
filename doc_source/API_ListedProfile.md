# ListedProfile<a name="API_ListedProfile"></a>

Returns the properties of the profile that was specified\.

## Contents<a name="API_ListedProfile_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-ListedProfile-Arn"></a>
The Amazon Resource Name \(ARN\) of the specified profile\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: No

 ** As2Id **   <a name="TransferFamily-Type-ListedProfile-As2Id"></a>
The `As2Id` is the *AS2\-name*, as defined in the [RFC 4130](https://datatracker.ietf.org/doc/html/rfc4130)\. For inbound transfers, this is the `AS2-From` header for the AS2 messages sent from the partner\. For outbound connectors, this is the `AS2-To` header for the AS2 messages sent to the partner using the `StartFileTransfer` API operation\. This ID cannot include spaces\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Pattern: `^[\p{Print}\s]*`   
Required: No

 ** ProfileId **   <a name="TransferFamily-Type-ListedProfile-ProfileId"></a>
A unique identifier for the local or partner AS2 profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** ProfileType **   <a name="TransferFamily-Type-ListedProfile-ProfileType"></a>
Indicates whether to list only `LOCAL` type profiles or only `PARTNER` type profiles\. If not supplied in the request, the command lists all types of profiles\.  
Type: String  
Valid Values:` LOCAL | PARTNER`   
Required: No

## See Also<a name="API_ListedProfile_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedProfile) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedProfile) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedProfile) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedProfile) 
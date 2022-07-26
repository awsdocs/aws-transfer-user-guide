# ListedAgreement<a name="API_ListedAgreement"></a>

Describes the properties of an agreement\.

## Contents<a name="API_ListedAgreement_Contents"></a>

 ** AgreementId **   <a name="TransferFamily-Type-ListedAgreement-AgreementId"></a>
A unique identifier for the agreement\. This identifier is returned when you create an agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^a-([0-9a-f]{17})$`   
Required: No

 ** Arn **   <a name="TransferFamily-Type-ListedAgreement-Arn"></a>
The Amazon Resource Name \(ARN\) of the specified agreement\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: No

 ** Description **   <a name="TransferFamily-Type-ListedAgreement-Description"></a>
The current description for the agreement\. You can change it by calling the `UpdateAgreement` operation and providing a new description\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** LocalProfileId **   <a name="TransferFamily-Type-ListedAgreement-LocalProfileId"></a>
A unique identifier for the AS2 local profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** PartnerProfileId **   <a name="TransferFamily-Type-ListedAgreement-PartnerProfileId"></a>
A unique identifier for the partner profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** ServerId **   <a name="TransferFamily-Type-ListedAgreement-ServerId"></a>
The unique identifier for the agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: No

 ** Status **   <a name="TransferFamily-Type-ListedAgreement-Status"></a>
The agreement can be either `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

## See Also<a name="API_ListedAgreement_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedAgreement) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedAgreement) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedAgreement) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedAgreement) 
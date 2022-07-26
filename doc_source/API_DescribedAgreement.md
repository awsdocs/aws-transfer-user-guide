# DescribedAgreement<a name="API_DescribedAgreement"></a>

Describes the properties of an agreement\.

## Contents<a name="API_DescribedAgreement_Contents"></a>

 ** AccessRole **   <a name="TransferFamily-Type-DescribedAgreement-AccessRole"></a>
With AS2, you can send files by calling `StartFileTransfer` and specifying the file paths in the request parameter, `SendFilePaths`\. We use the file’s parent directory \(for example, for `--send-file-paths /bucket/dir/file.txt`, parent directory is `/bucket/dir/`\) to temporarily store a processed AS2 message file, store the MDN when we receive them from the partner, and write a final JSON file containing relevant metadata of the transmission\. So, the `AccessRole` needs to provide read and write access to the parent directory of the file location used in the `StartFileTransfer` request\. Additionally, you need to provide read and write access to the parent directory of the files that you intend to send with `StartFileTransfer`\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** AgreementId **   <a name="TransferFamily-Type-DescribedAgreement-AgreementId"></a>
A unique identifier for the agreement\. This identifier is returned when you create an agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^a-([0-9a-f]{17})$`   
Required: No

 ** Arn **   <a name="TransferFamily-Type-DescribedAgreement-Arn"></a>
The unique Amazon Resource Name \(ARN\) for the agreement\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** BaseDirectory **   <a name="TransferFamily-Type-DescribedAgreement-BaseDirectory"></a>
The landing directory \(folder\) for files that are transferred by using the AS2 protocol\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: No

 ** Description **   <a name="TransferFamily-Type-DescribedAgreement-Description"></a>
The name or short description that's used to identify the agreement\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** LocalProfileId **   <a name="TransferFamily-Type-DescribedAgreement-LocalProfileId"></a>
A unique identifier for the AS2 local profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** PartnerProfileId **   <a name="TransferFamily-Type-DescribedAgreement-PartnerProfileId"></a>
A unique identifier for the partner profile used in the agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** ServerId **   <a name="TransferFamily-Type-DescribedAgreement-ServerId"></a>
A system\-assigned unique identifier for a server instance\. This identifier indicates the specific server that the agreement uses\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: No

 ** Status **   <a name="TransferFamily-Type-DescribedAgreement-Status"></a>
The current status of the agreement, either `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedAgreement-Tags"></a>
Key\-value pairs that can be used to group and search for agreements\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## See Also<a name="API_DescribedAgreement_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedAgreement) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedAgreement) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedAgreement) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedAgreement) 
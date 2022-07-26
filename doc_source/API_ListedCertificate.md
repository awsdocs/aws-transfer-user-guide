# ListedCertificate<a name="API_ListedCertificate"></a>

Describes the properties of a certificate\.

## Contents<a name="API_ListedCertificate_Contents"></a>

 ** ActiveDate **   <a name="TransferFamily-Type-ListedCertificate-ActiveDate"></a>
An optional date that specifies when the certificate becomes active\.  
Type: Timestamp  
Required: No

 ** Arn **   <a name="TransferFamily-Type-ListedCertificate-Arn"></a>
The Amazon Resource Name \(ARN\) of the specified certificate\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: No

 ** CertificateId **   <a name="TransferFamily-Type-ListedCertificate-CertificateId"></a>
An array of identifiers for the imported certificates\. You use this identifier for working with profiles and partner profiles\.  
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$`   
Required: No

 ** Description **   <a name="TransferFamily-Type-ListedCertificate-Description"></a>
The name or short description that's used to identify the certificate\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** InactiveDate **   <a name="TransferFamily-Type-ListedCertificate-InactiveDate"></a>
An optional date that specifies when the certificate becomes inactive\.  
Type: Timestamp  
Required: No

 ** Status **   <a name="TransferFamily-Type-ListedCertificate-Status"></a>
The certificate can be either `ACTIVE`, `PENDING_ROTATION`, or `INACTIVE`\. `PENDING_ROTATION` means that this certificate will replace the current certificate when it expires\.  
Type: String  
Valid Values:` ACTIVE | PENDING_ROTATION | INACTIVE`   
Required: No

 ** Type **   <a name="TransferFamily-Type-ListedCertificate-Type"></a>
The type for the certificate\. If a private key has been specified for the certificate, its type is `CERTIFICATE_WITH_PRIVATE_KEY`\. If there is no private key, the type is `CERTIFICATE`\.  
Type: String  
Valid Values:` CERTIFICATE | CERTIFICATE_WITH_PRIVATE_KEY`   
Required: No

 ** Usage **   <a name="TransferFamily-Type-ListedCertificate-Usage"></a>
Specifies whether this certificate is used for signing or encryption\.  
Type: String  
Valid Values:` SIGNING | ENCRYPTION`   
Required: No

## See Also<a name="API_ListedCertificate_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedCertificate) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedCertificate) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedCertificate) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedCertificate) 
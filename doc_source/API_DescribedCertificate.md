# DescribedCertificate<a name="API_DescribedCertificate"></a>

Describes the properties of a certificate\.

## Contents<a name="API_DescribedCertificate_Contents"></a>

 ** ActiveDate **   <a name="TransferFamily-Type-DescribedCertificate-ActiveDate"></a>
An optional date that specifies when the certificate becomes active\.  
Type: Timestamp  
Required: No

 ** Arn **   <a name="TransferFamily-Type-DescribedCertificate-Arn"></a>
The unique Amazon Resource Name \(ARN\) for the certificate\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** Certificate **   <a name="TransferFamily-Type-DescribedCertificate-Certificate"></a>
The file name for the certificate\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 16384\.  
Pattern: `^[\u0009\u000A\u000D\u0020-\u00FF]*`   
Required: No

 ** CertificateChain **   <a name="TransferFamily-Type-DescribedCertificate-CertificateChain"></a>
The list of certificates that make up the chain for the certificate\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2097152\.  
Pattern: `^[\u0009\u000A\u000D\u0020-\u00FF]*`   
Required: No

 ** CertificateId **   <a name="TransferFamily-Type-DescribedCertificate-CertificateId"></a>
An array of identifiers for the imported certificates\. You use this identifier for working with profiles and partner profiles\.  
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$`   
Required: No

 ** Description **   <a name="TransferFamily-Type-DescribedCertificate-Description"></a>
The name or description that's used to identity the certificate\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** InactiveDate **   <a name="TransferFamily-Type-DescribedCertificate-InactiveDate"></a>
An optional date that specifies when the certificate becomes inactive\.  
Type: Timestamp  
Required: No

 ** NotAfterDate **   <a name="TransferFamily-Type-DescribedCertificate-NotAfterDate"></a>
The final date that the certificate is valid\.  
Type: Timestamp  
Required: No

 ** NotBeforeDate **   <a name="TransferFamily-Type-DescribedCertificate-NotBeforeDate"></a>
The earliest date that the certificate is valid\.  
Type: Timestamp  
Required: No

 ** Serial **   <a name="TransferFamily-Type-DescribedCertificate-Serial"></a>
The serial number for the certificate\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 48\.  
Pattern: `^[\p{XDigit}{2}:?]*`   
Required: No

 ** Status **   <a name="TransferFamily-Type-DescribedCertificate-Status"></a>
The certificate can be either `ACTIVE`, `PENDING_ROTATION`, or `INACTIVE`\. `PENDING_ROTATION` means that this certificate will replace the current certificate when it expires\.  
Type: String  
Valid Values:` ACTIVE | PENDING_ROTATION | INACTIVE`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedCertificate-Tags"></a>
Key\-value pairs that can be used to group and search for certificates\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** Type **   <a name="TransferFamily-Type-DescribedCertificate-Type"></a>
If a private key has been specified for the certificate, its type is `CERTIFICATE_WITH_PRIVATE_KEY`\. If there is no private key, the type is `CERTIFICATE`\.  
Type: String  
Valid Values:` CERTIFICATE | CERTIFICATE_WITH_PRIVATE_KEY`   
Required: No

 ** Usage **   <a name="TransferFamily-Type-DescribedCertificate-Usage"></a>
Specifies whether this certificate is used for signing or encryption\.  
Type: String  
Valid Values:` SIGNING | ENCRYPTION`   
Required: No

## See Also<a name="API_DescribedCertificate_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedCertificate) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedCertificate) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedCertificate) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedCertificate) 
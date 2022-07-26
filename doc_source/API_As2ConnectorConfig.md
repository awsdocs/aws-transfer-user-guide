# As2ConnectorConfig<a name="API_As2ConnectorConfig"></a>

Contains the details for a connector object\. The connector object is used for AS2 outbound processes, to connect the AWS Transfer Family customer with the trading partner\.

## Contents<a name="API_As2ConnectorConfig_Contents"></a>

 ** Compression **   <a name="TransferFamily-Type-As2ConnectorConfig-Compression"></a>
Specifies whether the AS2 file is compressed\.  
Type: String  
Valid Values:` ZLIB | DISABLED`   
Required: No

 ** EncryptionAlgorithm **   <a name="TransferFamily-Type-As2ConnectorConfig-EncryptionAlgorithm"></a>
The algorithm that is used to encrypt the file\.  
Type: String  
Valid Values:` AES128_CBC | AES192_CBC | AES256_CBC`   
Required: No

 ** LocalProfileId **   <a name="TransferFamily-Type-As2ConnectorConfig-LocalProfileId"></a>
A unique identifier for the AS2 local profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** MdnResponse **   <a name="TransferFamily-Type-As2ConnectorConfig-MdnResponse"></a>
Used for outbound requests \(from an AWS Transfer Family server to a partner AS2 server\) to determine whether the partner response for transfers is synchronous or asynchronous\. Specify either of the following values:  
+  `SYNC`: The system expects a synchronous MDN response, confirming that the file was transferred successfully \(or not\)\.
+  `NONE`: Specifies that no MDN response is required\.
Type: String  
Valid Values:` SYNC | NONE`   
Required: No

 ** MdnSigningAlgorithm **   <a name="TransferFamily-Type-As2ConnectorConfig-MdnSigningAlgorithm"></a>
The signing algorithm for the MDN response\.  
If set to DEFAULT \(or not set at all\), the value for `SigningAlogorithm` is used\.
Type: String  
Valid Values:` SHA256 | SHA384 | SHA512 | SHA1 | NONE | DEFAULT`   
Required: No

 ** MessageSubject **   <a name="TransferFamily-Type-As2ConnectorConfig-MessageSubject"></a>
Used as the `Subject` HTTP header attribute in AS2 messages that are being sent with the connector\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^[\p{Print}\p{Blank}]+`   
Required: No

 ** PartnerProfileId **   <a name="TransferFamily-Type-As2ConnectorConfig-PartnerProfileId"></a>
A unique identifier for the partner profile for the connector\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: No

 ** SigningAlgorithm **   <a name="TransferFamily-Type-As2ConnectorConfig-SigningAlgorithm"></a>
The algorithm that is used to sign the AS2 messages sent with the connector\.  
Type: String  
Valid Values:` SHA256 | SHA384 | SHA512 | SHA1 | NONE`   
Required: No

## See Also<a name="API_As2ConnectorConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/As2ConnectorConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/As2ConnectorConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/As2ConnectorConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/As2ConnectorConfig) 
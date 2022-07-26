# ImportCertificate<a name="API_ImportCertificate"></a>

Imports the signing and encryption certificates that you need to create local \(AS2\) profiles and partner profiles\.

## Request Syntax<a name="API_ImportCertificate_RequestSyntax"></a>

```
{
   "ActiveDate": number,
   "Certificate": "string",
   "CertificateChain": "string",
   "Description": "string",
   "InactiveDate": number,
   "PrivateKey": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "Usage": "string"
}
```

## Request Parameters<a name="API_ImportCertificate_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ActiveDate](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-ActiveDate"></a>
An optional date that specifies when the certificate becomes active\.  
Type: Timestamp  
Required: No

 ** [Certificate](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-Certificate"></a>
The file that contains the certificate to import\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 16384\.  
Pattern: `^[\u0009\u000A\u000D\u0020-\u00FF]*`   
Required: Yes

 ** [CertificateChain](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-CertificateChain"></a>
An optional list of certificates that make up the chain for the certificate that's being imported\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2097152\.  
Pattern: `^[\u0009\u000A\u000D\u0020-\u00FF]*`   
Required: No

 ** [Description](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-Description"></a>
A short description that helps identify the certificate\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** [InactiveDate](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-InactiveDate"></a>
An optional date that specifies when the certificate becomes inactive\.  
Type: Timestamp  
Required: No

 ** [PrivateKey](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-PrivateKey"></a>
The file that contains the private key for the certificate that's being imported\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 16384\.  
Pattern: `^[\u0009\u000A\u000D\u0020-\u00FF]*`   
Required: No

 ** [Tags](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-Tags"></a>
Key\-value pairs that can be used to group and search for certificates\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** [Usage](#API_ImportCertificate_RequestSyntax) **   <a name="TransferFamily-ImportCertificate-request-Usage"></a>
Specifies whether this certificate is used for signing or encryption\.  
Type: String  
Valid Values:` SIGNING | ENCRYPTION`   
Required: Yes

## Response Syntax<a name="API_ImportCertificate_ResponseSyntax"></a>

```
{
   "CertificateId": "string"
}
```

## Response Elements<a name="API_ImportCertificate_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CertificateId](#API_ImportCertificate_ResponseSyntax) **   <a name="TransferFamily-ImportCertificate-response-CertificateId"></a>
An array of identifiers for the imported certificates\. You use this identifier for working with profiles and partner profiles\.  
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$` 

## Errors<a name="API_ImportCertificate_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_ImportCertificate_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ImportCertificate) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ImportCertificate) 
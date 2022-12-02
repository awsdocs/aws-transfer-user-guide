# UpdateCertificate<a name="API_UpdateCertificate"></a>

Updates the active and inactive dates for a certificate\.

## Request Syntax<a name="API_UpdateCertificate_RequestSyntax"></a>

```
{
   "ActiveDate": number,
   "CertificateId": "string",
   "Description": "string",
   "InactiveDate": number
}
```

## Request Parameters<a name="API_UpdateCertificate_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ActiveDate](#API_UpdateCertificate_RequestSyntax) **   <a name="TransferFamily-UpdateCertificate-request-ActiveDate"></a>
An optional date that specifies when the certificate becomes active\.  
Type: Timestamp  
Required: No

 ** [CertificateId](#API_UpdateCertificate_RequestSyntax) **   <a name="TransferFamily-UpdateCertificate-request-CertificateId"></a>
The identifier of the certificate object that you are updating\.  
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$`   
Required: Yes

 ** [Description](#API_UpdateCertificate_RequestSyntax) **   <a name="TransferFamily-UpdateCertificate-request-Description"></a>
A short description to help identify the certificate\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** [InactiveDate](#API_UpdateCertificate_RequestSyntax) **   <a name="TransferFamily-UpdateCertificate-request-InactiveDate"></a>
An optional date that specifies when the certificate becomes inactive\.  
Type: Timestamp  
Required: No

## Response Syntax<a name="API_UpdateCertificate_ResponseSyntax"></a>

```
{
   "CertificateId": "string"
}
```

## Response Elements<a name="API_UpdateCertificate_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CertificateId](#API_UpdateCertificate_ResponseSyntax) **   <a name="TransferFamily-UpdateCertificate-response-CertificateId"></a>
Returns the identifier of the certificate object that you are updating\.  
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$` 

## Errors<a name="API_UpdateCertificate_Errors"></a>

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

 ** ThrottlingException **   
The request was denied due to request throttling\.  
HTTP Status Code: 400

## Examples<a name="API_UpdateCertificate_Examples"></a>

### Example<a name="API_UpdateCertificate_Example_1"></a>

The following example updates the active date for a certificate, setting the active date to January 16, 2022 at 16:12:07 UTC \-5 hours\.

#### Sample Request<a name="API_UpdateCertificate_Example_1_Request"></a>

```
aws transfer update-certificate --certificate-id c-abcdefg123456hijk --active-date 2022-01-16T16:12:07-05:00
```

### Example<a name="API_UpdateCertificate_Example_2"></a>

The following is a sample response for this API call\.

#### Sample Response<a name="API_UpdateCertificate_Example_2_Response"></a>

```
"CertificateId": "c-abcdefg123456hijk"
```

## See Also<a name="API_UpdateCertificate_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/UpdateCertificate) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UpdateCertificate) 
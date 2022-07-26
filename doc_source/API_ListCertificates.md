# ListCertificates<a name="API_ListCertificates"></a>

Returns a list of the current certificates that have been imported into AWS Transfer Family\. If you want to limit the results to a certain number, supply a value for the `MaxResults` parameter\. If you ran the command previously and received a value for the `NextToken` parameter, you can supply that value to continue listing certificates from where you left off\.

## Request Syntax<a name="API_ListCertificates_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListCertificates_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListCertificates_RequestSyntax) **   <a name="TransferFamily-ListCertificates-request-MaxResults"></a>
The maximum number of certificates to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListCertificates_RequestSyntax) **   <a name="TransferFamily-ListCertificates-request-NextToken"></a>
When you can get additional results from the `ListCertificates` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional certificates\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

## Response Syntax<a name="API_ListCertificates_ResponseSyntax"></a>

```
{
   "Certificates": [ 
      { 
         "ActiveDate": number,
         "Arn": "string",
         "CertificateId": "string",
         "Description": "string",
         "InactiveDate": number,
         "Status": "string",
         "Type": "string",
         "Usage": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListCertificates_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Certificates](#API_ListCertificates_ResponseSyntax) **   <a name="TransferFamily-ListCertificates-response-Certificates"></a>
Returns an array of the certificates that are specified in the `ListCertificates` call\.  
Type: Array of [ListedCertificate](API_ListedCertificate.md) objects

 ** [NextToken](#API_ListCertificates_ResponseSyntax) **   <a name="TransferFamily-ListCertificates-response-NextToken"></a>
Returns the next token, which you can use to list the next certificate\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

## Errors<a name="API_ListCertificates_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidNextTokenException **   
The `NextToken` parameter that was passed is invalid\.  
HTTP Status Code: 400

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_ListCertificates_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListCertificates) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListCertificates) 
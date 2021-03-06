# DeleteAgreement<a name="API_DeleteAgreement"></a>

Delete the agreement that's specified in the provided `AgreementId`\.

## Request Syntax<a name="API_DeleteAgreement_RequestSyntax"></a>

```
{
   "AgreementId": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_DeleteAgreement_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgreementId](#API_DeleteAgreement_RequestSyntax) **   <a name="TransferFamily-DeleteAgreement-request-AgreementId"></a>
A unique identifier for the agreement\. This identifier is returned when you create an agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^a-([0-9a-f]{17})$`   
Required: Yes

 ** [ServerId](#API_DeleteAgreement_RequestSyntax) **   <a name="TransferFamily-DeleteAgreement-request-ServerId"></a>
The server ID associated with the agreement that you are deleting\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Elements<a name="API_DeleteAgreement_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteAgreement_Errors"></a>

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

## See Also<a name="API_DeleteAgreement_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DeleteAgreement) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DeleteAgreement) 
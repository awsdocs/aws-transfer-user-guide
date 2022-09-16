# UpdateHostKey<a name="API_UpdateHostKey"></a>

Updates the description for the host key that's specified by the `ServerId` and `HostKeyId` parameters\.

## Request Syntax<a name="API_UpdateHostKey_RequestSyntax"></a>

```
{
   "Description": "string",
   "HostKeyId": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_UpdateHostKey_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Description](#API_UpdateHostKey_RequestSyntax) **   <a name="TransferFamily-UpdateHostKey-request-Description"></a>
An updated description for the host key\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Pattern: `^[\p{Print}]*$`   
Required: Yes

 ** [HostKeyId](#API_UpdateHostKey_RequestSyntax) **   <a name="TransferFamily-UpdateHostKey-request-HostKeyId"></a>
The identifier of the host key that you are updating\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$`   
Required: Yes

 ** [ServerId](#API_UpdateHostKey_RequestSyntax) **   <a name="TransferFamily-UpdateHostKey-request-ServerId"></a>
The identifier of the server that contains the host key that you are updating\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_UpdateHostKey_ResponseSyntax"></a>

```
{
   "HostKeyId": "string",
   "ServerId": "string"
}
```

## Response Elements<a name="API_UpdateHostKey_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [HostKeyId](#API_UpdateHostKey_ResponseSyntax) **   <a name="TransferFamily-UpdateHostKey-response-HostKeyId"></a>
Returns the host key identifier for the updated host key\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$` 

 ** [ServerId](#API_UpdateHostKey_ResponseSyntax) **   <a name="TransferFamily-UpdateHostKey-response-ServerId"></a>
Returns the server identifier for the server that contains the updated host key\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_UpdateHostKey_Errors"></a>

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

## See Also<a name="API_UpdateHostKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/UpdateHostKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UpdateHostKey) 
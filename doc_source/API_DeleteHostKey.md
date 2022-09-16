# DeleteHostKey<a name="API_DeleteHostKey"></a>

Deletes the host key that's specified in the `HoskKeyId` parameter\.

## Request Syntax<a name="API_DeleteHostKey_RequestSyntax"></a>

```
{
   "HostKeyId": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_DeleteHostKey_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [HostKeyId](#API_DeleteHostKey_RequestSyntax) **   <a name="TransferFamily-DeleteHostKey-request-HostKeyId"></a>
The identifier of the host key that you are deleting\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$`   
Required: Yes

 ** [ServerId](#API_DeleteHostKey_RequestSyntax) **   <a name="TransferFamily-DeleteHostKey-request-ServerId"></a>
The identifier of the server that contains the host key that you are deleting\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Elements<a name="API_DeleteHostKey_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteHostKey_Errors"></a>

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

## See Also<a name="API_DeleteHostKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DeleteHostKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DeleteHostKey) 
# StartServer<a name="API_StartServer"></a>

Changes the state of a file transfer protocol\-enabled server from `OFFLINE` to `ONLINE`\. It has no impact on a server that is already `ONLINE`\. An `ONLINE` server can accept and process file transfer jobs\.

The state of `STARTING` indicates that the server is in an intermediate state, either not fully able to respond, or not fully online\. The values of `START_FAILED` can indicate an error condition\.

No response is returned from this call\.

## Request Syntax<a name="API_StartServer_RequestSyntax"></a>

```
{
   "ServerId": "string"
}
```

## Request Parameters<a name="API_StartServer_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_StartServer_RequestSyntax) **   <a name="TransferFamily-StartServer-request-ServerId"></a>
A system\-assigned unique identifier for a server that you start\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Elements<a name="API_StartServer_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_StartServer_Errors"></a>

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

## Examples<a name="API_StartServer_Examples"></a>

### Example<a name="API_StartServer_Example_1"></a>

The following example starts a server\.

#### Sample Request<a name="API_StartServer_Example_1_Request"></a>

```
{
   "ServerId": "s-01234567890abcdef"
}
```

### Example<a name="API_StartServer_Example_2"></a>

This is a sample response for this API call\.

#### Sample Response<a name="API_StartServer_Example_2_Response"></a>

```
{
   "ServerId": "s-01234567890abcdef"
}
```

## See Also<a name="API_StartServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/StartServer) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/StartServer) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/StartServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/StartServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/StartServer) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/StartServer) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/StartServer) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/StartServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/StartServer) 
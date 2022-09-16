# StartFileTransfer<a name="API_StartFileTransfer"></a>

Begins an outbound file transfer to a remote AS2 server\. You specify the `ConnectorId` and the file paths for where to send the files\. 

## Request Syntax<a name="API_StartFileTransfer_RequestSyntax"></a>

```
{
   "ConnectorId": "string",
   "SendFilePaths": [ "string" ]
}
```

## Request Parameters<a name="API_StartFileTransfer_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ConnectorId](#API_StartFileTransfer_RequestSyntax) **   <a name="TransferFamily-StartFileTransfer-request-ConnectorId"></a>
The unique identifier for the connector\.   
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^c-([0-9a-f]{17})$`   
Required: Yes

 ** [SendFilePaths](#API_StartFileTransfer_RequestSyntax) **   <a name="TransferFamily-StartFileTransfer-request-SendFilePaths"></a>
An array of strings\. Each string represents the absolute path for one outbound file transfer\. For example, ` DOC-EXAMPLE-BUCKET/myfile.txt `\.   
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 10 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^(.)+`   
Required: Yes

## Response Syntax<a name="API_StartFileTransfer_ResponseSyntax"></a>

```
{
   "TransferId": "string"
}
```

## Response Elements<a name="API_StartFileTransfer_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [TransferId](#API_StartFileTransfer_ResponseSyntax) **   <a name="TransferFamily-StartFileTransfer-response-TransferId"></a>
Returns the unique identifier for this file transfer\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 512\.  
Pattern: `^[0-9a-zA-Z./-]+$` 

## Errors<a name="API_StartFileTransfer_Errors"></a>

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

## See Also<a name="API_StartFileTransfer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/StartFileTransfer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/StartFileTransfer) 
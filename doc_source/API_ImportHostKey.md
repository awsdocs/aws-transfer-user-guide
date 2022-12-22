# ImportHostKey<a name="API_ImportHostKey"></a>

Adds a host key to the server that's specified by the `ServerId` parameter\.

## Request Syntax<a name="API_ImportHostKey_RequestSyntax"></a>

```
{
   "Description": "string",
   "HostKeyBody": "string",
   "ServerId": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_ImportHostKey_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Description](#API_ImportHostKey_RequestSyntax) **   <a name="TransferFamily-ImportHostKey-request-Description"></a>
The text description that identifies this host key\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Pattern: `^[\p{Print}]*$`   
Required: No

 ** [HostKeyBody](#API_ImportHostKey_RequestSyntax) **   <a name="TransferFamily-ImportHostKey-request-HostKeyBody"></a>
The private key portion of an SSH key pair\.  
 AWS Transfer Family accepts RSA, ECDSA, and ED25519 keys\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Required: Yes

 ** [ServerId](#API_ImportHostKey_RequestSyntax) **   <a name="TransferFamily-ImportHostKey-request-ServerId"></a>
The identifier of the server that contains the host key that you are importing\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [Tags](#API_ImportHostKey_RequestSyntax) **   <a name="TransferFamily-ImportHostKey-request-Tags"></a>
Key\-value pairs that can be used to group and search for host keys\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_ImportHostKey_ResponseSyntax"></a>

```
{
   "HostKeyId": "string",
   "ServerId": "string"
}
```

## Response Elements<a name="API_ImportHostKey_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [HostKeyId](#API_ImportHostKey_ResponseSyntax) **   <a name="TransferFamily-ImportHostKey-response-HostKeyId"></a>
Returns the host key identifier for the imported key\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$` 

 ** [ServerId](#API_ImportHostKey_ResponseSyntax) **   <a name="TransferFamily-ImportHostKey-response-ServerId"></a>
Returns the server identifier that contains the imported key\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_ImportHostKey_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceExistsException **   
The requested resource does not exist\.  
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

## See Also<a name="API_ImportHostKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ImportHostKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ImportHostKey) 
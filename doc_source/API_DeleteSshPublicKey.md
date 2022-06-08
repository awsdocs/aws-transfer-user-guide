# DeleteSshPublicKey<a name="API_DeleteSshPublicKey"></a>

Deletes a user's Secure Shell \(SSH\) public key\.

## Request Syntax<a name="API_DeleteSshPublicKey_RequestSyntax"></a>

```
{
   "ServerId": "string",
   "SshPublicKeyId": "string",
   "UserName": "string"
}
```

## Request Parameters<a name="API_DeleteSshPublicKey_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_DeleteSshPublicKey_RequestSyntax) **   <a name="TransferFamily-DeleteSshPublicKey-request-ServerId"></a>
A system\-assigned unique identifier for a file transfer protocol\-enabled server instance that has the user assigned to it\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [SshPublicKeyId](#API_DeleteSshPublicKey_RequestSyntax) **   <a name="TransferFamily-DeleteSshPublicKey-request-SshPublicKeyId"></a>
A unique identifier used to reference your user's specific SSH key\.  
Type: String  
Length Constraints: Fixed length of 21\.  
Pattern: `^key-[0-9a-f]{17}$`   
Required: Yes

 ** [UserName](#API_DeleteSshPublicKey_RequestSyntax) **   <a name="TransferFamily-DeleteSshPublicKey-request-UserName"></a>
A unique string that identifies a user whose public key is being deleted\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

## Response Elements<a name="API_DeleteSshPublicKey_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteSshPublicKey_Errors"></a>

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

## Examples<a name="API_DeleteSshPublicKey_Examples"></a>

### Example<a name="API_DeleteSshPublicKey_Example_1"></a>

The following example deletes a user's SSH public key\.

#### Sample Request<a name="API_DeleteSshPublicKey_Example_1_Request"></a>

```
{
   "ServerId": "s-01234567890abcdef",
   "SshPublicKeyId": "MyPublicKey",
   "UserName": "my_user"
}
```

## See Also<a name="API_DeleteSshPublicKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DeleteSshPublicKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DeleteSshPublicKey) 
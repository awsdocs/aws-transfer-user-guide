# ImportSshPublicKey<a name="API_ImportSshPublicKey"></a>

Adds a Secure Shell \(SSH\) public key to a user account identified by a `UserName` value assigned to the specific file transfer protocol\-enabled server, identified by `ServerId`\.

The response returns the `UserName` value, the `ServerId` value, and the name of the `SshPublicKeyId`\.

## Request Syntax<a name="API_ImportSshPublicKey_RequestSyntax"></a>

```
{
   "ServerId": "string",
   "SshPublicKeyBody": "string",
   "UserName": "string"
}
```

## Request Parameters<a name="API_ImportSshPublicKey_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_ImportSshPublicKey_RequestSyntax) **   <a name="TransferFamily-ImportSshPublicKey-request-ServerId"></a>
A system\-assigned unique identifier for a server\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [SshPublicKeyBody](#API_ImportSshPublicKey_RequestSyntax) **   <a name="TransferFamily-ImportSshPublicKey-request-SshPublicKeyBody"></a>
The public key portion of an SSH key pair\.  
 AWS Transfer Family accepts RSA, ECDSA, and ED25519 keys\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Required: Yes

 ** [UserName](#API_ImportSshPublicKey_RequestSyntax) **   <a name="TransferFamily-ImportSshPublicKey-request-UserName"></a>
The name of the user account that is assigned to one or more servers\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

## Response Syntax<a name="API_ImportSshPublicKey_ResponseSyntax"></a>

```
{
   "ServerId": "string",
   "SshPublicKeyId": "string",
   "UserName": "string"
}
```

## Response Elements<a name="API_ImportSshPublicKey_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ServerId](#API_ImportSshPublicKey_ResponseSyntax) **   <a name="TransferFamily-ImportSshPublicKey-response-ServerId"></a>
A system\-assigned unique identifier for a server\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

 ** [SshPublicKeyId](#API_ImportSshPublicKey_ResponseSyntax) **   <a name="TransferFamily-ImportSshPublicKey-response-SshPublicKeyId"></a>
The name given to a public key by the system that was imported\.  
Type: String  
Length Constraints: Fixed length of 21\.  
Pattern: `^key-[0-9a-f]{17}$` 

 ** [UserName](#API_ImportSshPublicKey_ResponseSyntax) **   <a name="TransferFamily-ImportSshPublicKey-response-UserName"></a>
A user name assigned to the `ServerID` value that you specified\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$` 

## Errors<a name="API_ImportSshPublicKey_Errors"></a>

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

## Examples<a name="API_ImportSshPublicKey_Examples"></a>

### Example<a name="API_ImportSshPublicKey_Example_1"></a>

This command imports an ECDSA key stored in the `id_ecdsa.pub` file\.

#### <a name="w385ab1c52c12c98c17b3b5"></a>

```
aws transfer import-ssh-public-key --server-id s-021345abcdef6789 --ssh-public-key-body file://id_ecdsa.pub --user-name jane-doe
```

### Example<a name="API_ImportSshPublicKey_Example_2"></a>

If you run the previous command, the system returns the following information\.

#### <a name="w385ab1c52c12c98c17b5b5"></a>

```
{
    "ServerId": "s-021345abcdef6789",
   "SshPublicKeyId": "key-1234567890abcdef0",
   "UserName": "jane-doe"
}
```

## See Also<a name="API_ImportSshPublicKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ImportSshPublicKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ImportSshPublicKey) 
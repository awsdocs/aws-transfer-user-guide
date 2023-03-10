# TestIdentityProvider<a name="API_TestIdentityProvider"></a>

If the `IdentityProviderType` of a file transfer protocol\-enabled server is `AWS_DIRECTORY_SERVICE` or `API_Gateway`, tests whether your identity provider is set up successfully\. We highly recommend that you call this operation to test your authentication method as soon as you create your server\. By doing so, you can troubleshoot issues with the identity provider integration to ensure that your users can successfully use the service\.

 The `ServerId` and `UserName` parameters are required\. The `ServerProtocol`, `SourceIp`, and `UserPassword` are all optional\. 

**Note**  
 You cannot use `TestIdentityProvider` if the `IdentityProviderType` of your server is `SERVICE_MANAGED`\. 
+  If you provide any incorrect values for any parameters, the `Response` field is empty\. 
+  If you provide a server ID for a server that uses service\-managed users, you get an error: 

   ` An error occurred (InvalidRequestException) when calling the TestIdentityProvider operation: s-server-ID not configured for external auth ` 
+  If you enter a Server ID for the `--server-id` parameter that does not identify an actual Transfer server, you receive the following error: 

   `An error occurred (ResourceNotFoundException) when calling the TestIdentityProvider operation: Unknown server` 

## Request Syntax<a name="API_TestIdentityProvider_RequestSyntax"></a>

```
{
   "ServerId": "string",
   "ServerProtocol": "string",
   "SourceIp": "string",
   "UserName": "string",
   "UserPassword": "string"
}
```

## Request Parameters<a name="API_TestIdentityProvider_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_TestIdentityProvider_RequestSyntax) **   <a name="TransferFamily-TestIdentityProvider-request-ServerId"></a>
A system\-assigned identifier for a specific server\. That server's user authentication method is tested with a user name and password\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [ServerProtocol](#API_TestIdentityProvider_RequestSyntax) **   <a name="TransferFamily-TestIdentityProvider-request-ServerProtocol"></a>
The type of file transfer protocol to be tested\.  
The available protocols are:  
+ Secure Shell \(SSH\) File Transfer Protocol \(SFTP\)
+ File Transfer Protocol Secure \(FTPS\)
+ File Transfer Protocol \(FTP\)
+ Applicability Statement 2 \(AS2\)
Type: String  
Valid Values:` SFTP | FTP | FTPS | AS2`   
Required: No

 ** [SourceIp](#API_TestIdentityProvider_RequestSyntax) **   <a name="TransferFamily-TestIdentityProvider-request-SourceIp"></a>
The source IP address of the account to be tested\.  
Type: String  
Length Constraints: Maximum length of 32\.  
Pattern: `^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$`   
Required: No

 ** [UserName](#API_TestIdentityProvider_RequestSyntax) **   <a name="TransferFamily-TestIdentityProvider-request-UserName"></a>
The name of the account to be tested\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

 ** [UserPassword](#API_TestIdentityProvider_RequestSyntax) **   <a name="TransferFamily-TestIdentityProvider-request-UserPassword"></a>
The password of the account to be tested\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Required: No

## Response Syntax<a name="API_TestIdentityProvider_ResponseSyntax"></a>

```
{
   "Message": "string",
   "Response": "string",
   "StatusCode": number,
   "Url": "string"
}
```

## Response Elements<a name="API_TestIdentityProvider_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Message](#API_TestIdentityProvider_ResponseSyntax) **   <a name="TransferFamily-TestIdentityProvider-response-Message"></a>
A message that indicates whether the test was successful or not\.  
If an empty string is returned, the most likely cause is that the authentication failed due to an incorrect username or password\.
Type: String

 ** [Response](#API_TestIdentityProvider_ResponseSyntax) **   <a name="TransferFamily-TestIdentityProvider-response-Response"></a>
The response that is returned from your API Gateway\.  
Type: String

 ** [StatusCode](#API_TestIdentityProvider_ResponseSyntax) **   <a name="TransferFamily-TestIdentityProvider-response-StatusCode"></a>
The HTTP status code that is the response from your API Gateway\.  
Type: Integer

 ** [Url](#API_TestIdentityProvider_ResponseSyntax) **   <a name="TransferFamily-TestIdentityProvider-response-Url"></a>
The endpoint of the service used to authenticate a user\.  
Type: String  
Length Constraints: Maximum length of 255\.

## Errors<a name="API_TestIdentityProvider_Errors"></a>

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

## Examples<a name="API_TestIdentityProvider_Examples"></a>

### Example<a name="API_TestIdentityProvider_Example_1"></a>

The following request returns a message from an identity provider that a user name and password combination is a valid identity to use with AWS Transfer Family\.

#### Sample Request<a name="API_TestIdentityProvider_Example_1_Request"></a>

```
{
   "ServerID": "s-01234567890abcdef",
   "UserName": "my_user",
   "UserPassword": "MyPassword-1"
}
```

### Example<a name="API_TestIdentityProvider_Example_2"></a>

The following response shows a sample response for a successful test\.

#### Sample Response<a name="API_TestIdentityProvider_Example_2_Response"></a>

```
      
      "Response":"
      {\"homeDirectory\":\"/mybucket001\",\"homeDirectoryDetails\":null,\"homeDirectoryType\":\"PATH\",\"posixProfile\":null,
      \"publicKeys\":\"[ssh-rsa-key]\",\"role\":\"arn:aws:iam::123456789012:role/my_role\",\"policy\":null,\"username\":\"transferuser002\",
      \"identityProviderType\":null,\"userConfigMessage\":null)"}     
      "StatusCode": "200",
      "Message": ""
```

### Example<a name="API_TestIdentityProvider_Example_3"></a>

The following response indicates that the specified user belongs to more than one group that has access\.

#### <a name="w225ab1c52c14d152c21b7b5"></a>

```
          "Response":"",
          "StatusCode":200,
          "Message":"More than one associated access found for user's groups."
```

### Example<a name="API_TestIdentityProvider_Example_4"></a>

 If you have created and configured a custom identity provider by using an API Gateway, you can enter the following command to test your user: 

 `aws transfer test-identity-provider --server-id s-0123456789abcdefg --user-name myuser ` 

 where *s\-0123456789abcdefg* is your transfer server, and *myuser* is the username for your custom user\. 

 If the command succeeds, your response is similar to the following, where: 
+  AWS account ID is *012345678901* 
+ User role is *user\-role\-api\-gateway* 
+ Home directory is *myuser\-bucket* 
+ Public key is *public\-key* 
+ Invocation URL is *invocation\-URL* 

#### <a name="w225ab1c52c14d152c21b9c13"></a>

```
{
    "Response": "{\"Role\": \"arn:aws:iam::012345678901:role/user-role-api-gateway\",\"HomeDirectory\": \"/myuser-bucket\",\"PublicKeys\": \"[public-key]\"}",
    "StatusCode": 200,
    "Message": "",
    "Url": "https://invocation-URL/servers/s-0123456789abcdefg/users/myuser/config"
}
```

## See Also<a name="API_TestIdentityProvider_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/TestIdentityProvider) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/TestIdentityProvider) 
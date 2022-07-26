# UpdateUser<a name="API_UpdateUser"></a>

Assigns new properties to a user\. Parameters you pass modify any or all of the following: the home directory, role, and policy for the `UserName` and `ServerId` you specify\.

The response returns the `ServerId` and the `UserName` for the updated user\.

## Request Syntax<a name="API_UpdateUser_RequestSyntax"></a>

```
{
   "HomeDirectory": "string",
   "HomeDirectoryMappings": [ 
      { 
         "Entry": "string",
         "Target": "string"
      }
   ],
   "HomeDirectoryType": "string",
   "Policy": "string",
   "PosixProfile": { 
      "Gid": number,
      "SecondaryGids": [ number ],
      "Uid": number
   },
   "Role": "string",
   "ServerId": "string",
   "UserName": "string"
}
```

## Request Parameters<a name="API_UpdateUser_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [HomeDirectory](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-HomeDirectory"></a>
The landing directory \(folder\) for a user when they log in to the server using the client\.  
A `HomeDirectory` example is `/bucket_name/home/mydirectory`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: No

 ** [HomeDirectoryMappings](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-HomeDirectoryMappings"></a>
Logical directory mappings that specify what Amazon S3 or Amazon EFS paths and keys should be visible to your user and how you want to make them visible\. You must specify the `Entry` and `Target` pair, where `Entry` shows how the path is made visible and `Target` is the actual Amazon S3 or Amazon EFS path\. If you only specify a target, it is displayed as is\. You also must ensure that your AWS Identity and Access Management \(IAM\) role provides access to paths in `Target`\. This value can be set only when `HomeDirectoryType` is set to *LOGICAL*\.  
The following is an `Entry` and `Target` pair example\.  
 `[ { "Entry": "/directory1", "Target": "/bucket_name/home/mydirectory" } ]`   
In most cases, you can use this value instead of the session policy to lock down your user to the designated home directory \("`chroot`"\)\. To do this, you can set `Entry` to '/' and set `Target` to the HomeDirectory parameter value\.  
The following is an `Entry` and `Target` pair example for `chroot`\.  
 `[ { "Entry": "/", "Target": "/bucket_name/home/mydirectory" } ]`   
Type: Array of [HomeDirectoryMapEntry](API_HomeDirectoryMapEntry.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** [HomeDirectoryType](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-HomeDirectoryType"></a>
The type of landing directory \(folder\) that you want your users' home directory to be when they log in to the server\. If you set it to `PATH`, the user will see the absolute Amazon S3 bucket or EFS paths as is in their file transfer protocol clients\. If you set it `LOGICAL`, you need to provide mappings in the `HomeDirectoryMappings` for how you want to make Amazon S3 or Amazon EFS paths visible to your users\.  
Type: String  
Valid Values:` PATH | LOGICAL`   
Required: No

 ** [Policy](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-Policy"></a>
A session policy for your user so that you can use the same AWS Identity and Access Management \(IAM\) role across multiple users\. This policy scopes down a user's access to portions of their Amazon S3 bucket\. Variables that you can use inside this policy include `${Transfer:UserName}`, `${Transfer:HomeDirectory}`, and `${Transfer:HomeBucket}`\.  
This policy applies only when the domain of `ServerId` is Amazon S3\. Amazon EFS does not use session policies\.  
For session policies, AWS Transfer Family stores the policy as a JSON blob, instead of the Amazon Resource Name \(ARN\) of the policy\. You save the policy as a JSON blob and pass it in the `Policy` argument\.  
For an example of a session policy, see [Example session policy](https://docs.aws.amazon.com/transfer/latest/userguide/session-policy.html)\.  
For more information, see [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) in the * AWS Security Token Service API Reference*\.
Type: String  
Length Constraints: Maximum length of 2048\.  
Required: No

 ** [PosixProfile](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-PosixProfile"></a>
Specifies the full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary groups IDs \(`SecondaryGids`\), that controls your users' access to your Amazon Elastic File Systems \(Amazon EFS\)\. The POSIX permissions that are set on files and directories in your file system determines the level of access your users get when transferring files into and out of your Amazon EFS file systems\.  
Type: [PosixProfile](API_PosixProfile.md) object  
Required: No

 ** [Role](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-Role"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that controls your users' access to your Amazon S3 bucket or Amazon EFS file system\. The policies attached to this role determine the level of access that you want to provide your users when transferring files into and out of your Amazon S3 bucket or Amazon EFS file system\. The IAM role should also contain a trust relationship that allows the server to access your resources when servicing your users' transfer requests\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** [ServerId](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-ServerId"></a>
A system\-assigned unique identifier for a server instance that the user account is assigned to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [UserName](#API_UpdateUser_RequestSyntax) **   <a name="TransferFamily-UpdateUser-request-UserName"></a>
A unique string that identifies a user and is associated with a server as specified by the `ServerId`\. This user name must be a minimum of 3 and a maximum of 100 characters long\. The following are valid characters: a\-z, A\-Z, 0\-9, underscore '\_', hyphen '\-', period '\.', and at sign '@'\. The user name can't start with a hyphen, period, or at sign\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

## Response Syntax<a name="API_UpdateUser_ResponseSyntax"></a>

```
{
   "ServerId": "string",
   "UserName": "string"
}
```

## Response Elements<a name="API_UpdateUser_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ServerId](#API_UpdateUser_ResponseSyntax) **   <a name="TransferFamily-UpdateUser-response-ServerId"></a>
A system\-assigned unique identifier for a server instance that the user account is assigned to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

 ** [UserName](#API_UpdateUser_ResponseSyntax) **   <a name="TransferFamily-UpdateUser-response-UserName"></a>
The unique identifier for a user that is assigned to a server instance that was specified in the request\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$` 

## Errors<a name="API_UpdateUser_Errors"></a>

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

## Examples<a name="API_UpdateUser_Examples"></a>

### Example<a name="API_UpdateUser_Example_1"></a>

The following example updates a user account\.

#### Sample Request<a name="API_UpdateUser_Example_1_Request"></a>

```
{
   "HomeDirectory": "/bucket2/documentation",
   "HomeDirectoryMappings": [ 
      { 
         "Entry": "/directory1",
         "Target": "/bucket_name/home/mydirectory"
      }
   ],
   "HomeDirectoryType:" "PATH",
   "Role": "AssumeRole",
   "ServerId": "s-01234567890abcdef",
   "UserName": "my_user"
}
```

### Example<a name="API_UpdateUser_Example_2"></a>

This is a sample response for this API call\.

#### Sample Response<a name="API_UpdateUser_Example_2_Response"></a>

```
{
   "ServerId": "s-01234567890abcdef",
   "UserName": "my_user"
}
```

## See Also<a name="API_UpdateUser_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/UpdateUser) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UpdateUser) 
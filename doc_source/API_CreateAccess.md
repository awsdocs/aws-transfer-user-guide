# CreateAccess<a name="API_CreateAccess"></a>

Used by administrators to choose which groups in the directory should have access to upload and download files over the enabled protocols using AWS Transfer Family\. For example, a Microsoft Active Directory might contain 50,000 users, but only a small fraction might need the ability to transfer files to the server\. An administrator can use `CreateAccess` to limit the access to the correct set of users who need this ability\.

## Request Syntax<a name="API_CreateAccess_RequestSyntax"></a>

```
{
   "ExternalId": "string",
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
   "ServerId": "string"
}
```

## Request Parameters<a name="API_CreateAccess_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ExternalId](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-ExternalId"></a>
A unique identifier that is required to identify specific groups within your directory\. The users of the group that you associate have access to your Amazon S3 or Amazon EFS resources over the enabled protocols using AWS Transfer Family\. If you know the group name, you can view the SID values by running the following command using Windows PowerShell\.  
 `Get-ADGroup -Filter {samAccountName -like "YourGroupName*"} -Properties * | Select SamAccountName,ObjectSid`   
In that command, replace *YourGroupName* with the name of your Active Directory group\.  
The regex used to validate this parameter is a string of characters consisting of uppercase and lowercase alphanumeric characters with no spaces\. You can also include underscores or any of the following characters: =,\.@:/\-  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^S-1-[\d-]+$`   
Required: Yes

 ** [HomeDirectory](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-HomeDirectory"></a>
The landing directory \(folder\) for a user when they log in to the server using the client\.  
A `HomeDirectory` example is `/bucket_name/home/mydirectory`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: No

 ** [HomeDirectoryMappings](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-HomeDirectoryMappings"></a>
Logical directory mappings that specify what Amazon S3 or Amazon EFS paths and keys should be visible to your user and how you want to make them visible\. You must specify the `Entry` and `Target` pair, where `Entry` shows how the path is made visible and `Target` is the actual Amazon S3 or Amazon EFS path\. If you only specify a target, it is displayed as is\. You also must ensure that your AWS Identity and Access Management \(IAM\) role provides access to paths in `Target`\. This value can only be set when `HomeDirectoryType` is set to *LOGICAL*\.  
The following is an `Entry` and `Target` pair example\.  
 `[ { "Entry": "/directory1", "Target": "/bucket_name/home/mydirectory" } ]`   
In most cases, you can use this value instead of the session policy to lock down your user to the designated home directory \("`chroot`"\)\. To do this, you can set `Entry` to `/` and set `Target` to the `HomeDirectory` parameter value\.  
The following is an `Entry` and `Target` pair example for `chroot`\.  
 `[ { "Entry": "/", "Target": "/bucket_name/home/mydirectory" } ]`   
Type: Array of [HomeDirectoryMapEntry](API_HomeDirectoryMapEntry.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** [HomeDirectoryType](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-HomeDirectoryType"></a>
The type of landing directory \(folder\) you want your users' home directory to be when they log into the server\. If you set it to `PATH`, the user will see the absolute Amazon S3 bucket or EFS paths as is in their file transfer protocol clients\. If you set it `LOGICAL`, you need to provide mappings in the `HomeDirectoryMappings` for how you want to make Amazon S3 or EFS paths visible to your users\.  
Type: String  
Valid Values:` PATH | LOGICAL`   
Required: No

 ** [Policy](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-Policy"></a>
A session policy for your user so that you can use the same IAM role across multiple users\. This policy scopes down user access to portions of their Amazon S3 bucket\. Variables that you can use inside this policy include `${Transfer:UserName}`, `${Transfer:HomeDirectory}`, and `${Transfer:HomeBucket}`\.  
This only applies when the domain of `ServerId` is S3\. EFS does not use session policies\.  
For session policies, AWS Transfer Family stores the policy as a JSON blob, instead of the Amazon Resource Name \(ARN\) of the policy\. You save the policy as a JSON blob and pass it in the `Policy` argument\.  
For an example of a session policy, see [Example session policy](https://docs.aws.amazon.com/transfer/latest/userguide/session-policy.html)\.  
For more information, see [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) in the * AWS Security Token Service API Reference*\.
Type: String  
Length Constraints: Maximum length of 2048\.  
Required: No

 ** [PosixProfile](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-PosixProfile"></a>
The full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary groups IDs \(`SecondaryGids`\), that controls your users' access to your Amazon EFS file systems\. The POSIX permissions that are set on files and directories in your file system determine the level of access your users get when transferring files into and out of your Amazon EFS file systems\.  
Type: [PosixProfile](API_PosixProfile.md) object  
Required: No

 ** [Role](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-Role"></a>
Specifies the Amazon Resource Name \(ARN\) of the IAM role that controls your users' access to your Amazon S3 bucket or EFS file system\. The policies attached to this role determine the level of access that you want to provide your users when transferring files into and out of your Amazon S3 bucket or EFS file system\. The IAM role should also contain a trust relationship that allows the server to access your resources when servicing your users' transfer requests\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: Yes

 ** [ServerId](#API_CreateAccess_RequestSyntax) **   <a name="TransferFamily-CreateAccess-request-ServerId"></a>
A system\-assigned unique identifier for a server instance\. This is the specific server that you added your user to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_CreateAccess_ResponseSyntax"></a>

```
{
   "ExternalId": "string",
   "ServerId": "string"
}
```

## Response Elements<a name="API_CreateAccess_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ExternalId](#API_CreateAccess_ResponseSyntax) **   <a name="TransferFamily-CreateAccess-response-ExternalId"></a>
The external ID of the group whose users have access to your Amazon S3 or Amazon EFS resources over the enabled protocols using AWS Transfer Family\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^S-1-[\d-]+$` 

 ** [ServerId](#API_CreateAccess_ResponseSyntax) **   <a name="TransferFamily-CreateAccess-response-ServerId"></a>
The ID of the server that the user is attached to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_CreateAccess_Errors"></a>

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

## See Also<a name="API_CreateAccess_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateAccess) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateAccess) 
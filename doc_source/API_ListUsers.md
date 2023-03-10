# ListUsers<a name="API_ListUsers"></a>

Lists the users for a file transfer protocol\-enabled server that you specify by passing the `ServerId` parameter\.

## Request Syntax<a name="API_ListUsers_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_ListUsers_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListUsers_RequestSyntax) **   <a name="TransferFamily-ListUsers-request-MaxResults"></a>
Specifies the number of users to return as a response to the `ListUsers` request\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListUsers_RequestSyntax) **   <a name="TransferFamily-ListUsers-request-NextToken"></a>
When you can get additional results from the `ListUsers` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional users\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [ServerId](#API_ListUsers_RequestSyntax) **   <a name="TransferFamily-ListUsers-request-ServerId"></a>
A system\-assigned unique identifier for a server that has users assigned to it\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_ListUsers_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "ServerId": "string",
   "Users": [ 
      { 
         "Arn": "string",
         "HomeDirectory": "string",
         "HomeDirectoryType": "string",
         "Role": "string",
         "SshPublicKeyCount": number,
         "UserName": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListUsers_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListUsers_ResponseSyntax) **   <a name="TransferFamily-ListUsers-response-NextToken"></a>
When you can get additional results from the `ListUsers` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional users\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [ServerId](#API_ListUsers_ResponseSyntax) **   <a name="TransferFamily-ListUsers-response-ServerId"></a>
A system\-assigned unique identifier for a server that the users are assigned to\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

 ** [Users](#API_ListUsers_ResponseSyntax) **   <a name="TransferFamily-ListUsers-response-Users"></a>
Returns the Transfer Family users and their properties for the `ServerId` value that you specify\.  
Type: Array of [ListedUser](API_ListedUser.md) objects

## Errors<a name="API_ListUsers_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidNextTokenException **   
The `NextToken` parameter that was passed is invalid\.  
HTTP Status Code: 400

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## Examples<a name="API_ListUsers_Examples"></a>

### Example<a name="API_ListUsers_Example_1"></a>

The `ListUsers` API call returns a list of users associated with a server you specify\.

#### Sample Request<a name="API_ListUsers_Example_1_Request"></a>

```
     
         {
          "MaxResults": 100,
          "NextToken": "eyJNYXJrZXIiOiBudWxsLCAiYm90b1X0cnVuU2F0ZV9hbW91bnQiOiAyfQ==",
          "ServerId": "s-01234567890abcdef"
          }
```

### Example<a name="API_ListUsers_Example_2"></a>

This is a sample response for this API call\.

#### Sample Response<a name="API_ListUsers_Example_2_Response"></a>

```
{
   "NextToken": "eyJNYXJrZXIiOiBudWxsLCAiYm90b1X0cnVuU2F0ZV9hbW91bnQiOiAyfQ==",
   "ServerId": "s-01234567890abcdef",
   "Users": [ 
      { 
         "Arn": "arn:aws:transfer:us-east-1:176354371281:user/s-01234567890abcdef/charlie",
         "HomeDirectory": "/tests/home/charlie",
         "SshPublicKeyCount": 1,
         "Role": "arn:aws:iam::176354371281:role/transfer-role1",
         "Tags": [ 
            { 
               "Key": "Name",
               "Value": "user1"
            }
         ],
         "UserName": "my_user"
      }
   ]
}
```

## See Also<a name="API_ListUsers_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListUsers) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListUsers) 
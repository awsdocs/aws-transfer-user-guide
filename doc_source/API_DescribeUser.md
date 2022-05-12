# DescribeUser<a name="API_DescribeUser"></a>

Describes the user assigned to the specific file transfer protocol\-enabled server, as identified by its `ServerId` property\.

The response from this call returns the properties of the user associated with the `ServerId` value that was specified\.

## Request Syntax<a name="API_DescribeUser_RequestSyntax"></a>

```
{
   "ServerId": "string",
   "UserName": "string"
}
```

## Request Parameters<a name="API_DescribeUser_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_DescribeUser_RequestSyntax) **   <a name="TransferFamily-DescribeUser-request-ServerId"></a>
A system\-assigned unique identifier for a server that has this user assigned\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [UserName](#API_DescribeUser_RequestSyntax) **   <a name="TransferFamily-DescribeUser-request-UserName"></a>
The name of the user assigned to one or more servers\. User names are part of the sign\-in credentials to use the AWS Transfer Family service and perform file transfer tasks\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 100\.  
Pattern: `^[\w][\w@.-]{2,99}$`   
Required: Yes

## Response Syntax<a name="API_DescribeUser_ResponseSyntax"></a>

```
{
   "ServerId": "string",
   "User": { 
      "Arn": "string",
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
      "SshPublicKeys": [ 
         { 
            "DateImported": number,
            "SshPublicKeyBody": "string",
            "SshPublicKeyId": "string"
         }
      ],
      "Tags": [ 
         { 
            "Key": "string",
            "Value": "string"
         }
      ],
      "UserName": "string"
   }
}
```

## Response Elements<a name="API_DescribeUser_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ServerId](#API_DescribeUser_ResponseSyntax) **   <a name="TransferFamily-DescribeUser-response-ServerId"></a>
A system\-assigned unique identifier for a server that has this user assigned\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

 ** [User](#API_DescribeUser_ResponseSyntax) **   <a name="TransferFamily-DescribeUser-response-User"></a>
An array containing the properties of the user account for the `ServerID` value that you specified\.  
Type: [DescribedUser](API_DescribedUser.md) object

## Errors<a name="API_DescribeUser_Errors"></a>

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

## Examples<a name="API_DescribeUser_Examples"></a>

### Example<a name="API_DescribeUser_Example_1"></a>

The following example returns the properties assigned to a server\.

#### Sample Request<a name="API_DescribeUser_Example_1_Request"></a>

```
{
   "ServerId": "s-01234567890abcdef",
   "UserName": "my_user"
}
```

### Example<a name="API_DescribeUser_Example_2"></a>

This example illustrates one usage of DescribeUser\.

#### Sample Response<a name="API_DescribeUser_Example_2_Response"></a>

```
{
   "User": { 
      "Arn": "arn:aws:transfer:us-east-1:176354371281:server/s-01234567890abcdef",
      "HomeDirectory": "/home/mydirectory",
      "HomeDirectoryType:" "PATH",
      "Role": "arn:aws:iam::176354371281:role/my_role",
      "SshPublicKeys": "AAAAB3NzaC1yc2EAAAADAQABAAABAQCOtfCAis3aHfM6yc8KWAlMQxVDBHyccCde9MdLf4DQNXn8HjAHf+Bc1vGGCAREFUL1NO2PEEKING3ALLOWEDfIf+JBecywfO35Cm6IKIV0JF2YOPXvOuQRs80hQaBUvQL9xw6VEb4xzbit2QB6",
      "Tags": [ 
         { 
            "Key": "Name",
            "Value": "MyServer"
         }
      "UserName": "my_user",
      ]
   }
}
```

## See Also<a name="API_DescribeUser_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeUser) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeUser) 
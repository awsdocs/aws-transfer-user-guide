# DescribeAccess<a name="API_DescribeAccess"></a>

Describes the access that is assigned to the specific file transfer protocol\-enabled server, as identified by its `ServerId` property and its `ExternalId`\.

The response from this call returns the properties of the access that is associated with the `ServerId` value that was specified\.

## Request Syntax<a name="API_DescribeAccess_RequestSyntax"></a>

```
{
   "ExternalId": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_DescribeAccess_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ExternalId](#API_DescribeAccess_RequestSyntax) **   <a name="TransferFamily-DescribeAccess-request-ExternalId"></a>
A unique identifier that is required to identify specific groups within your directory\. The users of the group that you associate have access to your Amazon S3 or Amazon EFS resources over the enabled protocols using AWS Transfer Family\. If you know the group name, you can view the SID values by running the following command using Windows PowerShell\.  
 `Get-ADGroup -Filter {samAccountName -like "YourGroupName*"} -Properties * | Select SamAccountName,ObjectSid`   
In that command, replace *YourGroupName* with the name of your Active Directory group\.  
The regular expression used to validate this parameter is a string of characters consisting of uppercase and lowercase alphanumeric characters with no spaces\. You can also include underscores or any of the following characters: =,\.@:/\-  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^S-1-[\d-]+$`   
Required: Yes

 ** [ServerId](#API_DescribeAccess_RequestSyntax) **   <a name="TransferFamily-DescribeAccess-request-ServerId"></a>
A system\-assigned unique identifier for a server that has this access assigned\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_DescribeAccess_ResponseSyntax"></a>

```
{
   "Access": { 
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
      "Role": "string"
   },
   "ServerId": "string"
}
```

## Response Elements<a name="API_DescribeAccess_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Access](#API_DescribeAccess_ResponseSyntax) **   <a name="TransferFamily-DescribeAccess-response-Access"></a>
The external identifier of the server that the access is attached to\.  
Type: [DescribedAccess](API_DescribedAccess.md) object

 ** [ServerId](#API_DescribeAccess_ResponseSyntax) **   <a name="TransferFamily-DescribeAccess-response-ServerId"></a>
A system\-assigned unique identifier for a server that has this access assigned\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_DescribeAccess_Errors"></a>

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

## See Also<a name="API_DescribeAccess_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeAccess) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeAccess) 
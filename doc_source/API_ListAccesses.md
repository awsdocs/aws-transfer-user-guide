# ListAccesses<a name="API_ListAccesses"></a>

Lists the details for all the accesses you have on your server\.

## Request Syntax<a name="API_ListAccesses_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_ListAccesses_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListAccesses_RequestSyntax) **   <a name="TransferFamily-ListAccesses-request-MaxResults"></a>
Specifies the maximum number of access SIDs to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListAccesses_RequestSyntax) **   <a name="TransferFamily-ListAccesses-request-NextToken"></a>
When you can get additional results from the `ListAccesses` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional accesses\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [ServerId](#API_ListAccesses_RequestSyntax) **   <a name="TransferFamily-ListAccesses-request-ServerId"></a>
A system\-assigned unique identifier for a server that has users assigned to it\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_ListAccesses_ResponseSyntax"></a>

```
{
   "Accesses": [ 
      { 
         "ExternalId": "string",
         "HomeDirectory": "string",
         "HomeDirectoryType": "string",
         "Role": "string"
      }
   ],
   "NextToken": "string",
   "ServerId": "string"
}
```

## Response Elements<a name="API_ListAccesses_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Accesses](#API_ListAccesses_ResponseSyntax) **   <a name="TransferFamily-ListAccesses-response-Accesses"></a>
Returns the accesses and their properties for the `ServerId` value that you specify\.  
Type: Array of [ListedAccess](API_ListedAccess.md) objects

 ** [NextToken](#API_ListAccesses_ResponseSyntax) **   <a name="TransferFamily-ListAccesses-response-NextToken"></a>
When you can get additional results from the `ListAccesses` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional accesses\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [ServerId](#API_ListAccesses_ResponseSyntax) **   <a name="TransferFamily-ListAccesses-response-ServerId"></a>
A system\-assigned unique identifier for a server that has users assigned to it\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_ListAccesses_Errors"></a>

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

## See Also<a name="API_ListAccesses_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListAccesses) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListAccesses) 
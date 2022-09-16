# ListHostKeys<a name="API_ListHostKeys"></a>

Returns a list of host keys for the server that's specified by the `ServerId` parameter\.

## Request Syntax<a name="API_ListHostKeys_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_ListHostKeys_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListHostKeys_RequestSyntax) **   <a name="TransferFamily-ListHostKeys-request-MaxResults"></a>
The maximum number of host keys to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListHostKeys_RequestSyntax) **   <a name="TransferFamily-ListHostKeys-request-NextToken"></a>
When there are additional results that were not returned, a `NextToken` parameter is returned\. You can use that value for a subsequent call to `ListHostKeys` to continue listing results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [ServerId](#API_ListHostKeys_RequestSyntax) **   <a name="TransferFamily-ListHostKeys-request-ServerId"></a>
The identifier of the server that contains the host keys that you want to view\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_ListHostKeys_ResponseSyntax"></a>

```
{
   "HostKeys": [ 
      { 
         "Arn": "string",
         "DateImported": number,
         "Description": "string",
         "Fingerprint": "string",
         "HostKeyId": "string",
         "Type": "string"
      }
   ],
   "NextToken": "string",
   "ServerId": "string"
}
```

## Response Elements<a name="API_ListHostKeys_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [HostKeys](#API_ListHostKeys_ResponseSyntax) **   <a name="TransferFamily-ListHostKeys-response-HostKeys"></a>
Returns an array, where each item contains the details of a host key\.  
Type: Array of [ListedHostKey](API_ListedHostKey.md) objects

 ** [NextToken](#API_ListHostKeys_ResponseSyntax) **   <a name="TransferFamily-ListHostKeys-response-NextToken"></a>
Returns a token that you can use to call `ListHostKeys` again and receive additional results, if there are any\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [ServerId](#API_ListHostKeys_ResponseSyntax) **   <a name="TransferFamily-ListHostKeys-response-ServerId"></a>
Returns the server identifier that contains the listed host keys\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$` 

## Errors<a name="API_ListHostKeys_Errors"></a>

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

## See Also<a name="API_ListHostKeys_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListHostKeys) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListHostKeys) 
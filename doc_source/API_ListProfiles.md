# ListProfiles<a name="API_ListProfiles"></a>

Returns a list of the profiles for your system\. If you want to limit the results to a certain number, supply a value for the `MaxResults` parameter\. If you ran the command previously and received a value for `NextToken`, you can supply that value to continue listing profiles from where you left off\.

## Request Syntax<a name="API_ListProfiles_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ProfileType": "string"
}
```

## Request Parameters<a name="API_ListProfiles_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListProfiles_RequestSyntax) **   <a name="TransferFamily-ListProfiles-request-MaxResults"></a>
The maximum number of profiles to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListProfiles_RequestSyntax) **   <a name="TransferFamily-ListProfiles-request-NextToken"></a>
When there are additional results that were not returned, a `NextToken` parameter is returned\. You can use that value for a subsequent call to `ListProfiles` to continue listing results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [ProfileType](#API_ListProfiles_RequestSyntax) **   <a name="TransferFamily-ListProfiles-request-ProfileType"></a>
Indicates whether to list only `LOCAL` type profiles or only `PARTNER` type profiles\. If not supplied in the request, the command lists all types of profiles\.  
Type: String  
Valid Values:` LOCAL | PARTNER`   
Required: No

## Response Syntax<a name="API_ListProfiles_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Profiles": [ 
      { 
         "Arn": "string",
         "As2Id": "string",
         "ProfileId": "string",
         "ProfileType": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListProfiles_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListProfiles_ResponseSyntax) **   <a name="TransferFamily-ListProfiles-response-NextToken"></a>
Returns a token that you can use to call `ListProfiles` again and receive additional results, if there are any\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [Profiles](#API_ListProfiles_ResponseSyntax) **   <a name="TransferFamily-ListProfiles-response-Profiles"></a>
Returns an array, where each item contains the details of a profile\.  
Type: Array of [ListedProfile](API_ListedProfile.md) objects

## Errors<a name="API_ListProfiles_Errors"></a>

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

## See Also<a name="API_ListProfiles_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListProfiles) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListProfiles) 
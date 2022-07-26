# ListAgreements<a name="API_ListAgreements"></a>

Returns a list of the agreements for the server that's identified by the `ServerId` that you supply\. If you want to limit the results to a certain number, supply a value for the `MaxResults` parameter\. If you ran the command previously and received a value for `NextToken`, you can supply that value to continue listing agreements from where you left off\.

## Request Syntax<a name="API_ListAgreements_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ServerId": "string"
}
```

## Request Parameters<a name="API_ListAgreements_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListAgreements_RequestSyntax) **   <a name="TransferFamily-ListAgreements-request-MaxResults"></a>
The maximum number of agreements to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListAgreements_RequestSyntax) **   <a name="TransferFamily-ListAgreements-request-NextToken"></a>
When you can get additional results from the `ListAgreements` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional agreements\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

 ** [ServerId](#API_ListAgreements_RequestSyntax) **   <a name="TransferFamily-ListAgreements-request-ServerId"></a>
The identifier of the server for which you want a list of agreements\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_ListAgreements_ResponseSyntax"></a>

```
{
   "Agreements": [ 
      { 
         "AgreementId": "string",
         "Arn": "string",
         "Description": "string",
         "LocalProfileId": "string",
         "PartnerProfileId": "string",
         "ServerId": "string",
         "Status": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListAgreements_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Agreements](#API_ListAgreements_ResponseSyntax) **   <a name="TransferFamily-ListAgreements-response-Agreements"></a>
Returns an array, where each item contains the details of an agreement\.  
Type: Array of [ListedAgreement](API_ListedAgreement.md) objects

 ** [NextToken](#API_ListAgreements_ResponseSyntax) **   <a name="TransferFamily-ListAgreements-response-NextToken"></a>
Returns a token that you can use to call `ListAgreements` again and receive additional results, if there are any\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

## Errors<a name="API_ListAgreements_Errors"></a>

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

## See Also<a name="API_ListAgreements_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListAgreements) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListAgreements) 
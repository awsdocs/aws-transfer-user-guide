# ListSecurityPolicies<a name="API_ListSecurityPolicies"></a>

Lists the security policies that are attached to your file transfer protocol\-enabled servers\.

## Request Syntax<a name="API_ListSecurityPolicies_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListSecurityPolicies_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListSecurityPolicies_RequestSyntax) **   <a name="TransferFamily-ListSecurityPolicies-request-MaxResults"></a>
Specifies the number of security policies to return as a response to the `ListSecurityPolicies` query\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListSecurityPolicies_RequestSyntax) **   <a name="TransferFamily-ListSecurityPolicies-request-NextToken"></a>
When additional results are obtained from the `ListSecurityPolicies` command, a `NextToken` parameter is returned in the output\. You can then pass the `NextToken` parameter in a subsequent command to continue listing additional security policies\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

## Response Syntax<a name="API_ListSecurityPolicies_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "SecurityPolicyNames": [ "string" ]
}
```

## Response Elements<a name="API_ListSecurityPolicies_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListSecurityPolicies_ResponseSyntax) **   <a name="TransferFamily-ListSecurityPolicies-response-NextToken"></a>
When you can get additional results from the `ListSecurityPolicies` operation, a `NextToken` parameter is returned in the output\. In a following command, you can pass in the `NextToken` parameter to continue listing security policies\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [SecurityPolicyNames](#API_ListSecurityPolicies_ResponseSyntax) **   <a name="TransferFamily-ListSecurityPolicies-response-SecurityPolicyNames"></a>
An array of security policies that were listed\.  
Type: Array of strings  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+` 

## Errors<a name="API_ListSecurityPolicies_Errors"></a>

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

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_ListSecurityPolicies_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListSecurityPolicies) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListSecurityPolicies) 
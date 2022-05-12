# DescribeSecurityPolicy<a name="API_DescribeSecurityPolicy"></a>

Describes the security policy that is attached to your file transfer protocol\-enabled server\. The response contains a description of the security policy's properties\. For more information about security policies, see [Working with security policies](https://docs.aws.amazon.com/transfer/latest/userguide/security-policies.html)\.

## Request Syntax<a name="API_DescribeSecurityPolicy_RequestSyntax"></a>

```
{
   "SecurityPolicyName": "string"
}
```

## Request Parameters<a name="API_DescribeSecurityPolicy_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [SecurityPolicyName](#API_DescribeSecurityPolicy_RequestSyntax) **   <a name="TransferFamily-DescribeSecurityPolicy-request-SecurityPolicyName"></a>
Specifies the name of the security policy that is attached to the server\.  
Type: String  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+`   
Required: Yes

## Response Syntax<a name="API_DescribeSecurityPolicy_ResponseSyntax"></a>

```
{
   "SecurityPolicy": { 
      "Fips": boolean,
      "SecurityPolicyName": "string",
      "SshCiphers": [ "string" ],
      "SshKexs": [ "string" ],
      "SshMacs": [ "string" ],
      "TlsCiphers": [ "string" ]
   }
}
```

## Response Elements<a name="API_DescribeSecurityPolicy_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [SecurityPolicy](#API_DescribeSecurityPolicy_ResponseSyntax) **   <a name="TransferFamily-DescribeSecurityPolicy-response-SecurityPolicy"></a>
An array containing the properties of the security policy\.  
Type: [DescribedSecurityPolicy](API_DescribedSecurityPolicy.md) object

## Errors<a name="API_DescribeSecurityPolicy_Errors"></a>

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

## See Also<a name="API_DescribeSecurityPolicy_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeSecurityPolicy) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeSecurityPolicy) 
# UntagResource<a name="API_UntagResource"></a>

Detaches a key\-value pair from a resource, as identified by its Amazon Resource Name \(ARN\)\. Resources are users, servers, roles, and other entities\.

No response is returned from this call\.

## Request Syntax<a name="API_UntagResource_RequestSyntax"></a>

```
{
   "Arn": "string",
   "TagKeys": [ "string" ]
}
```

## Request Parameters<a name="API_UntagResource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Arn](#API_UntagResource_RequestSyntax) **   <a name="TransferFamily-UntagResource-request-Arn"></a>
The value of the resource that will have the tag removed\. An Amazon Resource Name \(ARN\) is an identifier for a specific AWS resource, such as a server, user, or role\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** [TagKeys](#API_UntagResource_RequestSyntax) **   <a name="TransferFamily-UntagResource-request-TagKeys"></a>
TagKeys are key\-value pairs assigned to ARNs that can be used to group and search for resources by type\. This metadata can be attached to resources for any purpose\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Length Constraints: Maximum length of 128\.  
Required: Yes

## Response Elements<a name="API_UntagResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UntagResource_Errors"></a>

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

## Examples<a name="API_UntagResource_Examples"></a>

### Example<a name="API_UntagResource_Example_1"></a>

The following example removes a tag of a file transfer protocol\-enabled server\.

#### Sample Request<a name="API_UntagResource_Example_1_Request"></a>

```
{
   "Arn": "arn:aws:transfer:us-east-1:176354371281:server/s-01234567890abcdef",
   "TagKeys": "Europe" ]
}
```

### Example<a name="API_UntagResource_Example_2"></a>

This example illustrates one usage of UntagResource\.

#### Sample Response<a name="API_UntagResource_Example_2_Response"></a>

```
          HTTP 200 response with an empty HTTP body.
```

## See Also<a name="API_UntagResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/UntagResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/UntagResource) 
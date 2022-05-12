# ListTagsForResource<a name="API_ListTagsForResource"></a>

Lists all of the tags associated with the Amazon Resource Name \(ARN\) that you specify\. The resource can be a user, server, or role\.

## Request Syntax<a name="API_ListTagsForResource_RequestSyntax"></a>

```
{
   "Arn": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListTagsForResource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Arn](#API_ListTagsForResource_RequestSyntax) **   <a name="TransferFamily-ListTagsForResource-request-Arn"></a>
Requests the tags associated with a particular Amazon Resource Name \(ARN\)\. An ARN is an identifier for a specific AWS resource, such as a server, user, or role\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** [MaxResults](#API_ListTagsForResource_RequestSyntax) **   <a name="TransferFamily-ListTagsForResource-request-MaxResults"></a>
Specifies the number of tags to return as a response to the `ListTagsForResource` request\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** [NextToken](#API_ListTagsForResource_RequestSyntax) **   <a name="TransferFamily-ListTagsForResource-request-NextToken"></a>
When you request additional results from the `ListTagsForResource` operation, a `NextToken` parameter is returned in the input\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional tags\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.  
Required: No

## Response Syntax<a name="API_ListTagsForResource_ResponseSyntax"></a>

```
{
   "Arn": "string",
   "NextToken": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListTagsForResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Arn](#API_ListTagsForResource_ResponseSyntax) **   <a name="TransferFamily-ListTagsForResource-response-Arn"></a>
The ARN you specified to list the tags of\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*` 

 ** [NextToken](#API_ListTagsForResource_ResponseSyntax) **   <a name="TransferFamily-ListTagsForResource-response-NextToken"></a>
When you can get additional results from the `ListTagsForResource` call, a `NextToken` parameter is returned in the output\. You can then pass in a subsequent command to the `NextToken` parameter to continue listing additional tags\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 6144\.

 ** [Tags](#API_ListTagsForResource_ResponseSyntax) **   <a name="TransferFamily-ListTagsForResource-response-Tags"></a>
Key\-value pairs that are assigned to a resource, usually for the purpose of grouping and searching for items\. Tags are metadata that you define\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.

## Errors<a name="API_ListTagsForResource_Errors"></a>

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

## Examples<a name="API_ListTagsForResource_Examples"></a>

### Example<a name="API_ListTagsForResource_Example_1"></a>

The following example lists the tags for the resource with the ARN you specified\.

#### Sample Request<a name="API_ListTagsForResource_Example_1_Request"></a>

```
{
   "Arn": "arn:aws:transfer:us-east-1:176354371281:server/s-01234567890abcdef"
}
```

### Example<a name="API_ListTagsForResource_Example_2"></a>

This example illustrates one usage of ListTagsForResource\.

#### Sample Response<a name="API_ListTagsForResource_Example_2_Response"></a>

```
{
   "Tags": [ 
      { 
         "Key": "Name",
         "Value": "MyServer"
      }
   ]
}
```

## See Also<a name="API_ListTagsForResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/ListTagsForResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListTagsForResource) 
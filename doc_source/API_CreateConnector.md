# CreateConnector<a name="API_CreateConnector"></a>

Creates the connector, which captures the parameters for an outbound connection for the AS2 protocol\. The connector is required for sending files from a customer's non AWS server\. 

## Request Syntax<a name="API_CreateConnector_RequestSyntax"></a>

```
{
   "AccessRole": "string",
   "As2Config": { 
      "Compression": "string",
      "EncryptionAlgorithm": "string",
      "LocalProfileId": "string",
      "MdnResponse": "string",
      "MdnSigningAlgorithm": "string",
      "MessageSubject": "string",
      "PartnerProfileId": "string",
      "SigningAlgorithm": "string"
   },
   "LoggingRole": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "Url": "string"
}
```

## Request Parameters<a name="API_CreateConnector_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessRole](#API_CreateConnector_RequestSyntax) **   <a name="TransferFamily-CreateConnector-request-AccessRole"></a>
With AS2, you can send files by calling `StartFileTransfer` and specifying the file paths in the request parameter, `SendFilePaths`\. We use the file’s parent directory \(for example, for `--send-file-paths /bucket/dir/file.txt`, parent directory is `/bucket/dir/`\) to temporarily store a processed AS2 message file, store the MDN when we receive them from the partner, and write a final JSON file containing relevant metadata of the transmission\. So, the `AccessRole` needs to provide read and write access to the parent directory of the file location used in the `StartFileTransfer` request\. Additionally, you need to provide read and write access to the parent directory of the files that you intend to send with `StartFileTransfer`\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: Yes

 ** [As2Config](#API_CreateConnector_RequestSyntax) **   <a name="TransferFamily-CreateConnector-request-As2Config"></a>
A structure that contains the parameters for a connector object\.  
Type: [As2ConnectorConfig](API_As2ConnectorConfig.md) object  
Required: Yes

 ** [LoggingRole](#API_CreateConnector_RequestSyntax) **   <a name="TransferFamily-CreateConnector-request-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a connector to turn on CloudWatch logging for Amazon S3 events\. When set, you can view connector activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** [Tags](#API_CreateConnector_RequestSyntax) **   <a name="TransferFamily-CreateConnector-request-Tags"></a>
Key\-value pairs that can be used to group and search for connectors\. Tags are metadata attached to connectors for any purpose\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** [Url](#API_CreateConnector_RequestSyntax) **   <a name="TransferFamily-CreateConnector-request-Url"></a>
The URL of the partner's AS2 endpoint\.  
Type: String  
Length Constraints: Maximum length of 255\.  
Required: Yes

## Response Syntax<a name="API_CreateConnector_ResponseSyntax"></a>

```
{
   "ConnectorId": "string"
}
```

## Response Elements<a name="API_CreateConnector_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ConnectorId](#API_CreateConnector_ResponseSyntax) **   <a name="TransferFamily-CreateConnector-response-ConnectorId"></a>
The unique identifier for the connector, returned after the API call succeeds\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^c-([0-9a-f]{17})$` 

## Errors<a name="API_CreateConnector_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceExistsException **   
The requested resource does not exist\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## See Also<a name="API_CreateConnector_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateConnector) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateConnector) 
# CreateAgreement<a name="API_CreateAgreement"></a>

Creates an agreement\. An agreement is a bilateral trading partner agreement, or partnership, between an AWS Transfer Family server and an AS2 process\. The agreement defines the file and message transfer relationship between the server and the AS2 process\. To define an agreement, Transfer Family combines a server, local profile, partner profile, certificate, and other attributes\.

The partner is identified with the `PartnerProfileId`, and the AS2 process is identified with the `LocalProfileId`\.

## Request Syntax<a name="API_CreateAgreement_RequestSyntax"></a>

```
{
   "AccessRole": "string",
   "BaseDirectory": "string",
   "Description": "string",
   "LocalProfileId": "string",
   "PartnerProfileId": "string",
   "ServerId": "string",
   "Status": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateAgreement_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessRole](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-AccessRole"></a>
With AS2, you can send files by calling `StartFileTransfer` and specifying the file paths in the request parameter, `SendFilePaths`\. We use the file’s parent directory \(for example, for `--send-file-paths /bucket/dir/file.txt`, parent directory is `/bucket/dir/`\) to temporarily store a processed AS2 message file, store the MDN when we receive them from the partner, and write a final JSON file containing relevant metadata of the transmission\. So, the `AccessRole` needs to provide read and write access to the parent directory of the file location used in the `StartFileTransfer` request\. Additionally, you need to provide read and write access to the parent directory of the files that you intend to send with `StartFileTransfer`\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: Yes

 ** [BaseDirectory](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-BaseDirectory"></a>
The landing directory \(folder\) for files transferred by using the AS2 protocol\.  
A `BaseDirectory` example is `/DOC-EXAMPLE-BUCKET/home/mydirectory `\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^$|/.*`   
Required: Yes

 ** [Description](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-Description"></a>
A name or short description to identify the agreement\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[\p{Graph}]+`   
Required: No

 ** [LocalProfileId](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-LocalProfileId"></a>
A unique identifier for the AS2 local profile\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: Yes

 ** [PartnerProfileId](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-PartnerProfileId"></a>
A unique identifier for the partner profile used in the agreement\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$`   
Required: Yes

 ** [ServerId](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-ServerId"></a>
A system\-assigned unique identifier for a server instance\. This is the specific server that the agreement uses\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

 ** [Status](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-Status"></a>
The status of the agreement\. The agreement can be either `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

 ** [Tags](#API_CreateAgreement_RequestSyntax) **   <a name="TransferFamily-CreateAgreement-request-Tags"></a>
Key\-value pairs that can be used to group and search for agreements\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateAgreement_ResponseSyntax"></a>

```
{
   "AgreementId": "string"
}
```

## Response Elements<a name="API_CreateAgreement_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgreementId](#API_CreateAgreement_ResponseSyntax) **   <a name="TransferFamily-CreateAgreement-response-AgreementId"></a>
The unique identifier for the agreement\. Use this ID for deleting, or updating an agreement, as well as in any other API calls that require that you specify the agreement ID\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^a-([0-9a-f]{17})$` 

## Errors<a name="API_CreateAgreement_Errors"></a>

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

## Examples<a name="API_CreateAgreement_Examples"></a>

### Example<a name="API_CreateAgreement_Example_1"></a>

The following example creates an agreement, and returns the agreement ID\.

#### <a name="w339ab1c54c12c11c17b3b5"></a>

```
aws transfer create-agreement --server-id s-021345abcdef6789 --local-profile-id p-1234567890abcdef0 --partner-profile-id p-abcdef01234567890 --base-folder /DOC-EXAMPLE-BUCKET/AS2-files --access-role arn:aws:iam::111122223333:role/AS2-role
```

### Sample Response<a name="API_CreateAgreement_Example_2"></a>

The API call returns the agreement ID for the new agreement\.

#### <a name="w339ab1c54c12c11c17b5b5"></a>

```
{
    "AgreementId": "a-11112222333344444"
}
```

## See Also<a name="API_CreateAgreement_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateAgreement) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateAgreement) 
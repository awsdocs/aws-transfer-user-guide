# CreateProfile<a name="API_CreateProfile"></a>

Creates the local or partner profile to use for AS2 transfers\.

## Request Syntax<a name="API_CreateProfile_RequestSyntax"></a>

```
{
   "As2Id": "string",
   "CertificateIds": [ "string" ],
   "ProfileType": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateProfile_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [As2Id](#API_CreateProfile_RequestSyntax) **   <a name="TransferFamily-CreateProfile-request-As2Id"></a>
The `As2Id` is the *AS2\-name*, as defined in the [RFC 4130](https://datatracker.ietf.org/doc/html/rfc4130)\. For inbound transfers, this is the `AS2-From` header for the AS2 messages sent from the partner\. For outbound connectors, this is the `AS2-To` header for the AS2 messages sent to the partner using the `StartFileTransfer` API operation\. This ID cannot include spaces\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Pattern: `^[\p{Print}\s]*`   
Required: Yes

 ** [CertificateIds](#API_CreateProfile_RequestSyntax) **   <a name="TransferFamily-CreateProfile-request-CertificateIds"></a>
An array of identifiers for the imported certificates\. You use this identifier for working with profiles and partner profiles\.  
Type: Array of strings  
Length Constraints: Fixed length of 22\.  
Pattern: `^cert-([0-9a-f]{17})$`   
Required: No

 ** [ProfileType](#API_CreateProfile_RequestSyntax) **   <a name="TransferFamily-CreateProfile-request-ProfileType"></a>
Determines the type of profile to create:  
+ Specify `LOCAL` to create a local profile\. A local profile represents the AS2\-enabled Transfer Family server organization or party\.
+ Specify `PARTNER` to create a partner profile\. A partner profile represents a remote organization, external to Transfer Family\.
Type: String  
Valid Values:` LOCAL | PARTNER`   
Required: Yes

 ** [Tags](#API_CreateProfile_RequestSyntax) **   <a name="TransferFamily-CreateProfile-request-Tags"></a>
Key\-value pairs that can be used to group and search for AS2 profiles\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateProfile_ResponseSyntax"></a>

```
{
   "ProfileId": "string"
}
```

## Response Elements<a name="API_CreateProfile_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ProfileId](#API_CreateProfile_ResponseSyntax) **   <a name="TransferFamily-CreateProfile-response-ProfileId"></a>
The unique identifier for the AS2 profile, returned after the API call succeeds\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^p-([0-9a-f]{17})$` 

## Errors<a name="API_CreateProfile_Errors"></a>

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

 ** ThrottlingException **   
The request was denied due to request throttling\.  
HTTP Status Code: 400

## Examples<a name="API_CreateProfile_Examples"></a>

### Example<a name="API_CreateProfile_Example_1"></a>

The following example creates a profile, and returns the profile ID\.

The certificate IDs are created when you run `import-certificate`, one for the signing certificate, and one for the encryption certificate\.

#### <a name="w205ab1c52c12c17c15b3b7"></a>

```
aws transfer create-profile --as2-id MYCORP --certificate-ids c-abcdefg123456hijk
               c-987654aaaa321bbbb
```

### Sample Response<a name="API_CreateProfile_Example_2"></a>

The API call returns the profile ID for the new profile\.

#### <a name="w205ab1c52c12c17c15b5b5"></a>

```
{
    "ProfileId": "p-11112222333344444"
}
```

## See Also<a name="API_CreateProfile_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/CreateProfile) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/CreateProfile) 
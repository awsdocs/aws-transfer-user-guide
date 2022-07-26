# DescribedConnector<a name="API_DescribedConnector"></a>

Describes the parameters for the connector, as identified by the `ConnectorId`\.

## Contents<a name="API_DescribedConnector_Contents"></a>

 ** AccessRole **   <a name="TransferFamily-Type-DescribedConnector-AccessRole"></a>
With AS2, you can send files by calling `StartFileTransfer` and specifying the file paths in the request parameter, `SendFilePaths`\. We use the file’s parent directory \(for example, for `--send-file-paths /bucket/dir/file.txt`, parent directory is `/bucket/dir/`\) to temporarily store a processed AS2 message file, store the MDN when we receive them from the partner, and write a final JSON file containing relevant metadata of the transmission\. So, the `AccessRole` needs to provide read and write access to the parent directory of the file location used in the `StartFileTransfer` request\. Additionally, you need to provide read and write access to the parent directory of the files that you intend to send with `StartFileTransfer`\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** Arn **   <a name="TransferFamily-Type-DescribedConnector-Arn"></a>
The unique Amazon Resource Name \(ARN\) for the connector\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** As2Config **   <a name="TransferFamily-Type-DescribedConnector-As2Config"></a>
A structure that contains the parameters for a connector object\.  
Type: [As2ConnectorConfig](API_As2ConnectorConfig.md) object  
Required: No

 ** ConnectorId **   <a name="TransferFamily-Type-DescribedConnector-ConnectorId"></a>
The unique identifier for the connector\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^c-([0-9a-f]{17})$`   
Required: No

 ** LoggingRole **   <a name="TransferFamily-Type-DescribedConnector-LoggingRole"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows a connector to turn on CloudWatch logging for Amazon S3 events\. When set, you can view connector activity in your CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:.*role/.*`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedConnector-Tags"></a>
Key\-value pairs that can be used to group and search for connectors\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** Url **   <a name="TransferFamily-Type-DescribedConnector-Url"></a>
The URL of the partner's AS2 endpoint\.  
Type: String  
Length Constraints: Maximum length of 255\.  
Required: No

## See Also<a name="API_DescribedConnector_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedConnector) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedConnector) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedConnector) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedConnector) 
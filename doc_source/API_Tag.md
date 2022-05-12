# Tag<a name="API_Tag"></a>

Creates a key\-value pair for a specific resource\. Tags are metadata that you can use to search for and group a resource for various purposes\. You can apply tags to servers, users, and roles\. A tag key can take more than one value\. For example, to group servers for accounting purposes, you might create a tag called `Group` and assign the values `Research` and `Accounting` to that group\.

## Contents<a name="API_Tag_Contents"></a>

 ** Key **   <a name="TransferFamily-Type-Tag-Key"></a>
The name assigned to the tag that you create\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Required: Yes

 ** Value **   <a name="TransferFamily-Type-Tag-Value"></a>
Contains one or more values that you assigned to the key name you create\.  
Type: String  
Length Constraints: Maximum length of 256\.  
Required: Yes

## See Also<a name="API_Tag_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/Tag) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/Tag) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/Tag) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/Tag) 
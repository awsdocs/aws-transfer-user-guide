# HomeDirectoryMapEntry<a name="API_HomeDirectoryMapEntry"></a>

Represents an object that contains entries and targets for `HomeDirectoryMappings`\.

The following is an `Entry` and `Target` pair example for `chroot`\.

 `[ { "Entry": "/", "Target": "/bucket_name/home/mydirectory" } ]` 

## Contents<a name="API_HomeDirectoryMapEntry_Contents"></a>

 ** Entry **   <a name="TransferFamily-Type-HomeDirectoryMapEntry-Entry"></a>
Represents an entry for `HomeDirectoryMappings`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^/.*`   
Required: Yes

 ** Target **   <a name="TransferFamily-Type-HomeDirectoryMapEntry-Target"></a>
Represents the map target that is used in a `HomeDirectorymapEntry`\.  
Type: String  
Length Constraints: Maximum length of 1024\.  
Pattern: `^/.*`   
Required: Yes

## See Also<a name="API_HomeDirectoryMapEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/HomeDirectoryMapEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/HomeDirectoryMapEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/HomeDirectoryMapEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/HomeDirectoryMapEntry) 
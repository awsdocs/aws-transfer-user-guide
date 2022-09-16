# ListedHostKey<a name="API_ListedHostKey"></a>

Returns properties of the host key that's specified\.

## Contents<a name="API_ListedHostKey_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-ListedHostKey-Arn"></a>
The unique Amazon Resource Name \(ARN\) of the host key\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** DateImported **   <a name="TransferFamily-Type-ListedHostKey-DateImported"></a>
The date on which the host key was added to the server\.  
Type: Timestamp  
Required: No

 ** Description **   <a name="TransferFamily-Type-ListedHostKey-Description"></a>
The current description for the host key\. You can change it by calling the `UpdateHostKey` operation and providing a new description\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Pattern: `^[\p{Print}]*$`   
Required: No

 ** Fingerprint **   <a name="TransferFamily-Type-ListedHostKey-Fingerprint"></a>
The public key fingerprint, which is a short sequence of bytes used to identify the longer public key\.  
Type: String  
Required: No

 ** HostKeyId **   <a name="TransferFamily-Type-ListedHostKey-HostKeyId"></a>
A unique identifier for the host key\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$`   
Required: No

 ** Type **   <a name="TransferFamily-Type-ListedHostKey-Type"></a>
The encryption algorithm that is used for the host key\. The `Type` parameter is specified by using one of the following values:  
+  `ssh-rsa` 
+  `ssh-ed25519` 
+  `ecdsa-sha2-nistp256` 
+  `ecdsa-sha2-nistp384` 
+  `ecdsa-sha2-nistp521` 
Type: String  
Required: No

## See Also<a name="API_ListedHostKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ListedHostKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ListedHostKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ListedHostKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ListedHostKey) 
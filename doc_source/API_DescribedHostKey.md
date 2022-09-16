# DescribedHostKey<a name="API_DescribedHostKey"></a>

The details for a server host key\.

## Contents<a name="API_DescribedHostKey_Contents"></a>

 ** Arn **   <a name="TransferFamily-Type-DescribedHostKey-Arn"></a>
The unique Amazon Resource Name \(ARN\) for the host key\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 1600\.  
Pattern: `arn:.*`   
Required: Yes

 ** DateImported **   <a name="TransferFamily-Type-DescribedHostKey-DateImported"></a>
The date on which the host key was added to the server\.  
Type: Timestamp  
Required: No

 ** Description **   <a name="TransferFamily-Type-DescribedHostKey-Description"></a>
The text description for this host key\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Pattern: `^[\p{Print}]*$`   
Required: No

 ** HostKeyFingerprint **   <a name="TransferFamily-Type-DescribedHostKey-HostKeyFingerprint"></a>
The public key fingerprint, which is a short sequence of bytes used to identify the longer public key\.  
Type: String  
Required: No

 ** HostKeyId **   <a name="TransferFamily-Type-DescribedHostKey-HostKeyId"></a>
A unique identifier for the host key\.  
Type: String  
Length Constraints: Fixed length of 25\.  
Pattern: `^hostkey-[0-9a-f]{17}$`   
Required: No

 ** Tags **   <a name="TransferFamily-Type-DescribedHostKey-Tags"></a>
Key\-value pairs that can be used to group and search for host keys\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Required: No

 ** Type **   <a name="TransferFamily-Type-DescribedHostKey-Type"></a>
The encryption algorithm that is used for the host key\. The `Type` parameter is specified by using one of the following values:  
+  `ssh-rsa` 
+  `ssh-ed25519` 
+  `ecdsa-sha2-nistp256` 
+  `ecdsa-sha2-nistp384` 
+  `ecdsa-sha2-nistp521` 
Type: String  
Required: No

## See Also<a name="API_DescribedHostKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedHostKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedHostKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedHostKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedHostKey) 
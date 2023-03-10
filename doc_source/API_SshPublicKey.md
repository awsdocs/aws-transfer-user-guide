# SshPublicKey<a name="API_SshPublicKey"></a>

Provides information about the public Secure Shell \(SSH\) key that is associated with a Transfer Family user for the specific file transfer protocol\-enabled server \(as identified by `ServerId`\)\. The information returned includes the date the key was imported, the public key contents, and the public key ID\. A user can store more than one SSH public key associated with their user name on a specific server\.

## Contents<a name="API_SshPublicKey_Contents"></a>

 ** DateImported **   <a name="TransferFamily-Type-SshPublicKey-DateImported"></a>
Specifies the date that the public key was added to the Transfer Family user\.  
Type: Timestamp  
Required: Yes

 ** SshPublicKeyBody **   <a name="TransferFamily-Type-SshPublicKey-SshPublicKeyBody"></a>
Specifies the content of the SSH public key as specified by the `PublicKeyId`\.  
 AWS Transfer Family accepts RSA, ECDSA, and ED25519 keys\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Required: Yes

 ** SshPublicKeyId **   <a name="TransferFamily-Type-SshPublicKey-SshPublicKeyId"></a>
Specifies the `SshPublicKeyId` parameter contains the identifier of the public key\.  
Type: String  
Length Constraints: Fixed length of 21\.  
Pattern: `^key-[0-9a-f]{17}$`   
Required: Yes

## See Also<a name="API_SshPublicKey_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/SshPublicKey) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/SshPublicKey) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/SshPublicKey) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/SshPublicKey) 
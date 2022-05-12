# DescribedSecurityPolicy<a name="API_DescribedSecurityPolicy"></a>

Describes the properties of a security policy that was specified\. For more information about security policies, see [Working with security policies](https://docs.aws.amazon.com/transfer/latest/userguide/security-policies.html)\.

## Contents<a name="API_DescribedSecurityPolicy_Contents"></a>

 ** Fips **   <a name="TransferFamily-Type-DescribedSecurityPolicy-Fips"></a>
Specifies whether this policy enables Federal Information Processing Standards \(FIPS\)\.  
Type: Boolean  
Required: No

 ** SecurityPolicyName **   <a name="TransferFamily-Type-DescribedSecurityPolicy-SecurityPolicyName"></a>
Specifies the name of the security policy that is attached to the server\.  
Type: String  
Length Constraints: Maximum length of 100\.  
Pattern: `TransferSecurityPolicy-.+`   
Required: Yes

 ** SshCiphers **   <a name="TransferFamily-Type-DescribedSecurityPolicy-SshCiphers"></a>
Specifies the enabled Secure Shell \(SSH\) cipher encryption algorithms in the security policy that is attached to the server\.  
Type: Array of strings  
Length Constraints: Maximum length of 50\.  
Required: No

 ** SshKexs **   <a name="TransferFamily-Type-DescribedSecurityPolicy-SshKexs"></a>
Specifies the enabled SSH key exchange \(KEX\) encryption algorithms in the security policy that is attached to the server\.  
Type: Array of strings  
Length Constraints: Maximum length of 50\.  
Required: No

 ** SshMacs **   <a name="TransferFamily-Type-DescribedSecurityPolicy-SshMacs"></a>
Specifies the enabled SSH message authentication code \(MAC\) encryption algorithms in the security policy that is attached to the server\.  
Type: Array of strings  
Length Constraints: Maximum length of 50\.  
Required: No

 ** TlsCiphers **   <a name="TransferFamily-Type-DescribedSecurityPolicy-TlsCiphers"></a>
Specifies the enabled Transport Layer Security \(TLS\) cipher encryption algorithms in the security policy that is attached to the server\.  
Type: Array of strings  
Length Constraints: Maximum length of 50\.  
Required: No

## See Also<a name="API_DescribedSecurityPolicy_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribedSecurityPolicy) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribedSecurityPolicy) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribedSecurityPolicy) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribedSecurityPolicy) 
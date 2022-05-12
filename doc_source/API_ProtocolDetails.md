# ProtocolDetails<a name="API_ProtocolDetails"></a>

 The protocol settings that are configured for your server\. 

## Contents<a name="API_ProtocolDetails_Contents"></a>

 ** PassiveIp **   <a name="TransferFamily-Type-ProtocolDetails-PassiveIp"></a>
 Indicates passive mode, for FTP and FTPS protocols\. Enter a single dotted\-quad IPv4 address, such as the external IP address of a firewall, router, or load balancer\. For example:   
 ` aws transfer update-server --protocol-details PassiveIp=0.0.0.0 `   
Replace ` 0.0.0.0 ` in the example above with the actual IP address you want to use\.  
 If you change the `PassiveIp` value, you must stop and then restart your Transfer server for the change to take effect\. For details on using Passive IP \(PASV\) in a NAT environment, see [Configuring your FTPS server behind a firewall or NAT with AWS Transfer Family](http://aws.amazon.com/blogs/storage/configuring-your-ftps-server-behind-a-firewall-or-nat-with-aws-transfer-family/)\. 
Type: String  
Length Constraints: Maximum length of 15\.  
Required: No

 ** TlsSessionResumptionMode **   <a name="TransferFamily-Type-ProtocolDetails-TlsSessionResumptionMode"></a>
A property used with Transfer servers that use the FTPS protocol\. TLS Session Resumption provides a mechanism to resume or share a negotiated secret key between the control and data connection for an FTPS session\. `TlsSessionResumptionMode` determines whether or not the server resumes recent, negotiated sessions through a unique session ID\. This property is available during `CreateServer` and `UpdateServer` calls\. If a `TlsSessionResumptionMode` value is not specified during CreateServer, it is set to `ENFORCED` by default\.  
+  `DISABLED`: the server does not process TLS session resumption client requests and creates a new TLS session for each request\. 
+  `ENABLED`: the server processes and accepts clients that are performing TLS session resumption\. The server doesn't reject client data connections that do not perform the TLS session resumption client processing\.
+  `ENFORCED`: the server processes and accepts clients that are performing TLS session resumption\. The server rejects client data connections that do not perform the TLS session resumption client processing\. Before you set the value to `ENFORCED`, test your clients\.
**Note**  
Not all FTPS clients perform TLS session resumption\. So, if you choose to enforce TLS session resumption, you prevent any connections from FTPS clients that don't perform the protocol negotiation\. To determine whether or not you can use the `ENFORCED` value, you need to test your clients\.
Type: String  
Valid Values:` DISABLED | ENABLED | ENFORCED`   
Required: No

## See Also<a name="API_ProtocolDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/ProtocolDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/ProtocolDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/ProtocolDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/ProtocolDetails) 
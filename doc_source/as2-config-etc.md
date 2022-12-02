# AS2 configurations, limits, and error messages<a name="as2-config-etc"></a>

This section describes the supported configurations for transfers that use the Applicability Statement 2 \(AS2\) protocol, including the accepted ciphers and digests\. This section also describes the limits and known issues for AS2 transfers\. The various error codes that you might receive from AS2 file transfers are also provided\. 

## AS2 supported configurations<a name="as2-supported-configurations"></a>

**Signing, encryption, compression, MDN**

For both inbound and outbound transfers, the following items are either required or optional:
+ **Encryption** – Required \(for HTTP transport, which is the only transport method currently supported\)
+ **Signing** – Optional
+ **Compression** – Optional \(the only currently supported compression algorithm is ZLIB\)
+ **Message Disposition Notice \(MDN\)** – Optional

**Ciphers**

The following ciphers are supported:
+ **Inbound transfers** – AES128\_CBC, AES192\_CBC, AES256\_CBC, 3DES \(for backward compatibility only\)
+ **Outbound transfers** – AES128\_CBC, AES192\_CBC, AES256\_CBC

**Digests**

The following digests are supported:
+ **Inbound signing and MDN** – SHA1, SHA256, SHA384, SHA512
+ **Outbound signing and MDN** – SHA1, SHA256, SHA384, SHA512

**MDN**

For MDN responses, certain types are supported, as follows: 
+ **Inbound transfers** – Synchronous and asynchronous
+ **Outbound transfers** – Synchronous only
+ **Simple Mail Transfer Protocol \(SMTP\) \(email MDN\)** – Not supported

**Transports**
+ **Inbound transfers** – HTTP is the only currently supported transport, and you must specify it explicitly\.
**Note**  
If you need to use HTTPS for inbound transfers, you can terminate TLS on an Application Load Balancer or a Network Load Balancer\. For more information, see [TlsSessionResumptionMode](https://docs.aws.amazon.com/transfer/latest/userguide/API_ProtocolDetails.html#TransferFamily-Type-ProtocolDetails-TlsSessionResumptionMode)\.
+ **Outbound transfers** – If you use HTTP, you must also specify an encryption algorithm\. If you specify HTTPS, you should specify **NONE** for your encryption algorithm\.

## AS2 limits and limitations<a name="as2-limits-issues"></a>

**Limits**

The following limits are in place for AS2 file transfers\.


**AS2 limits**  

| Name | Default | Adjustable | 
| --- | --- | --- | 
| Inbound AS2 requests per second per server | 25 | Yes | 
| Inbound AS2 requests in progress per server | 100 | Yes | 
| Maximum number of file transfer requests per second per connector | 3 | Yes | 
| Maximum number of files per file transfer request | 10 | No | 
| Outbound AS2 requests in progress per connector | 100 | Yes | 
| Maximum file size \(compressed or uncompressed\) | 50 MB | Yes | 
| Inactivity timeout | 350 seconds | No | 
| Maximum number of partner profiles per account | 1000 \(up to 10 certificates per partner profile: not adjustable\) | Yes | 
| Maximum number of certificates per account | 1000 | Yes | 
| Maximum number of connectors per account | 100 | Yes | 
| Maximum number of agreements per server | 100 | Yes | 

**Known limitations**
+ Server\-side TCP keep\-alive is not supported\. The connection times out after 350 seconds of inactivity unless the client sends keep\-alive packets\.
+ For an active agreement to be accepted by the service and appear in Amazon CloudWatch logs, messages must contain valid AS2 headers\.
+ The server that's receiving messages from AWS Transfer Family for AS2 must support the Cryptographic Message Syntax \(CMS\) algorithm protection attribute for validating message signatures, as defined in [RFC 6211](https://datatracker.ietf.org/doc/html/rfc6211)\. This attribute is not supported in some older IBM Sterling products\.
+ Duplicate message IDs result in a processed/Warning: duplicate\-document message\.
+ When sending AS2 messages or asynchronous MDNs to a trading partner's HTTPS endpoint, the messages or MDNs must use a valid SSL certificate signed by a certificate authority \(CA\) that's trusted by AWS Transfer Family\. \(For a list of trusted CAs, see [https://www\.amazontrust\.com/repository/](https://www.amazontrust.com/repository/)\.\) Self\-signed certificates are not currently supported\. 
+ The endpoint must support the TLS version 1\.2 protocol and a cryptographic algorithm that's permitted by the security policy \(as described in [Working with security policies](security-policies.md)\)\.
+ Mutual TLS \(mTLS\) is not currently supported\.
+ Multiple attachments and certificate exchange messaging \(CEM\) from AS2 version 1\.2 is not currently supported\.
+ Basic authentication is not currently supported\.

## AS2 error codes<a name="as2-error-codes"></a>


**AS2 error codes**  

| Code | Error | Description | 
| --- | --- | --- | 
| DECRYPT\_FAILED | Failed to decrypt message message\-ID\. Ensure that the partner has the correct public encryption key\. | Decryption failed\. Confirm that the partner sent a payload by using a valid certificate and that encryption was performed by using a valid encryption algorithm\. | 
| ERROR\_DECRYPT\_UNSUPPORTED\_ENCRYPTION\_ALG | SMIME Payload Decryption requested using unsupported algorithm with ID: encryption\-ID\. | The remote sender has sent an AS2 payload with an unsupported encryption algorithm\. The sender must choose an encryption algorithm that's supported by AWS Transfer Family\. | 
| DECRYPT\_FAILED\_INVALID\_SMIME\_FORMAT | Unable to parse enveloped mimePart\. | MIME payload is either corrupt or in an unsupported SMIME format\. The sender should make sure that the format they're using is supported, and then resend the payload\. | 
| DECRYPT\_FAILED\_NO\_DECRYPTION\_KEY\_FOUND | No matching decryption key found\. | The partner profile did not have a certificate assigned that matched the message, or the certificates that matched the message are now expired or no longer valid\. You must update the partner profile and ensure that it contains a valid certificate\. | 
| ENCRYPTION\_FAILED | Failed to encrypt file file\-name\. | The file to be sent is not available for encryption\. Verify that the file is in its expected AS2 location and that AWS Transfer Family has permission to read the file\. | 
| VERIFICATION\_FAILED | Signature verification failed for AS2 message message\-ID or a MIC code did not match\. | Check that the sender's signing certificate matches the signing certificates for the remote profile\. Also check that the MIC algorithms are compatible with AWS Transfer Family\. | 
| SIGNING\_FAILED | Failed to sign file\. | The file to be sent is not available for signing, or signing could not be performed\. Verify that the file is in its expected AS2 location and that AWS Transfer Family has permission to read the file\. | 
| DECOMPRESSION\_FAILED | Failed to decompress message\. | Either the file sent is corrupt, or the compression algorithm is not valid\. Resend the message and verify that ZLIB compression is used, or resend the message without compression enabled\. | 
| AGREEMENT\_NOT\_FOUND | Agreement was not found\. | Either the agreement was not found, or the agreement is associated with an inactive profile\. Update the agreement within the Transfer Family server to include active profiles\. | 
| CONNECTOR\_NOT\_FOUND | Connector or related configuration was not found\. | Either the connector was not found, or the connector is associated with an inactive profile\. Update the connector to include active profiles\. | 
| INSUFFICENT\_MESSAGE\_SECURITY\_UNENCRYPTED | Encryption is required\. | The partner sent an unencrypted message to Transfer Family, which is not supported\. The sender must use an encrypted payload\. | 
| DUPLICATE\_MESSAGE | Duplicate or double processed step\. | The payload has a duplicate processing step\. For example, there are two encryption steps\. Resend the message with a single step for signing, compression, and encryption\. | 
| INVALID\_REQUEST | There is a problem with a message header\. | Check the as2\-from and as2\-to fields\. Make sure that the original message ID is accurate for the MDN format\. Also make sure that the message ID format is not missing any AS2 headers\. | 
| UNABLE\_TO\_RESOLVE\_HOSTNAME | Unable to resolve hostname hostname\.  | The Transfer Family server could not resolve the partner's hostname by using a public DNS server\. Check that the configured host is registered and that the DNS record has had time to publish\. | 
| HTTP\_ERROR\_RESPONSE\_FROM\_PARTNER |  *partner\-URL* returned status 400 for message with ID=*message\-id*\.  | Communicating with the partner's AS2 server returned an unexpected HTTP response code\. The partner might be able to provide more diagnostics from their AS2 server logs\. | 
| INVALID\_ENDPOINT\_PROTOCOL | Only HTTP and HTTPS are supported\. | You must specify HTTP or HTTPS as the protocol in your AS2 connector configuration\. | 
| UNABLE\_RESOLVE\_HOST\_TO\_IP\_ADDRESS | Unable to resolve hostname to IP addresses\. | Transfer Family is unable to perform DNS to IP address resolution on the public DNS server that is configured in the AS2 connector\. Update the connector to point to a valid partner URL\. | 
| UNABLE\_TO\_CONNECT\_TO\_REMOTE\_HOST\_OR\_IP | Connection to endpoint timed out\. | Transfer Family cannot establish a socket connection to the configured partner's AS2 server\. Check that the partner's AS2 server is available at the configured IP address\. | 
| SEND\_FILE\_NOT\_FOUND | File path file\-path not found\. | Transfer Family can't locate the file in the send file operation\. Check that the configured home directory and path are valid and that Transfer Family has read permissions for the file\. | 
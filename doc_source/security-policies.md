# Working with security policies<a name="security-policies"></a>

Server security policies in AWS Transfer Family allow you to limit the set of cryptographic algorithms \(message authentication codes \(MACs\), key exchanges \(KEXs\), and cipher suites\) associated with your server\. For a list of supported cryptographic algorithms, see [Cryptographic algorithms](#cryptographic-algorithms)\. For a list of supported key algorithms for use with server host keys and service\-managed user keys, see [Supported algorithms for user and server keys](key-management.md#key-algorithms)\.

**Note**  
 We support TLS 1\.2\.

The available security policies for the server are:

**Topics**
+ [Cryptographic algorithms](#cryptographic-algorithms)
+ [TransferSecurityPolicy\-2022\-03](#security-policy-transfer-2022-03)
+ [TransferSecurityPolicy\-2020\-06](#security-policy-transfer-2020-06)
+ [TransferSecurityPolicy\-2018\-11](#security-policy-transfer-2018-11)
+ [TransferSecurityPolicy\-FIPS\-2020\-06](#security-policy-transfer-fips-2020-06)

**Note**  
`TransferSecurityPolicy-2020-06` is the default security policy attached to your server when creating a server using the console\.
`TransferSecurityPolicy-2018-11` is the default security policy attached to your server when creating a server using the API or CLI\.

## Cryptographic algorithms<a name="cryptographic-algorithms"></a>

The following is a list of supported cryptographic algorithms for each security policy\.


| Security policy | 2022\-03 | 2020\-06 | FIPS\-2020\-06 | 2018\-11 | 
| --- |--- |--- |--- |--- |
|  SSH ciphers  | 
| --- |
|  aes128\-ctr  |     |  ♦  |  ♦  |  ♦  | 
|  aes128\-gcm@openssh\.com  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  aes192\-ctr  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  aes256\-ctr  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  aes256\-gcm@openssh\.com  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  chacha20\-poly1305@openssh\.com  |     |  ♦  |     |  ♦  | 
|  KEXs  | 
| --- |
|  diffie\-hellman\-group14\-sha256  |     |  ♦  |  ♦  |  ♦  | 
|  diffie\-hellman\-group16\-sha512  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  diffie\-hellman\-group18\-sha512  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  ecdh\-sha2\-nistp384  |     |  ♦  |  ♦  |  ♦  | 
|  ecdh\-sha2\-nistp521  |     |  ♦  |  ♦  |  ♦  | 
|  diffie\-hellman\-group\-exchange\-sha256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  diffie\-hellman\-group14\-sha1  |     |     |     |  ♦  | 
|  ecdh\-sha2\-nistp256  |     |  ♦  |  ♦  |  ♦  | 
|  curve25519\-sha256@libssh\.org  |  ♦  |     |     |  ♦  | 
|  curve25519\-sha256  |  ♦  |     |     |  ♦  | 
|  MACs  | 
| --- |
|  hmac\-sha2\-256\-etm@openssh\.com  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  hmac\-sha2\-256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  hmac\-sha2\-512\-etm@openssh\.com  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  hmac\-sha2\-512  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  hmac\-sha1\-etm@openssh\.com  |     |     |     |  ♦  | 
|  hmac\-sha1  |     |     |     |  ♦  | 
|  umac\-128\-etm@openssh\.com  |     |  ♦  |     |  ♦  | 
|  umac\-128@openssh\.com  |     |  ♦  |     |  ♦  | 
|  umac\-64\-etm@openssh\.com  |     |     |     |  ♦  | 
|  umac\-64@openssh\.com  |     |     |     |  ♦  | 
|  TLS ciphers  | 
| --- |
|  TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA384  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384  |  ♦  |  ♦  |  ♦  |  ♦  | 
|  TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256  |     |     |     |  ♦  | 
|  TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256  |     |     |     |  ♦  | 

## TransferSecurityPolicy\-2022\-03<a name="security-policy-transfer-2022-03"></a>

The following shows the TransferSecurityPolicy\-2022\-03 security policy\.

```
{
  "SecurityPolicy": {
    "Fips": false,
    "SecurityPolicyName": "TransferSecurityPolicy-2022-03",
    "SshCiphers": [
      "aes256-gcm@openssh.com",
      "aes128-gcm@openssh.com",
      "aes256-ctr",
      "aes192-ctr"
    ],
    "SshKexs": [
      "curve25519-sha256",
      "curve25519-sha256@libssh.org",
      "diffie-hellman-group16-sha512",
      "diffie-hellman-group18-sha512",
      "diffie-hellman-group-exchange-sha256"
    ],
    "SshMacs": [
      "hmac-sha2-512-etm@openssh.com",
      "hmac-sha2-256-etm@openssh.com",
      "hmac-sha2-512",
      "hmac-sha2-256"
    ],
    "TlsCiphers": [
      "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", 
      "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256", 
      "TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256", 
      "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", 
      "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384", 
      "TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384", 
      "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384"
    ]
  }
}
```

## TransferSecurityPolicy\-2020\-06<a name="security-policy-transfer-2020-06"></a>

The following shows the TransferSecurityPolicy\-2020\-06 security policy\. This is the default security policy for non\-FIPS enabled server endpoints\.

```
{
  "SecurityPolicy": {
    "Fips": false,
    "SecurityPolicyName": "TransferSecurityPolicy-2020-06",
    "SshCiphers": [
      "chacha20-poly1305@openssh.com",
      "aes128-ctr",
      "aes192-ctr",
      "aes256-ctr",
      "aes128-gcm@openssh.com",
      "aes256-gcm@openssh.com"
    ],
    "SshKexs": [
      "ecdh-sha2-nistp256",
      "ecdh-sha2-nistp384",
      "ecdh-sha2-nistp521",
      "diffie-hellman-group-exchange-sha256",
      "diffie-hellman-group16-sha512",
      "diffie-hellman-group18-sha512",
      "diffie-hellman-group14-sha256"
    ],
    "SshMacs": [
      "umac-128-etm@openssh.com",
      "hmac-sha2-256-etm@openssh.com",
      "hmac-sha2-512-etm@openssh.com",
      "umac-128@openssh.com",
      "hmac-sha2-256",
      "hmac-sha2-512"
    ],
    "TlsCiphers": [
      "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384"
    ]
  }
}
```

## TransferSecurityPolicy\-2018\-11<a name="security-policy-transfer-2018-11"></a>

The following shows the TransferSecurityPolicy\-2018\-11 security policy\. This security policy is the current set of all supported cryptographic algorithms\.

```
{
  "SecurityPolicy": {
    "Fips": false,
    "SecurityPolicyName": "TransferSecurityPolicy-2018-11",
    "SshCiphers": [
      "chacha20-poly1305@openssh.com",
      "aes128-ctr",
      "aes192-ctr",
      "aes256-ctr",
      "aes128-gcm@openssh.com",
      "aes256-gcm@openssh.com"
    ],
    "SshKexs": [
      "curve25519-sha256",
      "curve25519-sha256@libssh.org",
      "ecdh-sha2-nistp256",
      "ecdh-sha2-nistp384",
      "ecdh-sha2-nistp521",
      "diffie-hellman-group-exchange-sha256",
      "diffie-hellman-group16-sha512",
      "diffie-hellman-group18-sha512",
      "diffie-hellman-group14-sha256",
      "diffie-hellman-group14-sha1"
    ],
    "SshMacs": [
      "umac-64-etm@openssh.com",
      "umac-128-etm@openssh.com",
      "hmac-sha2-256-etm@openssh.com",
      "hmac-sha2-512-etm@openssh.com",
      "hmac-sha1-etm@openssh.com",
      "umac-64@openssh.com",
      "umac-128@openssh.com",
      "hmac-sha2-256",
      "hmac-sha2-512",
      "hmac-sha1"
    ],
    "TlsCiphers": [
      "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384",
      "TLS_RSA_WITH_AES_128_CBC_SHA256",
      "TLS_RSA_WITH_AES_256_CBC_SHA256"
    ]
  }
}
```

## TransferSecurityPolicy\-FIPS\-2020\-06<a name="security-policy-transfer-fips-2020-06"></a>

The FIPS certification details for AWS Transfer Family can be found at [https://csrc.nist.gov/projects/cryptographic-module-validation-program/validated-modules/search/all](https://csrc.nist.gov/projects/cryptographic-module-validation-program/validated-modules/search/all)

The following shows the TransferSecurityPolicy\-FIPS\-2020\-06 security policy\. This security policy contains all supported FIPS compliant cryptographic algorithms\. This is the default security policy for FIPS enabled server endpoints\.

**Note**  
The FIPS service endpoint and TransferSecurityPolicy\-FIPS\-2020\-06 security policy is only available in some AWS Regions\. For more information, see [AWS Transfer Family endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*\.

```
{
  "SecurityPolicy": {
    "Fips": true,
    "SecurityPolicyName": "TransferSecurityPolicy-FIPS-2020-06",
    "SshCiphers": [
      "aes128-ctr",
      "aes192-ctr",
      "aes256-ctr",
      "aes128-gcm@openssh.com",
      "aes256-gcm@openssh.com"
    ],
    "SshKexs": [
      "ecdh-sha2-nistp256",
      "ecdh-sha2-nistp384",
      "ecdh-sha2-nistp521",
      "diffie-hellman-group-exchange-sha256",
      "diffie-hellman-group16-sha512",
      "diffie-hellman-group18-sha512",
      "diffie-hellman-group14-sha256"
    ],
    "SshMacs": [
      "hmac-sha2-256-etm@openssh.com",
      "hmac-sha2-512-etm@openssh.com",
      "hmac-sha2-256",
      "hmac-sha2-512"
    ],
    "TlsCiphers": [
      "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256",
      "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384",
      "TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384",
      "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384"
    ]
  }
}
```
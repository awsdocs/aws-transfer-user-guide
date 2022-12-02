# DescribeServer<a name="API_DescribeServer"></a>

Describes a file transfer protocol\-enabled server that you specify by passing the `ServerId` parameter\.

The response contains a description of a server's properties\. When you set `EndpointType` to VPC, the response will contain the `EndpointDetails`\.

## Request Syntax<a name="API_DescribeServer_RequestSyntax"></a>

```
{
   "ServerId": "string"
}
```

## Request Parameters<a name="API_DescribeServer_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ServerId](#API_DescribeServer_RequestSyntax) **   <a name="TransferFamily-DescribeServer-request-ServerId"></a>
A system\-assigned unique identifier for a server\.  
Type: String  
Length Constraints: Fixed length of 19\.  
Pattern: `^s-([0-9a-f]{17})$`   
Required: Yes

## Response Syntax<a name="API_DescribeServer_ResponseSyntax"></a>

```
{
   "Server": { 
      "Arn": "string",
      "Certificate": "string",
      "Domain": "string",
      "EndpointDetails": { 
         "AddressAllocationIds": [ "string" ],
         "SecurityGroupIds": [ "string" ],
         "SubnetIds": [ "string" ],
         "VpcEndpointId": "string",
         "VpcId": "string"
      },
      "EndpointType": "string",
      "HostKeyFingerprint": "string",
      "IdentityProviderDetails": { 
         "DirectoryId": "string",
         "Function": "string",
         "InvocationRole": "string",
         "Url": "string"
      },
      "IdentityProviderType": "string",
      "LoggingRole": "string",
      "PostAuthenticationLoginBanner": "string",
      "PreAuthenticationLoginBanner": "string",
      "ProtocolDetails": { 
         "As2Transports": [ "string" ],
         "PassiveIp": "string",
         "SetStatOption": "string",
         "TlsSessionResumptionMode": "string"
      },
      "Protocols": [ "string" ],
      "SecurityPolicyName": "string",
      "ServerId": "string",
      "State": "string",
      "Tags": [ 
         { 
            "Key": "string",
            "Value": "string"
         }
      ],
      "UserCount": number,
      "WorkflowDetails": { 
         "OnPartialUpload": [ 
            { 
               "ExecutionRole": "string",
               "WorkflowId": "string"
            }
         ],
         "OnUpload": [ 
            { 
               "ExecutionRole": "string",
               "WorkflowId": "string"
            }
         ]
      }
   }
}
```

## Response Elements<a name="API_DescribeServer_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Server](#API_DescribeServer_ResponseSyntax) **   <a name="TransferFamily-DescribeServer-response-Server"></a>
An array containing the properties of a server with the `ServerID` you specified\.  
Type: [DescribedServer](API_DescribedServer.md) object

## Errors<a name="API_DescribeServer_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalServiceError **   
This exception is thrown when an error occurs in the AWSTransfer Family service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
This exception is thrown when a resource is not found by the AWSTransfer Family service\.  
HTTP Status Code: 400

 ** ServiceUnavailableException **   
The request has failed because the AWSTransfer Family service is not available\.  
HTTP Status Code: 500

## Examples<a name="API_DescribeServer_Examples"></a>

### Example<a name="API_DescribeServer_Example_1"></a>

The following example returns the properties assigned to a server\.

#### Sample Request<a name="API_DescribeServer_Example_1_Request"></a>

```
{
   "ServerId": "s-01234567890abcdef"
}
```

### Example<a name="API_DescribeServer_Example_2"></a>

This example illustrates one usage of DescribeServer\.

#### Sample Response<a name="API_DescribeServer_Example_2_Response"></a>

```
{
    "Server": {
        "Arn": "arn:aws:transfer:us-east-1:176354371281:server/s-01234567890abcdef",
        "EndpointDetails": {
            "AddressAllocationIds": [
                "eipalloc-01a2eabe3c04d5678",
                "eipalloc-102345be"
            ],
            "SubnetIds": [
                "subnet-047eaa7f0187a7cde",
                "subnet-0a2d0f474daffde18"
            ],
            "VpcEndpointId": "vpce-03fe0080e7cb008b8",
            "VpcId": "vpc-09047a51f1c8e1634"
        },
        "EndpointType": "VPC",
        "HostKeyFingerprint": "your host key,
        "IdentityProviderType": "SERVICE_MANAGED",
        "ServerId": "s-01234567890abcdef",
        "State": "ONLINE",
        "Tags": [],
        "UserCount": 0
    }
}
```

## See Also<a name="API_DescribeServer_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transfer-2018-11-05/DescribeServer) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/DescribeServer) 
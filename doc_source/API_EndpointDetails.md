# EndpointDetails<a name="API_EndpointDetails"></a>

The virtual private cloud \(VPC\) endpoint settings that are configured for your file transfer protocol\-enabled server\. With a VPC endpoint, you can restrict access to your server and resources only within your VPC\. To control incoming internet traffic, invoke the `UpdateServer` API and attach an Elastic IP address to your server's endpoint\.

**Note**  
 After May 19, 2021, you won't be able to create a server using `EndpointType=VPC_ENDPOINT` in your AWSaccount if your account hasn't already done so before May 19, 2021\. If you have already created servers with `EndpointType=VPC_ENDPOINT` in your AWSaccount on or before May 19, 2021, you will not be affected\. After this date, use `EndpointType`=`VPC`\.  
For more information, see [Discontinuing the use of VPC\_ENDPOINTYou can change the endpoint type for your server using the Transfer Family console, AWS CLI, API, SDKs, or AWS CloudFormation\. To change your server’s endpoint type, see [Updating the AWS Transfer Family server endpoint type from VPC\_ENDPOINT to VPC](update-endpoint-type-vpc.md)\.](create-server-in-vpc.md#deprecate-vpc-endpoint)\.

## Contents<a name="API_EndpointDetails_Contents"></a>

 ** AddressAllocationIds **   <a name="TransferFamily-Type-EndpointDetails-AddressAllocationIds"></a>
A list of address allocation IDs that are required to attach an Elastic IP address to your server's endpoint\.  
This property can only be set when `EndpointType` is set to `VPC` and it is only valid in the `UpdateServer` API\.
Type: Array of strings  
Required: No

 ** SecurityGroupIds **   <a name="TransferFamily-Type-EndpointDetails-SecurityGroupIds"></a>
A list of security groups IDs that are available to attach to your server's endpoint\.  
This property can only be set when `EndpointType` is set to `VPC`\.  
You can edit the `SecurityGroupIds` property in the [UpdateServer](https://docs.aws.amazon.com/transfer/latest/userguide/API_UpdateServer.html) API only if you are changing the `EndpointType` from `PUBLIC` or `VPC_ENDPOINT` to `VPC`\. To change security groups associated with your server's VPC endpoint after creation, use the Amazon EC2 [ModifyVpcEndpoint](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_ModifyVpcEndpoint.html) API\.
Type: Array of strings  
Length Constraints: Minimum length of 11\. Maximum length of 20\.  
Pattern: `^sg-[0-9a-f]{8,17}$`   
Required: No

 ** SubnetIds **   <a name="TransferFamily-Type-EndpointDetails-SubnetIds"></a>
A list of subnet IDs that are required to host your server endpoint in your VPC\.  
This property can only be set when `EndpointType` is set to `VPC`\.
Type: Array of strings  
Required: No

 ** VpcEndpointId **   <a name="TransferFamily-Type-EndpointDetails-VpcEndpointId"></a>
The identifier of the VPC endpoint\.  
This property can only be set when `EndpointType` is set to `VPC_ENDPOINT`\.  
For more information, see [Discontinuing the use of VPC\_ENDPOINTYou can change the endpoint type for your server using the Transfer Family console, AWS CLI, API, SDKs, or AWS CloudFormation\. To change your server’s endpoint type, see [Updating the AWS Transfer Family server endpoint type from VPC\_ENDPOINT to VPC](update-endpoint-type-vpc.md)\.](create-server-in-vpc.md#deprecate-vpc-endpoint)\.
Type: String  
Length Constraints: Fixed length of 22\.  
Pattern: `^vpce-[0-9a-f]{17}$`   
Required: No

 ** VpcId **   <a name="TransferFamily-Type-EndpointDetails-VpcId"></a>
The VPC identifier of the VPC in which a server's endpoint will be hosted\.  
This property can only be set when `EndpointType` is set to `VPC`\.
Type: String  
Required: No

## See Also<a name="API_EndpointDetails_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transfer-2018-11-05/EndpointDetails) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transfer-2018-11-05/EndpointDetails) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transfer-2018-11-05/EndpointDetails) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transfer-2018-11-05/EndpointDetails) 
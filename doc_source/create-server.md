# Creating a server<a name="create-server"></a>

Following, you can find how to create a file transfer protocol enabled server using the AWS Transfer Family service\. The following protocols are available:
+ Secure Shell \(SSH\) File Transfer Protocol \(SFTP\) – file transfer over SSH
+ File Transfer Protocol Secure \(FTPS\) – file transfer with TLS encryption
+ File Transfer Protocol \(FTP\) – unencrypted file transfer

You can create a server with multiple protocols\.

**Note**  
If you have multiple protocols enabled for the same server endpoint and want to provide access using the same user name over multiple protocols, you can do so as long as the credentials specific to the protocol have been set up in your identity provider\. For FTP, we recommend maintaining separate credentials from SFTP and FTPS\. This is because, unlike SFTP and FTPS, FTP transmits credentials in clear text\. By isolating FTP credentials from SFTP or FTPS, if FTP credentials are shared or exposed, your workloads using SFTP or FTPS remain secure\.

When you create a server, you choose a specific AWS Region to perform the file operation requests of users who are assigned to that server\. Along with assigning the server one or more protocols, you also assign one of the following identity provider types:
+ Service managed using SSH keys\. For details, see [Working with service\-managed users](service-managed-users.md)\.
+ AWS Managed Microsoft AD\. This method allows you integrate your Microsoft Active Directory groups to provide access to your Transfer Family servers\. For details, see [Using the AWS Directory Service identity provider](directory-services-users.md)\.
+ A custom method\. The custom identity provider method uses AWS Lambda or Amazon API Gateway and enables you to integrate your directory service to authenticate and authorize your users\. The service automatically assigns an identifier that uniquely identifies your server\. For details, see [Working with custom identity providers](custom-identity-provider-users.md)\.

You also assign the server an endpoint type \(publicly accessible or VPC hosted\) and a hostname using the default server endpoint, or a custom hostname using the Amazon Route 53 service or by using a Domain Name System \(DNS\) service of your choice\. A server hostname must be unique in the AWS Region where it's created\.

Additionally, you can assign an Amazon CloudWatch logging role to push events to your CloudWatch Logs, choose a security policy that contains the cryptographic algorithms enabled for use by your server, and add metadata to the server in the form of tags that are key\-value pairs\.

**Important**  
You incur costs for instantiated servers and for data transfer\. For information about pricing and to use AWS Pricing Calculator to get an estimate of the cost to use Transfer Family, see [AWS Transfer Family pricing](http://aws.amazon.com/aws-transfer-family/pricing/)\.

## Identity provider options<a name="identity-provider-details"></a>

AWS Transfer Family provides several methods for authenticating and managing users\. The following table compares the available identity providers you can use with Transfer Family\.


| Action | AWS Transfer Family service managed | AWS Directory Service for Microsoft Active Directory | Amazon API Gateway | Lambda | 
| --- | --- | --- | --- | --- | 
|  Logical home directory  |  Yes  |  Yes  |  Yes  |  Yes  | 
|  IAM and POSIX  |  Yes  |  Yes  |  Yes  |  Yes  | 
|  Ad hoc access structure  |  Yes  |  No  |  Yes  |  Yes  | 
|  Password authentication  |  No  |  Yes  |  Yes  |  Yes  | 
|  Key\-based authentication  |  Yes  |  No  |  Yes  |  Yes  | 
|  AWS Web Application Firewall  |  No  |  No  |  Yes  |  No  | 

Notes:
+ IAM is used to control access for Amazon S3 backing storage, and POSIX is used for Amazon EFS\.
+ *Ad hoc* refers to the ability to send the user profile at run time\. For example, you can land users in their home directories by passing the username as a variable\.
+ For details on AWS WAF, see [Add a web application firewall](web-application-firewall.md)\.

In the following procedures, you can create an SFTP\-enabled server, FTPS\-enabled server, or FTP\-enabled server\.

**Next step**
+ [Create an SFTP\-enabled server](create-server-sftp.md)
+ [Create an FTPS\-enabled server](create-server-ftps.md)
+ [Create an FTP\-enabled server](create-server-ftp.md)

## AWS Transfer Family endpoint type matrix<a name="endpoint-matrix"></a>

When you create a Transfer Family server, you choose the type of endpoint to use\. The following table describes characteristics for each type of endpoint\.


**Endpoint type matrix**  

| Characteristic | Public | VPC \- Internet | VPC \- Internal | VPC\_Endpoint \(deprecated\) | 
| --- | --- | --- | --- | --- | 
| Supported protocols | SFTP | SFTP, FTPS | SFTP, FTP, FTPS | SFTP | 
| Access | From over the internet\. This endpoint type doesn't require any special configuration in your VPC\. | Over the internet and from within VPC and VPC\-connected environments, such as an on\-premises data center over AWS Direct Connect or VPN\. | From within VPC and VPC\-connected environments, such as an on\-premises data center over AWS Direct Connect or VPN\. | From within VPC and VPC\-connected environments, such as an on\-premises data center over AWS Direct Connect or VPN\. | 
| Static IP address | You can’t attach a static IP address\. AWS provides IP addresses that are subject to change\. |  You can attach Elastic IP addresses to the endpoint\. These can be AWS\-owned IP addresses or your own IP addresses \([Bring your own IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-byoip.html)\)\. Elastic IP addresses attached to the endpoint don't change\. Private IP addresses attached to the server also don't change\.  | Private IP addresses attached to the endpoint don't change\. | Private IP addresses attached to the endpoint don't change\. | 
| Source IP allow list |  This endpoint type does not support allow lists by source IP addresses\. The endpoint is publicly accessible and listens for traffic over port 22\.  |  To allow access by source IP address, you can use security groups attached to the server endpoints and network ACLs attached to the subnet that the endpoint is in\.  |  To allow access by source IP address, you can use security groups attached to the server endpoints and network access control lists \(network ACLs\) attached to the subnet that the endpoint is in\.  |  To allow access by source IP address, you can use security groups attached to the server endpoints and network ACLs attached to the subnet that the endpoint is in\.  | 
| Client firewall allow list |  You must allow the DNS name of the server\. Because IP addresses are subject to change, avoid using IP addresses for your client firewall allow list\.  |  You can allow the DNS name of the server or the Elastic IP addresses attached to the server\.  |  You can allow the private IP addresses or the DNS name of the endpoints\.  |  You can allow the private IP addresses or the DNS name of the endpoints\.  | 

**Note**  
The `VPC_ENDPOINT` endpoint type is now deprecated and cannot be used to create new servers\. For details, see [Discontinuing the use of VPC\_ENDPOINTYou can change the endpoint type for your server using the Transfer Family console, AWS CLI, API, SDKs, or AWS CloudFormation\. To change your server’s endpoint type, see [Updating the AWS Transfer Family server endpoint type from VPC\_ENDPOINT to VPC](update-endpoint-type-vpc.md)\.](create-server-in-vpc.md#deprecate-vpc-endpoint)\.

Consider the following options to increase the security posture of your AWS Transfer Family server:
+ Use a VPC endpoint with internal access, so that the server is accessible only to clients within your VPC or VPC\-connected environments such as an on\-premises data center over AWS Direct Connect or VPN\.
+ To allow clients to access the endpoint over the internet and protect your server, use a VPC endpoint with internet\-facing access\. Then, modify the VPC's security groups to allow traffic only from certain IP addresses that host your users' clients\.
+ Use a Network Load Balancer in front of a VPC endpoint with internal access\. Change the listener port on the load balancer from port 22 to a different port\. This can reduce, but not eliminate, the risk of port scanners and bots probing your server, because port 22 is most commonly used for scanning\. However, if you use a Network Load Balancer, you can't use security groups to allow access from source IP addresses\.
+ If you require password\-based authentication and you use a custom identity provider with your server, it's a best practice that you set an aggressive password policy\. It's a best practice that your password policy prevents users from creating weak passwords and limits the number of failed login attempts\.
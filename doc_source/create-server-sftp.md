# Create an SFTP\-enabled server<a name="create-server-sftp"></a>

Secure Shell \(SSH\) File Transfer Protocol \(SFTP\) is a network protocol used for secure transfer of data over the internet\. The protocol supports the full security and authentication functionality of SSH\. It's widely used to exchange data, including sensitive information between business partners in a variety of industries such as financial services, healthcare, retail, and advertising\.

**Note**  
 SFTP servers for Transfer Family operate over port 22\. 

**To create an SFTP\-enabled server**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/) and select **Servers** from the navigation pane, then choose **Create server**\.

1. In **Choose protocols**, select **SFTP**, and then choose **Next**\.  
![\[Console screenshot showing Choose protocols dialog box with SFTP selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-protocols-sftp.png)

1. In **Choose an identity provider**, choose the identity provider that you want to use to manage user access\. You have the following options:
   + **Service managed**: you store user identities and keys in AWS Transfer Family\.   
![\[Console screenshot showing Choose identity provider dialog box with service managed selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-idp-service-managed.png)
   + **AWS Directory Service for Microsoft Active Directory**: you provide an AWS Directory Service directory to access the endpoint\. By doing so, you can use credentials stored in your Active Directory to authenticate your users\. To learn more about working with AWS Managed Microsoft AD identity providers, see [Using the AWS Directory Service identity provider](directory-services-users.md)\.
**Note**  
 Cross\-Account and Shared directories are not supported for AWS Managed Microsoft AD\.   
![\[Console screenshot showing Choose identity provider dialog box with Managed AD selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-idp-directory-services.png)
   + **Custom**: choose either of the following options:
     + **AWS Lambda** to integrate your identity provider: use your existing identity providers, backed by a Lambda function\. You provide the name of the Lambda function\. For more details, see [Using AWS Lambda to integrate your identity provider](custom-identity-provider-users.md#custom-lambda-idp)
     + **Amazon API Gateway method** backed by a Lambda function: create an API Gateway for use as an identity provider\. You provide an Amazon API Gateway URL and an invocation role\. For more details, see [Using Amazon API Gateway to integrate your identity provider](custom-identity-provider-users.md#authentication-api-gateway)\.  
![\[Console screenshot showing Choose identity provider dialog box with Custom selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/custom-lambda-console.png)

1. Choose **Next**\.

1. In **Choose an endpoint**, do the following:

   1. For **Endpoint type**, choose the **Publicly accessible** endpoint type\. For a **VPC hosted** endpoint, see [Create a server in a virtual private cloud](create-server-in-vpc.md)\.

   1. \(Optional\) For **Custom hostname**, choose **None**\.

      You get a server hostname provided by AWS Transfer Family\. The server hostname takes the form `serverId.server.transfer.regionId.amazonaws.com`\.

      For a custom hostname, you specify a custom alias for your server endpoint\. To learn more about working with custom hostnames, see [Working with custom hostnames](requirements-dns.md)\.

   1. \(Optional\) For **FIPS Enabled**, select the **FIPS Enabled endpoint** check box to ensure that the endpoint complies with Federal Information Processing Standards \(FIPS\)\.
**Note**  
FIPS\-enabled endpoints are only available in North American AWS Regions\. For available Regions, see [AWS Transfer Family endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*\. For more information about the available FIPS endpoints, see [ Federal Information Processing Standard \(FIPS\) 140\-2 ](http://aws.amazon.com/compliance/fips/)\.

   1. Choose **Next**\.  
![\[Console screenshot showing Choose endpoint dialog box with Publicly accessible selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-endpoint-type-public.png)

1. On the **Choose domain** page, choose the AWS storage service that you want to use to store and access your data over the selected protocol:
   + Choose **Amazon S3** to store and access your files as objects over the selected protocol\.
   + Choose **Amazon EFS** to store and access your files in your Amazon EFS file system over the selected protocol\.

   Choose **Next**\.

1. In **Configure additional details**, do the following:

   1. For **CloudWatch logging**, choose one of the following to enable Amazon CloudWatch logging of your user activity:
      + **Create a new role** to allow Transfer Family to create the IAM role automatically, as long as you have the right permissions to create a new role\. The IAM role that is created is called `AWSTransferLoggingAccess`\.
      + **Choose an existing role** to choose an existing IAM role from your account\. Under **Logging role**, choose the role\. This IAM role should include a trust policy with **Service** set to `transfer.amazonaws.com`\.

        For more information about CloudWatch logging, see [Log activity with CloudWatch](monitoring.md#monitoring-enabling)\.
**Note**  
You can't view end\-user activity in CloudWatch if you don't specify a logging role\.
If you don't want to set up a CloudWatch logging role, choose **Choose an existing role**, but don't select a logging role\.  
![\[Console screenshot showing CloudWatch logging section with Create new role selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-cloudwatch-logging.png)

   1. For **Cryptographic algorithm options**, choose a security policy that contains the cryptographic algorithms enabled for use by your server\.
**Note**  
By default:  
If **FIPS Enabled endpoint** is not selected, the `TransferSecurityPolicy-2020-06` security policy is attached to your server\.
If **FIPS Enabled endpoint** is selected, the `TransferSecurityPolicy-FIPS-2020-06` security policy is attached to your server\.

      For more information about security policies, see [Working with security policies](security-policies.md)\.  
![\[Console screenshot showing cryptographic algorithm options section with a security policy selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-cryptographic-algorithm-options.png)

   1. \(Optional\) For **Server Host Key**, enter an RSA, ED25519, or ECDSA private key that will be used to identify your server when clients connect to it over SFTP\.
**Note**  
This section is only for migrating users from an existing SFTP\-enabled server\.  
![\[Console screenshot showing server host key section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-server-host-key.png)

   1. \(Optional\) For **Tags**, for **Key** and **Value**, enter one or more tags as key\-value pairs, and then choose **Add tag**\.

   1. Choose **Next**\.  
![\[Console screenshot showing the tags section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-tags.png)

   1.  \(Optional\) For **Managed workflows**, select a workflow ID and a corresponding role that Transfer Family should assume when executing the workflow\. To learn more about processing your files using managed workflows, see [AWS Transfer Family managed workflows](transfer-workflows.md)\.  
![\[Console screenshot showing the tags section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-addtoserver.png)

   1. \(Optional\) You can configure AWS Transfer Family servers to display customized messages such as organizational policies or terms and conditions to your end users\. For **Display banner**, in the **Pre\-authentication display banner** text box, enter the text message that you want to display to your users before they authenticate\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/display-banner-sftp-only.png)

1. In **Review and create**, review your choices\.
   + If you want to edit any of them, choose **Edit** next to the step\.
**Note**  
You will need to review each step after the step you chose to edit\.
   + If you have no changes, choose **Create server** to create your server\. You are taken to the **Servers** page, shown following, where your new server is listed\.

It can take a couple of minutes before the status for your new server changes to **Online**\. At that point, your server can perform file operations for your users\.

![\[Console screenshot showing servers section with server id and status of starting.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/servers-page.png)
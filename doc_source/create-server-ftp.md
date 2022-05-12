# Create an FTP\-enabled server<a name="create-server-ftp"></a>

File Transfer Protocol \(FTP\) is a network protocol used for the transfer of data\. FTP uses a separate channel for control and data transfers\. The control channel is open until terminated or inactivity timeout\. The data channel is active for the duration of the transfer\. FTP uses clear text and does not support encryption of traffic\.

**To create an FTP\-enabled server**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/) and select **Servers** from the navigation pane, then choose **Create server**\.

1. In **Choose protocols**, select **FTP**, and then choose **Next**\.  


1. In **Choose an identity provider**, choose the identity provider that you want to use to manage user access\. You have the following options:
   + **AWS Directory Service for Microsoft Active Directory**: you provide an AWS Directory Service directory to access the endpoint\. By doing so, you can use credentials stored in your Active Directory to authenticate your users\. To learn more about working with AWS Managed Microsoft AD identity providers, see [Using the AWS Directory Service identity provider](directory-services-users.md)\.
**Note**  
 Cross\-Account and Shared directories are not supported for AWS Managed Microsoft AD\.   

   + **Custom**: choose either of the following options:
     + **AWS Lambda** to integrate your identity provider: use your existing identity providers, backed by a Lambda function\. You provide the name of the Lambda function\. For more details, see [Using AWS Lambda to integrate your identity provider](custom-identity-provider-users.md#custom-lambda-idp)
     + **Amazon API Gateway method** backed by a Lambda function: create an API Gateway for use as an identity provider\. You provide an Amazon API Gateway URL and an invocation role\. For more details, see [Using Amazon API Gateway to integrate your identity provider](custom-identity-provider-users.md#authentication-api-gateway)\.  


1. In **Choose an endpoint**, do the following:
**Note**  
 FTP servers for Transfer Family operate over Port 21 \(Control Channel\) and Port Range 8192\-8200 \(Data Channel\)\. 

   1. For **Endpoint type**, choose **VPC hosted** to host your server's endpoint\. For information about setting up your VPC hosted endpoint, see [Create a server in a virtual private cloud](create-server-in-vpc.md)\.
**Note**  
Publicly accessible endpoints are not supported\.

   1. For **FIPS Enabled**, keep the **FIPS Enabled endpoint** check box cleared\.
**Note**  
A FIPS\-enabled endpoint is not supported\.

   1. Choose **Next**\.  


1. On the **Choose domain** page, choose the AWS storage service that you want to use to store and access your data over the selected protocol\.
   + Choose **Amazon S3** to store and access your files as objects over the selected protocol\.
   + Choose **Amazon EFS** to store and access your files in your Amazon EFS file system over the selected protocol\.

   Choose **Next**\.

1. In **Configure additional details**, do the following:

   1. For **CloudWatch logging**, choose one of the following to enable Amazon CloudWatch logging of your user activity:
      + **Create a new role** to allow Transfer Family to automatically create the IAM role, as long as you have the right permissions to create a new role\. The IAM role that is created is called `AWSTransferLoggingAccess`\.
      + **Choose an existing role** to choose an existing IAM role from your account\. Under **Logging role**, choose the role\. This IAM role should include a trust policy with **Service** set to `transfer.amazonaws.com`\.

        For more information about CloudWatch logging, see [Log activity with CloudWatch](monitoring.md#monitoring-enabling)\.
**Note**  
You can't view end\-user activity in CloudWatch if you don't specify a logging role\.
If you don't want to set up a CloudWatch logging role, choose **Choose an existing role**, but don't select a logging role\.  


   1. For **Cryptographic algorithm options**, choose a security policy that contains the cryptographic algorithms enabled for use by your server\.
**Note**  
By default, the `TransferSecurityPolicy-2020-06` security policy is attached to your server\.

      For more information about security policies, see [Working with security policies](security-policies.md)\.  


   1. \(Optional\) For **Server Host Key**, keep it blank\.
**Note**  
This section is only for migrating users from an existing SFTP\-enabled server\.  


   1. \(Optional\) For **Tags**, for **Key** and **Value**, enter one or more tags as key\-value pairs, and then choose **Add tag**\.

   1. Choose **Next**\.  


   1.  \(Optional\) For **Managed workflows**, select a workflow ID and a corresponding role that Transfer Family should assume when executing the workflow\. To learn more about processing your files using managed workflows, see [AWS Transfer Family managed workflows](transfer-workflows.md)\.  
![\[Console screenshot showing the tags section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-addtoserver.png)

   1. \(Optional\) You can configure AWS Transfer Family servers to display customized messages such as organizational policies or terms and conditions to your end users\. You can also display customized Message of The Day \(MOTD\) to users who have successfully authenticated\.

      For **Display banner**, in the **Pre\-authentication display banner** text box, enter the text message that you want to display to your users before they authenticate, and in the **Post\-authentication display banner** text box, enter the text that you want to display to your users after they successfully authenticate\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/display-banner-non-sftp.png)

1. In **Review and create**, review your choices\.
   + If you want to edit any of them, choose **Edit** next to the step\.
**Note**  
You will need to review each step after the step you chose to edit\.
   + If you have no changes, choose **Create server** to create your server\. You are taken to the **Servers** page, shown following, where your new server is listed\.

It can take a couple of minutes before the status for your new server changes to **Online**\. At that point, your server can perform file operations for your users\.



**Next steps** – For the next step, continue on to [Working with custom identity providers](custom-identity-provider-users.md) to set up users\.
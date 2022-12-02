# Create an FTPS\-enabled server<a name="create-server-ftps"></a>

File Transfer Protocol over SSL \(FTPS\) is an extension to FTP\. It uses Transport Layer Security \(TLS\) and Secure Sockets Layer \(SSL\) cryptographic protocols to encrypt traffic\. FTPS allows encryption of both the control and data channel connections either concurrently or independently\.

**To create an FTPS\-enabled server**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/) and select **Servers** from the navigation pane, then choose **Create server**\.

1. In **Choose protocols**, select **FTPS**\.

   For **Server certificate**, choose a certificate stored in AWS Certificate Manager \(ACM\) which will be used to identify your server when clients connect to it over FTPS and then choose **Next**\.

   To request a new public certificate, see [Request a public certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html) in the *AWS Certificate Manager User Guide*\.

   To import an existing certificate into ACM, see [Importing certificates into ACM](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html) in the *AWS Certificate Manager User Guide*\.

   To request a private certificate to use FTPS through private IP addresses, see [Requesting a Private Certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-private.html) in the *AWS Certificate Manager User Guide*\.

   Certificates with the following cryptographic algorithms and key sizes are supported:
   + 2048\-bit RSA \(RSA\_2048\)
   + 4096\-bit RSA \(RSA\_4096\)
   + Elliptic Prime Curve 256 bit \(EC\_prime256v1\)
   + Elliptic Prime Curve 384 bit \(EC\_secp384r1\)
   + Elliptic Prime Curve 521 bit \(EC\_secp521r1\)
**Note**  
The certificate must be a valid SSL/TLS X\.509 version 3 certificate with FQDN or IP address specified and information about the issuer\.  
![\[The Choose protocols console section with FTPS selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-protocols-ftps-ACM.png)

1. In **Choose an identity provider**, choose the identity provider that you want to use to manage user access\. You have the following options:
   + **AWS Directory Service for Microsoft Active Directory** – You provide an AWS Directory Service directory to access the endpoint\. By doing so, you can use credentials stored in your Active Directory to authenticate your users\. To learn more about working with AWS Managed Microsoft AD identity providers, see [Using the AWS Directory Service identity provider](directory-services-users.md)\.
**Note**  
 Cross\-Account and Shared directories are not supported for AWS Managed Microsoft AD\.   
![\[The Choose an identity provider console section with AWS Directory Service selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-idp-directory-services.png)
   + **Custom identity provider** – Choose either of the following options:
     + **Use AWS Lambda to connect your identity provider** – You can use an existing identity provider, backed by a Lambda function\. You provide the name of the Lambda function\. For more information, see [Using AWS Lambda to integrate your identity provider](custom-identity-provider-users.md#custom-lambda-idp)\.
     + **Use Amazon API Gateway to connect your identity provider** – You can create an API Gateway method backed by a Lambda function for use as an identity provider\. You provide an Amazon API Gateway URL and an invocation role\. For more information, see [Using Amazon API Gateway to integrate your identity provider](custom-identity-provider-users.md#authentication-api-gateway)\.  
![\[The Choose an identity provider console section with Custom identity provider selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/custom-lambda-console.png)

1. In **Choose an endpoint**, do the following:
**Note**  
 FTPS servers for Transfer Family operate over Port 21 \(Control Channel\) and Port Range 8192–8200 \(Data Channel\)\. 

   1. For **Endpoint type**, choose the **VPC hosted** endpoint type to host your server's endpoint\. For information about setting up your VPC hosted endpoint, see [Create a server in a virtual private cloud](create-server-in-vpc.md)\.
**Note**  
Publicly accessible endpoints are not supported\.

   1. \(Optional\) For **FIPS Enabled**, select the **FIPS Enabled endpoint** check box to ensure that the endpoint complies with Federal Information Processing Standards \(FIPS\)\.
**Note**  
FIPS\-enabled endpoints are only available in North American AWS Regions\. For available Regions, see [AWS Transfer Family endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*\. For more information about the available FIPS endpoints, see [ Federal Information Processing Standard \(FIPS\) 140\-2 ](http://aws.amazon.com/compliance/fips/)\.

   1. Choose **Next**\.  
![\[The Choose an endpoint console section with VPC hosted selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-endpoint-vpc-internal.png)

1. On the **Choose domain** page, choose the AWS storage service that you want to use to store and access your data over the selected protocol:
   + Choose **Amazon S3** to store and access your files as objects over the selected protocol\.
   + Choose **Amazon EFS** to store and access your files in your Amazon EFS file system over the selected protocol\.

   Choose **Next**\.

1. In **Configure additional details**, do the following:

   1. For **CloudWatch logging**, choose one of the following to enable Amazon CloudWatch logging of your user activity:
      + **Create a new role** to allow Transfer Family to automatically create the IAM role, as long as you have the right permissions to create a new role\. The IAM role that is created is called `AWSTransferLoggingAccess`\.
      + **Choose an existing role** to choose an existing IAM role from your account\. Under **Logging role**, choose the role\. This IAM role should include a trust policy with **Service** set to `transfer.amazonaws.com`\.

        For more information about CloudWatch logging, see [Log activity with CloudWatch](monitoring.md#monitoring-enabling)\.
**Note**  
You can't view end user activity in CloudWatch if you don't specify a logging role\.
If you don't want to set up a CloudWatch logging role, choose **Choose an existing role**, but don't select a logging role\.  
![\[The CloudWatch logging console section with Create a new role selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-cloudwatch-logging.png)

   1. For **Cryptographic algorithm options**, choose a security policy that contains the cryptographic algorithms enabled for use by your server\.
**Note**  
By default:  
If **FIPS Enabled endpoint** is not selected, the `TransferSecurityPolicy-2020-06` security policy is attached to your server\.
If **FIPS Enabled endpoint** is selected, the `TransferSecurityPolicy-FIPS-2020-06` security policy is attached to your server\.

      For more information about security policies, see [Working with security policies](security-policies.md)\.  
![\[The Cryptographic algorithm options console section with a security policy selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-cryptographic-algorithm-options.png)

   1. For **Server Host Key**, keep it blank\.
**Note**  
The **Server Host Key** section is used only for migrating users from an existing SFTP\-enabled server\.  
![\[The Server host key console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-server-host-key.png)

   1. \(Optional\) For **Tags**, for **Key** and **Value**, enter one or more tags as key\-value pairs, and then choose **Add tag**\.

   1. Choose **Next**\.  
![\[The Tags console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-tags.png)

   1.  \(Optional\) For **Managed workflows**, choose workflow IDs \(and a corresponding role\) that Transfer Family should assume when executing the workflow\. You can choose one workflow to execute upon a complete upload, and another to execute upon a partial upload\. To learn more about processing your files by using managed workflows, see [AWS Transfer Family managed workflows](transfer-workflows.md)\.  
![\[The Managed workflows console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-addtoserver.png)

   1. \(Optional\) You can configure AWS Transfer Family servers to display customized messages such as organizational policies or terms and conditions to your end users\. You can also display customized Message of The Day \(MOTD\) to users who have successfully authenticated\.

      For **Display banner**, in the **Pre\-authentication display banner** text box, enter the text message that you want to display to your users before they authenticate, and in the **Post\-authentication display banner** text box, enter the text that you want to display to your users after they successfully authenticate\.  
![\[The Display banner console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/display-banner-non-sftp.png)

1. In **Review and create**, review your choices\.
   + If you want to edit any of them, choose **Edit** next to the step\.
**Note**  
You must review each step after the step that you chose to edit\.
   + If you have no changes, choose **Create server** to create your server\. You are taken to the **Servers** page, shown following, where your new server is listed\.

It can take a couple of minutes before the status for your new server changes to **Online**\. At that point, your server can perform file operations for your users\.



**Next steps**: For the next step, continue on to [Working with custom identity providers](custom-identity-provider-users.md) to set up users\.
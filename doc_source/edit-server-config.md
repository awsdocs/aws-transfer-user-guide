# Edit server details<a name="edit-server-config"></a>

After you create an AWS Transfer Family server, you can edit the server configuration\.

**Topics**
+ [Edit the file transfer protocols](#edit-protocols)
+ [Edit the server endpoint](#edit-endpoint-configuration)
+ [Edit Amazon CloudWatch logging](#edit-CloudWatch-logging)
+ [Edit the security policy](#edit-cryptographic-algorithm)
+ [Manage host keys for your SFTP\-enabled server](#configuring-servers-change-host-key)
+ [Change the managed workflow for your server](#configuring-servers-change-workflow)
+ [Change the display banners for your server](#configuring-servers-change-banner)
+ [Put your server online or offline](#edit-online-offline)



**To edit a server's configuration**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**\.

1. Choose the identifier in the **Server ID** column to see the **Server details** page, shown following\.

   You can change the server's properties on this page by choosing **Edit**:
   + To change the protocols, see [Edit the file transfer protocols](#edit-protocols)\.
   + For the identity provider, note that you can't change a server's identity provider type after you create the server\. To change the identity provider, delete the server and create a new one with the identity provider that you want\.
   + To change the endpoint type or custom hostname, see [Edit the server endpoint](#edit-endpoint-configuration)\.
   + To add an agreement, you need to first add AS2 as a protocol to your server\. For details, see [Edit the file transfer protocols](#edit-protocols)\.
   + To manage host keys for your server, see [Manage host keys for your SFTP\-enabled server](#configuring-servers-change-host-key)\.
   + Under **Additional details**, you can edit the following information:
     + To change the logging role, see [Edit Amazon CloudWatch logging](#edit-CloudWatch-logging)\.
     + To change the security policy, see [Edit the security policy](#edit-cryptographic-algorithm)\.
     + To change the server host key, see [Manage host keys for your SFTP\-enabled server](#configuring-servers-change-host-key)\.
     + To change the managed workflow for your server, see [Change the managed workflow for your server](#configuring-servers-change-workflow)\.
     + To edit the display banners for your server, see [Change the display banners for your server](#configuring-servers-change-banner)\.
   + To start or stop your server, see [Put your server online or offline](#edit-online-offline)\.
   + To delete a server, see [Delete a server](delete-server.md)\.
   + To edit a user's properties, see [Managing access controls](users-policies.md)\.  
![\[The server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-top.png)![\[The server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-endpoints.png)![\[The server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-users.png)![\[The server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-agreements.png)![\[The server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-hostkeys.png)
**Note**  
The server host key **Description** and **Date imported** values are new as of September 2022\. These values were introduced to support the multiple host keys feature\. This feature required migration of any single host keys that were in use before the introduction of multiple host keys\.   
The **Date imported** value for a migrated server host key is set to the last modified date for the server\. That is, the date that you see for your migrated host key corresponds to the date that you last modified the server in any way, before the server host key migration\.  
The only key that was migrated is your oldest or only server host key\. Any additional keys have their actual date from when you imported them\. Additionally, the migrated key has a description that makes it easy to identify it as having been migrated\.  
The migration occurred between September 2 and September 13\. The actual migration date within this range depends on the Region of your server\.  
![\[Continuation of the server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-additionaldetails.png)![\[Continuation of the server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-monitoring.png)![\[Continuation of the server details console page for a server.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-server-details-tags.png)

## Edit the file transfer protocols<a name="edit-protocols"></a>

On the AWS Transfer Family console, you can edit the file transfer protocol\. The file transfer protocol connects the client to your server's endpoint\.

**To edit the protocols**

1. On the **Server details** page, choose **Edit** next to **Protocols**\.

1. On the **Edit protocols** page, select or clear the protocol check box or check boxes to add or remove the following file transfer protocols:
   + Secure Shell \(SSH\) File Transfer Protocol \(SFTP\) – file transfer over SSH

     For more information about SFTP, see [Create an SFTP\-enabled server](create-server-sftp.md)\.
   + File Transfer Protocol Secure \(FTPS\) – file transfer with TLS encryption

     For more information about FTP, see [Create an FTPS\-enabled server](create-server-ftps.md)\.
   + File Transfer Protocol \(FTP\) – unencrypted file transfer

     For more information about FTPS, see [Create an FTP\-enabled server](create-server-ftp.md)\.
**Note**  
If you have an existing server enabled only for SFTP, and you want to add FTPS and FTP, you must ensure that you have the right identity provider and endpoint type settings that are compatible with FTPS and FTP\.  
![\[The Edit protocols console page.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-protocols.png)

   If you select **FTPS**, you must choose a certificate stored in AWS Certificate Manager \(ACM\) which will be used to identify your server when clients connect to it over FTPS\.

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
![\[The Choose protocols console page with FTPS selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-protocols-ftps-ACM.png)

1. Choose **Save**\. You are returned to the **Server details** page\.

## Edit the server endpoint<a name="edit-endpoint-configuration"></a>

On the AWS Transfer Family console, you can modify the server endpoint type and custom hostname\.

**To edit the server endpoint details**

1. On the **Server details** page, choose **Edit** next to **Endpoint details**\.

1. On the **Edit endpoint configuration** page, for **Endpoint type**, choose one of the following:
   + **Public** – This option makes your server accessible over the internet\.
   + **VPC ** – This option makes your server accessible in your virtual private cloud \(VPC\)\. For information about VPC, see [Create a server in a virtual private cloud](create-server-in-vpc.md)\.

1. For **Custom hostname**, choose one of the following:
   + **None** – If you don't want to use a custom domain, choose **None**\.

     You get a server hostname provided by AWS Transfer Family\. The server hostname takes the form `serverId.server.transfer.regionId.amazonaws.com`\.
   + **Amazon Route 53 DNS alias** – To use a DNS alias automatically created for you in Route 53, choose this option\.
   + **Other DNS** – To use a hostname that you already own in an external DNS service choose **Other DNS**\.

   Choosing **Amazon Route 53 DNS alias** or **Other DNS** specifies the name resolution method to associate with your server's endpoint\.

   For example, your custom domain might be `sftp.inbox.example.com`\. A custom hostname uses a DNS name that you provide and that a DNS service can resolve\. You can use Route 53 as your DNS resolver, or use your own DNS service provider\. To learn how AWS Transfer Family uses Route 53 to route traffic from your custom domain to the server endpoint, see [Working with custom hostnames](requirements-dns.md)\.  
![\[The Edit endpoint configuration console page.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-endpoint-configuration.png)

1. Choose **Save**\. You are returned to the **Server details** page\.

## Edit Amazon CloudWatch logging<a name="edit-CloudWatch-logging"></a>

On the AWS Transfer Family console, you can enable Amazon S3 event logging using Amazon CloudWatch\.

**Note**  
If Transfer Family created a CloudWatch logging IAM role for you when you created a server, the IAM role is called `AWSTransferLoggingAccess`\. You can use it for all your servers\.

**To edit the CloudWatch logging IAM role**

1. On the **Server details** page, choose **Edit** next to **Additional details**\.

1. In the **CloudWatch logging** section, do one of the following:
   + If Transfer Family created a CloudWatch logging IAM role for you when you created a server, the IAM role is called `AWSTransferLoggingAccess`\. Choose it from the **Logging role** list\.
   + If you chose an existing CloudWatch logging IAM role or you didn't choose a CloudWatch logging IAM role at all when you created this server, choose or modify the CloudWatch logging IAM role from the **Logging role** list\.

   For more information about CloudWatch logging, see [Log activity with CloudWatch](monitoring.md#monitoring-enabling)\.
**Note**  
You can't view end\-user activity in CloudWatch if you don't specify a logging role\.  
![\[The Edit additional details console page, showing the CloudWatch logging section with a logging role specified.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-cloudwatch-logging.png)

1. Choose **Save**\. You are returned to the **Server details** page\.

## Edit the security policy<a name="edit-cryptographic-algorithm"></a>

On the AWS Transfer Family console, you can modify the security policy attached to your server\.

**To edit the security policy**

1. On the **Server details** page, choose **Edit** next to **Additional details**\.

1. In the **Cryptographic algorithm options** section, choose a security policy that contains the cryptographic algorithms enabled for use by your server\.
**Note**  
If your endpoint is FIPS\-enabled, you can't change the FIPS security policy\.

   For more information about security policies, see [Working with security policies](security-policies.md)\.  
![\[The Cryptographic algorithm options console section with a security policy selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-cryptographic-algorithm-options.png)

1. Choose **Save**\. You are returned to the **Server details** page\.

## Manage host keys for your SFTP\-enabled server<a name="configuring-servers-change-host-key"></a>

**Important**  
If you aren't planning to migrate existing users from an existing SFTP\-enabled server to a new SFTP\-enabled server, ignore this section\. Accidentally changing a server's host key can be disruptive\.

By default, AWS Transfer Family provides a host key for your SFTP\-enabled server\. You can replace the default host key with a host key from another server\. Do so only if you plan to move existing users from an existing SFTP\-enabled server to your new SFTP\-enabled server\.

To prevent your users from being prompted to verify the authenticity of your SFTP\-enabled server again, import the host key for your on\-premises server to the SFTP\-enabled server\. Doing this also prevents your users from getting a warning about a potential man\-in\-the\-middle attack\.

You can also rotate host keys periodically, as an additional security measure\.

**Note**  
Although the Transfer Family console allows you to specify and add server host keys for all servers, these keys are only useful for servers that use the SFTP protocol\.

**Topics**
+ [Add an additional server host key](#server-host-key-add)
+ [Delete a server host key](#server-host-key-delete)
+ [Rotate the server host keys](#server-host-key-rotate)
+ [Additional server host key information](#server-host-key-other)

### Add an additional server host key<a name="server-host-key-add"></a>

On the AWS Transfer Family console, you can add an additional server host key\.

**To add an additional server host key**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**, and then choose a server that uses the SFTP protocol\.

1. On the server details page, scroll down to the **Server host keys** section\.  
![\[The Server host keys console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/server-host-keys.png)

1. Choose **Add host key**\.

   The **Add server host key** page displays\.

1. In the **Server Host Key** section, enter an RSA, ECDSA, or ED25519 private key that is used to identify your server when clients connect to it over the SFTP\-enabled server\.  
![\[The Server Host Key console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-configure-additional-details-server-host-key.png)

1. \(Optional\) Add a description to differentiate among multiple server host keys\. You can also add tags for your key\.

1. Choose **Add key**\. You are returned to the **Server details** page\.

To add a host key by using the AWS Command Line Interface \(AWS CLI\), use the [ImportHostKey](API_ImportHostKey.md) API operation and provide the new host key\. If you create a new SFTP\-enabled server, you provide your host key as a parameter in the [CreateServer](API_CreateServer.md) API operation\. You can also use the AWS CLI to update the description for an existing host key\.

The following example `import-host-key` AWS CLI command imports a host key for the specified SFTP\-enabled server\.

```
aws transfer import-host-key --description key-description --server-id your-server-id --host-key-body file://my-host-key 
```

### Delete a server host key<a name="server-host-key-delete"></a>

On the AWS Transfer Family console, you can delete a server host key\.

**To delete a server host key**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**, and then choose a server that uses the SFTP protocol\.

1. On the server details page, scroll down to the **Server host keys** section\.  
![\[The Server host keys console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/server-host-keys.png)

1. In the **Server Host Keys** section, select a key, and then under **Actions**, choose **Delete**\.

1. In the confirmation dialog box that appears, enter the word **delete**, and then choose **Delete** to confirm that you want to delete the host key\.

The host key is deleted from the **Servers** page\.

To delete the host key by using the AWS CLI, use the [DeleteHostKey](API_DeleteHostKey.md) API operation and provide the server ID and host key ID\.

The following example `delete-host-key` AWS CLI command deletes a host key for the specified SFTP\-enabled server\.

```
aws transfer delete-host-key --server-id your-server-id --host-key-id your-host-key-id
```

### Rotate the server host keys<a name="server-host-key-rotate"></a>

Periodically, you can rotate your server host key\.

**Note**  
Transfer Family uses the first added key for each algorithm as the active host key\. You can associate up to 10 host keys per SFTP server, but only one key per algorithm is active at any specific time\.

For example, assume that you have added the following set of server host keys to your server\.


**Server host keys**  

| Host key type | Date added to the server | Active? | 
| --- | --- | --- | 
| RSA | April 1, 2020 | No | 
| ECDSA | February 1, 2020 | No | 
| ED25519 | December 1, 2019 | No | 
| RSA | October 1, 2019 | Yes | 
| ECDSA | June 1, 2019 | Yes | 
| ED25519 | March 1, 2019 | Yes | 

The oldest key for each algorithm is active\. If you remove the RSA key that you added on October 1, 2019, then the RSA key that you added on April 1, 2020 becomes active\.

**To rotate the server host key**

1. Add a new server host key\. This procedure is described in [Add an additional server host key](#server-host-key-add)\.

1. Delete one or more of the host keys of the same type that you had added previously\. This procedure is described in [Delete a server host key](#server-host-key-delete)\.

1. Make sure that the earliest remaining key of the same type is the one that you want to make active\.

### Additional server host key information<a name="server-host-key-other"></a>

You can select a host key to display details for that key\.

![\[The hostkey details console screen.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/server-host-keys-details.png)

You can delete a host key, or edit its description from the **Actions** menu on the Server details screen\. Select the host key, then choose the appropriate action from the menu\.

![\[The server hostkey Actions menu.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/server-host-keys-actions.png)

## Change the managed workflow for your server<a name="configuring-servers-change-workflow"></a>

On the AWS Transfer Family console, you can change the managed workflow associated with the server\.

**To change the managed workflow**

1. On the **Server details** page, choose **Edit** next to **Additional details**\.

1. On the **Edit additional details** page, in the **Managed workflows** section, select a workflow to be run on all uploads\.
**Note**  
If you do not already have a workflow, choose **Create a new workflow** to create one\.

   1. Select the workflow ID to use\. 

   1. Choose an execution role\. This is the role that Transfer Family assumes when executing the workflow's steps\. For more information, see [IAM policies for workflows](workflow-execution-role.md)\. Choose **Save**\.  
![\[The Managed workflows console section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-addtoserver.png)

1. Choose **Save**\. You are returned to the **Server details** page\.

## Change the display banners for your server<a name="configuring-servers-change-banner"></a>

On the AWS Transfer Family console, you can change the display banners associated with the server\.

**To change the display banners**

1. On the **Server details** page, choose **Edit** next to **Additional details**\.

1. On the **Edit additional details** page, in the **Display banners** section, enter text for the available display banners\.

1. Choose **Save**\. You are returned to the **Server details** page\.

## Put your server online or offline<a name="edit-online-offline"></a>

On the AWS Transfer Family console, you can bring your server online or take it offline\.

**To bring your server online**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the navigation pane, choose **Servers**\.

1. Select the check box of the server that is offline\.

1. For **Actions**, choose **Start**\.

It can take a couple of minutes for a server to switch from offline to online\.

**Note**  
When you stop a server to take it offline, currently you are still accruing service charges for that server\. To eliminate additional server\-based charges, delete that server\.

**To take your server offline**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the navigation pane, choose **Servers**\.

1. Select the check box of the server that is online\.

1. For **Actions**, choose **Stop**\.

While a server is starting up or shutting down, servers aren't available for file operations\. The console doesn't show the starting and stopping states\.

If you find the error condition `START_FAILED` or `STOP_FAILED`, contact AWS Support to help resolve your issues\.
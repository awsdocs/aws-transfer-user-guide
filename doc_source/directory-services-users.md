# Using the AWS Directory Service identity provider<a name="directory-services-users"></a>

This topic describes how to use the AWS Directory Service identity provider for AWS Transfer Family\.

**Topics**
+ [Using AWS Directory Service for Microsoft Active Directory](#dir-services-ms-ad)
+ [Using AWS Directory Service for Azure Active Directory Domain Services](#azure-sftp)

## Using AWS Directory Service for Microsoft Active Directory<a name="dir-services-ms-ad"></a>

You can use AWS Transfer Family to authenticate your file transfer end users using AWS Directory Service for Microsoft Active Directory\. It enables seamless migration of file transfer workflows that rely on Active Directory authentication without changing end users’ credentials or needing a custom authorizer\. 

With AWS Managed Microsoft AD, you can securely provide AWS Directory Service users and groups access over SFTP, FTPS, and FTP for data stored in Amazon Simple Storage Service \(Amazon S3\) or Amazon Elastic File System \(Amazon EFS\)\. If you use Active Directory to store your users’ credentials, you now have an easier way to enable file transfers for these users\. 

You can provide access to Active Directory groups in AWS Managed Microsoft AD in your on\-premises environment or in the AWS Cloud using Active Directory connectors\. You can give users that are already configured in your Microsoft Windows environment, either in the AWS Cloud or in their on\-premises network, access to an AWS Transfer Family server that uses AWS Managed Microsoft AD for identity\. 

**Note**  
AWS Transfer Family does not support Simple AD\.
Transfer Family does not support cross\-region Active Directory configurations: we only support Active Directory integrations that are in the same region as that of the Transfer Family server\.
Transfer Family does not support using AD Connector to enable multi\-factor authentication \(MFA\) for your existing RADIUS\-based MFA infrastructure\.

To use AWS Managed Microsoft AD, you must perform the following steps:

1. Create one or more AWS Managed Microsoft AD directories using the AWS Directory Service console\.

1. Use the Transfer Family console to create a server that uses AWS Managed Microsoft AD as its identity provider\. 

1. Add access from one or more of your AWS Directory Service groups\. 

1. Although not required, we recommend that you test and verify user access\.

**Topics**
+ [Before you start using AWS Directory Service for Microsoft Active Directory](#managed-ad-prereq)
+ [Choosing AWS Managed Microsoft AD as your identity provider](#managed-ad-identity-provider)
+ [Granting access to groups](#directory-services-grant-access)
+ [Testing users](#directory-services-test-user)
+ [Deleting server access for a group](#directory-services-misc)
+ [Connecting to the server using SSH \(Secure Shell\)](#directory-services-ssh-procedure)
+ [Connecting AWS Transfer Family to a self\-managed Active Directory using forests and trusts](#directory-services-ad-trust)

### Before you start using AWS Directory Service for Microsoft Active Directory<a name="managed-ad-prereq"></a>

#### Provide a unique identifier for your AD groups<a name="add-identifier-adgroups"></a>

Before you can use AWS Managed Microsoft AD, you must provide a unique identifier for each group in your Microsoft AD directory\. You can use the security identifier \(SID\) for each group to do this\. The users of the group that you associate have access to your Amazon S3 or Amazon EFS resources over the enabled protocols using AWS Transfer Family\. 

Use the following Windows PowerShell command to retrieve the SID for a group, replacing *YourGroupName* with the name of the group\. 

```
Get-ADGroup -Filter {samAccountName -like "YourGroupName*"} -Properties * | Select SamAccountName,ObjectSid
```

**Note**  
If you are using AWS Directory Service as your identity provider, and if `userPrincipalName` and `SamAccountName` have different values, AWS Transfer Family accepts the value in `SamAccountName`\. Transfer Family does not accept the value specified in `userPrincipalName`\.

#### Add AWS Directory Service permissions to your role<a name="add-active-directory-permissions"></a>

You also need AWS Directory Service API permissions to use AWS Directory Service as your identity provider\. The following permissions are required or suggested:
+ `ds:DescribeDirectories` is required for Transfer Family to look up the directory
+ `ds:AuthorizeApplication` is required to add authorization for Transfer Family
+ `ds:UnauthorizeApplication` is suggested to remove any resources that are provisionally created, in case something goes wrong during the server creation process

Add these permissions to the role you are using for creating your Transfer Family servers\. For more details on these permissions, see [AWS Directory Service API permissions: Actions, resources, and conditions reference](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/UsingWithDS_IAM_ResourcePermissions.html)\.

### Choosing AWS Managed Microsoft AD as your identity provider<a name="managed-ad-identity-provider"></a>

This section describes how to use AWS Directory Service for Microsoft Active Directory with a server\.

**To use AWS Managed Microsoft AD with Transfer Family**

1. Sign in to the AWS Management Console and open the AWS Directory Service console at [https://console\.aws\.amazon\.com/directoryservicev2/](https://console.aws.amazon.com/directoryservicev2/)\.

   Use the AWS Directory Service console to configure one or more managed directories\. For more information, see [AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html) in the * AWS Directory Service Admin Guide*\.  
![\[Console screenshot of the Directory Service console showing a list of directories.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/directory-services-AD-list.png)

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/), and choose **Create server**\.

1. On the **Choose protocols** page, choose one or more protocols from the list\.
**Note**  
If you select **FTPS**, you must provide the AWS Certificate Manager certificate\. 

1. For **Choose an identity provider**, choose **AWS Directory Service**\.  
![\[Console screenshot showing Choose identity provider section with Directory Service selected.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-idp-directory-services.png)

1. The **Directory** list contains all the managed directories that you have configured\. Choose a directory from the list, and choose **Next**\.
**Note**  
 Cross\-Account and Shared directories are not supported for AWS Managed Microsoft AD\. 
To set up a server with Directory Service as your identity provider, you need to add some AWS Directory Service permissions\. For details, see [Before you start using AWS Directory Service for Microsoft Active Directory](#managed-ad-prereq)\.

1. To finish creating the server, use one of the following procedures:
   + [Create an SFTP\-enabled server](create-server-sftp.md)
   + [Create an FTPS\-enabled server](create-server-ftps.md)
   + [Create an FTP\-enabled server](create-server-ftp.md)

   In those procedures, continue with the step that follows choosing an identity provider\.

**Important**  
 You can't delete a Microsoft AD directory in AWS Directory Service if you used it in a Transfer Family server\. You must delete the server first, and then you can delete the directory\. 

### Granting access to groups<a name="directory-services-grant-access"></a>

 After you create the server, you must choose which groups in the directory should have access to upload and download files over the enabled protocols using AWS Transfer Family\. You do this by creating an *access*\.

**Note**  
Users must belong *directly* to the group to which you are granting access\. For example, assume that Bob is a user and he belongs to groupA, and groupA itself is included in groupB\.  
If you grant access to groupA, Bob is granted access\.
 If you grant access to groupB \(and not to groupA\), Bob does not have access\. 

**To grant access to a group**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. Navigate to your server details page\.

1.  In the **Accesses** section, choose **Add access**\. 

1.  Enter the SID for the AWS Managed Microsoft AD directory that you want to have access to this server\.
**Note**  
For information about how to find the SID for your group, see [Before you start using AWS Directory Service for Microsoft Active Directory](#managed-ad-prereq)\.

1. For **Access**, choose an AWS Identity and Access Management \(IAM\) role for the group\.

1.  In the **Policy** section, choose a policy\. The default setting is **None**\. 

1. For **Home directory**, choose an S3 bucket that corresponds to the group's home directory\.
**Note**  
You can limit the portions of the bucket that users see by creating a session policy\. For example, to limit users to their own folder under the `/filetest` directory, enter the following text in the box\.  

   ```
   /filetest/${transfer:UserName}
   ```
 To learn more about creating a session policy, see [Creating a session policy for an Amazon S3 bucket](users-policies.md#users-policies-session)\. 

1.  Choose **Add** to create the association\. 

1. Choose your server\.

1. Choose **Add access**\.

   1.  Enter the SID for the group\. 
**Note**  
For information about how to find the SID, see [Before you start using AWS Directory Service for Microsoft Active Directory](#managed-ad-prereq)\.

1. Choose **Add access**\.

 In the **Accesses** section, the accesses for the server are listed\. 

![\[Console screenshot showing the Accesses section with the server accesses listed.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/accesses-list.png)

### Testing users<a name="directory-services-test-user"></a>

You can test whether a user has access to the AWS Managed Microsoft AD directory for your server\.

**Note**  
A user must be in exactly one group \(an external ID\) that is listed in the **Access** section of the **Endpoint configuration** page\. If the user is in no groups, or is in more than a single group, that user is not granted access\.

**To test whether a specific user has access**

1. On the server details page, choose **Actions**, and then choose **Test**\.

1. For **Identity provider testing**, enter the user name and password for a user that is in one of the groups that has access\. 

1.  Choose **Test**\. 

You see a successful identity provider test, showing that the selected user has been granted access to the server\.

![\[Console screenshot of the successful identity provider testing response.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/identity-provider-test-success.png)

If the user belongs to more than one group that has access, you receive the following response\.

```
"Response":"",
"StatusCode":200,
"Message":"More than one associated access found for user's groups."
```

### Deleting server access for a group<a name="directory-services-misc"></a>

**To delete server access for a group**

1. On the server details page, choose **Actions**, and then choose **Delete Access**\.

1. In the dialog box, confirm that you want to remove access for this group\.

 When you return to the server details page, you see that the access for this group is no longer listed\. 

### Connecting to the server using SSH \(Secure Shell\)<a name="directory-services-ssh-procedure"></a>

After you configure your server and users, you can connect to the server using SSH and use the fully qualified user name for a user that has access\. 

```
sftp user@active-directory-domain@vpc-endpoint
```

For example: `transferuserexample@mycompany.com@vpce-0123456abcdef-789xyz.vpc-svc-987654zyxabc.us-east-1.vpce.amazonaws.com`\.

This format targets the search of the federation, limiting the search of a potentially large Active Directory\. 

**Note**  
You can specify the simple user name\. However, in this case, the Active Directory code has to search all the directories in the federation\. This might limit the search, and authentication might fail even if the user should have access\. 

After authenticating, the user is located in the home directory that you specified when you configured the user\.

### Connecting AWS Transfer Family to a self\-managed Active Directory using forests and trusts<a name="directory-services-ad-trust"></a>

Users in your self\-managed Active Directory \(AD\) can also use AWS IAM Identity Center \(successor to AWS Single Sign\-On\) for single sign\-on access to AWS accounts and Transfer Family servers\. To do that, AWS Directory Service has the following options available:
+ One\-way forest trust \(outgoing from AWS Managed Microsoft AD and incoming for on\-premises Active Directory\) works only for the root domain\.
+ For child domains, you can use either of the following:
  + Use two\-way trust between AWS Managed Microsoft AD and on\-premises Active Directory
  + Use one\-way external trust to each child domain\.

When connecting to the server using a trusted domain, the user needs to specify the trusted domain, for example `transferuserexample@mycompany.com`\.

## Using AWS Directory Service for Azure Active Directory Domain Services<a name="azure-sftp"></a>
+ To take advantage of your existing Active Directory forest for your SFTP Transfer needs, you can use [Active Directory Connector](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html)\.
+ If you want the benefits of Active Directory and high availability in a fully managed service, you can use AWS Directory Service for Microsoft Active Directory\. For details, see [Using the AWS Directory Service identity provider](#directory-services-users)\.

This topic describes how to use an Active Directory Connector and [Azure Active Directory Domain Services \(Azure ADDS\)](https://azure.microsoft.com/en-us/services/active-directory-ds/) to authenticate SFTP Transfer users with [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/)\.

**Topics**
+ [Before you start using AWS Directory Service for Azure Active Directory Domain Services](#azure-prereq)
+ [Step 1: Adding Azure Active Directory Domain Services](#azure-add-adds)
+ [Step 2: Creating a service account](#azure-create-service-acct)
+ [Step 3: Setting up AWS Directory using AD Connector](#azure-setup-directory)
+ [Step 4: Setting up AWS Transfer Family server](#azure-setup-transfer-server)
+ [Step 5: Granting access to groups](#azure-grant-access)
+ [Step 6: Testing users](#azure-test)

### Before you start using AWS Directory Service for Azure Active Directory Domain Services<a name="azure-prereq"></a>

For AWS, you need the following:
+ A virtual private cloud \(VPC\) in an AWS region where you are using your Transfer Family servers
+ At least two private subnets in your VPC
+ The VPC must have internet connectivity
+ A customer gateway and Virtual private gateway for site\-to\-site VPN connection with Microsoft Azure

For Microsoft Azure, you need the following:
+ An Azure Active Directory and Active directory domain service \(Azure ADDS\)
+ An Azure resource group
+ An Azure virtual network
+ VPN connectivity between your Amazon VPC and your Azure resource group
**Note**  
This can be through native IPSEC tunnels or using VPN appliances\. In this topic, we use IPSEC tunnels between an Azure Virtual network gateway and local network gateway\. The tunnels must be configured to allow traffic between your Azure ADDS endpoints and the subnets that house your AWS VPC\.
+ A customer gateway and Virtual private gateway for site\-to\-site VPN connection with Microsoft Azure

The following diagram shows the configuration needed before you begin\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-architecture.png)

### Step 1: Adding Azure Active Directory Domain Services<a name="azure-add-adds"></a>

 Azure AD does not support Domain joining instances by default\. To perform actions like Domain Join, and to use tools such as Group Policy, administrators must enable Azure Active Directory Domain Services\. If you have not already added Azure AD DS, or your existing implementation is not associated with the domain that you want your SFTP Transfer server to use, you must add a new instance\.

For information about enabling Azure Active Directory Domain Services \(Azure ADDS\), see [ Tutorial: Create and configure an Azure Active Directory Domain Services managed domain](https://docs.microsoft.com/en-us/azure/active-directory-domain-services/active-directory-ds-getting-started)\.

**Note**  
When you enable Azure ADDS, make sure it is configured for the resource group and the Azure AD domain to which you are connecting your SFTP Transfer server\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-ad-add-instance.png)

### Step 2: Creating a service account<a name="azure-create-service-acct"></a>

 Azure AD must have one service account that is part of an Admin group in Azure ADDS\. This account is used with the AWS Active Directory connector\. Make sure this account is in sync with Azure ADDS\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-service-acct.png)

### Step 3: Setting up AWS Directory using AD Connector<a name="azure-setup-directory"></a>

 After you have configured Azure ADDS, and created a service account with IPSEC VPN tunnels between your AWS VPC and Azure Virtual network, you can test the connectivity by pinging the Azure ADDS DNS IP address from any AWS EC2 instance\.

After you verify the connection is active, you can continue below\.

**To set up your AWS Directory using AD Connector**

1. Open the [Directory Service](https://console.aws.amazon.com/directoryservicev2/) console and select **Directories**\.

1. Select **Set up directory**\.

1. For directory type, choose **AD Connector**\.

1. Select a directory size, select **Next**, then select your VPC and Subnets\.

1. Select **Next**, then fill in the fields as follows:
   + **Directory DNS name**: enter the domain name you are using for your Azure ADDS\.
   + **DNS IP addresses**: enter you Azure ADDS IP addresses\.
   + **Server account username** and **password**: enter the details for the service account you created in *Step 2: Create a service account*\.

1. Complete the screens to create the directory service\.

Now the directory status should be **Active**, and it is ready to be used with an SFTP Transfer server\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-connector-ready.png)

### Step 4: Setting up AWS Transfer Family server<a name="azure-setup-transfer-server"></a>

Create an Transfer Family server with the SFTP protocol, and the identity provider type of **AWS Directory Service**\. From **Directory** drop down list, select the directory you added in *Step 3: Setup AWS Directory using AD Connector*\.

**Note**  
You can't delete a Microsoft AD directory in AWS Directory Service if you used it in a Transfer Family server\. You must delete the server first, and then you can delete the directory\. 

### Step 5: Granting access to groups<a name="azure-grant-access"></a>

 After you create the server, you must choose which groups in the directory should have access to upload and download files over the enabled protocols using AWS Transfer Family\. You do this by creating an *access*\.

**Note**  
Users must belong *directly* to the group to which you are granting access\. For example, assume that Bob is a user and he belongs to groupA, and groupA itself is included in groupB\.  
If you grant access to groupA, Bob is granted access\.
 If you grant access to groupB \(and not to groupA\), Bob does not have access\. 

 In order to grant access you need to retrieve the SID for the group\.

Use the following Windows PowerShell command to retrieve the SID for a group, replacing *YourGroupName* with the name of the group\. 

```
Get-ADGroup -Filter {samAccountName -like "YourGroupName*"} -Properties * | Select SamAccountName,ObjectSid
```

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-grant-access.png)

**Grant access to groups**

1. Open [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. Navigate to your server details page and in the **Accesses** section, choose **Add access**\. 

1. Enter the SID you received from the output of the previous procedure\.

1. For **Access**, choose an AWS Identity and Access Management role for the group\.

1. In the **Policy** section, choose a policy\. The default value is **None**\.

1. For **Home directory**, choose an S3 bucket that corresponds to the group's home directory\.

1. Choose **Add** to create the association\.

The details from your Transfer server should look similar to the following:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-assoc-1.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/azure-assoc-2.png)

### Step 6: Testing users<a name="azure-test"></a>

You can test \([Testing users](#directory-services-test-user)\) whether a user has access to the AWS Managed Microsoft AD directory for your server\. A user must be in exactly one group \(an external ID\) that is listed in the **Access** section of the **Endpoint configuration** page\. If the user is in no groups, or is in more than a single group, that user is not granted access\. 
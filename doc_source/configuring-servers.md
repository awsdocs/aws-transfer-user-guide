# Managing servers<a name="configuring-servers"></a>

In this section, you can find information on how to view a list of your servers, how to view your server details, how to edit your server details, and how to change the host key for your SFTP\-enabled server\.

**Topics**
+ [View a list of servers](#configuring-servers-view-server-list)
+ [Delete a server](#delete-server)
+ [View server details](configuring-servers-view-info.md)
+ [Edit server details](edit-server-config.md)
+ [Monitoring usage in the console](monitor-usage-transfer-console.md)

## View a list of servers<a name="configuring-servers-view-server-list"></a>

On the AWS Transfer Family console, you can find a list of all your servers that are located in the AWS Region that you chose\.

**To find a list of your servers that exist in an AWS Region**
+ Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

  If you have one or more servers in the current AWS Region, the console opens to show a list of your servers\. If you don't see a list of servers, make sure that you are in the correct Region\. You can also choose **Servers** from the navigation pane\.

  For more information about viewing your server details, see [View server details](configuring-servers-view-info.md)\.

## Delete a server<a name="delete-server"></a>

On the AWS Transfer Family console, you can delete your server\.

**Important**  
You are billed, for each of the protocols enabled to access your endpoint, until you delete the server\.

**Warning**  
Deleting a server results in all its users being deleted\. Data in the bucket that was accessed by using the server is not deleted, and remains accessible to AWS users that have privileges to those Amazon S3 buckets\.

**To delete a server**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the left navigation pane, choose **Servers**\.

1. Select the check box of the server that you want to delete\.

1. For **Actions**, choose **Delete**\.

1. In the confirmation dialog box that appears, enter the word **delete**, and then choose **Delete** to confirm that you want to delete the server\.

 The server is deleted from the **Servers** page and you are no longer billed for it\.
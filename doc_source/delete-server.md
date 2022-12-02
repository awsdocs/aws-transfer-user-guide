# Delete a server<a name="delete-server"></a>

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
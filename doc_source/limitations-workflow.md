# Managed workflows restrictions and limitations<a name="limitations-workflow"></a>

**Restrictions**

The following restrictions currently apply to post\-upload processing workflows for AWS Transfer Family\. 
+ Cross\-account and cross\-Region AWS Lambda functions are not supported\.
+ For a copy step, the source and destination Amazon S3 buckets must be in the same Region\. 
+ Only asynchronous custom steps are supported\.
+ Custom step timeouts are approximate\. That is, it might take slightly longer to time out than specified\. Additionally, the workflow is dependent upon the Lambda function\. Therefore, if the function is delayed during execution, the workflow is not aware of the delay\.
+ Copying across storage services and Regions is not supported\. You can, however, copy across accounts, provided that your AWS Identity and Access Management \(IAM\) policies are correctly configured\.
+ If you exceed your throttling limit, Transfer Family doesn't add workflow operations to the queue\.
+ Workflows are initiated upon successful file upload—end of STOR data stream for File Transfer Protocol \(FTP\), or CLOSE after write for Secure Shell \(SSH\) File Transfer Protocol \(SFTP\)—and not on partial upload \(for example an abrupt disconnect without closing\)\.
+ Workflows are not initiated for files that have a size of 0\. Files with a size greater than 0 do initiate the associated workflow\.

**Limitations**

 Additionally, the following functional limits apply to workflows for Transfer Family: 
+ The number of workflows per Region, per account, is limited to 10\.
+ The maximum timeout for custom steps is 30 minutes\.
+ The maximum number of steps in a workflow is 8\.
+ The maximum number of tags per workflow is 50\.
+ The new executions refill rate per workflow is one per second\.
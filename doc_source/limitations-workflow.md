# Managed workflows restrictions and limitations<a name="limitations-workflow"></a>

**Restrictions**

The following restrictions currently apply to post\-upload processing workflows for AWS Transfer Family\. 
+ Cross\-account and cross\-Region AWS Lambda functions are not supported\. You can, however, copy across accounts, provided that your AWS Identity and Access Management \(IAM\) policies are correctly configured\.
+ For a copy step, the source and destination Amazon S3 buckets must be in the same Region\. 
+ Similarly, for a decryption step, the decryption destination must match the source for Region and backing store \(for example, if the file to be decrypted is stored in Amazon S3, then the specified destination must also be in Amazon S3\)\.
+ Only asynchronous custom steps are supported\.
+ Custom step timeouts are approximate\. That is, it might take slightly longer to time out than specified\. Additionally, the workflow is dependent upon the Lambda function\. Therefore, if the function is delayed during execution, the workflow is not aware of the delay\.
+ If you exceed your throttling limit, Transfer Family doesn't add workflow operations to the queue\.
+ Workflows are not initiated for files that have a size of 0\. Files with a size greater than 0 do initiate the associated workflow\.

**Limitations**

 Additionally, the following functional limits apply to workflows for Transfer Family: 
+ The number of workflows per Region, per account, is limited to 10\.
+ The maximum timeout for custom steps is 30 minutes\.
+ The maximum number of steps in a workflow is 8\.
+ The maximum number of tags per workflow is 50\.
+ The maximum number of concurrent executions that contain a decrypt step is 250 per workflow\.
+ You can store a maximum of 3 PGP private keys, per Transfer Family server, per user\.
+ The maximum size for a decrypted file is 10 GB\.
+ We throttle the new execution rate using a [token bucket](https://en.wikipedia.org/wiki/Token_bucket) system with a burst capacity of 100 and a refill rate of 1\.
+ Anytime you remove a workflow from a server and replace it with a new one, or update server configuration \(which impacts a workflow's execution role\), you must wait approximately 10 minutes before executing the new workflow\. The Transfer Family server caches the workflow details, and it takes 10 minutes for the server to refresh its cache\.
# AWS Transfer Family managed workflows<a name="transfer-workflows"></a>

 AWS Transfer Family supports managed workflows for file processing\. With managed workflows, you can kick off a workflow after a file has been transferred over SFTP, FTPS, or FTP\. Using this feature, you can securely and cost effectively meet your compliance requirements for business\-to\-business \(B2B\) file exchanges by coordinating all the necessary steps required for file processing\. In addition, you benefit from end\-to\-end auditing and visibility\. 

![\[Flow diagram showing how managed workflows assist with file processing.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflows-diagram.png)

 

By orchestrating file\-processing tasks, managed workflows help you preprocess data before it is consumed by your downstream applications\. Such file\-processing tasks might include:
+ Moving files to user\-specific folders\.
+ Decrypting files as part of a workflow\.
+ Tagging files\.
+ Performing custom processing by creating and attaching an AWS Lambda function to a workflow\.
+ Sending notifications when a file has been successfully transferred\. \(For a blog post that details this use case, see [ Customize file delivery notifications using AWS Transfer Family managed workflows](http://aws.amazon.com/blogs/storage/customize-file-delivery-notifications-using-aws-transfer-family-managed-workflows/)\.\)

To quickly replicate and standardize common post\-upload file processing tasks spanning multiple business units in your organization, you can deploy workflows by using infrastructure as code \(IaC\)\. You can specify a managed workflow to be initiated on files that are uploaded in full\. You can also specify a different managed workflow to be initiated on files that are only partially uploaded because of a premature session disconnect\. Built\-in exception handling helps you quickly react to file\-processing outcomes, while offering you control over how to handle failures\. In addition, each workflow step produces detailed logs, which you can audit to trace the data lineage\.

To get started, perform the following tasks:

1. Set up your workflow to contain preprocessing actions, such as copying, tagging, and other steps based on your requirements\. See [Create a workflow](create-workflow.md) for details\.

1. Configure an execution role, which Transfer Family uses to run the workflow\. See [IAM policies for workflows](workflow-execution-role.md) for details\.

1. Map the workflow to a server, so that on file arrival, the actions specified in this workflow are evaluated and initiated in real time\. See [ Configure and run a workflow](create-workflow.md#configure-workflow) for details\.

To monitor your workflow executions, see [Using CloudWatch metrics for Transfer Family](monitoring.md#metrics)\. For detailed execution logs and troubleshooting information, see [Troubleshoot workflow\-related errors using Amazon CloudWatch](troubleshooting.md#workflows-cloudwatch-errors)\.

**Topics**
+ [Create a workflow](create-workflow.md)
+ [Use predefined steps](nominal-steps-workflow.md)
+ [Use custom file\-processing steps](custom-step-details.md)
+ [IAM policies for workflows](workflow-execution-role.md)
+ [Exception handling for a workflow](exception-workflow.md)
+ [Monitor workflow execution](cloudwatch-workflow.md)
+ [Create a workflow from a template](workflow-template.md)
+ [Managed workflows restrictions and limitations](limitations-workflow.md)
+ [Tutorial: Setting up a managed workflow for decrypting a file](workflow-decrypt-tutorial.md)

For more help getting started with managed workflows, see the following resources: 
+ [AWS Transfer Family Managed Workflows Demo video](https://www.youtube.com/watch?v=t-iNqCRospw)
+ [Building a Cloud\-Native File Transfer Platform Using AWS Transfer Family Workflows blog post](http://aws.amazon.com/blogs/architecture/building-a-cloud-native-file-transfer-platform-using-aws-transfer-family-workflows/)
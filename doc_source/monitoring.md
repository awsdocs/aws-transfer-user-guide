# Monitoring server usage<a name="monitoring"></a>

You can monitor activity in your server using Amazon CloudWatch and AWS CloudTrail\. For further analysis, you can also record server activity as readable, near real\-time metrics\.

**Topics**
+ [Enable AWS CloudTrail logging](#monitoring-enable-cloudtrail)
+ [Creating Amazon CloudWatch alarms](#monitoring-cloudwatch-examples)
+ [Logging Amazon S3 API calls to S3 access logs](#monitoring-s3-access-logs)
+ [Log activity with CloudWatch](#monitoring-enabling)
+ [Examples to limit confused deputy problem](#cloudwatch-confused-deputy)
+ [Using CloudWatch metrics for Transfer Family](#metrics)

## Enable AWS CloudTrail logging<a name="monitoring-enable-cloudtrail"></a>

You can monitor AWS Transfer Family API calls using AWS CloudTrail\. By monitoring API calls, you can get useful security and operational information\. For more information about how to work with CloudTrail and AWS Transfer Family, see [Logging and monitoring in AWS Transfer Family](logging-using-cloudtrail.md)\.

If you have [Amazon S3 object level logging enabled](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/enable-cloudtrail-events.html), `RoleSessionName` is contained in the Requester field as `[AWS:Role Unique Identifier]/username.sessionid@server-id`\. For more information about AWS Identity and Access Management \(IAM\) role unique identifiers, see [Unique identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-unique-ids) in the *AWS Identity and Access Management User Guide*\.

**Important**  
The maximum length of the `RoleSessionName` is 64 characters\. If the `RoleSessionName` is longer, the `server-id` gets truncated\.

## Creating Amazon CloudWatch alarms<a name="monitoring-cloudwatch-examples"></a>

The following example shows how to create Amazon CloudWatch alarms using the AWS Transfer Family metric, `FilesIn`\.

------
#### [ CDK ]

```
new cloudwatch.Metric({
  namespace: "AWS/Transfer",
  metricName: "FilesIn",
  dimensionsMap: { ServerId: "s-00000000000000000" },
  statistic: "Average",
  period: cdk.Duration.minutes(1),
}).createAlarm(this, "AWS/Transfer FilesIn", {
  threshold: 1000,
  evaluationPeriods: 10,
  datapointsToAlarm: 5,
  comparisonOperator: cloudwatch.ComparisonOperator.GREATER_THAN_OR_EQUAL_TO_THRESHOLD,
});
```

------
#### [ AWS CloudFormation ]

```
Type: AWS::CloudWatch::Alarm
Properties:
  Namespace: AWS/Transfer
  MetricName: FilesIn
  Dimensions:
    - Name: ServerId
      Value: s-00000000000000000
  Statistic: Average
  Period: 60
  Threshold: 1000
  EvaluationPeriods: 10
  DatapointsToAlarm: 5
  ComparisonOperator: GreaterThanOrEqualToThreshold
```

------

## Logging Amazon S3 API calls to S3 access logs<a name="monitoring-s3-access-logs"></a>

If you are [using Amazon S3 access logs to identify S3 requests](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-s3-access-logs-to-identify-requests.html) made on behalf of your file transfer users, `RoleSessionName` is used to display which IAM role was assumed to service the file transfers\. It also displays additional information such as the user name, session id, and server\-id used for the transfers\. The format is `[AWS:Role Unique Identifier]/username.sessionid@server-id` and is contained in the Requester field\. For example, the following are the contents for a sample Requester field from an S3 access log for a file that was copied to the S3 bucket\.

`arn:aws:sts::AWS-Account-ID:assumed-role/IamRoleName/username.sessionid@server-id`

In the Requester field above, it shows the IAM Role called `IamRoleName`\. For more information about IAM role unique identifiers, see [Unique identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-unique-ids) in the *AWS Identity and Access Management User Guide*\.

## Log activity with CloudWatch<a name="monitoring-enabling"></a>

To set access, you create a resource\-based IAM policy and an IAM role that provides that access information\.

To enable Amazon CloudWatch logging, you start by creating an IAM policy that enables CloudWatch logging\. You then create an IAM role and attach the policy to it\. You can do this when you are [creating a server](getting-started.md#getting-started-server) or by [editing an existing server](edit-server-config.md)\. For more information about CloudWatch, see [What Is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) and [What is Amazon CloudWatch Logs?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html) in the *Amazon CloudWatch User Guide*\.

**To create an IAM policy**
+ Use the following example policy to create your own IAM policy that allows CloudWatch logging\. For information about how to create a policy for AWS Transfer Family, see [Create an IAM role and policy](requirements-roles.md)\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "VisualEditor0",
              "Effect": "Allow",
              "Action": [
                  "logs:CreateLogStream",
                  "logs:DescribeLogStreams",
                  "logs:CreateLogGroup",
                  "logs:PutLogEvents"
              ],
              "Resource": "arn:aws:logs:*:*:log-group:/aws/transfer/*"
          }
      ]
  }
  ```

You then create a role and attach the CloudWatch Logs policy that you created\.

**To create an IAM role and attach a policy**

1. In the navigation pane, choose **Roles**, and then choose **Create role**\.

   On the **Create role** page, make sure that **AWS service** is chosen\.

1. Choose **Transfer** from the service list, and then choose **Next: Permissions**\. This establishes a trust relationship between AWS Transfer Family and the IAM role\. Additionally, add `aws:SourceAccount` and `aws:SourceArn` condition keys to protect yourself against the *confused deputy* problem\. See the following documentation for more details:
   + Procedure for establishing a trust relationship with AWS Transfer Family: [To establish a trust relationship](requirements-roles.md#establish-trust-transfer) 
   + Description for confused deputy problem: [the confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)

1. In the **Attach permissions policies** section, locate and choose the CloudWatch Logs policy that you just created, and choose **Next: Tags**\.

1. \(Optional\) Enter a key and value for a tag, and choose **Next: Review**\.

1. On the **Review** page, enter a name and description for your new role, and then choose **Create role**\.

1. To view the logs, choose the **Server ID** to open the server configuration page, and choose **View logs**\. You are redirected to the CloudWatch console where you can see your log streams\.

On the CloudWatch page for your server, you can see records of user authentication \(success and failure\), data uploads \(`PUT` operations\), and data downloads \(`GET` operations\)\.

## Examples to limit confused deputy problem<a name="cloudwatch-confused-deputy"></a>

The confused deputy problem is a security issue where an entity that doesn't have permission to perform an action can coerce a more\-privileged entity to perform the action\. In AWS, cross\-service impersonation can result in the confused deputy problem\. For more details, see [Cross\-service confused deputy prevention](confused-deputy.md)\.

**Note**  
In the following examples, replace each *user input placeholder* with your own information\.

The following example logging/invocation policy allows any server in the account to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAllServers",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:server/*"
                }
            }
        }
    ]
}
```

The following example logging/invocation policy allows a specific server to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowSpecificServer",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnEquals": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:/server/server-id"
                }
            }
        }
    ]
}
```

## Using CloudWatch metrics for Transfer Family<a name="metrics"></a>

**Note**  
 You can also get metrics for Transfer Family from within the Transfer Family console itself\. For details, see [ Monitoring server usage in the console ](monitor-usage-transfer-console.md) 

You can get information about your server using CloudWatch metrics\. A *metric* represents a time\-ordered set of data points that are published to CloudWatch\. When using metrics, you must specify the Transfer Family namespace, metric name, and [dimension](#cw-dimensions)\. For more information about metrics, see [Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric) in the *Amazon CloudWatch User Guide*\.

 The following table describes the CloudWatch metrics for Transfer Family\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transfer/latest/userguide/monitoring.html)

### Transfer Family dimensions<a name="cw-dimensions"></a>

A *dimension* is a name/value pair that is part of the identity of a metric\. For more information about dimensions, see [Dimensions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Dimension) in the *Amazon CloudWatch User Guide*\.

The following table describes the CloudWatch dimension for Transfer Family\.


| Dimension | Description | 
| --- | --- | 
| `ServerId` | The unique ID of the server\. | 
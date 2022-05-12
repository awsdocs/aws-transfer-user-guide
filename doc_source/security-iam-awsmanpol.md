# AWS managed policies for AWS Transfer Family<a name="security-iam-awsmanpol"></a>



To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create AWS Identity and Access Management \(IAM\) customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions that they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the `ReadOnlyAccess` AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSTransferLoggingAccess<a name="security-iam-awsmanpol-transferloggingaccess"></a>

 The `AWSTransferLoggingAccess` policy grants AWS Transfer Family full access to create log streams and groups and put log events to your account\. 

**Permissions details**

This policy includes the following permissions for Amazon CloudWatch Logs\.
+ `CreateLogStream` – Grants permissions for principals to create a log stream\.
+ `DescribeLogStreams` – Grants permissions for principals to list the log streams for the log group\.
+ `CreateLogGroup` – Grants permissions for principals to create log groups\.
+ `PutLogEvents` – Grants permissions for principals to upload a batch of log events to a log stream\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:DescribeLogStreams",
                "logs:CreateLogGroup",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSTransferConsoleFullAccess<a name="security-iam-awsmanpol-transferconsolefullaccess"></a>

The `AWSTransferConsoleFullAccess` policy provides full access to Transfer Family through the AWS Management Console\.

**Permissions details**

This policy includes the following permissions\.
+ `acm:ListCertificates` – Grants permission to retrieve a list of the certificate Amazon Resource Names \(ARNs\) and the domain name for each ARN\.
+ `ec2:DescribeAddresses` – Grants permission to describe one or more Elastic IP addresses\.
+ `ec2:DescribeAvailabilityZones` – Grants permission to describe one or more of the Availability Zones that are available to you\.
+ `ec2:DescribeNetworkInterfaces` – Grants permission to describe one or more elastic network interfaces\.
+ `ec2:DescribeSecurityGroups` – Grants permission to describe one or more security groups\.
+ `ec2:DescribeSubnets` – Grants permission to describe one or more subnets\.
+ `ec2:DescribeVpcs` – Grants permission to describe one or more virtual private clouds \(VPCs\)\.
+ `ec2:DescribeVpcEndpoints` – Grants permission to describe one or more VPC endpoints\.
+ `health:DescribeEventAggregates` – Returns the number of events of each event type \(issue, scheduled change, and account notification\)\.
+ `iam:GetPolicyVersion` – Grants permission to retrieve information about a version of the specified managed policy, including the policy document\.
+ `iam:ListPolicies` – Grants permission to list all managed policies\.
+ `iam:ListRoles` – Grants permission to list the IAM roles that have the specified path prefix\.
+ `iam:PassRole` – Grants permission to pass an IAM role to Transfer Family\. For more details, see [Granting a user permissions to pass a role to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html)\.
+ `route53:ListHostedZones` – Grants permission to get a list of the public and private hosted zones that are associated with the current AWS account\.
+ `s3:ListAllMyBuckets` – Grants permission to list all buckets owned by the authenticated sender of the request\.
+ `transfer:*` – Grants access to Transfer Family resources\. The asterisk \(`*`\) grants access to all resources\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "transfer.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "acm:ListCertificates",
                "ec2:DescribeAddresses",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeSubnets",
                "ec2:DescribeVpcs",
                "ec2:DescribeVpcEndpoints",
                "health:DescribeEventAggregates",
                "iam:GetPolicyVersion",
                "iam:ListPolicies",
                "iam:ListRoles",
                "route53:ListHostedZones",
                "s3:ListAllMyBuckets",
                "transfer:*"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSTransferFullAccess<a name="security-iam-awsmanpol-transferfullaccess"></a>

 The `AWSTransferFullAccess` policy provides full access to Transfer Family services\. 

**Permissions details**

This policy includes the following permissions\.
+ `transfer:*` – Grants permission to access Transfer Family resources\. The asterisk \(`*`\) grants access to all resources\.
+ `iam:PassRole` – Grants permission to pass an IAM role to Transfer Family\. For more details, see [Granting a user permissions to pass a role to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html)\.
+ `ec2:DescribeAddresses` – Grants permission to describe one or more Elastic IP addresses\.
+ `ec2:DescribeNetworkInterfaces` – Grants permission to describe one or more network interfaces\.
+ `ec2:DescribeVpcEndpoints` – Grants permission to describe one or more VPC endpoints\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "transfer:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "transfer.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeVpcEndpoints",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeAddresses"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSTransferReadOnlyAccess<a name="security-iam-awsmanpol-transferreadonlyaccess"></a>

 The `AWSTransferReadOnlyAccess` policy provides read\-only access to Transfer Family services\. 

**Permissions details**

This policy includes the following permissions for Transfer Family\.
+ `DescribeUser` – Grants permissions for principals to view the descriptions for users\.
+ `DescribeServer` – Grants permissions for principals to view the descriptions for servers\.
+ `ListUsers` – Grants permissions for principals to list users for a server\.
+ `ListServers` – Grants permissions for principals to list the servers for the account\.
+ `TestIdentityProvider` – Grants permissions for principals to test whether the configured identity provider is set up correctly\.
+ `ListTagsForResource` – Grants permissions for principals to list the tags for a resource\.



```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "transfer:DescribeUser",
                "transfer:DescribeServer",
                "transfer:ListUsers",
                "transfer:ListServers",
                "transfer:TestIdentityProvider",
                "transfer:ListTagsForResource"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS Transfer Family updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

View details about updates to AWS managed policies for AWS Transfer Family since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the [Document history for AWS Transfer Family](doc-history.md) page\.




| Change | Description | Date | 
| --- | --- | --- | 
|   Documentation update   |  Added sections for each of the Transfer Family managed policies\.  |  January 27, 2022  | 
|   [AWSTransferReadOnlyAccess](#security-iam-awsmanpol-transferreadonlyaccess) – Update to an existing policy   |  AWS Transfer Family added new permissions to allow the policy to read AWS Managed Microsoft AD\.  |  September 30, 2021  | 
|  AWS Transfer Family started tracking changes  |  AWS Transfer Family started tracking changes for its AWS managed policies\.  | June 15, 2021 | 
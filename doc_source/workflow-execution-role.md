# IAM policies for workflows<a name="workflow-execution-role"></a>

When you add a workflow to a server, you must select an execution role\. The server uses this role when it executes the workflow\. If the role does not have the proper permissions, AWS Transfer Family cannot run the workflow\. 

This section describes one possible set of AWS Identity and Access Management \(IAM\) permissions that you can use to execute a workflow\. Other examples are described later in this topic\. 

**To create an execution role for your workflow**

1. Create a new IAM role, and add the AWS managed policy `AWSTransferFullAccess` to the role\. For more information about creating a new IAM role, see [Create an IAM role and policy](requirements-roles.md)\.

1. Create another policy with the following permissions, and attach it to your role\. Replace each `user input placeholder` with your own information\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "ConsoleAccess",
               "Effect": "Allow",
               "Action": "s3:GetBucketLocation",
               "Resource": "*"
           },
           {
               "Sid": "ListObjectsInBucket",
               "Effect": "Allow",
               "Action": "s3:ListBucket",
               "Resource": [
                   "arn:aws:s3:::DOC-EXAMPLE-BUCKET"
               ]
           },
           {
               "Sid": "AllObjectActions",
               "Effect": "Allow",
               "Action": "s3:*Object",
               "Resource": [
                   "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
               ]
           },
           {
               "Sid": "GetObjectVersion",
               "Effect": "Allow",
               "Action": "s3:GetObjectVersion",
               "Resource": [
                   "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
               ]
           },
           {
               "Sid": "Custom",
               "Effect": "Allow",
               "Action": [
                   "lambda:InvokeFunction"
               ],
               "Resource": [
                   "arn:aws:lambda:region:account-id:function:${FunctionName}"
               ]
           },
           {
               "Sid": "Tag",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObjectTagging",
                   "s3:PutObjectVersionTagging"
               ],
               "Resource": [
                   "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
               ]
           }
       ]
   }
   ```

1. Save this role and specify it as the execution role when you add a workflow to a server\.
**Note**  
When you're constructing IAM roles, AWS recommends that you restrict access to your resources as much as is possible for your workflow\.

## Workflow trust relationships<a name="workflows-trust"></a>

Workflow execution roles also require a trust relationship with `transfer.amazonaws.com`\. To establish a trust relationship for AWS Transfer Family, see [To establish a trust relationship](requirements-roles.md#establish-trust-transfer)\.

While you're establishing your trust relationship, you can also take steps to avoid the *confused deputy* problem\. For a description of this problem, as well as examples of how to avoid it, see [Cross\-service confused deputy prevention](confused-deputy.md)\.

## Example execution role: Copy and tag<a name="example-workflow-role-copy-tag"></a>

If you have a workflow that copies an object to a different Amazon S3 location and tags the copied object, use the following IAM policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CopyRead",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectTagging"
            ],
            "Resource": "arn:aws:s3:::${SourceBucketName}/${ObjectName}"
        },
        {
            "Sid": "CopyWrite",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectTagging"
            ],
            "Resource": "arn:aws:s3:::${DestinationBucketName}/${ObjectName}"
        },
        {
            "Sid": "CopyList",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": [
                "arn:aws:s3:::${SourceBucketName}",
                "arn:aws:s3:::${DestinationBucketName}"
            ]
        },
        {
            "Sid": "Tag",
            "Effect": "Allow",
            "Action": [
                "s3:PutObjectTagging",
                "s3:PutObjectVersionTagging"
            ],
            "Resource": "arn:aws:s3:::${DestinationBucketName}/${ObjectName}",
            "Condition": {
                "StringEquals": {
                    "s3:RequestObjectTag/Archive": "yes"
                }
            }
        }
    ]
}
```

## Example execution role: Run function and delete<a name="example-workflow-role-custom-delete"></a>

In this example, you have a workflow that invokes an AWS Lambda function\. If the workflow deletes the uploaded file and has an exception handler step to act upon a failed workflow execution in the previous step, use the following IAM policy\. Replace each `user input placeholder` with your own information\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Delete",
            "Effect": "Allow",
            "Action": [
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::${BucketName}/${ObjectName}"
        },
        {
            "Sid": "Custom",
            "Effect": "Allow",
            "Action": [
                "lambda:InvokeFunction"
            ],
            "Resource": [
                "arn:aws:lambda:region:account-id:function:${FunctionName}"
            ]
        }
    ]
}
```
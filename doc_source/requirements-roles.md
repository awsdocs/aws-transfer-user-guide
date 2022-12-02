# Create an IAM role and policy<a name="requirements-roles"></a>

When you create a user, you make a number of decisions about user access\. These decisions include which Amazon S3 buckets or Amazon EFS file systems that the user can access, what portions of each Amazon S3 bucket and which files in the file system are accessible, and what permissions the user has \(for example, `PUT` or `GET`\)\.

To set access, you create an identity\-based AWS Identity and Access Management \(IAM\) policy and role that provide that access information\. As part of this process, you provide access for your user to the Amazon S3 bucket or Amazon EFS file system that is the target or source for file operations\. To do this, take the following high\-level steps, described in detail later:

1. Create an IAM policy for AWS Transfer Family\. This is described in [To create an IAM role for AWS Transfer Family](#iam-role-procedure)\.

1. Create an IAM role and attach the new IAM policy\. See the following example policies:
   + [Example read/write access policy](read-write-access.md)
   + [Example session policy](session-policy.md)

   For information about session policies, see [Session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session) in the *IAM User Guide*\.

1. Establish a trust relationship between AWS Transfer Family and the IAM role\. This is described in [To establish a trust relationship](#establish-trust-transfer)\.

The following procedures describe how to create an IAM policy and role\. 

**To create an IAM policy for AWS Transfer Family**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**, and then choose **Create policy**\.

1. On the **Create Policy** page, choose the **JSON** tab\.

1. In the editor that appears, replace the contents of the editor with the IAM policy that you want attach to the IAM role\.

   You can grant read/write access or restrict users to their home directory\. For more information, see the following examples:
   + [Example read/write access policy](read-write-access.md)
   + [Example session policy](session-policy.md)

1. Choose **Review policy** and provide a name and description for your policy, and then choose **Create policy**\.

Next, you create an IAM role and attach the new IAM policy to it\.<a name="iam-role-procedure"></a>

**To create an IAM role for AWS Transfer Family**

1. In the navigation pane, choose **Roles**, and then choose **Create role**\.

   On the **Create role** page, make sure that **AWS service** is chosen\.

1. Choose **Transfer** from the service list, and then choose **Next: Permissions**\. This establishes a trust relationship between AWS Transfer Family and AWS\.

1. In the **Attach permissions policies** section, locate and choose the policy that you just created, and choose **Next: Tags**\.

1. \(Optional\) Enter a key and value for a tag, and choose **Next: Review**\.

1. On the **Review** page, enter a name and description for your new role, and then choose **Create role**\.

Next, you establish a trust relationship between AWS Transfer Family and AWS\.<a name="establish-trust-transfer"></a>

**To establish a trust relationship**
**Note**  
In our examples, we use both `ArnLike` and `ArnEquals`\. They are functionally identical, and therefore you may use either when you construct your policies\. Transfer Family documentation uses `ArnLike` when the condition contains a wildcard character, and `ArnEquals` to indicate an exact match condition\.

1. In the IAM console, choose the role that you just created\.

1. On the **Summary** page, choose **Trust relationships**, and then choose **Edit trust relationship**\.

1. In the **Edit Trust Relationship** editor, make sure **service** is `"transfer.amazonaws.com"`\. The access policy is shown following\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "transfer.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

   We recommend that you use the `aws:SourceAccount` and `aws:SourceArn` condition keys to protect yourself against the confused deputy problem\. The source account is the owner of the server and the source ARN is the ARN of the user\. For example:

   ```
   "Condition": {
       "StringEquals": {
           "aws:SourceAccount": "account_id"
       },
       "ArnLike": {
           "aws:SourceArn": "arn:aws:transfer:region:account_id:user/*"
       }
   }
   ```

   You can also use the `ArnLike` condition if you are looking to restrict to a particular server instead of any server in the user account\. For example: 

   ```
   "Condition": {    
       "ArnLike": {
           "aws:SourceArn": "arn:aws:transfer:region:account-id:user/server-id/*"
       }
   }
   ```
**Note**  
In the examples above, replace each *user input placeholder* with your own information\.

   For details on the confused deputy problem and more examples, see [Cross\-service confused deputy prevention](confused-deputy.md)\.

1. Choose **Update Trust Policy** to update the access policy\.

You have now created an IAM role that allows AWS Transfer Family to call AWS services on your behalf\. You attached to the role the IAM policy that you created to give access to your user\. In the [Tutorial: Getting started with AWS Transfer Family](getting-started.md) section, this role and policy are assigned to your user or users\.

Optionally, you can create a session policy that limits users' access to their home directories only, as described earlier in this topic\. For more information about session policies, see [Example session policy](session-policy.md)\.

For more general information about IAM roles, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\.

To learn more about identity\-based policies for Amazon S3 resources, see [Identity and access management in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-access-control.html) in the *Amazon Simple Storage Service User Guide*\.
# Managing access controls<a name="users-policies"></a>

**Note**  
This section applies only to the service\-managed identity provider\. If you are using a custom identity provider, see [Working with custom identity providers](custom-identity-provider-users.md)\.

**Topics**
+ [Allowing read and write access to an Amazon S3 bucket](#users-policies-all-access)
+ [Creating a session policy for an Amazon S3 bucket](#users-policies-session)
+ [Preventing users from running `mkdir` in an S3 bucket](#prevent-mkdir)

You can control a user's access to AWS Transfer Family resources by using an AWS Identity and Access Management \(IAM\) policy\. An IAM policy is a statement, typically in JSON format, that allows a certain level of access to a resource\. You use an IAM policy to define what file operations that you want to allow your users to perform and not perform\. You can also use an IAM policy to define what Amazon S3 bucket or buckets that you want to give your users access to\. To specify these policies for users, you create an IAM role for AWS Transfer Family that has the IAM policy and trust relationship associated with it\.

Each user is assigned an IAM role\. When a user logs in to your server, AWS Transfer Family assumes the IAM role mapped to the user\. To learn about creating an IAM role that provides a user access to an Amazon S3 bucket, see following\. For information about how to create a role and delegate permissions, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\.

The type of IAM role that AWS Transfer Family uses is called a service role\.

**Note**  
 If your Amazon S3 bucket is encrypted using AWS Key Management Service \(AWS KMS\), you must specify additional permissions in your policy\. For details, see [Data encryption](encryption-at-rest.md)\. Additionally, you can see more information about [session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session.html) in the *IAM User Guide*\. 

## Allowing read and write access to an Amazon S3 bucket<a name="users-policies-all-access"></a>

Following, you can see how to create an IAM policy that allows read and write access to a specific Amazon S3 bucket\. Assigning an IAM role that has this IAM policy to your user gives that user read/write access to the specified Amazon S3 bucket\.

The following policy provides programmatic read and write access to an Amazon S3 bucket\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid":"ReadWriteS3",
      "Action": [
            "s3:ListBucket"
                ],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::bucketname"]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject",              
        "s3:DeleteObjectVersion",
        "s3:GetObjectVersion",
        "s3:GetObjectACL",
        "s3:PutObjectACL"
      ],
      "Resource": ["arn:aws:s3:::bucketname/*"]
    }
  ]
}
```

The `ListBucket` action requires permission to the bucket itself\. The `PUT`, `GET`, and `DELETE` actions require object permissions\. Because these are different entities, they are specified using different Amazon Resource Names \(ARNs\)\.

If your bucket is enabled for AWS Key Management Service \(AWS KMS\) encryption, you need to enable additional actions in the policy\. For more information about AWS KMS, see [What is AWS Key Management Service?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) 

To further restrict your users' access to only the `home` directory of the specified Amazon S3 bucket, see [Creating a session policy for an Amazon S3 bucket](#users-policies-session)\.

## Creating a session policy for an Amazon S3 bucket<a name="users-policies-session"></a>

A *session policy* is an AWS Identity and Access Management \(IAM\) policy that restricts users to certain portions of an Amazon S3 bucket\. It does so by evaluating access in real time\.

**Note**  
 Session policies are only used with Amazon S3\. For Amazon EFS, you use POSIX file permissions to limit access\. 

You can use a session policy when you need to give the same access to a group of users to a particular portion of your Amazon S3 bucket\. For example, a group of users might need access to only the `home` directory\. That group of users share the same IAM role\.

**Note**  
 The maximum length of a session policy is 2048 characters\. For more details, see the [Policy request parameter](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#API_CreateUser_RequestSyntax) for the `CreateUser` action in the *API reference*\. 

To create a session policy, use the following policy variables in your IAM policy:
+ `${transfer:HomeBucket}`
+ `${transfer:HomeDirectory}`
+ `${transfer:HomeFolder}`
+ `${transfer:UserName}`

**Important**  
You can't use the variables listed preceding in Managed Policies\. Nor can you use them as policy variables in an IAM role definition\. You create these variables in an IAM policy and supply them directly when setting up your user\. Also, you can't use the `${aws:Username}` variable in this session policy\. This variable refers to an IAM user name and not the user name required by AWS Transfer Family\.

An example of a session policy is shown in the code example following\.

```
{
  "Version": "2012-10-17",
  "Statement": [
      {
          "Sid": "AllowListingOfUserFolder",
          "Action": [
              "s3:ListBucket"
          ],
          "Effect": "Allow",
          "Resource": [
              "arn:aws:s3:::${transfer:HomeBucket}"
          ],
          "Condition": {
              "StringLike": {
                  "s3:prefix": [
                      "${transfer:HomeFolder}/*",
                      "${transfer:HomeFolder}"
                  ]
              }
          }
      },
      {
          "Sid": "HomeDirObjectAccess",
          "Effect": "Allow",
          "Action": [
              "s3:PutObject",
              "s3:GetObject",
              "s3:DeleteObjectVersion",
              "s3:DeleteObject",
              "s3:GetObjectVersion",
              "s3:GetObjectACL",
              "s3:PutObjectACL"
          ],
          "Resource": "arn:aws:s3:::${transfer:HomeDirectory}*"
       }
  ]
}
```

**Note**  
In the policy above, it is assumed that users have their home directories set to include a trailing slash, to signify that it is a directory\. If, on the other hand, you set a user's `HomeDirectory` without the trailing slash, then you should include it as part of your policy\.

In the previous example policy, note the use of the `transfer:HomeFolder`, `transfer:HomeBucket`, and `transfer:HomeDirectory` policy parameters\. These parameters are set for the `HomeDirectory` that is configured for the user, as described in [HomeDirectory](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#TransferFamily-CreateUser-request-HomeDirectory) and [Implementing your API Gateway method](custom-identity-provider-users.md#authentication-api-method)\. These parameters have the following definitions:
+ The `transfer:HomeBucket` parameter is replaced with the first component of `HomeDirectory`\.
+ The `transfer:HomeFolder` parameter is replaced with the remaining portions of the `HomeDirectory` parameter\.
+ The `transfer:HomeDirectory` parameter has the leading forward slash \(`/`\) removed so that it can be used as part of an S3 Amazon Resource Name \(ARN\) in a `Resource` statement\.

**Note**  
 If you are using Logical directories—that is, the user's `homeDirectoryType` is `LOGICAL`—these policy parameters \(`HomeBucket`, `HomeDirectory`, and `HomeFolder`\) are not supported\. 

For example, assume that the `HomeDirectory` parameter that is configured for the Transfer Family user is `/home/bob/amazon/stuff/`\.
+ `transfer:HomeBucket` is set to `/home`\.
+ `transfer:HomeFolder` is set to `/bob/amazon/stuff/`\.
+ `transfer:HomeDirectory` becomes `home/bob/amazon/stuff/`\.

The first `"Sid"` allows the user to list all directories starting from `/home/bob/amazon/stuff/`\.

The second `"Sid"` limits the user'`put` and `get` access to that same path, `/home/bob/amazon/stuff/`\.

With the preceding policy in place, when a user logs in, they can access only objects in their home directory\. At connection time, AWS Transfer Family replaces these variables with the appropriate values for the user\. Doing this makes it easier to apply the same policy documents to multiple users\. This approach reduces the overhead of IAM role and policy management for managing your users' access to your Amazon S3 bucket\.

You can also use a session policy to customize access for each of your users based on your business requirements\. For more information, see [Permissions for AssumeRole, AssumeRoleWithSAML, and AssumeRoleWithWebIdentity](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_control-access_assumerole.html) in the *IAM User Guide*\.

**Note**  
AWS Transfer Family stores the policy JSON, instead of the Amazon Resource Name \(ARN\) of the policy\. So when you change the policy in the IAM console, you need to return to AWS Transfer Family console and update your users with the latest policy contents\. You can update the user under **Policy Info** tab in the **User configuration** section\. For more information, see [Managing access controls](#users-policies)\.  
If you are using the AWS CLI, you can use the following command to update the policy\.  

```
aws transfer update-user --server-id server --user-name user --policy \
   "$(aws iam get-policy-version --policy-arn policy --version-id version --output json)"
```

## Preventing users from running `mkdir` in an S3 bucket<a name="prevent-mkdir"></a>

You can limit users ability to create a directory in an Amazon S3 bucket\. To do so, you create an IAM policy that allows the `s3:PutObject` action but also denies it when the key ends with a "/" \(forward slash\)\. The following example policy allows users to upload files to an Amazon S3 bucket but denies the mkdir command in the Amazon S3 bucket\.

```
{
   "Sid":"DenyMkdir",
   "Action":[
      "s3:PutObject"
   ],
   "Effect":"Deny",
   "Resource":"arn:aws:s3:::my-sftp-bucket/*/"
}
```
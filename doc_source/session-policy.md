# Example session policy<a name="session-policy"></a>

When an administrator creates a role, the role often includes broad permissions to cover multiple use cases or team members\. If an administrator configures a [console URL](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use.html), they can reduce permissions for the resulting session by using a *session policy*\. For example, if you create a role with [read/write access](read-write-access.md), you can set up a URL that limits users’ access to only their home directories\.

Session policies are advanced policies that you pass as a parameter when you programmatically create a temporary session for a role or user\. Session policies are useful for locking down users so that they have access only to portions of your bucket where object prefixes contain their username\. The session policy's permissions are the intersection of the session policies and the resource\-based policies plus the intersection of the session policies and identity\-based policies\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/EffectivePermissions-session-rbp-id.png)

For more details, see [Session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session) in the *IAM User Guide*\.

In AWS Transfer Family, a session policy is supported only when you are transferring to or from Amazon S3\.

**Note**  
 The maximum length of a session policy is 2048 characters\. For more details, see the [Policy request parameter](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#API_CreateUser_RequestSyntax) for the `CreateUser` action in the *API reference*\. 

The following example policy is a session policy that limits users' access to their `home` directories only\.

**Note**  
 If your Amazon S3 bucket is encrypted using AWS Key Management Service \(AWS KMS\), you must specify additional permissions in your policy\. For details, see [Data encryption](encryption-at-rest.md)\. Additionally, you can see more information about [session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session.html) in the *IAM User Guide*\. 

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
                "s3:DeleteObject",
                "s3:DeleteObjectVersion",
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
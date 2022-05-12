# Example read/write access policy<a name="read-write-access"></a>

**Grant read/write access to Amazon S3 bucket**  
The following example policy for AWS Transfer Family grants read/write access to objects in your Amazon S3 bucket\.

**Note**  
In the following example, replace *bucket\_name* with the name of your S3 bucket\.  
Also, note that the `GetObjectACL` and `PutObjectACL` statements are only required if you are doing Cross Account Access\. That is, your Transfer Family server needs to access a bucket in a different account\.

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
                "arn:aws:s3:::bucket_name"
            ]
        },
        {
            "Sid": "HomeDirObjectAccess",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:DeleteObjectVersion",
                "s3:GetBucketLocation", 
                "s3:GetObjectVersion",
                "s3:GetObjectACL",
                "s3:PutObjectACL"
            ],
            "Resource": "arn:aws:s3:::bucket_name/*"
        }
    ]
}
```

**Grant file system access to files in Amazon EFS file system**  


**Note**  
In addition to the policy, you must also make sure your POSIX file permissions are granting the appropriate access\. For more information, see [Working with users, groups, and permissions at the Network File System \(NFS\) Level](https://docs.aws.amazon.com/efs/latest/ug/accessing-fs-nfs-permissions.html) in the *Amazon Elastic File System User Guide*\.

The following example policy grants root file system access to files in your Amazon EFS file system\.

**Note**  
In the following examples, replace *region* with your region, *account\-id* with the account the file is in, and *file\-system\-id* with the ID of your Amazon Elastic File System \(Amazon EFS\)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "RootFileSystemAccess",
            "Effect": "Allow",
            "Action": [
                "elasticfilesystem:ClientRootAccess",
                "elasticfilesystem:ClientMount",
                "elasticfilesystem:ClientWrite"
            ],
            "Resource": "arn:aws:elasticfilesystem:region:account-id:file-system/file-system-id"
        }
    ]
}
```

The following example policy grants user file system access to files in your Amazon EFS file system\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "UserFileSystemAccess",
            "Effect": "Allow",
            "Action": [
                "elasticfilesystem:ClientMount",
                "elasticfilesystem:ClientWrite"
            ],
            "Resource": "arn:aws:elasticfilesystem:region:account-id:file-system/file-system-id"
        }
    ]
}
```
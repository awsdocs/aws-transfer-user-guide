# Create an Amazon S3 bucket<a name="requirements-S3"></a>

AWS Transfer Family accesses your Amazon S3 bucket to service your users' transfer requests, so you need to provide an Amazon S3 bucket as part of setting up your file transfer protocol\-enabled server\. You can use an existing bucket, or you can create a new one\.

**Note**  
You don't have to use a server and Amazon S3 bucket that are in the same AWS Region, but we recommend this as a best practice\.

When you set up your users, you assign them each an IAM role\. This role determines the level of access that they have to your Amazon S3 bucket\.

For information on creating a new bucket, see [How do I create an S3 bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
 You can use Amazon S3 Object Lock to prevent objects from being overwritten for a fixed amount of time or indefinitely\. This works the same way with Transfer Family as with other services\. If an object exists and is protected, writing to that file or deleting it is not allowed\. For more details on Amazon S3 Object Lock, see [Using Amazon S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/object-lock.html) in the *Amazon Simple Storage Service User Guide*\. 

## Amazon S3 access points<a name="access-points"></a>

AWS Transfer Family supports [Amazon S3 Access Points](http://aws.amazon.com/s3/features/access-points/), a feature of Amazon S3 that allows you to easily manage granular access to shared data sets\. You can use S3 Access Point aliases anywhere you use an S3 bucket name\. You can create hundreds of access points in Amazon S3 for users who have different permissions to access shared data in an Amazon S3 bucket\.

For example, you can use access points to allow three different teams to have access to the same shared dataset where one team can read data from S3, a second team can write data to S3, and the third team can read, write, and delete data from S3\. To implement a granular access control as mentioned above, you can create an S3 access point that contains a policy that gives asymmetrical access to different teams\. You can use S3 access points with your Transfer Family server to achieve a fine\-grained access control, without creating a complex S3 bucket policy that spans hundreds of use cases\. To learn more about how to use S3 access points with a Transfer Family server, refer to the [ Enhance data access control with AWS Transfer Family and Amazon S3](http://aws.amazon.com/blogs/storage/enhance-data-access-control-with-aws-transfer-family-and-amazon-s3-access-points/) blog post\.

**Note**  
AWS Transfer Family does not currently support Amazon S3 Multi\-Region Access Points\.

## Amazon S3 HeadObject behavior<a name="head-object-behavior"></a>

In Amazon S3, buckets and objects are the primary resources, and objects are stored in buckets\. Amazon S3 can mimic a hierarchical file system, but can sometimes behave differently than a typical file system\. For example, directories are not a first\-class concept in Amazon S3 but instead are based on object keys\. AWS Transfer Family infers a directory path by splitting an object's key by the forward slash character \(**/**\), treating the last element as the file name, then grouping file names which have the same prefix together under the same path\. Zero\-byte objects are created to represent a folder's path when you create an empty directory using `mkdir` or by using the Amazon S3 console\. The key for these objects ends in a training forward slash\. These zero\-byte objects are described in [Organizing objects in the Amazon S3 console using folders](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-folders.html) in the *Amazon S3 User Guide*\.

When you run an `ls` command, and some results are Amazon S3 zero\-byte objects \(these objects have keys that end in the forward slash character\), Transfer Family issues a `HeadObject` request for each of these objects \(see [HeadObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_HeadObject.html) in the *Amazon Simple Storage Service API Reference* for details\)\. This can result in the following problems when using Amazon S3 as your storage with Transfer Family\.

### Grant ability to only write and list files<a name="headobject-access-denied"></a>

 In some cases, customers want to only offer write access to their Amazon S3 objects\. They want to provide access to write/upload and list objects in a bucket, but not read/download\. This translates to the Amazon S3 permissions `ListObjects` and `PutOjbect` to perform `ls` and `mkdir` commands using file transfer clients\. However, when Transfer Family needs to make a `HeadObject` call to either write or list files, it fails with an error of **Access denied**, because this call requires the `GetObject` permission\.

In this case, you can grant access by adding a policy condition that adds the `GetObject` permission for any objects that end in a **/**\. This prevents `GetObject` on files so they cannot be read, while allowing the user to list and traverse folders\. The following example policy offers only write and list access to their Amazon S3 buckets \(replace *DOC\-EXAMPLE\-BUCKET* with the actual name of your bucket\)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowListing",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::DOC-EXAMPLE-BUCKET"
        },
        {
            "Sid": "AllowReadWrite",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:GetobjectVersion"
            ],
            "Resource": [
                "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
            ]
         },
      {
            "Sid": "DenyIfNotFolder",
            "Effect": "Deny",
            "Action": [
                "s3:GetObject",
                "se:GetObjectVersion"
            ],
            "NotResource": [
                "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*/"
            ]
         }
      ]
}
```

**Note**  
This policy does not allow for appending to a file\. That is, a user that is assigned to this policy cannot open files to add content to them, or to modify them\. Also, if your use case involves issuing a `HeadObject` call before uploading a file, this policy won't work for you\.

### Large number of zero\-byte objects causing latency issues<a name="headobject-latency"></a>

 If your Amazon S3 buckets contain a large number of these zero\-byte objects, Transfer Family issues a lot of `HeadObject` calls, which can result processing delays\.

One possible solution to this problem is to delete all of your zero\-byte objects\. Note the following:
+ Empty directories will no longer exist\. Directories only exist as a result of their names being in the key of an object\.
+ Doesn’t prevent someone from calling `mkdir` and breaking things all over again\. You could mitigate this by crafting a policy which prevents directory creation\.
+ Some scenarios make use of these 0\-byte objects\. For example, you have a structure like **/inboxes/customer1000** and the inbox directory gets cleaned every day\.

Another possible solution is to limit the number of objects visible through a policy condition to reduce the number of `HeadObject` calls\. For this to be a workable solution, you need to accept that you might only be able to view a limited set of all of your sub\-directories\.
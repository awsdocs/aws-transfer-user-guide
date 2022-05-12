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
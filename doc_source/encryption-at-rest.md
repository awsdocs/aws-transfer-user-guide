# Data encryption<a name="encryption-at-rest"></a>

AWS Transfer Family uses the default encryption options you set for your Amazon S3 bucket to encrypt your data\. When you enable encryption on a bucket, all objects are encrypted when they are stored in the bucket\. The objects are encrypted using server\-side encryption with either Amazon S3\-managed keys \(SSE\-S3\) or AWS KMS\-managed keys \(SSE\-KMS\)\. For information about server\-side encryption, see [Protecting data using server\-side encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html) in the *Amazon Simple Storage Service User Guide*\.

The following steps show you how to encrypt data in AWS Transfer Family\.

**To allow encryption in AWS Transfer Family**

1. Enable default encryption for your Amazon S3 bucket\. For instructions, see [Amazon S3 default encryption for S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html) in the *Amazon Simple Storage Service User Guide*\.

1. Update the AWS Identity and Access Management \(IAM\) role policy that is attached to the user to grant the required AWS Key Management Service \(AWS KMS\) permissions\.

1. If you are using session policy for the user, the session policy must grant the required AWS KMS permissions\.

The following example shows an IAM policy that grants the minimum permissions required when using AWS Transfer Family with an Amazon S3 bucket that is enabled for AWS KMS encryption\. Include this example policy in both the user IAM role policy and session policy, if you are using one\.

```
{
	"Sid": "Stmt1544140969635",
	"Action": [
		"kms:Decrypt",
		"kms:Encrypt",
		"kms:GenerateDataKey"
	],
	"Effect": "Allow",
	"Resource": "arn:aws:kms:region:account-id:key/kms-key-id"
}
```

**Note**  
The KMS key ID that you specify in this policy must be the same as the one specified for the default encryption in step 1\.  
Root, or the IAM role that is used for the user, must be allowed in the AWS KMS key policy\. For information about the AWS KMS key policy, see [Using key policies in AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html) in the *AWS Key Management Service Developer Guide*\.
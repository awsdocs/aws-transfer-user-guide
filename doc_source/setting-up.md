# Setting up<a name="setting-up"></a>

The following sections describe the prerequisites required to use the AWS Transfer Family service\. At a minimum, you need to create an Amazon Simple Storage Service \(Amazon S3\) bucket and provide access to that bucket through an AWS Identity and Access Management \(IAM\) role\. Your role also needs to establish a trust relationship\. This trust relationship allows Transfer Family to assume the IAM role to access your bucket so that it can service your users' file transfer requests\.

**Topics**
+ [Supported AWS Regions, endpoints and quotas](regions.md)
+ [Sign up for AWS](requirements-aws-signup.md)
+ [Create an Amazon S3 bucket](requirements-S3.md)
+ [Create an Amazon EFS file system](requirements-efs.md)
+ [Create an IAM role and policy](requirements-roles.md)
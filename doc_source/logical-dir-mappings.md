# Using logical directories to simplify your Transfer Family directory structures<a name="logical-dir-mappings"></a>

To simplify your AWS Transfer Family server directory structure, you can use logical directories\. With logical directories, you can construct a virtual directory structure that uses user\-friendly names that your users navigate when they connect to your Amazon S3 bucket or Amazon EFS file system\. When you use logical directories, you can avoid disclosing absolute directory paths, Amazon S3 bucket names, and EFS file system names to your end users\.

You can use logical directories to set the user’s root directory to a desired location within your storage hierarchy, by performing what is known as a chroot operation\. In this mode, users are not able to navigate to a directory outside of the home or root directory that you've configured for them\. 

For example, although an Amazon S3 user has been scoped down to access only `/mybucket/home/${transfer:UserName}`, some clients allow users to traverse up a folder to `/mybucket/home`\. In this situation, the user lands back on their intended home directory only after logging out of and back in to the Transfer Family server again\. Performing a chroot operation can prevent this situation from occurring\.

You can create your own directory structure across buckets and prefixes\. This feature is useful if you have a workflow that is expecting a specific directory structure that you can't replicate through bucket prefixes\. You can also link to multiple non\-contiguous locations within Amazon S3, similar to creating a symbolic link in a Linux file system where your directory path references a different location in the file system\.

## Rules for using logical directories<a name="logical-dir-rules"></a>

Before you build your logical directory mappings, you should understand the following rules:
+ When `Entry` is `"/"`, you can have only one mapping because overlapping paths are not allowed\.
+ Targets can use the `${transfer:UserName}` variable if the bucket or file system path has been parameterized based on the username\.
+ Targets can be paths in different buckets or file systems, but you must make sure that the mapped IAM role \(the `Role` parameter in the response\) provides access to those buckets or file systems\.
+ Do not specify the `HomeDirectory` parameter because this value is implied by the `Entry` `Target` pairs when using the `LOGICAL` value for the `HomeDirectoryType` parameter\.
+ Targets should begin with a slash \(/\) character, but do not use trailing slashes \(/\) when you specify the `Target`\. For example, `/DOC-EXAMPLE-BUCKET/images` is acceptable, while `DOC-EXAMPLE-BUCKET/images` and `/DOC-EXAMPLE-BUCKET/images/` are not\.
+ Note that Amazon S3 is an object store, which means that folders are a virtual concept, and there is no actual directory hierarchy\. If your application issues a `stat` operation from a client, everything is classified as a file when you are using Amazon S3 for storage\. This behavior is described in [ Organizing objects in the Amazon S3 console using folders](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-folders.html)\. If your application requires that `stat` accurately show whether something is a file or folder, you can use Amazon EFS as the storage option for your Transfer Family servers\.

**Important**  
The root directory must exist on start\-up\. For Amazon S3, this means you must have already created an empty\-byte object ending with `/` to create the root folder\.

## Implementing logical directories and chroot<a name="implement-log-dirs"></a>

To use logical directories and chroot features, you must do the following:

Turn on logical directories for each user\. Do this by setting the `HomeDirectoryType` parameter to `LOGICAL` when you create or update your user\. 

```
"HomeDirectoryType": "LOGICAL"
```

### Chroot<a name="chroot"></a>

For chroot, create a directory structure that consists of a single `Entry` and `Target` pairing for each user\. The root folder is the `Entry` point, and the `Target` is the location in your bucket or file system to map to\.

------
#### [ Example for Amazon S3 ]

```
[{"Entry": "/", "Target": "/mybucket/jane"}]
```

------
#### [ Example for Amazon EFS ]

```
[{"Entry": "/", "Target": "/fs-faa1a123/jane"}]
```

------

You can use an absolute path as in the previous example, or you can use a dynamic substitution for the username with `${transfer:UserName}`, as in the following example\.

```
[{"Entry": "/", "Target":
"/mybucket/${transfer:UserName}"}]
```

In the preceding example, the user is locked to their root directory and cannot traverse up higher in the hierarchy\.

### Virtual directory structure<a name="virtual-dirs"></a>

For a virtual directory structure, you can create multiple `Entry` `Target` pairings, with targets anywhere in your S3 buckets or EFS file systems, including across multiple buckets or file systems, as long as the user’s IAM role mapping has permissions to access them\.

In the following virtual structure example, when the user logs into AWS SFTP, they are in the root directory with subdirectories of `/pics`, `/doc`, `/reporting`, and `/anotherpath/subpath/financials`\. 

```
[
{"Entry": "/pics", "Target": "/bucket1/pics"}, 
{"Entry": "/doc", "Target": "/bucket1/anotherpath/docs"},
{"Entry": "/reporting", "Target": "/reportingbucket/Q1"},
{"Entry": "/anotherpath/subpath/financials", "Target": "/reportingbucket/financials"}]
```



**Note**  
 You can only upload files to the specific folders that you map\. This means that in the previous example, you cannot upload to `/anotherpath` or `anotherpath/subpath` directories; only `anotherpath/subpath/financials`\. You also cannot map to those paths directly, as overlapping paths are not allowed\.  
 For example, assume that you create the following mappings:   

```
{
   "Entry": "/pics", 
   "Target": "/mybucket/pics"
}, 
{
   "Entry": "/doc", 
   "Target": "/mybucket/mydocs"
}, 
{
   "Entry": "/temp", 
   "Target": "/mybucket"
}
```
 You can only upload files to those buckets\. When you first connect through `sftp`, you are dropped into the root directory, `/`\. If you attempt to upload a file to that directory, the upload fails\. The following commands show an example sequence:   

```
sftp> pwd
Remote working directory: /
sftp> put file
Uploading file to /file
remote open("/file"): No such file or directory
```
To upload to any `directory/sub-directory`, you must explicitly map the path to the `sub-directory`\.

For more information about configuring logical directories and chroot for your users, including an AWS CloudFormation template that you can download and use, see [ Simplify your AWS SFTP Structure with chroot and logical directories](http://aws.amazon.com/blogs/storage/simplify-your-aws-sftp-structure-with-chroot-and-logical-directories/) in the AWS Storage Blog\.

## Custom AWS Lambda response<a name="auth-lambda-response"></a>

You can use logical directories with a Lambda function that connects to your custom identity provider\. To do so, in your Lambda function, you specify the `HomeDirectoryType` as **LOGICAL**, and add `Entry` and `Target` values for the `HomeDirectoryDetails` parameter\. For example:

```
HomeDirectoryType: "LOGICAL"
HomeDirectoryDetails: "[{\"Entry\": \"/\", \"Target\": \"/DOC-EXAMPLE-BUCKET/theRealFolder"}]"
```

The following code is an example of a successful response from a custom Lambda authentication call\. 

```
aws transfer test-identity-provider --server-id s-1234567890abcdef0 --user-name myuser
{
    "Url": "https://a1b2c3d4e5.execute-api.us-east-2.amazonaws.com/prod/servers/s-1234567890abcdef0/users/myuser/config", 
    "Message": "", 
    "Response": "{\"Role\": \"arn:aws:iam::123456789012:role/bob-usa-role\",\"HomeDirectoryType\": \"LOGICAL\",\"HomeDirectoryDetails\": \"[{\\\"Entry\\\":\\\"/myhome\\\",\\\"Target\\\":\\\"/DOC-EXAMPLE-BUCKET/theRealFolder\\\"}]\",\"PublicKeys\": \"[ssh-rsa myrsapubkey]\"}", 
    "StatusCode": 200
}
```

**Note**  
The `"Url":` line is returned only if you are using an API Gateway method as your custom identity provider\.
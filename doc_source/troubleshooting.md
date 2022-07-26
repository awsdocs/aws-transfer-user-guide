# Troubleshooting<a name="troubleshooting"></a>

 This section describes some common issues that might arise when using AWS Transfer Family and how to fix them\. 

**Topics**
+ [Troubleshoot Amazon EFS service\-managed users](#transfer-service-managed-efs)
+ [Troubleshoot Amazon API Gateway issues](#transfer-apigateway)
+ [Troubleshoot policies for encrypted Amazon S3 buckets](#encrypted-buckets)
+ [Troubleshoot authentication issues](#auth-issues)
+ [Troubleshoot workflow\-related errors using Amazon CloudWatch](#workflows-cloudwatch-errors)
+ [Troubleshoot workflow copy errors](#source-bucket-region)
+ [Troubleshoot missing POSIX profile](#missing-posix-profile)
+ [Troubleshoot testing your identity provider](#blank-test-identity-provider)
+ [Troubleshoot file upload issues](#file-upload-issues)
+ [Troubleshoot AS2 issues](#as2-troubleshooting-issues)

## Troubleshoot Amazon EFS service\-managed users<a name="transfer-service-managed-efs"></a>

**Description**

 You run the `sftp` command and the prompt doesn't appear, and instead you see the following message: 

```
Couldn't canonicalize: Permission denied
           Need cwd
```

**Cause**

 Your AWS Identity and Access Management \(IAM\) user's role does not have permission to access Amazon Elastic File System \(Amazon EFS\)\. 

 **Solution** 

 Increase the policy permissions for your user's role\. You can add an AWS managed policy, such as `AmazonElasticFileSystemClientFullAccess`\. 

## Troubleshoot Amazon API Gateway issues<a name="transfer-apigateway"></a>

This section describes possible solutions for the following issues:

**Topics**
+ [Too many authentication failures](#auth-failures-sftp)
+ [Connection closed](#connection-closed)

### Too many authentication failures<a name="auth-failures-sftp"></a>

**Description**

When you try to connect to your server using Secure Shell \(SSH\) File Transfer Protocol \(SFTP\), you get the following error:

```
Received disconnect from 3.15.127.197 port 22:2: Too many authentication failures
Authentication failed.
Couldn't read packet: Connection reset by peer
```

**Cause**

You might have entered an incorrect password for your user\. Try again to enter the correct password\.

If the password is correct, the issue might be caused by a role Amazon Resource Name \(ARN\) that is not valid\. To confirm that this is the issue, test the identity provider for your server\. If you see a response similar to the following, the role ARN is a placeholder only, as indicated by the role ID value of all zeros:

```
{
    "Response": "{\"Role\": \"arn:aws:iam::000000000000:role/MyUserS3AccessRole\",\"HomeDirectory\": \"/\"}",
    "StatusCode": 200,
    "Message": "",
    "Url": "https://api-gateway-ID.execute-api.us-east-1.amazonaws.com/prod/servers/transfer-server-ID/users/myuser/config"
}
```

**Solution**

Replace the placeholder role ARN with an actual role that has permission to access the server\.

**To update the role**

1. 

   Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. In the left navigation pane, choose **Stacks**\. 

1. In the **Stacks** list, choose your stack, and then choose the **Parameters** tab\.

1. Choose **Update**\. On the **Update stack** page, choose **Use current template**, and then choose **Next**\. 

1. Replace **UserRoleArn** with a role ARN that has sufficient permissions for accessing your Transfer Family server\. 
**Note**  
To grant the necessary permissions, you can add the `AmazonAPIGatewayAdministrator` and the `AmazonS3FullAccess` managed policies to your role\. 

1. Choose **Next**, and then choose **Next** again\. On the **Review *stack*** page, select **I acknowledge that AWS CloudFormation might create IAM resources**, and then choose **Update stack**\. 

### Connection closed<a name="connection-closed"></a>

**Description**

When you try to connect to your server using Secure Shell \(SSH\) File Transfer Protocol \(SFTP\), you get the following error:

```
Connection closed
```

**Cause**

One possible cause for this issue is that your Amazon CloudWatch logging role does not have a trust relationship with Transfer Family\.

**Solution**

Make sure that the logging role for the server has a trust relationship with Transfer Family\. For more information, see [To establish a trust relationship](requirements-roles.md#establish-trust-transfer)\.

## Troubleshoot policies for encrypted Amazon S3 buckets<a name="encrypted-buckets"></a>

**Description**

You have an encrypted Amazon S3 bucket that you are using as storage for your Transfer Family server\. If you try to upload a file to the server, you receive the error `Couldn't close file: Permission denied`\. 

And if you view the server logs, you see the following errors: 

```
ERROR Message="Access denied" Operation=CLOSE Path=/bucket/user/test.txt BytesIn=13
ERROR Message="Access denied"
```

**Cause**

Your IAM user's policy does not have permission to access the encrypted bucket\. 

 **Solution** 

 You must specify additional permissions in your policy to grant the required AWS Key Management Service \(AWS KMS\) permissions\. For details, see [Data encryption](encryption-at-rest.md)\.

## Troubleshoot authentication issues<a name="auth-issues"></a>

This section describes possible solutions for the following issues:

**Topics**
+ [Authentication failures—SSH/SFTP](#publickey-auth)
+ [Miscellaneous authentication issues](#misc-auth-issues)

### Authentication failures—SSH/SFTP<a name="publickey-auth"></a>

**Description**

When you try to connect to your server using Secure Shell \(SSH\) File Transfer Protocol \(SFTP\), you receive a message similar to the following: 

```
Received disconnect from 3.130.115.105 port 22:2: Too many authentication failures
  Authentication failed.
```

**Note**  
If you are using an API Gateway and receive this error, see [Too many authentication failures](#auth-failures-sftp)\.

**Cause**

You have not added an RSA key pair for your user, so you must authenticate using a password instead\.

 **Solution** 

When you run the `sftp` command, specify the `-o PubkeyAuthentication=no` option\. This option forces the system to request your password\. For example:

```
sftp -o PubkeyAuthentication=no sftp-user@server-id.server.transfer.region-id.amazonaws.com
```

### Miscellaneous authentication issues<a name="misc-auth-issues"></a>

**Cause**

If you receive an authentication error and none of the other troubleshooting works, you might have specified a target for a logical directory that contains a leading or trailing slash \(/\)\.

 **Solution** 

Update your logical directory target, to make sure it begins with a slash, and does not contain a trailing slash\. For example, `/DOC-EXAMPLE-BUCKET/images` is acceptable, while `DOC-EXAMPLE-BUCKET/images` and `/DOC-EXAMPLE-BUCKET/images/` are not\.

## Troubleshoot workflow\-related errors using Amazon CloudWatch<a name="workflows-cloudwatch-errors"></a>

**Description**

 If you are having issues with your workflows, you can use Amazon CloudWatch to investigate the cause\. 

**Cause**

There can be several causes\. Use Amazon CloudWatch Logs to investigate\.

**Solution**

Transfer Family emits workflow execution status into CloudWatch Logs\. The following types of workflow errors can appear in CloudWatch Logs: 
+ `"type": "StepErrored"`
+ `"type": "ExecutionErrored"`
+ `"type": "ExecutionThrottled"`

You can filter your workflow's execution logs using different filter and pattern syntax\. For example, you can create a log filter in your CloudWatch logs to capture workflow execution logs that contain the **ExecutionErrored** message\. For details, see [Real\-time processing of log data with subscriptions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Subscriptions.html) and [Filter and pattern syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/FilterAndPatternSyntax.html) in the *Amazon CloudWatch Logs User Guide*\.

*StepErrored*

```
2021-10-29T12:57:26.272-05:00
            {"type":"StepErrored","details":{"errorType":"BAD_REQUEST","errorMessage":"Cannot
            tag Efs file","stepType":"TAG","stepName":"successful_tag_step"},
            "workflowId":"w-abcdef01234567890","executionId":"1234abcd-56ef-78gh-90ij-1234klmno567",
            "transferDetails":{"serverId":"s-1234567890abcdef0","username":"lhr","sessionId":"1234567890abcdef0"}
```

Here, `StepErrored` indicates that a step within the workflow has generated an error\. In a single workflow, you can have multiple steps configured\. This error tells you in which step the error occurred and provides an error message\. In this particular example, the step was configured to tag a file; however, tagging a file in an Amazon EFS file system is not supported, so the step generated an error\.

*ExecutionErrored*

```
2021-10-29T12:57:26.618-05:00
            {"type":"ExecutionErrored","details":{},"workflowId":"w-w-abcdef01234567890",
            "executionId":"1234abcd-56ef-78gh-90ij-1234klmno567","transferDetails":{"serverId":"s-1234567890abcdef0",
            "username":"lhr","sessionId":"1234567890abcdef0"}}
```

When a workflow is not able to execute any step, it generates an `ExecutionErrored` message\. For example, if you have configured a single step in a given workflow, and if the step is not able to execute, the overall workflow fails\.

*Executionthrottled*

Execution is throttled if a workflow is getting triggered at a rate that is faster than the system can support\. This log message indicates that you must slow down your execution rate for workflows\. If you are not able to scale down your workflow\-execution rate, contact AWS Support at [Contact AWS](https://aws.amazon.com/contact-us)\.

## Troubleshoot workflow copy errors<a name="source-bucket-region"></a>

**Description**

 If you're executing a workflow that contains a step to copy the uploaded file, you could encounter the following error: 

```
{
  "type": "StepErrored", "details": {
    "errorType": "BAD_REQUEST", "errorMessage": "Bad Request (Service: Amazon S3; Status Code: 400; Error Code: 400 Bad Request;
    Request ID: request-ID; S3 Extended Request ID: request-ID Proxy: null)", "stepType": "COPY", "stepName": "copy-step-name" },
  "workflowId": "workflow-ID",
  "executionId": "execution-ID",
  "transferDetails": {
     "serverId": "server-ID",
     "username": "user-name",
     "sessionId": "session-ID"
  }
}
```

**Cause**

The source file is in an Amazon S3 bucket that is in a different AWS Region than the destination bucket\.

**Solution**

If you're executing a workflow that includes a copy step, make sure that the source and destination buckets are in the same AWS Region\.

## Troubleshoot missing POSIX profile<a name="missing-posix-profile"></a>

**Description**

If you're using Amazon EFS storage for your server and you're using a custom identity provider, you must provide your AWS Lambda function with a POSIX profile\.

**Cause**

One possible cause is that the templates that we provide for creating an AWS Lambda\-backed Amazon API Gateway method do not currently contain POSIX information\. 

If you did provide POSIX information, the format that you used for providing the POSIX information might not be getting parsed correctly by Transfer Family\.

**Solution**

Make sure that you are providing a JSON element to Transfer Family for the `PosixProfile` parameter\.

For example, if you're using Python, you could add the following line where you parse the `PosixProfile` parameter:

```
if PosixProfile: 
        response_data["PosixProfile"] = json.loads(PosixProfile)
```

Or, in JavaScript, you could add the following line, where the `uid-value` and `gid-value` are integers, 0 or greater, that represent the User ID \(UID\) and Group ID \(GID\) respectively:

```
PosixProfile: {"Uid": uid-value, "Gid": gid-value},
```

 

These code examples send the `PosixProfile` parameter to Transfer Family as a JSON object, rather than as a string\.

Also, within AWS Secrets Manager, you must store the `PosixProfile` parameter as follows\. Replace `your-uid` and `your-gid` with your actual values for the GID and UID\.

```
{"Uid": your-uid, "Gid": your-gid, "SecondaryGids": []}
```



## Troubleshoot testing your identity provider<a name="blank-test-identity-provider"></a>

**Description**

If you test your identity provider using the console or the `TestIdentityProvider` API call, the returned message is blank\.

**Cause**

The most likely cause is that the authentication failed because of an incorrect user name or password\.

**Solution**

Make sure that you are using the correct credentials for your user, and make updates to the user name or password, if necessary\.

## Troubleshoot file upload issues<a name="file-upload-issues"></a>

This section describes possible solutions for the following issues:

**Topics**
+ [Troubleshoot Amazon S3 file upload errors](#random-access-writes-s3)
+ [Troubleshoot unreadable file names](#non-utf8-issues)

### Troubleshoot Amazon S3 file upload errors<a name="random-access-writes-s3"></a>

**Description**

When you are attempting to upload a file to Amazon S3 storage using Transfer Family, you receive the following error message: AWS Transfer does not support random access writes to S3 objects\.

**Cause**

When you're using Amazon S3 for your server's storage, Transfer Family does not support multiple connections for a single transfer\.

**Solution**

If your Transfer Family server is using Amazon S3 for its storage, disable any options for your client software that mention using multiple connections for a single transfer\.

### Troubleshoot unreadable file names<a name="non-utf8-issues"></a>

**Description**

You see corrupted file names in some of your uploaded files\. Users sometimes encounter problems with FTP and SFTP transfers that garble certain characters in file names, such as umlauts, accented letters, or certain scripts, such as Chinese or Arabic\. 

**Cause**

Although the FTP and SFTP protocols can allow for character encoding of files names to be negotiated by clients, Amazon S3 and Amazon EFS do not\. Instead, they require UTF\-8 character encoding\. As a result, certain characters are not rendered correctly\. 

**Solution**

To solve this problem, review your client application for file name character encoding and make sure it is set to UTF\-8\.

## Troubleshoot AS2 issues<a name="as2-troubleshooting-issues"></a>

Error messages and troubleshooting tips for Applicability Statement 2 \(AS2\)\-enabled servers are described here: [AS2 error codes](as2-config-etc.md#as2-error-codes)\.
# Working with custom identity providers<a name="custom-identity-provider-users"></a>

To authenticate your users, you can use your existing identity provider with AWS Transfer Family\. You integrate your identity provider using an AWS Lambda function, which authenticates and authorizes your users for access to Amazon S3 or Amazon Elastic File System \(Amazon EFS\)\. For details, see [Using AWS Lambda to integrate your identity provider](#custom-lambda-idp)\. You can also access CloudWatch graphs for metrics such as number of files and bytes transferred in the AWS Transfer Family Management Console, giving you a single pane of glass to monitor file transfers using a centralized dashboard\.

Alternatively, you can provide a RESTful interface with a single Amazon API Gateway method\. Transfer Family calls this method to connect to your identity provider, which authenticates and authorizes your users for access to Amazon S3 or Amazon EFS\. Use this option if you need a RESTful API to integrate your identity provider or if you want to use AWS WAF to leverage its capabilities for geo\-blocking or rate\-limiting requests\. For details, see [Using Amazon API Gateway to integrate your identity provider](#authentication-api-gateway)\.

In either case, you can create a new server using the [AWS Transfer Family console](https://console.aws.amazon.com/transfer/) or the [CreateServer](API_CreateServer.md) API operation\.

**Topics**
+ [Using AWS Lambda to integrate your identity provider](#custom-lambda-idp)
+ [Lambda resource\-based policy](#lambda-resource-policy)
+ [Event message structure](#event-message-structure)
+ [Lambda functions for authentication](#authentication-lambda-examples)
+ [Using Amazon API Gateway to integrate your identity provider](#authentication-api-gateway)

## Using AWS Lambda to integrate your identity provider<a name="custom-lambda-idp"></a>

Create an AWS Lambda function that connects to your custom identity provider\. You can use any custom identity provider, such as Okta, Secrets Manager, OneLogin, or a custom data store that includes authorization and authentication logic\. 

**Note**  
Before you create a Transfer Family server that uses Lambda as the identity provider, you must create the function\. For an example Lambda function, see [Default Lambda function](#authentication-lambda-examples-default)\. Or, you can deploy a CloudFormation stack that uses a [Lambda function templates](#lambda-idp-templates)\. Also, make sure your Lambda function uses a resource\-based policy that trusts Transfer Family\. For an example policy, see [Lambda resource\-based policy](#lambda-resource-policy)\.

1. Open the [AWS Transfer Family console](https://console.aws.amazon.com/transfer/)\.

1. Choose **Create server** to open the **Create server** page\. For **Choose an identity provider**, choose **Custom Identity Provider**, as shown in the following screenshot\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/custom-lambda-console.png)

1. Make sure the default value, **Use AWS Lambda to connect your identity provider**, is selected\.

1. For ** AWS Lambda function**, choose the name of your Lambda function\.

1. Fill in the remaining boxes, and then choose **Create server**\. For details on the remaining steps for creating a server, see [Creating a server](create-server.md)\.

## Lambda resource\-based policy<a name="lambda-resource-policy"></a>

You must have a policy that references the Transfer Family server and Lambda ARNs\. For example, you could use the following policy with your Lambda function that connects to your identity provider\. 

```
{
  "Version": "2012-10-17",
  "Id": "default",
  "Statement": [
    {
      "Sid": "AllowTransferInvocation",
      "Effect": "Allow",
      "Principal": {
        "Service": "transfer.amazonaws.com"
      },
      "Action": "lambda:InvokeFunction",
      "Resource": "$lambda_arn",
      "Condition": {
        "ArnLike": {
          "AWS:SourceArn": "$server_arn"
        }
      }
    }
  ]
}
```

## Event message structure<a name="event-message-structure"></a>

The event message structure from SFTP server sent to the authorizer Lambda function for a custom IDP is as follows\.

```
{
    'username': 'value',
    'password': 'value',
    'protocol': 'SFTP',
    'serverId': 's-abcd123456',
    'sourceIp': '192.168.0.100'
}
```

Where `username` and `password` are the values for username and password that are sent to the server\.

For example, you enter the following command to connect:

```
sftp bobusa@server_hostname
```

You are then prompted to enter your password:

```
Enter password:
    mysecretpassword
```

You can check this from your Lambda function by printing the passed event from within the Lambda function\. It should look similar to the following text block\.

```
{
    'username': 'bobusa',
    'password': 'mysecretpassword',
    'protocol': 'SFTP',
    'serverId': 's-abcd123456',
    'sourceIp': '192.168.0.100'
}
```

The event structure is similar for FTP and FTPS: the only difference is those values are used for the `protocol` parameter, rather than SFTP\.

## Lambda functions for authentication<a name="authentication-lambda-examples"></a>

To implement different authentication strategies, edit the Lambda function\. To help you meet your application's needs, you can deploy a CloudFormation stack\. For more information about Lambda, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) or [ Building Lambda functions with Node\.js](https://docs.aws.amazon.com/lambda/latest/dg/lambda-nodejs.html)\.

### Lambda function templates<a name="lambda-idp-templates"></a>

You can deploy an AWS CloudFormation stack that uses a Lambda function for authentication\. We provide several templates that authenticate and authorize your users using username and password\. You can modify these templates or AWS Lambda code to further customize user access\.

**To create an AWS CloudFormation stack to use for authentication**

1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. Follow the instructions for deploying an AWS CloudFormation stack from an existing template in [Selecting a stack template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-using-console-create-stack-template.html) in the *AWS CloudFormation User Guide*\.

1. Use one of the following templates to create a Lambda function to use for authentication in Transfer Family\. 
**Important**  
We recommend that you edit the default user and password credentials\.
   + [Classic \(Cognito\) stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-basic-lambda-cognito-s3.template.yml)

     A basic template for creating a AWS Lambda for use as a custom identity provider in AWS Transfer Family\. It authenticates against cognito for password\-based authentication and public keys are returned from an Amazon S3 bucket if public key based authentication is used\. After deployment, you can modify the Lambda function code to do something different\.
   + [AWS Secrets Manager stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-secrets-manager-lambda.template.yml)

     A basic template that uses AWS Lambda with an AWS Transfer Family server to integrate Secrets Manager as an identity provider\. It authenticates against an entry in AWS Secrets Manager of the format `SFTP/username`\. Additionally, the secret must hold the key\-value pairs for all user properties returned to Transfer Family\. After deployment, you can modify the Lambda function code to do something different\.
   + [Okta stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-okta-lambda.template.yml): A basic template that uses AWS Lambda with an AWS Transfer Family server to integrate Okta as a custom identity provider\.
   + [Okta\-mfa stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-okta-mfa-lambda.template.yml): A basic template that uses AWS Lambda with an AWS Transfer Family server to integrate Okta, with MultiFactor Authentication, as a custom identity provider\.

   After the stack has been deployed, you can view details about it on the **Outputs** tab in the CloudFormation console\.

   Deploying one of these stacks is the easiest way to integrate a custom identity provider into the Transfer Family workflow\. By default, the Lambda function authenticates a single user called `myuser` with a password of `MySuperSecretPassword`\. After deployment, you can edit these credentials or update the Lambda function code to do something different\.

### Valid Lambda values<a name="lambda-valid-values"></a>

The following table describes details for the values that Transfer Family accepts for Lambda functions that are used for custom identity providers\.


|  Value  |  Description  |  Required  | 
| --- | --- | --- | 
|  `Role`  |  Specifies the Amazon Resource Name \(ARN\) of the IAM role that controls your users' access to your Amazon S3 bucket or Amazon EFS file system\. The policies attached to this role determine the level of access that you want to provide your users when transferring files into and out of your Amazon S3 or Amazon EFS file system\. The IAM role should also contain a trust relationship that allows the server to access your resources when servicing your users' transfer requests\.  |  Required  | 
|  `PosixProfile`  |  The full POSIX identity, including user ID \(`Uid`\), group ID \(`Gid`\), and any secondary group IDs \(`SecondaryGids`\), that controls your users' access to your Amazon EFS file systems\. The POSIX permissions that are set on files and directories in your file system determine the level of access your users get when transferring files into and out of your Amazon EFS file systems\.  |  Required for Amazon EFS backing storage  | 
|  `PublicKeys`  |  A list of SSH public key values that are valid for this user\. An empty list implies that this is not a valid login\. Must not be returned during password authentication\.  |  Optional  | 
|  `Policy`  |  A session policy for your user so that you can use the same IAM role across multiple users\. This policy scopes down user access to portions of their Amazon S3 bucket\.   |  Optional  | 
|  `HomeDirectoryType`  |  The type of landing directory \(folder\) that you want your users' home directory to be when they log in to the server\. If you set it to `PATH`, the user sees the absolute Amazon S3 bucket or Amazon EFS paths as is in their file transfer protocol clients\. If you set it to `LOGICAL`, you must provide mappings in the `HomeDirectoryMappings` parameter for how you want to make Amazon S3 or Amazon EFS paths visible to your users\.  |  Optional  | 
|  `HomeDirectoryDetails`  |  Logical directory mappings that specify which Amazon S3 or Amazon EFS paths and keys should be visible to your user and how you want to make them visible\. You must specify the `Entry` and `Target` pair, where `Entry` shows how the path is made visible and `Target` is the actual Amazon S3 or Amazon EFS path\.  |  Required if `HomeDirectoryType` has a value of `LOGICAL`  | 
|  `HomeDirectory`  |  The landing directory for a user when they log in to the server using the client\.  |  Optional  | 

### Testing your configuration<a name="authentication-test-configuration"></a>

After you create your custom identity provider, you should test your configuration\.

------
#### [ Console ]

**To test your configuration by using the AWS Transfer Family console**

1. Open the [AWS Transfer Family console](https://console.aws.amazon.com/transfer/)\. 

1. On the **Servers** page, choose your new server, choose **Actions**, and then choose **Test**\.

1. Enter the text for **Username** and **Password** that you set when you deployed the AWS CloudFormation stack\. If you kept the default options, the user name is `myuser` and the password is `MySuperSecretPassword`\.

1. Choose the **Server protocol** and enter the IP address for **Source IP**, if you set them when you deployed the AWS CloudFormation stack\.

------
#### [ CLI ]

**To test your configuration by using the AWS CLI**

1. Run the [test\-identity\-provider](https://docs.aws.amazon.com/cli/latest/reference/transfer/test-identity-provider.html) command\. Replace each `user input placeholder` with your own information, as described in the subsequent steps\.

   ```
   aws transfer test-identity-provider --server-id s-1234abcd5678efgh --user-name myuser --user-password MySuperSecretPassword --server-protocol FTP --source-ip 127.0.0.1
   ```

1. Enter the server ID\.

1. Enter the user name and password that you set when you deployed the AWS CloudFormation stack\. If you kept the default options, the user name is `myuser` and the password is `MySuperSecretPassword`\.

1. Enter the server protocol and source IP address, if you set them when you deployed the AWS CloudFormation stack\.

------

If user authentication succeeds, the test returns a `StatusCode: 200` HTTP response and a JSON object containing the details of the user's roles and permissions, as shown in the following example\.

```
{
    "Response": "{\"Policy\": \"{\n \"Version\": \"2012-10-17\",\n \"Statement\": [\n{\n \"Sid\": \"ReadAndListAllBuckets\",\n 
    \"Effect\": \"Allow\",\n \"Action\": [\n \"s3:ListAllMybuckets\",\n \"s3:GetBucketLocation\",\n \"s3:ListBucket\",\n 
    \"s3:GetObjectVersion\",\n \"s3:GetObjectVersion\"\n],\n \"Resource\":\"*\"\n}\n]\n}\",\"Role\": 
    \"arn:aws:iam::000000000000:role/MyUserS3AccessRole\",\"HomeDirectory\": \"/\"}",
    "StatusCode": 200,
    "Message": "",
    "Url": "https://abcde1234.execute-api.us-east-2.amazonaws.com/prod/servers/s-123a4567bcd891e23/users/myuser/config"
}
```

**Note**  
The `"Url":` line is returned only if you are using an API Gateway method as your custom identity provider\.

## Using Amazon API Gateway to integrate your identity provider<a name="authentication-api-gateway"></a>

This section describes how to use an AWS Lambda function to back an API Gateway method\. Use this option if you need a RESTful API to integrate your identity provider or if you want to use AWS WAF to leverage its capabilities for geo\-blocking or rate\-limiting requests\.

**Limitations if using an API Gateway to integrate your identity provider**
+ This configuration does not support custom domains\.
+ This configuration does not support a private API Gateway URL\.

If you need either of these, you can use Lambda as an identity provider, without API Gateway\. For details, see [Using AWS Lambda to integrate your identity provider](#custom-lambda-idp)\.

### Authenticating using an API Gateway method<a name="authentication-custom-ip"></a>

You can create an API Gateway method for use as an identity provider for Transfer Family\. This approach provides a highly secure way for you to create and provide APIs\. With API Gateway, you can create an HTTPS endpoint so that all incoming API calls are transmitted with greater security\. For more details about the API Gateway service, see the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)\.

API Gateway offers an authentication method named `AWS_IAM`, which gives you the same authentication based on AWS Identity and Access Management \(IAM\) that AWS uses internally\. If you enable authentication with `AWS_IAM`, only callers with explicit permissions to call an API can reach that API's API Gateway method\.

To use your API Gateway method as a custom identity provider for Transfer Family, enable IAM for your API Gateway method\. As part of this process, you provide an IAM role with permissions for Transfer Family to use your gateway\.

**Note**  
To improve security, you can configure a web application firewall\. AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway\. For details, see [Add a web application firewall](web-application-firewall.md)\.

**To use your API Gateway method for custom authentication with Transfer Family**

1. Create an AWS CloudFormation stack\. To do this:

   1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

   1. Follow the instructions for deploying an AWS CloudFormation stack from an existing template in [Selecting a stack template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-using-console-create-stack-template.html) in the *AWS CloudFormation User Guide*\.

   1. Use one of the following basic templates to create an AWS Lambda\-backed API Gateway method for use as a custom identity provider in Transfer Family\.
      + [Basic stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-basic-apig.template.yml)

        By default, your API Gateway method is used as a custom identity provider to authenticate a single user in a single server using a hardcoded SSH \(Secure Shell\) key or password\. After deployment, you can modify the Lambda function code to do something different\.
      + [AWS Secrets Manager stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-secrets-manager-apig.template.yml)

        By default, your API Gateway method authenticates against an entry in Secrets Manager of the format `SFTP/username`\. Additionally, the secret must hold the key\-value pairs for all user properties returned to Transfer Family\. After deployment, you can modify the Lambda function code to do something different\. For more information, see [Enable password authentication for AWS Transfer Family using AWS Secrets Manager](http://aws.amazon.com/blogs/storage/enable-password-authentication-for-aws-transfer-family-using-aws-secrets-manager-updated/)\.
      + [Okta stack template](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-okta-apig.template.yml)

        Your API Gateway method integrates with Okta as a custom identity provider in Transfer Family\. For more information, see [Using Okta as an identity provider with AWS Transfer Family](http://aws.amazon.com/blogs/storage/using-okta-as-an-identity-provider-with-aws-transfer-for-sftp/)\.

   Deploying one of these stacks is the easiest way to integrate a custom identity provider into the Transfer Family workflow\. Each stack uses the Lambda function to support your API method based on API Gateway\. You can then use your API method as a custom identity provider in Transfer Family\. By default, the Lambda function authenticates a single user called `myuser` with a password of `MySuperSecretPassword`\. After deployment, you can edit these credentials or update the Lambda function code to do something different\.
**Important**  
We recommend that you edit the default user and password credentials\.

   After the stack has been deployed, you can view details about it on the **Outputs** tab in the CloudFormation console\. These details include the stack's Amazon Resource Name \(ARN\), the ARN of the IAM role that the stack created, and the URL for your new gateway\.
**Note**  
If you are using the custom identity provider option to enable password–based authentication for your users, and you enable the request and response logging provided by API Gateway, API Gateway logs your users' passwords to your Amazon CloudWatch Logs\. We don't recommend using this log in your production environment\. For more information, see [Set up CloudWatch API logging in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html) in the *API Gateway Developer Guide*\.

1. Check the API Gateway method configuration for your server\. To do this:

   1. Open the API Gateway console at [https://console\.aws\.amazon\.com/apigateway/](https://console.aws.amazon.com/apigateway/)\. 

   1. Choose the **Transfer Custom Identity Provider basic template API** that the AWS CloudFormation template generated\.

      The following screenshot shows the complete API configuration\. In this example, the method is backed by a Lambda function, but many other integration types are also possible\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/apig-config-method.png)

   1. In the **Resources** pane, choose **GET**, and then choose **Method Request**\. The following screenshot shows the correct method configuration\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/apig-config-method-fields.png)

   At this point, your API gateway is ready to be deployed\.

1. For **Actions**, choose **Deploy API**\. For **Deployment stage**, choose **prod**, and then choose **Deploy**\.

   After the API Gateway method is successfully deployed, view its performance in the **Stage Editor** section, as shown in the following screenshot\.
**Note**  
Copy the **Invoke URL** address that appears at the top of the screen\. You will need it for the next step\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/apig-config-method-invoke.png)

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. Choose **Create server** to open the **Create server** page\. For **Choose an identity provider**, choose **Custom**, then select **Use Amazon API Gateway to connect to your identity provider**, as shown in the following screenshot\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/create-server-choose-idp-custom.png)

1. In the **Provide an Amazon API Gateway URL** text box, paste the **Invoke URL** address of the API Gateway endpoint that you created in step 3 of this procedure\.

1. For **Role**, choose the IAM role that was created by the AWS CloudFormation template\. This role allows Transfer Family to invoke your API gateway method\.

   The invocation role contains the AWS CloudFormation stack name that you selected for the stack that you created in step 1\. It has the following format: `CloudFormation-stack-name-TransferIdentityProviderRole-ABC123DEF456GHI`\.

1. Fill in the remaining boxes, and then choose **Create server**\. For details on the remaining steps for creating a server, see [Creating a server](create-server.md)\.

### Implementing your API Gateway method<a name="authentication-api-method"></a>

To create a custom identity provider for Transfer Family, your API Gateway method must implement a single method that has a resource path of `/servers/serverId/users/username/config`\. The `serverId` and `username` values come from the RESTful resource path\. Also, add `sourceIp` and `protocol` as **URL Query String Parameters** in the **Method Request**, as shown in the following image\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/apig-config-method-request.png)

**Note**  
The user name must be a minimum of 3 and a maximum of 100 characters\. You can use the following characters in the user name: a–z, A\-Z, 0–9, underscore \(\_\), hyphen \(\-\), period \(\.\), and at sign \(@\)\. However, the user name can't start with a hyphen \(\-\), period \(\.\), or at sign \(@\)\.

If Transfer Family attempts password authentication for your user, the service supplies a `Password:` header field\. In the absence of a `Password:` header, Transfer Family attempts public key authentication to authenticate your user\.

When you are using an identity provider to authenticate and authorize end users, in addition to validating their credentials, you can allow or deny access requests based on the IP addresses of the clients used by your end users\. You can use this feature to ensure that data stored in your S3 buckets or your Amazon EFS file system can be accessed over the supported protocols only from IP addresses that you have specified as trusted\. To enable this feature, you must include `sourceIp` in the Query string\.

If you have multiple protocols enabled for your server and want to provide access using the same user name over multiple protocols, you can do so as long as the credentials specific to each protocol have been set up in your identity provider\. To enable this feature, you must include the `protocol` value in the RESTful resource path\.

Your API Gateway method should always return HTTP status code `200`\. Any other HTTP status code means that there was an error accessing the API\.

**Amazon S3 example response**  
The example response body is a JSON document of the following form for Amazon S3\.

```
{
 "Role": "IAM role with configured S3 permissions",
 "PublicKeys": [
     "ssh-rsa public-key1",
     "ssh-rsa public-key2"
  ],
 "Policy": "STS Assume role session policy",
 "HomeDirectory": "/bucketName/path/to/home/directory"
}
```

**Note**  
 The policy is escaped JSON as a string\. For example:   

```
"Policy":
"{
  \"Version\": \"2012-10-17\",
  \"Statement\":
     [
     {\"Condition\":
        {\"StringLike\":
            {\"s3:prefix\":
               [\"user/*\", \"user/\"]}},
     \"Resource\": \"arn:aws:s3:::bucket\",
     \"Action\": \"s3:ListBucket\",
     \"Effect\": \"Allow\",
     \"Sid\": \"ListHomeDir\"},
     {\"Resource\": \"arn:aws:s3:::*\",
        \"Action\": [\"s3:PutObject\",
        \"s3:GetObject\",
        \"s3:DeleteObjectVersion\",
        \"s3:DeleteObject\",
        \"s3:GetObjectVersion\",
        \"s3:GetObjectACL\",
        \"s3:PutObjectACL\"],
     \"Effect\": \"Allow\",
     \"Sid\": \"HomeDirObjectAccess\"}]
}"
```

The following example response shows that a user has a logical home directory type\.

```
{
   \"Role\": \"arn:aws:iam::123456789012:role/role-api-gateway-s3\",
   \"HomeDirectoryType\":\"LOGICAL\",
   \"HomeDirectoryDetails\":\"[{\\\"Entry\\\":\\\"/\\\",\\\"Target\\\":\\\"/my-home-bucket\\\"}]\",
   \"PublicKeys\":[\"\"]
}
```

**Amazon EFS example response**  
The example response body is a JSON document of the following form for Amazon EFS\.

```
{
 "Role": "IAM role with configured EFS permissions",
 "PublicKeys": [
     "ssh-rsa public-key1",
     "ssh-rsa public-key2"
  ],
 "PosixProfile": {
   "Uid": "POSIX user ID",
   "Gid": "POSIX group ID",
   "SecondaryGids": [Optional list of secondary Group IDs],
 },
 "HomeDirectory": "/fs-id/path/to/home/directory"
}
```

The `Role` field shows that successful authentication occurred\. When doing password authentication \(when you supply a `Password:` header\), you don't need to provide SSH public keys\. If a user can't be authenticated, for example, if the password is incorrect, your method should return a response without `Role` set\. An example of such a response is an empty JSON object\.

 The following example response shows a user that has a logical home directory type\. 

```
{
    \"Role\": \"arn:aws:iam::123456789012:role/role-api-gateway-efs\",
    \"HomeDirectoryType\": \"LOGICAL\",
    \"HomeDirectoryDetails\":\"[{\\\"Entry\\\":\\\"/\\\",\\\"Target\\\":\\\"/faa1a123\\\"}]\",
    \"PublicKeys\":[\"\"],
    \"PosixProfile\":{\"Uid\":65534,\"Gid\":65534}
}
```

You can include user policies in the Lambda function in JSON format\. For more information about configuring user policies in Transfer Family, see [Managing access controls](users-policies.md)\.

### Default Lambda function<a name="authentication-lambda-examples-default"></a>

To implement different authentication strategies, edit the Lambda function that your gateway uses\. To help you meet your application's needs, you can use the following example Lambda functions in Node\.js\. For more information about Lambda, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) or [ Building Lambda functions with Node\.js](https://docs.aws.amazon.com/lambda/latest/dg/lambda-nodejs.html)\.

The following example Lambda function takes your user name, password \(if you're performing password authentication\), server ID, protocol, and client IP address\. You can use a combination of these inputs to look up your identity provider and determine if the login should be accepted\.

**Note**  
If you have multiple protocols enabled for your server and want to provide access using the same user name over multiple protocols, you can do so as long as the credentials specific to the protocol have been set up in your identity provider\.  
For File Transfer Protocol \(FTP\), we recommend maintaining separate credentials from Secure Shell \(SSH\) File Transfer Protocol \(SFTP\) and File Transfer Protocol over SSL \(FTPS\)\. We recommend maintaining separate credentials for FTP because, unlike SFTP and FTPS, FTP transmits credentials in clear text\. By isolating FTP credentials from SFTP or FTPS, if FTP credentials are shared or exposed, your workloads using SFTP or FTPS remain secure\.

This example function works only with Amazon S3\. This example function returns the role and logical home directory details, along with the public keys \(if it performs public key authentication\)\.

The [HomeDirectoryType](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#TransferFamily-CreateUser-request-HomeDirectoryType) parameter specifies the type of landing directory \(folder\) that you want your user's home directory to be when they log in to the server\. If you set this parameter to `PATH`, the user sees the absolute Amazon S3 bucket or Amazon EFS paths as is in their file transfer protocol clients\. If you set this parameter to `LOGICAL`, you must provide mappings in the [HomeDirectoryMappings](https://docs.aws.amazon.com/transfer/latest/userguide/API_CreateUser.html#TransferFamily-CreateUser-request-HomeDirectoryMappings) parameter for how you want to make Amazon S3 or Amazon EFS paths visible to your users\.

------
#### [ PATH home directory ]

This function is for users that are using `PATH` for their `HomeDirectoryType`\.

```
// GetUserConfig Lambda

exports.handler = (event, context, callback) => {
  console.log("Username:", event.username, "ServerId: ", event.serverId);

  var response;
  // Check if the user name presented for authentication is correct. This doesn't check the value of the serverId, only that it is provided.
  // There is also event.protocol (one of "FTP", "FTPS", "SFTP") and event.sourceIp (e.g., "127.0.0.1") to further restrict logins.
  if (event.serverId !== "" && event.username == '${UserName}') {
    response = {
      Role: '${UserRoleArn}', // The user will be authenticated if and only if the Role field is not blank
      Policy: '', // Optional JSON blob to further restrict this user's permissions
      HomeDirectory: '${UserHomeDirectory}' // Not required, defaults to '/'
    };
    
    // Check if password is provided
    if (event.password == "") {
      // If no password provided, return the user's SSH public key
     response['PublicKeys'] = [ "${UserPublicKey1}" ];
    // Check if password is correct
    } else if (event.password !== '${UserPassword}') {
      // Return HTTP status 200 but with no role in the response to indicate authentication failure
      response = {};
    } 
  } else {
    // Return HTTP status 200 but with no role in the response to indicate authentication failure
    response = {};
  }
  callback(null, response);
};
```

------
#### [ LOGICAL home directory ]

 The following Lambda function provides the details for a user that has a [logical home directory](logical-dir-mappings.md)\. The user, role, POSIX profile, password, and home directory details in this function are all examples, and must be replaced with your actual values\. 

```
// GetUserConfig Lambda

exports.handler = (event, context, callback) => {
  console.log("Username:", event.username, "ServerId: ", event.serverId);

  var response;
  // Check if the username presented for authentication is correct. This doesn't check the value of the serverId, only that it is provided.
  if (event.serverId !== "" && event.username == 'example-user') {
    response = {
      Role: 'arn:aws:iam::123456789012:role/role-api-gateway', // The user will be authenticated if and only if the Role field is not blank
      PosixProfile: {"Gid": 65534, "Uid": 65534},
      HomeDirectoryDetails: "[{\"Entry\": \"/\", \"Target\": \"/fs-faa1a123\"}]",
      HomeDirectoryType: "LOGICAL",
      //HomeDirectory: '/fs-faa1a123' // Not required, defaults to '/'
    };

    // Check if password is provided
    if (event.password == "") {
      // If no password provided, return the user's SSH public key
      response['PublicKeys'] = [ "" ];
    // Check if password is correct
    } else if (event.password !== 'Password1234') {
      // Return HTTP status 200 but with no role in the response to indicate authentication failure
      response = {};
    }
  } else {
    // Return HTTP status 200 but with no role in the response to indicate authentication failure
    response = {};
  }
  callback(null, response);
};
```

------

### Lambda function for use with AWS Secrets Manager<a name="authentication-lambda-examples-secrets-mgr"></a>

To use AWS Secrets Manager as your identity provider, you can work with the Lambda function in the sample AWS CloudFormation template\. The Lambda function queries the Secrets Manager service with your credentials and, if successful, returns a designated secret\. For more information about Secrets Manager, see the [AWS Secrets Manager User Guide](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.

To download a sample AWS CloudFormation template that uses this Lambda function, go to the [Amazon S3 bucket provided by AWS Transfer Family](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-secrets-manager-apig.template.yml)\.
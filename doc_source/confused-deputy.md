# Cross\-service confused deputy prevention<a name="confused-deputy"></a>

The confused deputy problem is a security issue where an entity that doesn't have permission to perform an action can coerce a more\-privileged entity to perform the action\. In AWS, cross\-service impersonation can result in the confused deputy problem\. Cross\-service impersonation can occur when one service \(the *calling service*\) calls another service \(the *called service*\)\. The calling service can be manipulated to use its permissions to act on another customer's resources in a way that it should not otherwise have permission to access\. To prevent this, AWS provides tools that help you protect your data for all services with service principals that have been given access to resources in your account\. For a detailed description of this problem, see [the confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html) in the *IAM User Guide*\.

We recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in resource policies to limit the permissions that AWS Transfer Family has for the resource\. If you use both global condition context keys, the `aws:SourceAccount` value and the account in the `aws:SourceArn` value must use the same account ID when used in the same policy statement\. 

The most effective way to protect against the confused deputy problem is to use the exact Amazon Resource Name \(ARN\) of the resource you want to allow\. If you are specifying multiple resources, use the `aws:SourceArn` global context condition key with wildcard characters \(`*`\) for the unknown portions of the ARN\. For example, `arn:aws:transfer::region::account-id:server/*`\.

AWS Transfer Family uses the following types of roles:
+ *user role*: allows service\-managed users to access the necessary Transfer Family resources\. Transfer assumes this in the context of a Transfer user ARN\.
+ *access role*: provides access to the proper Amazon S3 files being transferred\. For inbound AS2 transfers, it uses the Amazon Resource Name \(ARN\) for the agreement\. For outbound AS2 transfers, it uses the ARN for the connector\.
+ *invocation role*: for use with Amazon API Gateway as the server’s Custom Identity Provider\. Transfer assumes this in the context of a Transfer server ARN\.
+ *logging role*: used to log entries into Amazon CloudWatch\. Transfer uses this role to log success and failure details along with information about file transfers\. Transfer assumes this in the context of a Transfer server ARN\. For outbound AS2 transfers, it uses the connector ARN\.
+ *workflow role*: allows a Transfer Family user to call and launch workflows\. Transfer assumes this in the context of a Transfer workflow ARN\.

For more information, see [Policies and permissions in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.

**Note**  
In the following examples, replace each *user input placeholder* with your own information\. 

**Note**  
In our examples, we use both `ArnLike` and `ArnEquals`\. They are functionally identical, and therefore you may use either when you construct your policies\. Transfer Family documentation uses `ArnLike` when the condition contains a wildcard character, and `ArnEquals` to indicate an exact match condition\.

## AWS Transfer Family User role cross\-service confused deputy prevention<a name="user-role-cross-service"></a>

The following example policy allows any user of any server in the account to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:user/*"
                }
            }
        }
    ]
}
```

The following example policy allows any user of a specific server to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnEquals": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:user/server-id/*"
                }
            }
        }
    ]
}
```

The following example logging policy allows a specific user of a specific server to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:user/server-id/user-name"
                }
            }
        }
    ]
}
```

## AWS Transfer Family workflow role cross\-service confused deputy prevention<a name="workflow-role-cross-service"></a>

The following example policy allows any workflow in the account to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:workflow/*"
                }
            }
        }
    ]
}
```

The following example policy allows a specific workflow to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:workflow/workflow-id"
                }
            }
        }
    ]
}
```

## AWS Transfer Family logging and invocation role cross\-service confused deputy prevention<a name="logging-role-cross-service"></a>

**Note**  
The following examples can be used in both logging and invocation roles\.

The following example logging/invocation policy allows any server in the account to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAllServers",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:server/*"
                }
            }
        }
    ]
}
```

The following example logging/invocation policy allows a specific server to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowSpecificServer",
            "Effect": "Allow",
            "Principal": {
                "Service": "transfer.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                },
                "ArnEquals": {
                    "aws:SourceArn": "arn:aws:transfer:region:account-id:/server/server-id"
                }
            }
        }
    ]
}
```
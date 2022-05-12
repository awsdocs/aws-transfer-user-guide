# AWS Transfer Family tag\-based policy examples<a name="security_iam_tag-based-policy-examples"></a>

The following are examples of how to control access to AWS Transfer Family resources based on tags\.

## Using tags to control access to AWS Transfer Family resources<a name="tag-access-control"></a>

Conditions in IAM policies are part of the syntax that you use to specify permissions to AWS Transfer Family resources\. You can control access to AWS Transfer Family resources \(such as users, servers, roles, and other entities\) based on tags on those resources\. Tags are key\-value pairs\. For more information about tagging resources, see [Tagging AWS resources](https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html) in the *AWS General Reference*\. 

In AWS Transfer Family, resources can have tags, and some actions can include tags\. When you create an IAM policy, you can use tag condition keys to control the following:
+ Which users can perform actions on an AWS Transfer Family resource, based on tags that the resource has\.
+ What tags can be passed in an action's request\.
+ Whether specific tag keys can be used in a request\.

By using tag\-based access control, you can apply finer control than at the API level\. You also can apply more dynamic control than by using resource\-based access control\. You can create IAM policies that allow or deny an operation based on tags provided in the request \(request tags\)\. You can also create IAM policies based on tags on the resource that is being operated on \(resource tags\)\. In general, resource tags are for tags that are already on resources, request tags are for when you're adding tags to or removing tags from a resource\.

For the complete syntax and semantics of tag condition keys, see [Controlling access to AWS resources using resource tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html) in the *IAM User Guide*\. For details about specifying IAM policies with API Gateway, see [Control access to an API with IAM permissions](https://docs.aws.amazon.com/apigateway/latest/developerguide/permissions.html) in the *API Gateway Developer Guide*\.

### Example 1: Deny actions based on resource tags<a name="transfer-deny-actions-resource-tag"></a>

You can deny an action to be performed on a resource based on tags\. The following example policy denies `TagResource`, `UntagResource`, `StartServer`, `StopServer`, `DescribeServer`, and `DescribeUser` operations if the user or server resource is tagged with the key `stage` and the value `prod`\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "transfer:TagResource",
                "transfer:UntagResource",
                "transfer:StartServer",
                "transfer:StopServer", 
                "transfer:DescribeServer",
                "transfer:DescribeUser
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/stage": "prod"
                }
            }
        }
    ]
}
```

### Example 2: Allow actions based on resource tags<a name="transfer-allow-actions-resource-tag"></a>

You can allow an action to be performed on a resource based on tags\. The following example policy allows `TagResource`, `UntagResource`, `StartServer`, `StopServer`, `DescribeServer`, and `DescribeUser` operations if the user or server resource is tagged with the key `stage` and the value `prod`\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "transfer:TagResource",
                "transfer:UntagResource",
                "transfer:StartServer",
                "transfer:StopServer", 
                "transfer:DescribeServer",
                "transfer:DescribeUser                            
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/stage": "prod"
                }
            }
        }
    ]
}
```

### Example 3: Deny creation of a user or server based on request tags<a name="transfer-deny-server-creation-tag"></a>

The following example policy contains two statements\. The first statement denies the `CreateServer` operation on all resources if the cost center key for the tag doesn't have a value\.

The second statement denies the `CreateServer` operation if the cost center key for the tag contains any other value besides 1, 2 or 3\.

**Note**  
This policy does allow creating or deleting a resource that contains a key called `costcenter` and a value of `1`, `2`, or `3`\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        { 
            "Effect": "Deny",
            "Action": [
                "transfer:CreateServer"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "Null":  {
                    "aws:RequestTag/costcenter": "true"
                }
            }
        },
        {
            "Effect": "Deny",
            "Action": "transfer:CreateServer",
            "Resource": [
                "*"
            ],
            "Condition": {
                "ForAnyValue:StringNotEquals": {
                    "aws:RequestTag/costcenter": [
                        "1",
                        "2",
                        "3"
                    ]
                }
            }
        }           
    ]
}
```
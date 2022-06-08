# How AWS Transfer Family works with IAM<a name="security_iam_service-with-iam"></a>

Before you use AWS Identity and Access Management \(IAM\) to manage access to AWS Transfer Family, you should understand what IAM features are available to use with AWS Transfer Family\. To get a high\-level view of how AWS Transfer Family and other AWS services work with IAM, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [AWS Transfer Family identity\-based policies](#security_iam_service-with-iam-id-based-policies)
+ [AWS Transfer Family resource\-based policies](#security_iam_service-with-iam-resource-based-policies)
+ [Authorization based on AWS Transfer Family tags](#security_iam_service-with-iam-tags)
+ [AWS Transfer Family IAM roles](#security_iam_service-with-iam-roles)

## AWS Transfer Family identity\-based policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources as well as the conditions under which actions are allowed or denied\. AWS Transfer Family supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON policy elements reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *AWS Identity and Access Management User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Action` element of a JSON policy describes the actions that you can use to allow or deny access in a policy\. Policy actions usually have the same name as the associated AWS API operation\. There are some exceptions, such as *permission\-only actions* that don't have a matching API operation\. There are also some operations that require multiple actions in a policy\. These additional actions are called *dependent actions*\.

Include actions in a policy to grant permissions to perform the associated operation\.

 Policy actions in AWS Transfer Family use the following prefix before the action: `transfer:`\. For example, to grant someone permission to create a server, with the Transfer Family `CreateServer` API operation, you include the `transfer:CreateServer` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. AWS Transfer Family defines its own set of actions that describe tasks that you can perform with this service\.

To specify multiple actions in a single statement, separate them with commas as follows\.

```
"Action": [
      "transfer:action1",
      "transfer:action2"
```

You can specify multiple actions using wildcards \(\*\)\. For example, to specify all actions that begin with the word `Describe`, include the following action\.

```
"Action": "transfer:Describe*"
```

To see a list of AWS Transfer Family actions, see [Actions defined by AWS Transfer Family](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awstransferfamily.html#awstransferfamily-actions-as-permissions) in the *Service Authorization Reference*\.

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Resource` JSON policy element specifies the object or objects to which the action applies\. Statements must include either a `Resource` or a `NotResource` element\. As a best practice, specify a resource using its [Amazon Resource Name \(ARN\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\. You can do this for actions that support a specific resource type, known as *resource\-level permissions*\.

For actions that don't support resource\-level permissions, such as listing operations, use a wildcard \(\*\) to indicate that the statement applies to all resources\.

```
"Resource": "*"
```

The Transfer Family server resource has the following ARN\.

```
arn:aws:transfer:${Region}:${Account}:server/${ServerId}
```

For example, to specify the `s-01234567890abcdef` Transfer Family server in your statement, use the following ARN\.

```
"Resource": "arn:aws:transfer:us-east-1:123456789012:server/s-01234567890abcdef"
```

For more information about the format of ARNs, see [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *Service Authorization Reference*, or [IAM ARNs](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-arns) in the *IAM User Guide*\.

To specify all instances that belong to a specific account, use the wildcard \(\*\)\.

```
"Resource": "arn:aws:transfer:us-east-1:123456789012:server/*"
```

Some AWS Transfer Family actions are performed on multiple resources, such as those used in IAM policies\. In those cases, you must use the wildcard \(\*\)\.

```
"Resource": "arn:aws:transfer:*:123456789012:server/*"
```

In some cases you need to specify more than one type of resource, for example, if you create a policy that allows access to Transfer Family servers and users\. To specify multiple resources in a single statement, separate the ARNs with commas\.

```
"Resource": [
      "resource1",
      "resource2"
            ]
```

To see a list of AWS Transfer Family resources, see [Resource types defined by AWS Transfer Family](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awstransferfamily.html#awstransferfamily-resources-for-iam-policies) in the *Service Authorization Reference*\.

### Condition keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Condition` element \(or `Condition` *block*\) lets you specify conditions in which a statement is in effect\. The `Condition` element is optional\. You can create conditional expressions that use [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html), such as equals or less than, to match the condition in the policy with values in the request\. 

If you specify multiple `Condition` elements in a statement, or multiple keys in a single `Condition` element, AWS evaluates them using a logical `AND` operation\. If you specify multiple values for a single condition key, AWS evaluates the condition using a logical `OR` operation\. All of the conditions must be met before the statement's permissions are granted\.

 You can also use placeholder variables when you specify conditions\. For example, you can grant an IAM user permission to access a resource only if it is tagged with their IAM user name\. For more information, see [IAM policy elements: variables and tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_variables.html) in the *IAM User Guide*\. 

AWS supports global condition keys and service\-specific condition keys\. To see all AWS global condition keys, see [AWS global condition context keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

AWS Transfer Family defines its own set of condition keys and also supports using some global condition keys\. To see a list of AWS Transfer Family condition keys, see [Condition keys for AWS Transfer Family](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awstransferfamily.html#awstransferfamily-policy-keys) in the *Service Authorization Reference*\.

### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>

To view examples of AWS Transfer Family identity\-based policies, see [AWS Transfer Family identity\-based policy examples](security_iam_id-based-policy-examples.md)\.

## AWS Transfer Family resource\-based policies<a name="security_iam_service-with-iam-resource-based-policies"></a>

Resource\-based policies are JSON policy documents that specify what actions a specified principal can perform on the AWS Transfer Family resource and under what conditions\. Amazon S3 supports resource\-based permissions policies for Amazon S3 *buckets*\. Resource\-based policies let you grant usage permission to other accounts on a per\-resource basis\. You can also use a resource\-based policy to allow an AWS service to access your Amazon S3 *buckets*\.

To enable cross\-account access, you can specify an entire account or IAM entities in another account as the [principal in a resource\-based policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. Adding a cross\-account principal to a resource\-based policy is only half of establishing the trust relationship\. When the principal and the resource are in different AWS accounts, you must also grant the principal entity permission to access the resource\. Grant permission by attaching an identity\-based policy to the entity\. However, if a resource\-based policy grants access to a principal in the same account, no additional identity\-based policy is required\. For more information, see [How IAM roles differ from resource\-based policies ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)in the *AWS Identity and Access Management User Guide*\.

The Amazon S3 service supports only one type of resource\-based policy called a **bucket* policy*, which is attached to a *bucket*\. This policy defines which principal entities \(accounts, users, roles, and federated users\) can perform actions on the object\.

### Examples<a name="security_iam_service-with-iam-resource-based-policies-examples"></a>



To view examples of AWS Transfer Family resource\-based policies, see [AWS Transfer Family tag\-based policy examples](security_iam_tag-based-policy-examples.md)\.

## Authorization based on AWS Transfer Family tags<a name="security_iam_service-with-iam-tags"></a>

You can attach tags to AWS Transfer Family resources or pass tags in a request to AWS Transfer Family\. To control access based on tags, you provide tag information in the [condition element](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) of a policy using the `transfer:ResourceTag/key-name`, `aws:RequestTag/key-name`, or `aws:TagKeys` condition keys\. For information about how to use tags to control access to AWS Transfer Family resources, see [AWS Transfer Family tag\-based policy examples](security_iam_tag-based-policy-examples.md)\.

## AWS Transfer Family IAM roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using temporary credentials with AWS Transfer Family<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS STS API operations such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\.

AWS Transfer Family supports using temporary credentials\.
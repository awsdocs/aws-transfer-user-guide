# Working with custom hostnames<a name="requirements-dns"></a>

Your *server host name* is the hostname that your users enter in their clients when they connect to your server\. You can use a custom domain that you have registered for your server hostname when you work with AWS Transfer Family\. For example, you might use a custom hostname like `mysftpserver.mysubdomain.domain.com`\.

To redirect traffic from your registered custom domain to your server endpoint, you can use Amazon Route 53 or any Domain Name System \(DNS\) provider\. Route 53 is the DNS service that AWS Transfer Family natively supports\.

**Topics**
+ [Use Amazon Route 53 as your DNS provider](#requirements-use-r53)
+ [Use other DNS providers](#requirements-use-alt-dns)
+ [Custom hostnames for non\-console created servers](#tag-custom-hostname-cdk)

On the console, you can choose one of these options for setting up a custom hostname:
+ **Amazon Route 53 DNS alias** – if the hostname that you want to use is registered with Route 53\. You can then enter the hostname\.
+ **Other DNS** – if the hostname that you want to use is registered with another DNS provider\. You can then enter the hostname\.
+ **None** – to use the server's endpoint and not use a custom hostname\.

You set this option when you create a new server or edit the configuration of an existing server\. For more information about creating a new server, see [Step 2: Create an SFTP\-enabled server](getting-started.md#getting-started-server)\. For more information about editing the configuration of an existing server, see [Edit server details](edit-server-config.md)\.

For more details about using your own domain for the server hostname and how AWS Transfer Family uses Route 53, see the following sections\.

## Use Amazon Route 53 as your DNS provider<a name="requirements-use-r53"></a>

When you create a server, you can use Amazon Route 53 as your DNS provider\. Before you use a domain with Route 53, you register the domain\. For more information, see [How Domain Registration Works](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-domain-registration.html) in the *Amazon Route 53 Developer Guide*\.

When you use Route 53 to provide DNS routing to your server, AWS Transfer Family uses the custom hostname that you entered to extract its hosted zone\. When AWS Transfer Family extracts a hosted zone, three things can happen:

1. If you're new to Route 53 and don't have a hosted zone, AWS Transfer Family adds a new hosted zone and a `CNAME` record\. The value of this `CNAME` record is the endpoint hostname for your server\. A *CNAME* is an alternate domain name\.

1. If you have a hosted zone in Route 53 without any `CNAME` records, AWS Transfer Family adds a `CNAME` record to the hosted zone\.

1. If the service detects that a `CNAME` record already exists in the hosted zone, you see an error indicating that a `CNAME` record already exists\. In this case, change the value of the `CNAME` record to the hostname of your server\. 
**Note**  
If this step is part of a server creation workflow, your server is successfully created and your custom hostname is set to **None**\.

For more information about hosted zones in Route 53, see [Hosted Zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/CreatingHostedZone.html) in the *Amazon Route 53 Developer Guide*\.

## Use other DNS providers<a name="requirements-use-alt-dns"></a>

When you create a server, you can also use DNS providers other than Amazon Route 53\. If you use an alternate DNS provider, make sure that traffic from your domain is directed to your server endpoint\.

To do so, set your domain to the endpoint hostname for the server\. An endpoint hostname looks like this in the console: 

`serverid.server.transfer.region.amazonaws.com`

## Custom hostnames for non\-console created servers<a name="tag-custom-hostname-cdk"></a>

When you create a server using AWS Cloud Development Kit \(AWS CDK\) or through the CLI, you must add a tag if you want that server to have a custom hostname\. When you create a Transfer Family server by using the console, the tagging is done automatically\.

**Note**  
You also need to create a DNS record to redirect traffic from your domain to your server endpoint\.

Use the following keys for your custom hostname:

**Important**  
You cannot add the tags described in this section in an AWS CloudFormation template\. AWS CloudFormation does not allow keys for tags that begin with `aws:`\.
+ Add `aws:transfer:customHostname` to display the custom hostname in the console\.
+ If you are using Route 53 as your DNS provider, add `aws:transfer:route53HostedZoneId`\. This tag links the custom hostname to your Route 53 Hosted Zone ID\.

To add the custom hostname, issue the following CLI command\.

```
aws transfer tag-resource --arn server-ARN:server/server-ID --tags Key=aws:transfer:customHostname,Value="custom-host-name"
```

For example:

```
aws transfer tag-resource --arn arn:aws:transfer:us-east-1:111122223333:server/s-1234567890abcdef0 --tags Key=aws:transfer:customHostname,Value="abc.example.com"
```

If you are using Route 53, issue the following command to link your custom hostname to your Route 53 Hosted Zone ID\.

```
aws transfer tag-resource --arn server-ARN:server/server-ID --tags Key=aws:transfer:route53HostedZoneId,Value=HOSTED-ZONE-ID
```

For example:

```
aws transfer tag-resource --arn arn:aws:transfer:us-east-1:111122223333:server/s-1234567890abcdef0 --tags Key=aws:transfer:route53HostedZoneId,Value=ABCDE1111222233334444
```

Assuming the sample values from the previous command, run the following command to view your tags:

```
aws transfer list-tags-for-resource --arn arn:aws:transfer:us-east-1:111122223333:server/s-1234567890abcdef0
```

```
"Tags": [
   {
      "Key": "aws:transfer:route53HostedZoneId",
      "Value": "/hostedzone/ABCDE1111222233334444"
   },
   {
      "Key": "aws:transfer:customHostname",
      "Value": "abc.example.com"
   }
 ]
```

**Note**  
 Your public, hosted zones and their IDs are available on Amazon Route 53\.   
Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.
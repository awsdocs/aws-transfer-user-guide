# Add a web application firewall<a name="web-application-firewall"></a>

AWS WAF is a web application firewall that helps protect web applications and APIs from attacks\. You can use it to configure a set of rules known as a *web access control list* \(web ACL\) that allow, block, or count web requests based on customizable web security rules and conditions that you define\. For more information, see [Using AWS WAF to protect your APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-aws-waf.html)\.

**To add AWS WAF**

1. Open the API Gateway console at [https://console\.aws\.amazon\.com/apigateway/](https://console.aws.amazon.com/apigateway/)\.

1. In the **APIs** navigation pane, and then choose your custom identity provider template\.

1. Choose **Stages**\.

1. In the **Stages** pane, choose the name of the stage\.

1. In the **Stage Editor** pane, choose the **Settings** tab\.

1. Do one of the following:
   + Under **Web Application Firewall \(WAF\)**, for **Web ACL**, choose the web ACL that you want to associate with this stage\.
   + If the web ACL you need doesn't exist, you will need to create one by doing the following:

     1. Choose **Create Web ACL**\.

     1. On the AWS WAF service homepage, choose **Create web ACL**\.

     1. In **Web ACL details**, for **Name**, type the name of the web ACL\.

     1. In **Rules**, choose **Add rules**, then choose **Add my own rules and rule groups**\.

     1. For **Rule type**, choose IP set to identify a specific list of IP addresses\.

     1. For **Rule**, enter the name of the rule\.

     1. For **IP set**, choose an existing IP set\. To create an IP set, see [Creating an IP set](https://docs.aws.amazon.com/waf/latest/developerguide/waf-ip-set-creating.html)\.

     1. For **IP address to use as the originating address**, choose **IP address in header**\.

     1. For **Header field name**, enter `SourceIP`\.

     1. For **Position inside header**, choose **First IP address**\.

     1. For **Fallback for missing IP address**, choose **Match** or ** No Match** depending on how you want to handle an invalid \(or missing\) IP address in the header\.

     1. For **Action**, choose the action of the IP set\.

     1. For **Default web ACL action for requests that don't match any rules**, choose **Allow** or **Block** and then click **Next**\.

     1. For steps 4 and 5, choose **Next**\.

     1. In **Review and create**, review your choices, and then choose **Create web ACL**\.

1. Choose **Save Changes**\.

1. Choose **Resources**\.

1. For **Actions**, choose **Deploy API**\.

 For information on how secure AWS Transfer Family with AWS web application firewall, see [Securing AWS Transfer Family with AWS Application Firewall and Amazon API Gateway](http://aws.amazon.com/blogs/storage/securing-aws-transfer-family-with-aws-web-application-firewall-and-amazon-api-gateway/) 
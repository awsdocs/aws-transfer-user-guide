# Security in AWS Transfer Family<a name="security"></a>

Cloud security at AWS is the highest priority\. As an AWS customer, you benefit from a data center and network architecture that is built to meet the requirements of the most security\-sensitive organizations\.

Security is a shared responsibility between AWS and you\. The [shared responsibility model](http://aws.amazon.com/compliance/shared-responsibility-model/) describes this as security *of* the cloud and security *in* the cloud:

Third\-party auditors assess the security and compliance of AWS services as part of multiple AWS compliance programs, such as SOC, PCI, FedRAMP, and HIPAA\.

To learn whether AWS Transfer Family or other AWS services are within the scope of specific compliance programs, see [AWS Services in Scope by Compliance Program](http://aws.amazon.com/compliance/services-in-scope/)\. For general information, see [AWS Compliance Programs](http://aws.amazon.com/compliance/programs/)\.

You can download third\-party audit reports using AWS Artifact\. For more information, see [Downloading Reports in AWS Artifact](https://docs.aws.amazon.com/artifact/latest/ug/downloading-documents.html)\.

Your compliance responsibility when using AWS services is determined by the sensitivity of your data, your company's compliance objectives, and applicable laws and regulations\. AWS provides the following resources to help with compliance:
+ [Security and Compliance Quick Start Guides](http://aws.amazon.com/quickstart/?awsf.quickstart-homepage-filter=categories%23security-identity-compliance) – These deployment guides discuss architectural considerations and provide steps for deploying baseline environments on AWS that are security and compliance focused\.
+ [Architecting for HIPAA Security and Compliance on Amazon Web Services](https://docs.aws.amazon.com/whitepapers/latest/architecting-hipaa-security-and-compliance-on-aws/welcome.html) – This whitepaper describes how companies can use AWS to create HIPAA\-eligible applications\.
**Note**  
Not all AWS services are HIPAA eligible\. For more information, see the [HIPAA Eligible Services Reference](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/)\.
+ [AWS Compliance Resources](http://aws.amazon.com/compliance/resources/) – This collection of workbooks and guides might apply to your industry and location\.
+ [Evaluating Resources with Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html) in the *AWS Config Developer Guide* – The AWS Config service assesses how well your resource configurations comply with internal practices, industry guidelines, and regulations\.
+ [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html) – This AWS service provides a comprehensive view of your security state within AWS that helps you check your compliance with security industry standards and best practices\.
+ [AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html) – This AWS service helps you continuously audit your AWS usage to simplify how you manage risk and compliance with regulations and industry standards\.

This documentation helps you understand how to apply the shared responsibility model when using AWS Transfer Family\. The following topics show you how to configure AWS Transfer Family to meet your security and compliance objectives\. You also learn how to use other AWS services that help you to monitor and secure your AWS Transfer Family resources\.

**Topics**
+ [Data protection in AWS Transfer Family](data-protection.md)
+ [Identity and access management for AWS Transfer Family](security-iam.md)
+ [Logging and monitoring in AWS Transfer Family](logging-using-cloudtrail.md)
+ [Compliance validation for AWS Transfer Family](transfer-compliance.md)
+ [Resilience in AWS Transfer Family](disaster-recovery-resiliency.md)
+ [Infrastructure security in AWS Transfer Family](infrastructure-security.md)
+ [Add a web application firewall](web-application-firewall.md)
+ [Cross\-service confused deputy prevention](confused-deputy.md)
+ [AWS managed policies for AWS Transfer Family](security-iam-awsmanpol.md)
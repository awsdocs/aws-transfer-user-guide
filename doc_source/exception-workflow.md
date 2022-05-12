# Exception handling for a workflow<a name="exception-workflow"></a>

If any errors occur during a workflow's execution, the exception\-handling steps that you specified are executed\. You specify the error\-handling steps for a workflow in the same manner as you specify the workflow steps themselves\. For example, suppose that you've configured custom processing in nominal steps to validate incoming files\. If the file validation fails, an exception\-handling step can send an email to the administrator\.

The following example workflow contains one nominal step, to check whether the uploaded file is in CSV format, and then an exception\-handling step that sends an email in case the uploaded file is not in the CSV format\. To initiate the exception\-handling step, the AWS Lambda function in the nominal step must respond with `Status="FAILURE"`\. For more information about error handling in workflows, see [Use custom file\-processing steps](custom-step-details.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/workflow-exception-sample.png)
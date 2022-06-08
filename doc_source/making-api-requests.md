# Making API Requests<a name="making-api-requests"></a>

In addition to using the console, you can use the AWS Transfer Family API to programmatically configure and manage your servers\. This section describes the AWS Transfer Family operations, request signing for authentication and the error handling\. For information about the regions and endpoints available for Transfer Family, see [AWS Transfer Family Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*

**Note**  
You can also use the AWS SDKs when developing applications with Transfer Family;\. The AWS SDKs for Java, \.NET, and PHP wrap the underlying Transfer Family API, simplifying your programming tasks\. For information about downloading the SDK libraries, see [Sample Code Libraries](http://aws.amazon.com/code)\.

**Topics**
+ [Transfer Family required request headers](#request-headers)
+ [Transfer Family Request Inputs and Signing](#tf-request-structure)
+ [Error Responses](#RESTErrorResponses)
+ [Available Libraries](#using-libraries)

## Transfer Family required request headers<a name="request-headers"></a>

This section describes the required headers that you must send with every POST request to AWS Transfer Family\. You include HTTP headers to identify key information about the request including the operation you want to invoke, the date of the request, and information that indicates the authorization of you as the sender of the request\. Headers are case insensitive and the order of the headers is not important\.

The following example shows headers that are used in the [ListServers](https://docs.aws.amazon.com/transfer/latest/userguide/API_ListServers.html) operation\.

```
POST / HTTP/1.1
Host: transfer.us-east-1.amazonaws.com
x-amz-target: TransferService.ListServers
x-amz-date: 20220507T012034Z
Authorization: AWS4-HMAC-SHA256 Credential=AKIDEXAMPLE/20220507/us-east-1/transfer/aws4_request,
    SignedHeaders=content-type;host;x-amz-date;x-amz-target,
    Signature=13550350a8681c84c861aac2e5b440161c2b33a3e4f302ac680ca5b686de48de
Content-Type: application/x-amz-json-1.1
Content-Length: 17

{"MaxResults":10}
```

The following are the headers that must include with your POST requests to Transfer Family\. Headers shown below that begin with "x\-amz" are AWS\-specific headers\. All other headers listed are common header used in HTTP transactions\.


| Header | Description  | 
| --- | --- | 
|  Authorization  |  Authorization header is required\. The format is standard Sigv4 request signature, which is documented at [Signature Version 4 signing process](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html)\.  | 
| Content\-Type |  Use `application/x-amz-json-1.1` as the content type for all requests to Transfer Family\.  <pre>Content-Type: application/x-amz-json-1.1</pre>  | 
| Host |  Use the host header to specify the Transfer Family endpoint where you send your request\. For example, `transfer.us-east-1.amazonaws.com` is the endpoint for the US East \(Ohio\) region\. For more information about the endpoints available for Transfer Family, see [AWS Transfer Family Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transfer-service.html) in the *AWS General Reference*\. <pre>Host: transfer.region.amazonaws.com</pre>  | 
| x\-amz\-date |  You must provide the time stamp in either the HTTP `Date` header or the AWS `x-amz-date` header\. \(Some HTTP client libraries don't let you set the `Date` header\.\) When an `x-amz-date` header is present, the Transfer Family ignores any `Date` header during the request authentication\. The `x-amz-date` format must be ISO8601, in the YYYYMMDD'T'HHMMSS'Z' format\.  <pre>x-amz-date: YYYYMMDD'T'HHMMSS'Z'</pre>  | 
| x\-amz\-target |  This header specifies the version of the API and the operation that you are requesting\. The target header values are formed by concatenating the API version with the API name and are in the following format\.  <pre>x-amz-target: TransferService.operationName</pre> The *operationName* value \(for example `ListServers`\) can be found from the API list, [ListServers](https://docs.aws.amazon.com/transfer/latest/userguide/API_ListServers.html)\.  | 
| x\-amz\-security\-token | This header is required when credentials used to sign the request are temporary or session credentials \( for details, see [Using temporary credentials with AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_use-resources.html) in the IAM User Guide\. See [Add the signature to the HTTP request](https://docs.aws.amazon.com/genera/latest/gr/sigv4-add-signature-to-request.html) in the Amazon Web Services General Reference for more information\. | 

## Transfer Family Request Inputs and Signing<a name="tf-request-structure"></a>

All request inputs must be sent as part of JSON payload in request body\. For Actions in which all request fields are optional, for example `ListServers`, you still need to provide an empty JSON object in the request body, such as `{}`\. The structure of Transfer Family payload request/response is documented in existing the API reference, for example [DescribeServer](https://docs.aws.amazon.com/transfer/latest/API_DescribeServer.html)\. 

Transfer Family supports authentication using [AWS Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html)\. For details about how to sign AWS API requests, see [Signing AWS API requests](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_request.html)\.

## Error Responses<a name="RESTErrorResponses"></a>

When there is an error, the response header information contains:
+ Content\-Type: application/x\-amz\-json\-1\.1 
+ An appropriate `4xx` or `5xx` HTTP status code

The body of an error response contains information about the error that occurred\. The following sample error response shows the output syntax of response elements common to all error responses\.

```
{
    "__type": "String",
    "Message": "String", <!-- Message is lowercase in some instances -->
    "Resource": String,
    "ResourceType": String
    "RetryAfterSeconds": String
}
```

 The following table explains the JSON error response fields shown in the preceding syntax\.

**\_\_type**  
One of the exceptions from a Transfer Family API call\.   
*Type*: String

**Message** or **message**  
One of the operation error code messages\.  
Some exceptions use `message`, and others use `Message`\. You can check the code for your interface to determine the proper case\. Alternatively, you can test each option to see which works\.
*Type*: String

**Resource**  
The resource for which the error is invoked\. For example, if you try to create a user that already exists, the `Resource` is the user name for the existing user\.  
*Type*: String

**ResourceType**  
The resource type for which the error is invoked\. For example, if you try to create a user that already exists, the `ResourceType` is `User`\.  
*Type*: String

**RetryAfterSeconds**  
The number of seconds to wait before retrying the command\.  
*Type*: String

### Error Response Examples<a name="RESTErrorResponsesExamples"></a>

 The following JSON body is returned if you use the DescribeServer API and specify a server that does not exist\.

```
{
  "__type": "ResourceNotFoundException",
  "Message": "Unknown server",
  "Resource": "s-11112222333344444",
  "ResourceType": "Server"
}
```

The following JSON body is returned if executing an API causes throttling to occur\.

```
{
   "__type":"ThrottlingException",
   "RetryAfterSeconds":"1"
}
```

The following JSON body is returned if you use the `CreateServer` API and you do not have sufficient permissions to create a Transfer Family server\.

```
{
  "__type": "AccessDeniedException",
  "Message": "You do not have sufficient access to perform this action."
}
```

The following JSON body is returned if you use the `CreateUser` API and specify a user that already exists\.

```
{  
  "__type": "ResourceExistsException",  
  "Message": "User already exists",
  "Resource": "Alejandro-Rosalez",
  "ResourceType": "User"
}
```

## Available Libraries<a name="using-libraries"></a>

AWS provides libraries, sample code, tutorials, and other resources for software developers who prefer to build applications using language\-specific APIs instead of the command\-line tools and Query API\. These libraries provide basic functions \(not included in the APIs\), such as request authentication, request retries, and error handling so that it is easier to get started\. See [Tools to Build on AWS](https://aws.amazon.com/tools/?id=docs_gateway)

For libraries and sample code in all languages, see [Sample Code & Libraries](http://aws.amazon.com/code)\.
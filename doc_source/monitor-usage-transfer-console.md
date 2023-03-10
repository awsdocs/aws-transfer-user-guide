# Monitoring usage in the console<a name="monitor-usage-transfer-console"></a>

 You can get information about your server's metrics on its **Server details** page\. This provides you with a single place to monitor your file\-transfers workloads\. You can track how many files you have exchanged with your partners and closely track their usage using a centralized dashboard\. For details, see [View server details](configuring-servers-view-info.md)\. The following table describes the metrics available for Transfer Family\. 

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transfer/latest/userguide/monitor-usage-transfer-console.html)

 The **Monitoring** section contains four, individual graphs\. These graphs show the bytes in, bytes out, files in, and files out\. 

![\[The Monitoring console section showing the BytesIn, BytesOut, FilesIn, and FilesOut graphs.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/metrics.png)

For servers that have the AS2 protocol enabled, there is an **AS2 Monitoring** section below the **Monitoring** information\. This section contains details for the number of inbound messages, both successful and failed\.

![\[The AS2 Monitoring console section showing the InboundMessages, and InboundMessagesFailed details.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/as2-metrics-inbound.png)

 To open the selected graph in its own window, choose the expand icon \(![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/expand.png)\)\. You can also click a graph's vertical ellipsis icon \(![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/vertical-ellipsis.png)\) to open a dropdown menu with the following items: 
+ **Enlarge** – Opens the selected graph in its own window\.
+ **Refresh** – Reloads the graph with the most recent data\.
+ **View in metrics** – Opens the corresponding metrics details in Amazon CloudWatch\.
+ **View logs** – Opens the corresponding log group in CloudWatch\.
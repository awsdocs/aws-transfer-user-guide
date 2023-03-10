# Monitoring AS2 usage<a name="as2-monitoring"></a>

You can monitor AS2 activity using Amazon CloudWatch and AWS CloudTrail\. To view other Transfer Family server metrics, see [Monitoring Transfer Family usage](monitoring.md)


**AS2 Metrics**  

| Metric | Description | 
| --- | --- | 
| InboundMessage |  The total number of AS2 messages successfully received from a trading partner\. Units: Count Period: 5 minutes  | 
| InboundFailedMessage |  The total number of AS2 messages that were unsuccessfully received from a trading partner\. That is, a trading partner sent a message, but the Transfer Family server was not able to successfully process it\. Units: Count Period: 5 minutes  | 
| OutboundMessage |  The total number of AS2 messages successfully sent from the Transfer Family server to a trading partner\. Units: Count Period: 5 minute  | 
| OutboundFailedMessage |  The total number of AS2 messages that were unsuccessfully sent to a trading partner\. That is, they were sent from the Transfer Family server, but were not successfully received by the trading partner\. Units: Count Period: 5 minutes  | 
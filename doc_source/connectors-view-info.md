# View connector details<a name="connectors-view-info"></a>

You can find a list of details and properties for an individual AWS Transfer Family connector\. Connector properties include URL, roles, profiles, MDNs, tags, and monitoring metrics\.

**To view connector details**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. In the navigation pane, choose **Connectors**\. 

1. Choose the identifier in the **Connector ID** column to see the **Connector details** page, shown following\.

   You can change the connector's properties on this page by choosing **Edit**\.  
![\[Shows the details for the selected connector.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/as2-connector-details.png)
**Note**  
You can get much of this information, albeit in a different format, by running the following AWS CLI command:  

   ```
   aws transfer describe-connector --connector-id your-connector-id
   ```
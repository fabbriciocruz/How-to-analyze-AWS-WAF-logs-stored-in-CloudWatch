## How to analyze AWS WAF logs stored in CloudWatch

1. Enable WAF ACL login to CloudWatch

2. Open the CloudWatch console, go to Logs Insights and select the log group for the WAF ACL

3. The following shows basic queries

    > Tip: Select the time range at the top right corner of the CloudWatch console

* Show the total number of records (request) on a spcific time range

    ```sh
    fields @timestamp, @message
    ```
* Show the total number of records (request) on a spcific time range - sort by timestamp - limit to 20 request to show
    ```sh 
    fields @timestamp, @message
    | sort @timestamp desc
    | limit 20
    ```
* Search if the string exists (In the example we're searching for the string "EXCLUDED_AS_COUNT" - All requests that match to a WAF ACL Rule which has been configured as COUNT will be tagged with "EXCLUDED_AS_COUNT")
    > Reference: Examples: Match substrings from [CloudWatch Logs Insights query syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax.html)
    ```sh
    fields @message as f1
    | filter f1 like "EXCLUDED_AS_COUNT"
    ```
    
## References

* Best Doc !! [What are my options to analyze AWS WAF logs stored in CloudWatch or Amazon S3?](https://aws.amazon.com/premiumsupport/knowledge-center/waf-analyze-logs-stored-cloudwatch-s3/?nc1=h_ls)
* [How are the metrics and logs formatted for the count rule action in AWS WAF?](https://aws.amazon.com/premiumsupport/knowledge-center/waf-analyze-count-action-rules/)

# Using the AWS Schema Conversion Tool with the AWS Database Migration Service<a name="CHAP_DMSIntegration"></a>

## Using an AWS SCT Replication Agent with AWS DMS<a name="CHAP_DMSIntegration.ReplicationAgent"></a>

For very large database migrations, you can use a AWS SCT replication agent to copy data from your on\-premises database to Amazon S3 or an Amazon Snowball device\. The replication agent works in conjunction with AWS DMS, and the replication agent can work in the background while AWS SCT is closed\. 

When working with Amazon Snowball, the AWS SCT agent extracts data to the Amazon Snowball device\. The device is then sent to AWS and the data is loaded to an Amazon S3 bucket\. During this time, the AWS SCT agent continues to run\. The agent then takes the data on Amazon S3 and copies the data to the target endpoint\.

For more information, see the [ AWS DMS documentation](http://docs.aws.amazon.com/dms/latest/userguide/CHAP_LargeDBs.html)\.
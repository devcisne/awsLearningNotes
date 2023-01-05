# AWS CloudTrail

AWS CloudTrail is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

CloudTrail is enabled on your AWS account when you create it. When activity occurs in your AWS account, that activity is recorded in a CloudTrail event. You can easily view recent events in the CloudTrail console by going to Event history. For an ongoing record of activity and events in your AWS account, create a trail.

Visibility into your AWS account activity is a key aspect of security and operational best practices. You can use CloudTrail to view, search, download, archive, analyze, and respond to account activity across your AWS infrastructure. You can identify who or what took which action, what resources were acted upon, when the event occurred, and other details to help you analyze and respond to activity in your AWS account. Optionally, you can enable AWS CloudTrail Insights on a trail to help you identify and respond to unusual activity.

---

## How CloudTrail works

Event history allows you to view, search, and download the past 90 days of activity in your AWS account. In addition, you can create a CloudTrail trail to archive, analyze, and respond to changes in your AWS resources. A trail is a configuration that enables delivery of events to an Amazon S3 bucket that you specify. You can also deliver and analyze events in a trail with Amazon CloudWatch Logs and Amazon EventBridge. You can create a trail with the CloudTrail console, the AWS CLI, or the CloudTrail API.

You can create two types of trails for an AWS account:

- A trail that applies to all regions

  When you create a trail that applies to all regions, CloudTrail records events in each region and delivers the CloudTrail event log files to an S3 bucket that you specify. If a region is added after you create a trail that applies to all regions, that new region is automatically included, and events in that region are logged. Because creating a trail in all regions is a recommended best practice, so you capture activity in all regions in your account, an all-regions trail is the default option when you create a trail in the CloudTrail console. You can only update a single-region trail to log all regions by using the AWS CLI.

- A trail that applies to one region

  When you create a trail that applies to one region, CloudTrail records the events in that region only. It then delivers the CloudTrail event log files to an Amazon S3 bucket that you specify. You can only create a single-region trail by using the AWS CLI. If you create additional single trails, you can have those trails deliver CloudTrail event log files to the same Amazon S3 bucket or to separate buckets. This is the default option when you create a trail using the AWS CLI or the CloudTrail API.

You can change the configuration of a trail after you create it, including whether it logs events in one region or all regions. To change a single-region trail to an all-region trail, or vice-versa, you must run the AWS CLI update-trail command. You can also change whether it logs data or CloudTrail Insights events. Changing whether a trail logs events in one region or in all regions affects which events are logged.

By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE). You can also choose to encrypt your log files with an AWS Key Management Service (AWS KMS) key. You can store your log files in your bucket for as long as you want. You can also define Amazon S3 lifecycle rules to archive or delete log files automatically. If you want notifications about log file delivery and validation, you can set up Amazon SNS notifications.

CloudTrail publishes log files multiple times an hour, about every five minutes. These log files contain API calls from services in the account that support CloudTrail.

---

## What are CloudTrail events?

An event in CloudTrail is the record of an activity in an AWS account. This activity can be an action taken by a user, role, or service that is monitorable by CloudTrail. CloudTrail events provide a history of both API and non-API account activity made through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. There are three types of events that can be logged in CloudTrail: management events, data events, and CloudTrail Insights events. By default, trails log management events, but not data or Insights events.
All event types use a CloudTrail JSON log format.

### What are management events?

Management events provide information about management operations that are performed on resources in your AWS account. These are also known as control plane operations. e.g:

- Configuring security (for example, AWS Identity and Access Management AttachRolePolicy API operations).

- Registering devices (for example, Amazon EC2 CreateDefaultVpc API operations).

Management events can also include non-API events that occur in your account. For example, when a user signs in to your account, CloudTrail logs the ConsoleLogin event.

### What are data events?

Data events provide information about the resource operations performed on or in a resource. These are also known as data plane operations. Data events are often high-volume activities.e.g:

- Amazon S3 object-level API activity (for example, GetObject, DeleteObject, and PutObject API operations) on buckets and objects in buckets
- AWS Lambda function execution activity (the Invoke API)

Data events are not logged by default when you create a trail. To record CloudTrail data events, you must explicitly add to a trail the supported resources or resource types for which you want to collect activity.

### What are Insights events?

CloudTrail Insights events capture unusual API call rate or error rate activity in your AWS account. If you have Insights events enabled, and CloudTrail detects unusual activity, Insights events are logged to a different folder or prefix in the destination S3 bucket for your trail. You can also see the type of insight and the incident time period when you view Insights events on the CloudTrail console. Insights events provide relevant information, such as the associated API, error code, incident time, and statistics, that help you understand and act on unusual activity.

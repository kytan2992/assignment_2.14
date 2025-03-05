# Assignment 2.14
## Does SNS guarantee exactly once delivery to subscribers?

No, SNS guarantees at least once delivery to its subscribers, meaning that in some cases, messages might be delivered multiple times, especially in the event of network issues, retries, or failures in the delivery process.

## What is the purpose of the Dead-letter Queue (DLQ)? This is a feature available to SQS/SNS/EventBridge.

It allows you to capture and handle messages that can't be successfully processed by their respective consumers or targets. The DLQ acts as a "safety net" for messages that fail to be delivered or processed, providing a way to isolate and troubleshoot those failed messages.

## How would you enable a notification to your email when messages are added to the DLQ?

You can use Amazon SNS (Simple Notification Service) in combination with the DLQ.
  - Create an SNS topic
  - Subscribe email to SNS topic
  - Configure DLQ to associate it with SNS topic
  - Set the Redrive Policy for the main queue to move messages to the DLQ when processing fails
  - Create a Cloudwatch alarm to trigger when number of messages in DLQ exceed zero

This setup makes it so that when messages are added to your DLQ (either due to processing failures or other issues), CloudWatch will trigger the alarm, which in turn will notify you via the SNS topic. This will send an email to your subscribed address whenever there is a change in the DLQ, such as messages being added.

---
title: Creating a Subscription and Handling Webhooks
---
This document will cover the process of creating a subscription for work item updates and handling the subsequent webhook events. We'll cover:

1. Setting up a webhook subscription
2. Processing incoming webhook requests
3. Handling updated work items
4. Syncing assignee information with Sentry.

Technical document: <SwmLink doc-title="Creating a Subscription and Handling Webhooks">[Creating a Subscription and Handling Webhooks](/.swm/creating-a-subscription-and-handling-webhooks.03pw19q1.sw.md)</SwmLink>

# [Setting up a Webhook Subscription](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/03pw19q1#creating-a-subscription)

The process begins with setting up a webhook subscription for work item updates. This involves sending a request to the VSTS API to create a subscription. The subscription specifies the event type ('workitem.updated'), the consumer ('webHooks'), and the URL to be called when the event occurs. This URL is where the webhook will send POST requests whenever a work item is updated.

# [Processing Incoming Webhook Requests](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/03pw19q1#handling-the-post-request)

When a work item is updated, a POST request is sent to the webhook URL. This request contains data about the event, including the event type and external ID. The system processes this request by extracting the event type and verifying the webhook secret to ensure the request is legitimate. If the event type is 'workitem.updated', the system proceeds to handle the updated work item.

# [Handling Updated Work Items](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/03pw19q1#handling-updated-work-item)

Once the system verifies that the event type is 'workitem.updated', it processes the data from the updated work item. This involves extracting necessary information such as the work item ID, project ID, assigned user, and any status changes. This information is crucial for keeping track of the work item's progress and ensuring that the right people are notified of any updates.

# [Syncing Assignee Information with Sentry](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/03pw19q1#syncing-group-assignee)

The final step involves syncing the assignee information with Sentry. This is done by parsing the email of the assigned user and calling a function to sync the assignee information. This ensures that the work item is correctly assigned to the right user in Sentry, allowing for seamless integration and tracking of work items across platforms.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

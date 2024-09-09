---
title: Processing Attachments and Events
---
This document will cover the process of handling attachments and events, focusing on user reports. The steps include:

1. Processing the initial message
2. Saving the user report
3. Converting the report to feedback
4. Creating a feedback issue.

Technical document: <SwmLink doc-title="Processing Attachments and Events">[Processing Attachments and Events](/.swm/processing-attachments-and-events.7ddcc2b6.sw.md)</SwmLink>

# [Processing the Initial Message](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/7ddcc2b6#processing-attachments-and-events)

The process begins with handling the initial message, which could be an attachment, event, or user report. The system identifies the type of message and fetches the associated project. For user reports, the system extracts the feedback and prepares it for further processing.

# [Saving the User Report](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/7ddcc2b6#processing-user-reports)

Once the user report is identified, the system attempts to save it. This involves extracting the feedback payload from the message and ensuring it is valid. If the report is invalid or an error occurs, the system logs the issue and stops further processing. Valid reports are saved for conversion into feedback events.

# [Converting to Feedback](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/7ddcc2b6#shimming-to-feedback)

After saving the user report, the system converts it into a feedback event. This step involves extracting relevant information from the user report and any associated events. The goal is to create a comprehensive feedback event that can be used to generate actionable insights.

# [Creating Feedback Issue](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/7ddcc2b6#creating-feedback-issues)

The final step is creating a feedback issue from the feedback event. The system checks if the feedback should be filtered and processes the event data to ensure it is valid. It then produces the occurrence to Kafka and tracks the outcome. This step ensures that the feedback is actionable and not spam, and notifies the relevant parties.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

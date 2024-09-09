---
title: Processing Occurrence Groups
---
This document will cover the process of processing occurrence groups, which includes:

1. Handling incoming messages
2. Processing status change messages
3. Processing occurrence messages
4. Creating or updating groups based on occurrences.

Technical document: <SwmLink doc-title="Processing Occurrence Groups">[Processing Occurrence Groups](/.swm/processing-occurrence-groups.dn4fenui.sw.md)</SwmLink>

# [Handling Incoming Messages](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dn4fenui#handling-status-change-messages)

The process begins by handling incoming messages and determining their type. If the message is a status change, it updates the relevant group. For occurrence messages, it extracts necessary data, sets metrics, and processes the event and issue occurrence. This ensures that the event ID matches and saves the occurrence data. Finally, it checks if a new group should be created or an existing one should be updated.

# [Processing Status Change Messages](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dn4fenui#processing-status-change-messages)

When a status change message is received, the system retrieves the necessary data, such as the project and organization, and updates the status of the relevant group. This step ensures that the status change is correctly processed and associated with the appropriate group. Metrics and logs are also updated to track the status change process.

# [Processing Occurrence Messages](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dn4fenui#handling-occurrence-messages)

For occurrence messages, the system extracts necessary data from the message and sets various tags for metrics and transaction tracking. It then checks if the group type allows ingestion for the organization. Depending on the presence of event data and whether spans are buffered, it either creates or processes events and issue occurrences or looks up and processes issue occurrences.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

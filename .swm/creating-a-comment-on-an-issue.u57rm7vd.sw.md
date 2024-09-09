---
title: Creating a Comment on an Issue
---
This document will cover the process of creating a comment on an issue. We'll cover:

1. Extracting the comment text
2. Formatting the comment with user attribution
3. Updating the work item with the new comment.

Technical document: <SwmLink doc-title="Creating a Comment Flow">[Creating a Comment Flow](/.swm/creating-a-comment-flow.dhft996i.sw.md)</SwmLink>

# [Extracting the Comment Text](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dhft996i#creating-a-comment)

The first step in creating a comment is to extract the text of the comment from the provided data. This involves retrieving the comment text from the `group_note` data. The `group_note` contains various pieces of information about the comment, including the text itself. Extracting this text is essential as it forms the basis of the comment that will be added to the issue.

# [Formatting the Comment with User Attribution](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dhft996i#creating-a-comment)

Once the comment text is extracted, it needs to be formatted to include information about the user who made the comment. This step is crucial for maintaining context and accountability. The system adds user attribution by quoting the comment and appending the user's details. This ensures that anyone reading the comment knows who made it, which is important for tracking and communication purposes.

# [Updating the Work Item with the New Comment](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/dhft996i#creating-a-comment)

After the comment has been formatted with user attribution, the next step is to update the relevant work item with this new comment. This involves using a client that handles communication with the external system where the work item resides. The client ensures that the comment is correctly added to the issue, making it visible to all users who have access to the work item. This step is essential for keeping the issue up-to-date with the latest comments and ensuring that all team members are aware of the ongoing discussions.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

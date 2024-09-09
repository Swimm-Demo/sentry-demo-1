---
title: Bulk Mutating Issue Attributes
---
This document will cover the process of bulk mutating issue attributes, which includes:

1. Initiating the bulk mutation request
2. Validating and filtering the issues
3. Applying the updates to the issues.

Technical document: <SwmLink doc-title="Bulk Mutating Issue Attributes">[Bulk Mutating Issue Attributes](/.swm/bulk-mutating-issue-attributes.3na6spk0.sw.md)</SwmLink>

# [Initiating the Bulk Mutation Request](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3na6spk0#bulk-mutate-issues)

The process begins when a user initiates a bulk mutation request. This request includes a list of issue IDs and a JSON object containing the new attributes to be applied. The user can specify various attributes to be updated, such as status, assignment, and visibility. This step is crucial as it allows users to efficiently manage multiple issues at once, saving time and ensuring consistency across similar issues.

# [Validating and Filtering the Issues](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3na6spk0#applying-updates-to-groups)

Once the bulk mutation request is received, the system validates and filters the issues based on the provided IDs. This involves checking if the issues exist and if the user has the necessary permissions to modify them. The system also ensures that the data provided in the JSON object is valid. This step is important to prevent unauthorized or incorrect modifications, ensuring the integrity and security of the issue management process.

# [Applying Updates to the Issues](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3na6spk0#applying-updates-to-groups)

After validation, the system applies the updates to the filtered issues. This includes changing the status, priority, and resolution details as specified in the request. The system handles special cases, such as resolving issues in the next release or in a specific commit. This step ensures that the issues are updated accurately and according to the user's specifications, improving the efficiency of issue management and resolution.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

---
title: Backfilling Seer Grouping Records
---
This document will cover the process of backfilling Seer grouping records, which includes:

1. Initializing the backfill
2. Updating groups with similarity data
3. Deleting old Seer grouping records
4. Extracting event data from the nodestore.

Technical document: <SwmLink doc-title="Backfilling Seer Grouping Records">[Backfilling Seer Grouping Records](/.swm/backfilling-seer-grouping-records.jheyhchq.sw.md)</SwmLink>

# [Initializing the Backfill](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jheyhchq#initialization-process)

The backfill process begins by setting up the necessary project and group information. This involves retrieving the project and initializing the last processed group and project indices. This step ensures that the system knows where to start the backfill process and maintains consistency in the data being processed.

# [Updating Groups with Similarity Data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jheyhchq#updating-groups)

In this step, the groups are updated with new similarity data received from Seer. The system filters the groups and updates their metadata with the new similarity information. This ensures that the groups have the most up-to-date similarity data, which is crucial for accurate grouping and analysis.

# [Deleting Old Seer Grouping Records](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jheyhchq#deleting-seer-grouping-records)

After updating the groups, the old Seer grouping records are deleted to ensure data consistency. This step removes outdated similarity data from the project's group metadata, preventing any potential conflicts or inaccuracies in future analyses.

# [Extracting Event Data from Nodestore](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jheyhchq#extracting-and-processing-event-data)

The final step involves extracting event data from the nodestore. The system retrieves the event data and processes it to generate new grouping records. This step is essential for updating the project's metadata with the latest event information, ensuring that the grouping records are accurate and up-to-date.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

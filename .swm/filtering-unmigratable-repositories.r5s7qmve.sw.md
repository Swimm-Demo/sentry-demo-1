---
title: Filtering Unmigratable Repositories
---
This document will cover the process of filtering unmigratable repositories, which includes:

1. Retrieving all repositories associated with an organization
2. Collecting identifiers of repositories to exclude
3. Returning a list of repositories that are not in the exclusion list.

Technical document: <SwmLink doc-title="Filtering Unmigratable Repositories">[Filtering Unmigratable Repositories](/.swm/filtering-unmigratable-repositories.bkp48cpp.sw.md)</SwmLink>

# [Retrieving all repositories](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/bkp48cpp#retrieving-repositories)

The first step in filtering unmigratable repositories is to retrieve all repositories associated with an organization. This involves accessing the repository service to get a list of repositories linked to the organization. This step ensures that we have a comprehensive list of all repositories before any filtering is applied.

# [Collecting identifiers to exclude](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/bkp48cpp#filtering-unmigratable-repositories)

Next, we collect the identifiers of repositories that should be excluded from the list. These identifiers are gathered from a predefined set of repositories that have already been migrated. By identifying these repositories, we can ensure that they are not included in the final list of repositories to be migrated.

# [Returning non-excluded repositories](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/bkp48cpp#filtering-unmigratable-repositories)

Finally, we return a list of repositories that are not in the exclusion list. This is done by comparing the identifiers of all retrieved repositories with the identifiers of the excluded repositories. Only those repositories whose identifiers are not in the exclusion list are included in the final list. This ensures that the returned list contains only those repositories that are eligible for migration.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

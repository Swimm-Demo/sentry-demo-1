---
title: Post-Installation Tasks
---
This document will cover the post-installation tasks for the Sentry integration, which includes:

1. Retrieving repositories associated with the organization
2. Applying migration tasks to each repository.

Technical document: <SwmLink doc-title="Post-Installation Tasks">[Post-Installation Tasks](/.swm/post-installation-tasks.pcdtohea.sw.md)</SwmLink>

# [Retrieving Repositories](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/pcdtohea#get_repositories)

After the installation of an integration, the first step is to gather all the repositories linked to the organization. This is done to ensure that the integration has access to all relevant repositories. The system fetches the list of repositories from the VSTS client, handling any potential errors and formatting the repository data into a list of dictionaries containing the repository name and identifier. This step is crucial for retrieving the necessary repository information needed for further processing.

# [Applying Migration Tasks](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/pcdtohea#post_install)

Once the repositories are retrieved, the next step is to apply a migration task to each repository. This ensures that each repository is properly set up and any necessary data migration is performed. The migration task involves updating the repository settings and moving any required data to ensure compatibility with the new integration. This step is essential to make sure that the integration works seamlessly with the existing repositories and that all data is correctly migrated.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

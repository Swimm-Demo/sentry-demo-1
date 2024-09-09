---
title: Build Integration Process
---
The Build Integration Process involves several steps to initialize an integration by gathering necessary data and constructing an integration object. This document will cover:

1. Collecting essential data
2. Creating an integration object
3. Checking for an active integration model
4. Setting up a new subscription if needed.

Technical document: <SwmLink doc-title="Build Integration Process">[Build Integration Process](/.swm/build-integration-process.jowgncub.sw.md)</SwmLink>

# [Collecting Essential Data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jowgncub#building-integration)

The process begins by collecting essential data such as OAuth details, user information, and account specifics. This data is crucial for authenticating and identifying the user and their account. For example, OAuth data includes tokens that allow secure access to the user's account, while user information and account details help in identifying the specific user and their associated account within the system.

# [Creating an Integration Object](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jowgncub#building-integration)

Once the essential data is collected, an integration object is created. This object includes the account name, external ID, domain name, and scopes. The integration object serves as a structured representation of the integration, encapsulating all necessary details required for further processing. For instance, the external ID uniquely identifies the account, while the domain name and scopes define the permissions and access levels.

# [Checking for Active Integration Model](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jowgncub#building-integration)

The next step is to check if there is already an active integration model. This involves querying the database to see if an integration with the same external ID and provider already exists. If an active integration model is found, it means the integration is already set up and ready to use. This step ensures that duplicate integrations are not created, maintaining data integrity and avoiding unnecessary resource usage.

# [Setting Up a New Subscription if Needed](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/jowgncub#building-integration)

If no active integration model is found, a new subscription is set up. This involves creating a new record in the database with the integration details. Setting up a new subscription ensures that the integration is properly initialized and ready to use. This step is crucial for enabling the integration's functionality, allowing users to start using the integration features immediately.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

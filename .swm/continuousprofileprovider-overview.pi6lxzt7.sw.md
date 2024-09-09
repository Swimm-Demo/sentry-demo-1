---
title: ContinuousProfileProvider Overview
---
This document will cover the ContinuousProfileProvider feature, which includes:

1. Initializing necessary hooks
2. Fetching profiling data
3. Updating the state with fetched profiles.

Technical document: <SwmLink doc-title="ContinuousProfileProvider Overview">[ContinuousProfileProvider Overview](/.swm/continuousprofileprovider-overview.ygr8cpkj.sw.md)</SwmLink>

# [Initializing necessary hooks](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/ygr8cpkj#continuousprofileprovider)

The ContinuousProfileProvider function begins by initializing several hooks. These hooks gather essential data required for profiling. The hooks include:

- useApi: Initializes the API client for making requests.
- useParams: Retrieves parameters from the URL.
- useOrganization: Fetches organization details.
- useProjects: Retrieves project details. These hooks ensure that all necessary data is available for the profiling process.

# [Fetching profiling data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/ygr8cpkj#fetchcontinuousprofileflamegraph)

The fetchContinuousProfileFlamegraph function is responsible for making an API request to fetch profiling data. It constructs a request to the endpoint with the necessary query parameters, including the project and organization slugs. If the parameters are invalid or the project is not found, it logs errors. Upon successful data retrieval, it updates the state with the fetched profiles.

# [Updating the state with fetched profiles](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/ygr8cpkj#continuousprofileprovider)

Once the profiling data is successfully retrieved, the ContinuousProfileProvider updates the state with the fetched profiles. This updated state is then provided to child components through context, allowing them to consume and display the profiling data. This ensures that the profiling data is readily available for any component that needs it.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

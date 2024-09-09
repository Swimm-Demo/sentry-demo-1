---
title: Rate Limiting Process
---
The rate limiting process ensures that the number of requests an organization can make to the Sentry API within a certain time frame is controlled. This document will cover:

1. Determining rate limits for an organization
2. Applying rate limits to manage system load
3. Handling different data functions based on conditions.

Technical document: <SwmLink doc-title="Rate Limiting Process">[Rate Limiting Process](/.swm/rate-limiting-process.3cle1wpo.sw.md)</SwmLink>

# [Determining Rate Limits](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3cle1wpo#rate_limits-function)

The rate limiting process begins with determining the appropriate rate limits for an organization. This is done by checking if the organization exists and then applying either legacy, increased, or reduced rate limits based on the organization's configuration. This ensures that each organization is treated according to its specific needs and usage patterns.

# [Applying Rate Limits](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3cle1wpo#rate_limit_events-function)

Once the rate limits are determined, they are applied to manage the load on the system. This involves checking the organization's configuration and applying the appropriate rate limits. For example, if an organization is in an increased rate limit category, it will be allowed to make more requests compared to an organization in a reduced rate limit category. This step ensures that the system remains stable and responsive by preventing any single organization from overwhelming the API.

# [Handling Different Data Functions Based on Conditions](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/3cle1wpo#handling-different-data-functions-based-on-conditions)

The system handles different data functions based on specific conditions. For instance, if a `discover_saved_query_id` is present, the `_discover_data_fn` function is called to fetch data for discover queries. If `metrics_enhanced` is not enabled and `dashboard_widget_id` is not present, the `_data_fn` function is called to perform the actual data query. Otherwise, the `_dashboards_data_fn` function is called. This step ensures that the appropriate data function is used based on the context, optimizing the data retrieval process.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

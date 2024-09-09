---
title: Processing Trending Event Statistics
---
This document will cover the process of processing trending event statistics. We'll cover:

1. Retrieving profiling data
2. Querying the data analytics service
3. Formatting and aggregating the results.

Technical document: <SwmLink doc-title="Processing Trending Event Statistics">[Processing Trending Event Statistics](/.swm/processing-trending-event-statistics.wz032i1j.sw.md)</SwmLink>

# [Retrieving Profiling Data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/wz032i1j#get)

The process begins by retrieving profiling data for an organization. This involves handling an HTTP GET request to gather the necessary data. The system checks if the organization has the required features enabled. If not, it returns a 404 status. If the features are enabled, it proceeds to gather the necessary parameters for querying the data analytics service.

# [Querying the Data Analytics Service](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/wz032i1j#query)

Once the profiling data is retrieved, the next step is to query the data analytics service. This involves constructing a query with the necessary parameters such as dataset, start and end times, groupings, conditions, and aggregations. The query is then sent to the data analytics service, which processes it and returns the raw results. These results are then formatted to match the expected structure.

# [Formatting and Aggregating the Results](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/wz032i1j#get_stats_data_for_trending_events)

After querying the data analytics service, the raw results need to be formatted and aggregated. This involves mapping each function to its respective project and fingerprint. The system iterates over the results to format the data, including statistics and worst-case examples. The formatted data is then appended to a list and returned. This ensures that the data is presented in a user-friendly manner, making it easier for users to understand the trending event statistics.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

---
title: Calculating Crash-Free Rates
---
This document will cover the process of calculating crash-free rates, which includes:

1. Setting up parameters
2. Gathering data
3. Processing data to calculate crash-free rates.

Technical document: <SwmLink doc-title="Calculating Crash-Free Rates">[Calculating Crash-Free Rates](/.swm/calculating-crash-free-rates.deixzuwf.sw.md)</SwmLink>

# [Setting up parameters](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/deixzuwf#get_crash_free_breakdown)

The process begins by setting up the necessary parameters. This involves identifying the project and organization IDs, the release name, the start time, and any relevant environments. These parameters are essential for defining the scope of the data that will be gathered and analyzed.

# [Gathering data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/deixzuwf#_get_crash_free_breakdown_fn)

Once the parameters are set, the next step is to gather data. This involves constructing query conditions to filter the data based on the specified parameters. The data is then retrieved over predefined time intervals. This step ensures that we have all the necessary data points to calculate the crash-free rates accurately.

# [Processing data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/deixzuwf#_get_data)

After gathering the data, it needs to be processed. This involves executing the metrics query and processing the raw results to extract the total and crashed <SwmPath>[src/sentry/users/services/user/](src/sentry/users/services/user/)</SwmPath> counts. This step is crucial for transforming the raw data into meaningful metrics that can be used to calculate the crash-free rates.

# [Calculating crash-free rates](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/deixzuwf#get_series)

The final step is to calculate the crash-free rates. This is done by using the processed data to determine the percentage of sessions and users that did not experience a crash. The crash-free rate is a key performance indicator that helps in monitoring the stability and reliability of the application.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

---
title: Overview
---
The repository 'sentry-demo-1' demonstrates how to use Sentry, a developer-first error tracking and performance monitoring platform, to identify and solve issues in applications.

## Main Components

```mermaid
graph TD;
 nekr4(Application Modules) --> 6lcos(Static Files)
 6lcos(Static Files) --> nekr4(Application Modules)
```

### Languages

&nbsp;

### Overview

- Total component: 17
- High Priority components: 4

### Component Priority matrix

| Component Name | Type   | Complexity (1-10) | Change Frequency | Modernization Priority | Key Dependencies       | Notes                     |
| -------------- | ------ | ----------------- | ---------------- | ---------------------- | ---------------------- | ------------------------- |
| Auth Service   | Module | 7                 | Weekly           | High                   | User DB, External Auth | Needs security audit      |
| Data Processor | Class  | 5                 | Monthly          | Medium                 | File Storage           | Consider parallelizing    |
| API Gateway    | Module | 8                 | Daily            | High                   | All Services           | Bottleneck, needs scaling |
| ...            | ...    | ...               | ...              | ...                    | ...                    | ...                       |

## High Priority Actions

1. \[Action Item 1\]

2. \[Action Item 2\]

3. \[Action Item 3\]

### Recent Changes

- \[Date\]: \[Significant change or decision\]
- \[Date\]: \[Significant change or decision\]
- \[Date\]: \[Significant change or decision\]

## Edge Cases and Risks

- \[Component Name\]: \[Description of edge case or risk\]

- \[Component Name\]: \[Description of edge case or risk\]

- \[Component Name\]: \[Description of edge case or risk\]

## Next Steps

1. \[Next step 1\]

2. \[Next step 2\]

3. \[Next step 3\]

&nbsp;

### Application Modules

Application modules are distinct components within an application that encapsulate specific functionality or features. They help in organizing the codebase into manageable sections, making it easier to maintain and scale. Each module typically contains related code, such as models, views, and controllers, and can be independently developed and tested.

- <SwmLink doc-title="Identity in Application Modules">[Identity in Application Modules](/.swm/identity-in-application-modules.7tklrhd4.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of Notification Actions">[Overview of Notification Actions](/.swm/overview-of-notification-actions.lkua1aec.sw.md)</SwmLink>
- <SwmLink doc-title="Understanding Issues in Application Modules">[Understanding Issues in Application Modules](/.swm/understanding-issues-in-application-modules.xen0cjj1.sw.md)</SwmLink>
- <SwmLink doc-title="Introduction to Backup in Application Modules">[Introduction to Backup in Application Modules](/.swm/introduction-to-backup-in-application-modules.637vh4ti.sw.md)</SwmLink>
- <SwmLink doc-title="Introduction to Discover Functionality">[Introduction to Discover Functionality](/.swm/introduction-to-discover-functionality.aoxbrf3n.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of Middleware in Application Modules">[Overview of Middleware in Application Modules](/.swm/overview-of-middleware-in-application-modules.hq8hvpal.sw.md)</SwmLink>
- <SwmLink doc-title="Receivers in Application Modules">[Receivers in Application Modules](/.swm/receivers-in-application-modules.49jrwffh.sw.md)</SwmLink>
- <SwmLink doc-title="Getting Started with Ingestion Process">[Getting Started with Ingestion Process](/.swm/getting-started-with-ingestion-process.aurt39h4.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of Runner Module">[Overview of Runner Module](/.swm/overview-of-runner-module.ew7ep9pw.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of Search Functionality">[Overview of Search Functionality](/.swm/overview-of-search-functionality.aj4wb3e3.sw.md)</SwmLink>
- <SwmLink doc-title="Introduction to Mediators in Application Modules">[Introduction to Mediators in Application Modules](/.swm/introduction-to-mediators-in-application-modules.n8g5x0vj.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of Database Operations">[Overview of Database Operations](/.swm/overview-of-database-operations.1jjcrmay.sw.md)</SwmLink>
- **Dynamic sampling**
  - <SwmLink doc-title="Overview of Dynamic Sampling Rules">[Overview of Dynamic Sampling Rules](/.swm/overview-of-dynamic-sampling-rules.5ly7xppw.sw.md)</SwmLink>
  - <SwmLink doc-title="Understanding Dynamic Sampling Tasks">[Understanding Dynamic Sampling Tasks](/.swm/understanding-dynamic-sampling-tasks.u6fifefx.sw.md)</SwmLink>
  - <SwmLink doc-title="The Model class">[The Model class](/.swm/the-model-class.xeqen.sw.md)</SwmLink>
- **Interfaces**
  - <SwmLink doc-title="Overview of Interfaces in Application Modules">[Overview of Interfaces in Application Modules](/.swm/overview-of-interfaces-in-application-modules.eka7e3e0.sw.md)</SwmLink>
  - <SwmLink doc-title="The Exception class">[The Exception class](/.swm/the-exception-class.tjyif.sw.md)</SwmLink>
- **Auth**
  - <SwmLink doc-title="Overview of Authentication Providers">[Overview of Authentication Providers](/.swm/overview-of-authentication-providers.egih5baj.sw.md)</SwmLink>
  - <SwmLink doc-title="Authentication Pipeline Completion">[Authentication Pipeline Completion](/.swm/authentication-pipeline-completion.ozfsihpj.sw.md)</SwmLink>
  - **Services**
    - <SwmLink doc-title="Overview of Auth Services">[Overview of Auth Services](/.swm/overview-of-auth-services.vz7jgv34.sw.md)</SwmLink>
    - <SwmLink doc-title="The OrgAuthTokenService class">[The OrgAuthTokenService class](/.swm/the-orgauthtokenservice-class.ykdjf.sw.md)</SwmLink>
- **Incidents**
  - <SwmLink doc-title="Overview of Incident Management">[Overview of Incident Management](/.swm/overview-of-incident-management.64k8758m.sw.md)</SwmLink>
  - <SwmLink doc-title="Understanding Incident Endpoints">[Understanding Incident Endpoints](/.swm/understanding-incident-endpoints.4kvvfgsv.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Main Function Overview">[Main Function Overview](/.swm/main-function-overview.uvb6s0cp.sw.md)</SwmLink>
    - <SwmLink doc-title="Handling Subscription Updates">[Handling Subscription Updates](/.swm/handling-subscription-updates.ja6uvibm.sw.md)</SwmLink>
    - <SwmLink doc-title="Update Process Overview">[Update Process Overview](/.swm/update-process-overview.aug9eeda.sw.md)</SwmLink>
    - <SwmLink doc-title="Creating Alert Rules">[Creating Alert Rules](/.swm/creating-alert-rules.zn6siko8.sw.md)</SwmLink>
- **Notifications**
  - <SwmLink doc-title="Introduction to Notification Actions">[Introduction to Notification Actions](/.swm/introduction-to-notification-actions.54iwypk8.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting Started with Activity Notifications">[Getting Started with Activity Notifications](/.swm/getting-started-with-activity-notifications.8poeoho7.sw.md)</SwmLink>
- **Flows**
  - <SwmLink doc-title="Data Import and Validation Flow">[Data Import and Validation Flow](/.swm/data-import-and-validation-flow.ftlxhv9s.sw.md)</SwmLink>
  - <SwmLink doc-title="Importing Data Flow">[Importing Data Flow](/.swm/importing-data-flow.opos8asp.sw.md)</SwmLink>
  - <SwmLink doc-title="Global Data Import Process">[Global Data Import Process](/.swm/global-data-import-process.xakzhqsc.sw.md)</SwmLink>
  - <SwmLink doc-title="User Import Process">[User Import Process](/.swm/user-import-process.65slrc64.sw.md)</SwmLink>
  - <SwmLink doc-title="Importing Organizations Flow">[Importing Organizations Flow](/.swm/importing-organizations-flow.bmt4i4sh.sw.md)</SwmLink>
  - <SwmLink doc-title="Importing Configuration and Administrator Accounts">[Importing Configuration and Administrator Accounts](/.swm/importing-configuration-and-administrator-accounts.98an8cp0.sw.md)</SwmLink>
  - <SwmLink doc-title="Exporting Data to an Encrypted Tarball">[Exporting Data to an Encrypted Tarball](/.swm/exporting-data-to-an-encrypted-tarball.3pxpc311.sw.md)</SwmLink>
- **Tasks**
  - <SwmLink doc-title="Overview of Tasks in Application Modules">[Overview of Tasks in Application Modules](/.swm/overview-of-tasks-in-application-modules.3hxcdf5b.sw.md)</SwmLink>
  - <SwmLink doc-title="Backfilling Seer Grouping Records">[Backfilling Seer Grouping Records](/.swm/backfilling-seer-grouping-records.jheyhchq.sw.md)</SwmLink>
- **Monitors**
  - <SwmLink doc-title="Exploring Monitors in Application Modules">[Exploring Monitors in Application Modules](/.swm/exploring-monitors-in-application-modules.zv817r6a.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring Monitor Endpoints">[Exploring Monitor Endpoints](/.swm/exploring-monitor-endpoints.w0x7ik7z.sw.md)</SwmLink>
- **Integrations**
  - <SwmLink doc-title="Overview of Integration Middleware">[Overview of Integration Middleware](/.swm/overview-of-integration-middleware.47nydgon.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Integration Parsers">[Overview of Integration Parsers](/.swm/overview-of-integration-parsers.msqq98x3.sw.md)</SwmLink>
- **Api**
  - <SwmLink doc-title="Exploring API in Application Modules">[Exploring API in Application Modules](/.swm/exploring-api-in-application-modules.h4xllm60.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring API Helpers">[Exploring API Helpers](/.swm/exploring-api-helpers.vipb9n10.sw.md)</SwmLink>
  - <SwmLink doc-title="Relocations in Endpoints">[Relocations in Endpoints](/.swm/relocations-in-endpoints.7vn6j7ns.sw.md)</SwmLink>
  - **Serializers**
    - <SwmLink doc-title="Overview of Serializers in API">[Overview of Serializers in API](/.swm/overview-of-serializers-in-api.329x9ky1.sw.md)</SwmLink>
    - <SwmLink doc-title="Getting Started with Rest Framework Serializers">[Getting Started with Rest Framework Serializers](/.swm/getting-started-with-rest-framework-serializers.dw6yj5ya.sw.md)</SwmLink>
    - <SwmLink doc-title="Introduction to Models in Serializers">[Introduction to Models in Serializers](/.swm/introduction-to-models-in-serializers.4103izlw.sw.md)</SwmLink>
    - <SwmLink doc-title="The Serializer class">[The Serializer class](/.swm/the-serializer-class.gz0jb.sw.md)</SwmLink>
  - **Bases**
    - <SwmLink doc-title="API Bases Overview">[API Bases Overview](/.swm/api-bases-overview.j15ia64a.sw.md)</SwmLink>
    - <SwmLink doc-title="Processing Event Statistics">[Processing Event Statistics](/.swm/processing-event-statistics.zr8nfqj9.sw.md)</SwmLink>
    - **Classes**
      - <SwmLink doc-title="The ProjectEndpoint class">[The ProjectEndpoint class](/.swm/the-projectendpoint-class.wo6um.sw.md)</SwmLink>
      - <SwmLink doc-title="The OrganizationPermission class">[The OrganizationPermission class](/.swm/the-organizationpermission-class.yrh4u.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Filtering Spans by Operation Names">[Filtering Spans by Operation Names](/.swm/filtering-spans-by-operation-names.o85n45iz.sw.md)</SwmLink>
    - <SwmLink doc-title="Filtering Spans with Wrapped Function">[Filtering Spans with Wrapped Function](/.swm/filtering-spans-with-wrapped-function.137i3vhx.sw.md)</SwmLink>
    - <SwmLink doc-title="Rate Limiting Process">[Rate Limiting Process](/.swm/rate-limiting-process.3cle1wpo.sw.md)</SwmLink>
    - <SwmLink doc-title="Fetching Event Statistics Flow">[Fetching Event Statistics Flow](/.swm/fetching-event-statistics-flow.cqif79ai.sw.md)</SwmLink>
    - <SwmLink doc-title="Fetching and Processing Paginated Results">[Fetching and Processing Paginated Results](/.swm/fetching-and-processing-paginated-results.pb2xhn7q.sw.md)</SwmLink>
    - <SwmLink doc-title="Fetching Deploy Data Flow">[Fetching Deploy Data Flow](/.swm/fetching-deploy-data-flow.s7k3kuai.sw.md)</SwmLink>
    - <SwmLink doc-title="Initialization Process Overview">[Initialization Process Overview](/.swm/initialization-process-overview.b2np65p9.sw.md)</SwmLink>
    - <SwmLink doc-title="Serialization Process Overview">[Serialization Process Overview](/.swm/serialization-process-overview.owsjb5k4.sw.md)</SwmLink>
    - <SwmLink doc-title="Role of the Decision-Maker Function">[Role of the Decision-Maker Function](/.swm/role-of-the-decision-maker-function.v1gach8w.sw.md)</SwmLink>
    - <SwmLink doc-title="Updating Member Roles">[Updating Member Roles](/.swm/updating-member-roles.pzkopumj.sw.md)</SwmLink>
    - <SwmLink doc-title="Updating Project Settings">[Updating Project Settings](/.swm/updating-project-settings.xf24fdw7.sw.md)</SwmLink>
    - <SwmLink doc-title="Retrieving and Processing User Span Data">[Retrieving and Processing User Span Data](/.swm/retrieving-and-processing-user-span-data.rl7u8kqm.sw.md)</SwmLink>
    - <SwmLink doc-title="Counting Performance Issues">[Counting Performance Issues](/.swm/counting-performance-issues.g8qh6m6h.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Handling Slack Events">[Handling Slack Events](/.swm/handling-slack-events.j4okfnjr.sw.md)</SwmLink>
    - <SwmLink doc-title="Tracking HTTP Response Metrics">[Tracking HTTP Response Metrics](/.swm/tracking-http-response-metrics.cme1hm5e.sw.md)</SwmLink>
    - <SwmLink doc-title="Wrapper Function Overview">[Wrapper Function Overview](/.swm/wrapper-function-overview.i52vkzfv.sw.md)</SwmLink>
    - <SwmLink doc-title="Handling Snuba Exceptions">[Handling Snuba Exceptions](/.swm/handling-snuba-exceptions.700bfeau.sw.md)</SwmLink>
    - <SwmLink doc-title="Handling Exceptions with Decorators">[Handling Exceptions with Decorators](/.swm/handling-exceptions-with-decorators.hfkr760s.sw.md)</SwmLink>
    - <SwmLink doc-title="Constructing Trend Columns and Handling Query Results">[Constructing Trend Columns and Handling Query Results](/.swm/constructing-trend-columns-and-handling-query-results.0z0xb6dc.sw.md)</SwmLink>
    - <SwmLink doc-title="Generating Trending Event Statistics">[Generating Trending Event Statistics](/.swm/generating-trending-event-statistics.r4r3rkqi.sw.md)</SwmLink>
    - <SwmLink doc-title="Processing Trending Event Statistics">[Processing Trending Event Statistics](/.swm/processing-trending-event-statistics.wz032i1j.sw.md)</SwmLink>
    - <SwmLink doc-title="Fetching Event Statistics Metrics">[Fetching Event Statistics Metrics](/.swm/fetching-event-statistics-metrics.vt457eaq.sw.md)</SwmLink>
- **Models**
  - <SwmLink doc-title="Models in Application Modules">[Models in Application Modules](/.swm/models-in-application-modules.ttm6xw2v.sw.md)</SwmLink>
  - <SwmLink doc-title="Understanding Files in Models">[Understanding Files in Models](/.swm/understanding-files-in-models.tdev18i4.sw.md)</SwmLink>
- **Users**
  - <SwmLink doc-title="Getting Started with User Services">[Getting Started with User Services](/.swm/getting-started-with-user-services.po4pt9le.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to User Models">[Introduction to User Models](/.swm/introduction-to-user-models.ntw15qvo.sw.md)</SwmLink>
- **Events**
  - <SwmLink doc-title="Basic Concepts of Events in Search">[Basic Concepts of Events in Search](/.swm/basic-concepts-of-events-in-search.0n78qysp.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting started with Datasets in Events">[Getting started with Datasets in Events](/.swm/getting-started-with-datasets-in-events.1lmt4eib.sw.md)</SwmLink>
- **Plugins**
  - <SwmLink doc-title="Introduction to Plugins in Application Modules">[Introduction to Plugins in Application Modules](/.swm/introduction-to-plugins-in-application-modules.7em3hpxi.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic Concepts of Base Plugins">[Basic Concepts of Base Plugins](/.swm/basic-concepts-of-base-plugins.f6ib11s7.sw.md)</SwmLink>
- **Sentry metrics**
  - <SwmLink doc-title="Exploring Metric Indexer">[Exploring Metric Indexer](/.swm/exploring-metric-indexer.jrwoples.sw.md)</SwmLink>
  - <SwmLink doc-title="Consumers in Sentry Metrics">[Consumers in Sentry Metrics](/.swm/consumers-in-sentry-metrics.wfos9hs4.sw.md)</SwmLink>
  - **Querying**
    - <SwmLink doc-title="Understanding Querying in Sentry Metrics">[Understanding Querying in Sentry Metrics](/.swm/understanding-querying-in-sentry-metrics.1401nxur.sw.md)</SwmLink>
    - <SwmLink doc-title="Basic concepts of Data in Querying">[Basic concepts of Data in Querying](/.swm/basic-concepts-of-data-in-querying.ivfyt413.sw.md)</SwmLink>
- **Models**
  - <SwmLink doc-title="Basic Concepts of Models in Django">[Basic Concepts of Models in Django](/.swm/basic-concepts-of-models-in-django.m3mq6449.sw.md)</SwmLink>
  - <SwmLink doc-title="Fields in Models">[Fields in Models](/.swm/fields-in-models.a69wsg56.sw.md)</SwmLink>
- **Rules**
  - <SwmLink doc-title="Basic Concepts of Actions in Rules">[Basic Concepts of Actions in Rules](/.swm/basic-concepts-of-actions-in-rules.4rw3sgf6.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to Conditions in Rules">[Introduction to Conditions in Rules](/.swm/introduction-to-conditions-in-rules.sbtdrben.sw.md)</SwmLink>
- **Flows**
  - <SwmLink doc-title="Producing Occurrences to Kafka">[Producing Occurrences to Kafka](/.swm/producing-occurrences-to-kafka.7zdkpkk9.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of the Save Process">[Overview of the Save Process](/.swm/overview-of-the-save-process.30mk50cj.sw.md)</SwmLink>
  - <SwmLink doc-title="Understanding should_use_on_demand_metrics">[Understanding should_use_on_demand_metrics](.swm/understanding-should_use_on_demand_metrics.3s0uegjl.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Missing Values with resolve_weak">[Handling Missing Values with resolve_weak](/.swm/handling-missing-values-with-resolve_weak.jayh5bmv.sw.md)</SwmLink>
  - <SwmLink doc-title="Querying Replays with Pagination">[Querying Replays with Pagination](/.swm/querying-replays-with-pagination.grxhqpyn.sw.md)</SwmLink>
  - <SwmLink doc-title="Updating and Creating Widgets">[Updating and Creating Widgets](/.swm/updating-and-creating-widgets.4u5nsbi2.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating an Alert Rule Trigger">[Creating an Alert Rule Trigger](/.swm/creating-an-alert-rule-trigger.mvbodav2.sw.md)</SwmLink>
  - <SwmLink doc-title="Comparing Commits Flow">[Comparing Commits Flow](/.swm/comparing-commits-flow.m1m6cyd4.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating Issue Configurations Without a Group">[Creating Issue Configurations Without a Group](/.swm/creating-issue-configurations-without-a-group.qep6p6vj.sw.md)</SwmLink>
  - <SwmLink doc-title="Processing Occurrence Groups">[Processing Occurrence Groups](/.swm/processing-occurrence-groups.dn4fenui.sw.md)</SwmLink>
  - <SwmLink doc-title="Updating an Issue">[Updating an Issue](/.swm/updating-an-issue.b7upif8h.sw.md)</SwmLink>
  - <SwmLink doc-title="Bulk Mutating Issue Attributes">[Bulk Mutating Issue Attributes](/.swm/bulk-mutating-issue-attributes.3na6spk0.sw.md)</SwmLink>
  - <SwmLink doc-title="Digest Function Overview">[Digest Function Overview](/.swm/digest-function-overview.u7kxxjwl.sw.md)</SwmLink>
  - <SwmLink doc-title="Gathering Health Data for Project Releases">[Gathering Health Data for Project Releases](/.swm/gathering-health-data-for-project-releases.9eee553r.sw.md)</SwmLink>
  - <SwmLink doc-title="Processing a Single Message Flow">[Processing a Single Message Flow](/.swm/processing-a-single-message-flow.ihybh8cb.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Check-ins Flow">[Handling Check-ins Flow](/.swm/handling-check-ins-flow.goyp6ca9.sw.md)</SwmLink>
  - <SwmLink doc-title="Retrieving and Updating Repository Data">[Retrieving and Updating Repository Data](/.swm/retrieving-and-updating-repository-data.6s0bp1wo.sw.md)</SwmLink>
  - <SwmLink doc-title="Managing VSTS Subscriptions">[Managing VSTS Subscriptions](/.swm/managing-vsts-subscriptions.l9rsz8ut.sw.md)</SwmLink>
  - <SwmLink doc-title="Synchronizing Assignees">[Synchronizing Assignees](/.swm/synchronizing-assignees.8gdxh8z4.sw.md)</SwmLink>
  - <SwmLink doc-title="Retrieving and Formatting Issue Details">[Retrieving and Formatting Issue Details](/.swm/retrieving-and-formatting-issue-details.7pxhq4xd.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Clock Tasks">[Handling Clock Tasks](/.swm/handling-clock-tasks.9bc7g9ee.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Post Requests for Alert Triggers">[Handling Post Requests for Alert Triggers](/.swm/handling-post-requests-for-alert-triggers.8xwvvl8e.sw.md)</SwmLink>
  - <SwmLink doc-title="Organization Configuration Flow">[Organization Configuration Flow](/.swm/organization-configuration-flow.hyjz2zkr.sw.md)</SwmLink>
  - <SwmLink doc-title="Synchronizing External Issue Status">[Synchronizing External Issue Status](/.swm/synchronizing-external-issue-status.slvvyvh5.sw.md)</SwmLink>
  - <SwmLink doc-title="Post-Installation Tasks">[Post-Installation Tasks](/.swm/post-installation-tasks.pcdtohea.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating an Issue">[Creating an Issue](/.swm/creating-an-issue.t5juouxz.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Discord Interactions">[Handling Discord Interactions](/.swm/handling-discord-interactions.ini5zklv.sw.md)</SwmLink>
  - <SwmLink doc-title="Filtering Unmigratable Repositories">[Filtering Unmigratable Repositories](/.swm/filtering-unmigratable-repositories.bkp48cpp.sw.md)</SwmLink>
  - <SwmLink doc-title="Determining Issue Resolution State">[Determining Issue Resolution State](/.swm/determining-issue-resolution-state.38lzwca9.sw.md)</SwmLink>
  - <SwmLink doc-title="Checking Repository Access">[Checking Repository Access](/.swm/checking-repository-access.r4z2dcwu.sw.md)</SwmLink>
  - <SwmLink doc-title="Dispatch Process Overview">[Dispatch Process Overview](/.swm/dispatch-process-overview.72prpqpg.sw.md)</SwmLink>
  - <SwmLink doc-title="Build Integration Process">[Build Integration Process](/.swm/build-integration-process.jowgncub.sw.md)</SwmLink>
  - <SwmLink doc-title="Gathering Release Attributes">[Gathering Release Attributes](/.swm/gathering-release-attributes.6banb79i.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating and Processing Feedback Issues">[Creating and Processing Feedback Issues](/.swm/creating-and-processing-feedback-issues.b5jbdvxz.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of the &#39;get&#39; Function Flow">[Overview of the 'get' Function Flow](/.swm/overview-of-the-get-function-flow.10pdhtie.sw.md)</SwmLink>
  - <SwmLink doc-title="User Registration and Invitation Acceptance Flow">[User Registration and Invitation Acceptance Flow](/.swm/user-registration-and-invitation-acceptance-flow.6yoft3zb.sw.md)</SwmLink>
  - <SwmLink doc-title="Synchronizing Issue Status with Jira">[Synchronizing Issue Status with Jira](/.swm/synchronizing-issue-status-with-jira.7eq84djp.sw.md)</SwmLink>
  - <SwmLink doc-title="Synchronizing Sentry and Jira Issue Status">[Synchronizing Sentry and Jira Issue Status](/.swm/synchronizing-sentry-and-jira-issue-status.s8porjvu.sw.md)</SwmLink>
  - <SwmLink doc-title="Gathering Group Attributes">[Gathering Group Attributes](/.swm/gathering-group-attributes.96qfp85z.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a Comment in Jira">[Creating a Comment in Jira](/.swm/creating-a-comment-in-jira.w2n5rcak.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating an Issue in Jira">[Creating an Issue in Jira](/.swm/creating-an-issue-in-jira.p2vkfepz.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Authentication">[Handling Authentication](/.swm/handling-authentication.72u6auwl.sw.md)</SwmLink>
  - <SwmLink doc-title="Jira Server Integration Flow">[Jira Server Integration Flow](/.swm/jira-server-integration-flow.qn58m030.sw.md)</SwmLink>
  - <SwmLink doc-title="Access Token and Webhook Processing Flow">[Access Token and Webhook Processing Flow](/.swm/access-token-and-webhook-processing-flow.vmo6ffib.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a Comment Flow">[Creating a Comment Flow](/.swm/creating-a-comment-flow.x5lbigv6.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating an Issue Flow">[Creating an Issue Flow](/.swm/creating-an-issue-flow.w0ayawja.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling OAuth and Webhook Requests">[Handling OAuth and Webhook Requests](/.swm/handling-oauth-and-webhook-requests.naptzvbp.sw.md)</SwmLink>
  - <SwmLink doc-title="Profiling Process Overview">[Profiling Process Overview](/.swm/profiling-process-overview.fqvnqqgf.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of get_attrs Function">[Overview of get_attrs Function](/.swm/overview-of-get_attrs-function.zum1d1z0.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Metric Operations">[Handling Metric Operations](/.swm/handling-metric-operations.w1o0vl60.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a Comment Flow">[Creating a Comment Flow](/.swm/creating-a-comment-flow.dhft996i.sw.md)</SwmLink>
  - <SwmLink doc-title="Authorizing a Request">[Authorizing a Request](/.swm/authorizing-a-request.6z884pwm.sw.md)</SwmLink>
  - <SwmLink doc-title="Retrieving Issue Attributes">[Retrieving Issue Attributes](/.swm/retrieving-issue-attributes.5y24yb61.sw.md)</SwmLink>
  - <SwmLink doc-title="Initiating VSTS Subscription Check">[Initiating VSTS Subscription Check](/.swm/initiating-vsts-subscription-check.v5q2m4cv.sw.md)</SwmLink>
  - <SwmLink doc-title="Validating a Repository">[Validating a Repository](/.swm/validating-a-repository.hter470m.sw.md)</SwmLink>
  - <SwmLink doc-title="Identity Retrieval and Usage">[Identity Retrieval and Usage](/.swm/identity-retrieval-and-usage.fuqcelre.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a Subscription and Handling Webhooks">[Creating a Subscription and Handling Webhooks](/.swm/creating-a-subscription-and-handling-webhooks.03pw19q1.sw.md)</SwmLink>
  - <SwmLink doc-title="Updating Release Metadata">[Updating Release Metadata](/.swm/updating-release-metadata.8oswlhzd.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a New Release">[Creating a New Release](/.swm/creating-a-new-release.3hb83lv7.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of get_result Function">[Overview of get_result Function](/.swm/overview-of-get_result-function.lo66rpm5.sw.md)</SwmLink>
  - <SwmLink doc-title="Calculating Crash-Free Rates">[Calculating Crash-Free Rates](/.swm/calculating-crash-free-rates.deixzuwf.sw.md)</SwmLink>
  - <SwmLink doc-title="Bulk Mutation of Issues">[Bulk Mutation of Issues](/.swm/bulk-mutation-of-issues.f6jjyg87.sw.md)</SwmLink>
  - <SwmLink doc-title="Bulk Update and Delete Views Flow">[Bulk Update and Delete Views Flow](/.swm/bulk-update-and-delete-views-flow.k15du8ob.sw.md)</SwmLink>
  - <SwmLink doc-title="Issue Resolution Cleanup">[Issue Resolution Cleanup](/.swm/issue-resolution-cleanup.5j5ti396.sw.md)</SwmLink>
  - <SwmLink doc-title="Event Attribute Collection and Serialization">[Event Attribute Collection and Serialization](/.swm/event-attribute-collection-and-serialization.ny09n17k.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling POST Requests">[Handling POST Requests](/.swm/handling-post-requests.btoaek2g.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of the data_fn Function">[Overview of the data_fn Function](/.swm/overview-of-the-data_fn-function.2oyncsca.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of the data_fn Function">[Overview of the data_fn Function](/.swm/overview-of-the-data_fn-function.8h71kha8.sw.md)</SwmLink>
  - <SwmLink doc-title="Creating a New Release">[Creating a New Release](/.swm/creating-a-new-release.ynfvhysw.sw.md)</SwmLink>
  - <SwmLink doc-title="Flow of data_fn Function">[Flow of data_fn Function](/.swm/flow-of-data_fn-function.8w9nbfgp.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Query Stats Function">[Overview of Query Stats Function](/.swm/overview-of-query-stats-function.etyw02nv.sw.md)</SwmLink>
  - <SwmLink doc-title="Notification Sending Process">[Notification Sending Process](/.swm/notification-sending-process.wzkkf4dg.sw.md)</SwmLink>
  - <SwmLink doc-title="Role of data_fn">[Role of data_fn](.swm/role-of-data_fn.10oj30x0.sw.md)</SwmLink>
  - <SwmLink doc-title="Retrieving Release Information">[Retrieving Release Information](/.swm/retrieving-release-information.yq9rw89n.sw.md)</SwmLink>
  - <SwmLink doc-title="Retrieving and Processing User Reports">[Retrieving and Processing User Reports](/.swm/retrieving-and-processing-user-reports.ax9hin48.sw.md)</SwmLink>
  - <SwmLink doc-title="Purpose of the Validate Function">[Purpose of the Validate Function](/.swm/purpose-of-the-validate-function.jqsszrtb.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Discord Commands">[Handling Discord Commands](/.swm/handling-discord-commands.srdioo7b.sw.md)</SwmLink>
  - <SwmLink doc-title="Processing Attachments and Events">[Processing Attachments and Events](/.swm/processing-attachments-and-events.7ddcc2b6.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Slack Command Requests">[Handling Slack Command Requests](/.swm/handling-slack-command-requests.01x8hlcm.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Message Events">[Handling Message Events](/.swm/handling-message-events.jemqdizi.sw.md)</SwmLink>
  - <SwmLink doc-title="Managing Development Services">[Managing Development Services](/.swm/managing-development-services.lm1rl02c.sw.md)</SwmLink>
  - <SwmLink doc-title="OpenAI Integration">[OpenAI Integration](/.swm/openai-integration.7qyrvjk8.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling Commits Flow">[Handling Commits Flow](/.swm/handling-commits-flow.tvp209vd.sw.md)</SwmLink>
  - <SwmLink doc-title="Data Fetching and Analysis Flow">[Data Fetching and Analysis Flow](/.swm/data-fetching-and-analysis-flow.oknwwqnq.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of the Query Execution Flow">[Overview of the Query Execution Flow](/.swm/overview-of-the-query-execution-flow.ihzh2dfz.sw.md)</SwmLink>
- **Classes**
  - <SwmLink doc-title="The PipelineView class">[The PipelineView class](/.swm/the-pipelineview-class.sarn9.sw.md)</SwmLink>
  - <SwmLink doc-title="The RpcModel class">[The RpcModel class](/.swm/the-rpcmodel-class.sp6e2.sw.md)</SwmLink>
  - <SwmLink doc-title="The BaseTSDB class">[The BaseTSDB class](/.swm/the-basetsdb-class.k43bm.sw.md)</SwmLink>

### Static Files

Static files are assets that do not change during the execution of the application. They include resources like fonts, stylesheets, images, and scripts, which are served directly to the client without any server-side processing.

- <SwmLink doc-title="Managing Plugins in Static Files">[Managing Plugins in Static Files](/.swm/managing-plugins-in-static-files.4634narp.sw.md)</SwmLink>
- <SwmLink doc-title="Introduction to Stores">[Introduction to Stores](/.swm/introduction-to-stores.5dzgb4c7.sw.md)</SwmLink>
- **Views**
  - <SwmLink doc-title="Profiling in Views">[Profiling in Views](/.swm/profiling-in-views.2f53l3op.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring Issue List View">[Exploring Issue List View](/.swm/exploring-issue-list-view.nt80j6y4.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring Replays in Views">[Exploring Replays in Views](/.swm/exploring-replays-in-views.7v1u993j.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting Started with Metrics in Views">[Getting Started with Metrics in Views](/.swm/getting-started-with-metrics-in-views.7ot9ezpw.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring Issues in Alerts">[Exploring Issues in Alerts](/.swm/exploring-issues-in-alerts.4kf863e0.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic Concepts of Project Detail View">[Basic Concepts of Project Detail View](/.swm/basic-concepts-of-project-detail-view.3503r3iq.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Admin in Views">[Overview of Admin in Views](/.swm/overview-of-admin-in-views.o8b7hr4y.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to Discover Feature">[Introduction to Discover Feature](/.swm/introduction-to-discover-feature.3qdlyd4u.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting Started with Detailed Issue Information">[Getting Started with Detailed Issue Information](/.swm/getting-started-with-detailed-issue-information.q4gqtduq.sw.md)</SwmLink>
  - <SwmLink doc-title="Releases List Overview">[Releases List Overview](/.swm/releases-list-overview.vrl1pgku.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic concepts of Monitors in Views">[Basic concepts of Monitors in Views](/.swm/basic-concepts-of-monitors-in-views.ih8cebbb.sw.md)</SwmLink>
  - **Performance**
    - <SwmLink doc-title="Overview of Performance Trends">[Overview of Performance Trends](/.swm/overview-of-performance-trends.n5ugqm8j.sw.md)</SwmLink>
    - <SwmLink doc-title="Getting Started with Trace Details">[Getting Started with Trace Details](/.swm/getting-started-with-trace-details.5la0287z.sw.md)</SwmLink>
    - **Transaction summary**
      - <SwmLink doc-title="Understanding Transaction Spans">[Understanding Transaction Spans](/.swm/understanding-transaction-spans.gm0ic6j6.sw.md)</SwmLink>
      - <SwmLink doc-title="Transaction Overview Components and Endpoints">[Transaction Overview Components and Endpoints](/.swm/transaction-overview-components-and-endpoints.ktap2osz.sw.md)</SwmLink>
    - **Trace drawer**
      - <SwmLink doc-title="Overview of Trace Drawer Component">[Overview of Trace Drawer Component](/.swm/overview-of-trace-drawer-component.vf3vxjwm.sw.md)</SwmLink>
      - <SwmLink doc-title="Exploring Trace Details">[Exploring Trace Details](/.swm/exploring-trace-details.1o523h71.sw.md)</SwmLink>
    - **Flows**
      - <SwmLink doc-title="Navigating the Trace Tree">[Navigating the Trace Tree](/.swm/navigating-the-trace-tree.vbe0s498.sw.md)</SwmLink>
      - <SwmLink doc-title="Trace View Waterfall Component">[Trace View Waterfall Component](/.swm/trace-view-waterfall-component.b3fyyq7y.sw.md)</SwmLink>
      - <SwmLink doc-title="Trace Flow Overview">[Trace Flow Overview](/.swm/trace-flow-overview.ury2uwre.sw.md)</SwmLink>
    - **Landing**
      - <SwmLink doc-title="Overview of the Performance Landing Page">[Overview of the Performance Landing Page](/.swm/overview-of-the-performance-landing-page.qeotmzq2.sw.md)</SwmLink>
      - <SwmLink doc-title="Understanding Performance Widgets">[Understanding Performance Widgets](/.swm/understanding-performance-widgets.wdhd8x19.sw.md)</SwmLink>
  - **Organization stats**
    - <SwmLink doc-title="Getting Started with Organization Usage Stats">[Getting Started with Organization Usage Stats](/.swm/getting-started-with-organization-usage-stats.9x53zfpg.sw.md)</SwmLink>
    - <SwmLink doc-title="Getting Started with Team Insights">[Getting Started with Team Insights](/.swm/getting-started-with-team-insights.mfv5rbrm.sw.md)</SwmLink>
  - **Dashboards**
    - <SwmLink doc-title="Dashboard Rendering and Management">[Dashboard Rendering and Management](/.swm/dashboard-rendering-and-management.hlt5vit1.sw.md)</SwmLink>
    - <SwmLink doc-title="Basic Concepts of Widget Card in Dashboards">[Basic Concepts of Widget Card in Dashboards](/.swm/basic-concepts-of-widget-card-in-dashboards.jk3gfgh7.sw.md)</SwmLink>
  - **Detail**
    - <SwmLink doc-title="Overview of Replay Details">[Overview of Replay Details](/.swm/overview-of-replay-details.mx9i2b9j.sw.md)</SwmLink>
    - <SwmLink doc-title="Understanding Network Details">[Understanding Network Details](/.swm/understanding-network-details.teq0oj1x.sw.md)</SwmLink>
  - **Metric**
    - <SwmLink doc-title="Understanding Metrics in Alerts">[Understanding Metrics in Alerts](/.swm/understanding-metrics-in-alerts.l5px4k5w.sw.md)</SwmLink>
    - <SwmLink doc-title="Details in Metric Overview">[Details in Metric Overview](/.swm/details-in-metric-overview.mz5bqbty.sw.md)</SwmLink>
  - **Settings**
    - <SwmLink doc-title="Getting Started with Organization Teams Settings">[Getting Started with Organization Teams Settings](/.swm/getting-started-with-organization-teams-settings.vfcy3sx2.sw.md)</SwmLink>
    - <SwmLink doc-title="Overview of Account Settings">[Overview of Account Settings](/.swm/overview-of-account-settings.o414jrft.sw.md)</SwmLink>
    - <SwmLink doc-title="Understanding Organization Integrations in Settings">[Understanding Organization Integrations in Settings](/.swm/understanding-organization-integrations-in-settings.rwwpuyol.sw.md)</SwmLink>
    - <SwmLink doc-title="Getting Started with Settings Components">[Getting Started with Settings Components](/.swm/getting-started-with-settings-components.cqvlqe2u.sw.md)</SwmLink>
    - **Data scrubbing**
      - <SwmLink doc-title="Understanding Data Scrubbing in Components">[Understanding Data Scrubbing in Components](/.swm/understanding-data-scrubbing-in-components.otjyeaue.sw.md)</SwmLink>
      - <SwmLink doc-title="Basic Concepts of Modals in Data Scrubbing">[Basic Concepts of Modals in Data Scrubbing](/.swm/basic-concepts-of-modals-in-data-scrubbing.lyms3x9l.sw.md)</SwmLink>
    - **Project**
      - <SwmLink doc-title="Understanding Project Settings">[Understanding Project Settings](/.swm/understanding-project-settings.jysunon4.sw.md)</SwmLink>
      - <SwmLink doc-title="Introduction to Project Ownership">[Introduction to Project Ownership](/.swm/introduction-to-project-ownership.xtvj9qfx.sw.md)</SwmLink>
  - **Detail**
    - <SwmLink doc-title="Getting Started with Release Details">[Getting Started with Release Details](/.swm/getting-started-with-release-details.m6kc6zex.sw.md)</SwmLink>
    - <SwmLink doc-title="Introduction to Overview of Release Details">[Introduction to Overview of Release Details](/.swm/introduction-to-overview-of-release-details.xeutf34w.sw.md)</SwmLink>
- **Components**
  - <SwmLink doc-title="Understanding Metrics in Components">[Understanding Metrics in Components](/.swm/understanding-metrics-in-components.4cvas3wj.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Forms in Components">[Overview of Forms in Components](/.swm/overview-of-forms-in-components.xeu4g2ln.sw.md)</SwmLink>
  - <SwmLink doc-title="Understanding Sidebar in Components">[Understanding Sidebar in Components](/.swm/understanding-sidebar-in-components.u1yh60du.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting Started with Organizations in Sentry Components">[Getting Started with Organizations in Sentry Components](/.swm/getting-started-with-organizations-in-sentry-components.o8zg7epn.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to Onboarding in Components">[Introduction to Onboarding in Components](/.swm/introduction-to-onboarding-in-components.9mj3s01y.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Modals in Components">[Overview of Modals in Components](/.swm/overview-of-modals-in-components.jsdua4hk.sw.md)</SwmLink>
  - <SwmLink doc-title="Exploring the Dev Toolbar">[Exploring the Dev Toolbar](/.swm/exploring-the-dev-toolbar.qajpclws.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Chart Component in Application">[Overview of Chart Component in Application](/.swm/overview-of-chart-component-in-application.1v1c09tr.sw.md)</SwmLink>
  - <SwmLink doc-title="Search Component Overview">[Search Component Overview](/.swm/search-component-overview.9rz0860v.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to Feedback Components">[Introduction to Feedback Components](/.swm/introduction-to-feedback-components.9oy5lxcu.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to Replays in Components">[Introduction to Replays in Components](/.swm/introduction-to-replays-in-components.s9uufxdn.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of Profiling Components">[Overview of Profiling Components](/.swm/overview-of-profiling-components.nmmloybr.sw.md)</SwmLink>
  - **Group**
    - <SwmLink doc-title="Overview of Group in Components">[Overview of Group in Components](/.swm/overview-of-group-in-components.md80dwxs.sw.md)</SwmLink>
    - <SwmLink doc-title="Getting Started with External Issues List">[Getting Started with External Issues List](/.swm/getting-started-with-external-issues-list.wcjaynk2.sw.md)</SwmLink>
  - **Events**
    - <SwmLink doc-title="Introduction to Autofix in Events">[Introduction to Autofix in Events](/.swm/introduction-to-autofix-in-events.5mt1rxv9.sw.md)</SwmLink>
    - <SwmLink doc-title="Understanding Event Contexts">[Understanding Event Contexts](/.swm/understanding-event-contexts.qnyp8d8x.sw.md)</SwmLink>
    - <SwmLink doc-title="Understanding Event Statistical Detector">[Understanding Event Statistical Detector](/.swm/understanding-event-statistical-detector.jkgtmtcz.sw.md)</SwmLink>
    - **Interfaces**
      - <SwmLink doc-title="Introduction to Frame Component">[Introduction to Frame Component](/.swm/introduction-to-frame-component.ukqm79pi.sw.md)</SwmLink>
      - <SwmLink doc-title="Exploring Spans in Interfaces">[Exploring Spans in Interfaces](/.swm/exploring-spans-in-interfaces.8j4hwf3z.sw.md)</SwmLink>
      - <SwmLink doc-title="The Generic class">[The Generic class](/.swm/the-generic-class.9vqff.sw.md)</SwmLink>
      - **Crash content**
        - <SwmLink doc-title="Introduction to Crash Details">[Introduction to Crash Details](/.swm/introduction-to-crash-details.z3a27qhm.sw.md)</SwmLink>
        - <SwmLink doc-title="Overview of Exception Handling in Crash Content">[Overview of Exception Handling in Crash Content](/.swm/overview-of-exception-handling-in-crash-content.bybbpkq0.sw.md)</SwmLink>
      - **Debug meta**
        - <SwmLink doc-title="Basic Concepts of Debug Metadata">[Basic Concepts of Debug Metadata](/.swm/basic-concepts-of-debug-metadata.4o4sgij6.sw.md)</SwmLink>
        - <SwmLink doc-title="Exploring Debug Image Information">[Exploring Debug Image Information](/.swm/exploring-debug-image-information.mk0zb5jr.sw.md)</SwmLink>
- **Flows**
  - <SwmLink doc-title="Overview of FormField Component">[Overview of FormField Component](/.swm/overview-of-formfield-component.g648wjaw.sw.md)</SwmLink>
  - <SwmLink doc-title="Field Change Notification and Undo Flow">[Field Change Notification and Undo Flow](/.swm/field-change-notification-and-undo-flow.jutfzmpw.sw.md)</SwmLink>
  - <SwmLink doc-title="Dashboard List Overview">[Dashboard List Overview](/.swm/dashboard-list-overview.9qliw58c.sw.md)</SwmLink>
  - <SwmLink doc-title="Fetching Organization Details">[Fetching Organization Details](/.swm/fetching-organization-details.n4ddpsz4.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of ConfigureIntegration Function">[Overview of ConfigureIntegration Function](/.swm/overview-of-configureintegration-function.v9gmkwh0.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of CodeOwnerFileTable">[Overview of CodeOwnerFileTable](/.swm/overview-of-codeownerfiletable.m2ixa9cm.sw.md)</SwmLink>
  - <SwmLink doc-title="Overview of useGenericDiscoverQuery">[Overview of useGenericDiscoverQuery](/.swm/overview-of-usegenericdiscoverquery.8i2fpsuo.sw.md)</SwmLink>
  - <SwmLink doc-title="Making Event Requests">[Making Event Requests](/.swm/making-event-requests.e9ns5q40.sw.md)</SwmLink>
  - <SwmLink doc-title="Query Function Flow">[Query Function Flow](/.swm/query-function-flow.9nu2nxpw.sw.md)</SwmLink>
  - <SwmLink doc-title="SudoModal Component Overview">[SudoModal Component Overview](/.swm/sudomodal-component-overview.5p4rwl88.sw.md)</SwmLink>
  - <SwmLink doc-title="Alert Rule Details Flow">[Alert Rule Details Flow](/.swm/alert-rule-details-flow.hheakc1d.sw.md)</SwmLink>
  - <SwmLink doc-title="QueryBatchNode Overview">[QueryBatchNode Overview](/.swm/querybatchnode-overview.93fmzvgi.sw.md)</SwmLink>
  - <SwmLink doc-title="Query Context Menu Overview">[Query Context Menu Overview](/.swm/query-context-menu-overview.p58q0whr.sw.md)</SwmLink>
  - <SwmLink doc-title="Query Handling Overview">[Query Handling Overview](/.swm/query-handling-overview.hleqpcn6.sw.md)</SwmLink>
  - <SwmLink doc-title="Handling User Actions">[Handling User Actions](/.swm/handling-user-actions.kmrw6qxf.sw.md)</SwmLink>
  - <SwmLink doc-title="Query Batching Process">[Query Batching Process](/.swm/query-batching-process.xw1vqty8.sw.md)</SwmLink>

### Flows

- <SwmLink doc-title="ContinuousProfileProvider Overview">[ContinuousProfileProvider Overview](/.swm/continuousprofileprovider-overview.ygr8cpkj.sw.md)</SwmLink>

## Build Tools

- <SwmLink doc-title="Makefile">[Makefile](.swm/makefile.dzp4yvct.sw.md)</SwmLink>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="other"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>

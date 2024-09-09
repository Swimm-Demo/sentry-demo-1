---
title: Basic concepts of Monitors in Views
---
# Overview

Monitors are used to track the execution of scheduled tasks, known as crons, and ensure they are running as expected. They provide visibility into the status of these tasks, allowing developers to identify and address issues such as missed or failed executions.

# <SwmToken path="static/app/views/monitors/index.tsx" pos="5:2:2" line-data="function MonitorsContainer({children}: {children?: React.ReactNode}) {">`MonitorsContainer`</SwmToken> Component

The <SwmToken path="static/app/views/monitors/index.tsx" pos="5:2:2" line-data="function MonitorsContainer({children}: {children?: React.ReactNode}) {">`MonitorsContainer`</SwmToken> component ensures that the organization context is available and wraps the children components with necessary project and page filters.

<SwmSnippet path="/static/app/views/monitors/index.tsx" line="1">

---

The <SwmToken path="static/app/views/monitors/index.tsx" pos="5:2:2" line-data="function MonitorsContainer({children}: {children?: React.ReactNode}) {">`MonitorsContainer`</SwmToken> component uses <SwmToken path="static/app/views/monitors/index.tsx" pos="1:2:2" line-data="import NoProjectMessage from &#39;sentry/components/noProjectMessage&#39;;">`NoProjectMessage`</SwmToken> to display a message when no project is selected and <SwmToken path="static/app/views/monitors/index.tsx" pos="2:2:2" line-data="import PageFiltersContainer from &#39;sentry/components/organizations/pageFilters/container&#39;;">`PageFiltersContainer`</SwmToken> to wrap the children components with necessary filters.

```tsx
import NoProjectMessage from 'sentry/components/noProjectMessage';
import PageFiltersContainer from 'sentry/components/organizations/pageFilters/container';
import useOrganization from 'sentry/utils/useOrganization';

function MonitorsContainer({children}: {children?: React.ReactNode}) {
  const organization = useOrganization();

  return (
    <NoProjectMessage organization={organization}>
      <PageFiltersContainer>{children}</PageFiltersContainer>
```

---

</SwmSnippet>

# <SwmToken path="static/app/views/monitors/components/overviewTimeline/overviewRow.tsx" pos="45:4:4" line-data="export function OverviewRow({">`OverviewRow`</SwmToken> Component

The <SwmToken path="static/app/views/monitors/components/overviewTimeline/overviewRow.tsx" pos="45:4:4" line-data="export function OverviewRow({">`OverviewRow`</SwmToken> component handles the display of individual monitor data, including actions like deleting environments and toggling mute status.

<SwmSnippet path="/static/app/views/monitors/components/overviewTimeline/overviewRow.tsx" line="1">

---

The <SwmToken path="static/app/views/monitors/components/overviewTimeline/overviewRow.tsx" pos="45:4:4" line-data="export function OverviewRow({">`OverviewRow`</SwmToken> component imports various UI components and utilities to manage and display monitor data.

```tsx
import {useState} from 'react';
import {css} from '@emotion/react';
import styled from '@emotion/styled';

import Tag from 'sentry/components/badge/tag';
import {Button} from 'sentry/components/button';
import {openConfirmModal} from 'sentry/components/confirm';
import {DropdownMenu} from 'sentry/components/dropdownMenu';
import ActorBadge from 'sentry/components/idBadge/actorBadge';
import ProjectBadge from 'sentry/components/idBadge/projectBadge';
```

---

</SwmSnippet>

# <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken> Component

The <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken> component displays issues related to a specific cron monitor, providing insights into any problems detected.

<SwmSnippet path="/static/app/views/monitors/components/monitorIssues.tsx" line="1">

---

The <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken> component imports necessary components and utilities to display issues related to a specific monitor.

```tsx
import {Fragment, useState} from 'react';
import styled from '@emotion/styled';

import {LinkButton} from 'sentry/components/button';
import EmptyStateWarning from 'sentry/components/emptyStateWarning';
import GroupList from 'sentry/components/issues/groupList';
import Panel from 'sentry/components/panels/panel';
import PanelBody from 'sentry/components/panels/panelBody';
import {SegmentedControl} from 'sentry/components/segmentedControl';
import {t} from 'sentry/locale';
```

---

</SwmSnippet>

# <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="21:4:4" line-data="export function useMonitorStats({monitors, timeWindowConfig}: Options) {">`useMonitorStats`</SwmToken> Hook

The <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="21:4:4" line-data="export function useMonitorStats({monitors, timeWindowConfig}: Options) {">`useMonitorStats`</SwmToken> hook fetches statistical data for a list of monitors, aiding in the analysis of their performance over time.

<SwmSnippet path="/static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" line="1">

---

The <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="21:4:4" line-data="export function useMonitorStats({monitors, timeWindowConfig}: Options) {">`useMonitorStats`</SwmToken> hook uses the <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="1:3:3" line-data="import {useApiQuery} from &#39;sentry/utils/queryClient&#39;;">`useApiQuery`</SwmToken> hook to fetch monitor statistics data.

```tsx
import {useApiQuery} from 'sentry/utils/queryClient';
import useOrganization from 'sentry/utils/useOrganization';
import useRouter from 'sentry/utils/useRouter';

import type {MonitorBucketData, TimeWindowConfig} from '../types';

interface Options {
  /**
   * The list of monitor IDs to fetch stats for
   */
```

---

</SwmSnippet>

# Main Functions

There are several main functions in this folder. Some of them are Monitors, <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken>, <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken>, and <SwmToken path="static/app/views/monitors/components/monitorStats.tsx" pos="31:2:2" line-data="function MonitorStats({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorStats`</SwmToken>. We will dive a little into each of these functions.

## Monitors

The <SwmToken path="static/app/views/monitors/overview.tsx" pos="51:6:6" line-data="export default function Monitors() {">`Monitors`</SwmToken> function is responsible for fetching and displaying a list of monitors. It uses the <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="1:3:3" line-data="import {useApiQuery} from &#39;sentry/utils/queryClient&#39;;">`useApiQuery`</SwmToken> hook to fetch monitor data and process errors. It also handles search functionality and navigation.

<SwmSnippet path="/static/app/views/monitors/overview.tsx" line="51">

---

The <SwmToken path="static/app/views/monitors/overview.tsx" pos="51:6:6" line-data="export default function Monitors() {">`Monitors`</SwmToken> function fetches monitor data using the <SwmToken path="static/app/views/monitors/overview.tsx" pos="67:5:5" line-data="  } = useApiQuery&lt;Monitor[]&gt;(queryKey, {">`useApiQuery`</SwmToken> hook and handles various functionalities like search and navigation.

```tsx
export default function Monitors() {
  const api = useApi();
  const organization = useOrganization();
  const navigate = useNavigate();
  const location = useLocation();
  const platform = decodeScalar(location.query?.platform) ?? null;
  const guide = decodeScalar(location.query?.guide);
  const project = decodeList(location.query?.project);

  const queryKey = makeMonitorListQueryKey(organization, location.query);

  const {
    data: monitorList,
    getResponseHeader: monitorListHeaders,
    isPending,
    refetch,
  } = useApiQuery<Monitor[]>(queryKey, {
    staleTime: 0,
  });

  const processingErrorQueryKey = makeMonitorListErrorsQueryKey(organization, project);
```

---

</SwmSnippet>

## <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken>

The <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken> function fetches and displays recent <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken> for a specific monitor. It uses the <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="1:3:3" line-data="import {useApiQuery} from &#39;sentry/utils/queryClient&#39;;">`useApiQuery`</SwmToken> hook to fetch <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="116:7:9" line-data="                    tooltipTitle={tct(&#39;Check-in Status: [status]&#39;, {">`Check-in`</SwmToken> data and handles error states. It also generates download URLs for <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="116:7:9" line-data="                    tooltipTitle={tct(&#39;Check-in Status: [status]&#39;, {">`Check-in`</SwmToken> attachments.

<SwmSnippet path="/static/app/views/monitors/components/monitorCheckIns.tsx" line="51">

---

The <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken> function uses the <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="71:5:5" line-data="  } = useApiQuery&lt;CheckIn[]&gt;(queryKey, {staleTime: 0});">`useApiQuery`</SwmToken> hook to fetch recent <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken> for a monitor and handles error states.

```tsx
function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {
  const location = useLocation();
  const organization = useOrganization();
  const queryKey = [
    `/projects/${orgSlug}/${monitor.project.slug}/monitors/${monitor.slug}/checkins/`,
    {
      query: {
        per_page: '10',
        environment: monitorEnvs.map(e => e.name),
        expand: 'groups',
        ...location.query,
      },
    },
  ] as const;

  const {
    data: checkInList,
    getResponseHeader,
    isPending,
    isError,
  } = useApiQuery<CheckIn[]>(queryKey, {staleTime: 0});
```

---

</SwmSnippet>

## <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken>

The <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken> function displays issues related to a specific cron monitor. It constructs a query to fetch issues based on the monitor's slug and environments, and provides a segmented control to filter issues by type.

<SwmSnippet path="/static/app/views/monitors/components/monitorIssues.tsx" line="45">

---

The <SwmToken path="static/app/views/monitors/components/monitorIssues.tsx" pos="45:2:2" line-data="function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {">`MonitorIssues`</SwmToken> function constructs a query to fetch issues related to a specific monitor and provides a segmented control to filter issues by type.

```tsx
function MonitorIssues({orgSlug, monitor, monitorEnvs}: Props) {
  const {selection} = usePageFilters();
  const {start, end, period} = selection.datetime;
  const timeProps =
    start && end
      ? {
          start: getUtcDateString(start),
          end: getUtcDateString(end),
        }
      : {
          statsPeriod: period,
        };

  const [issuesType, setIssuesType] = useState<IssuesType>(IssuesType.UNRESOLVED);

  const monitorFilter = `monitor.slug:${monitor.slug}`;
  const envFilter = `environment:[${monitorEnvs.map(e => e.name).join(',')}]`;
  const issueTypeFilter = issuesType === IssuesType.UNRESOLVED ? 'is:unresolved' : '';
  const issueQuery = `${monitorFilter} ${envFilter} ${issueTypeFilter}`;

  const issueSearchLocation = {
```

---

</SwmSnippet>

## <SwmToken path="static/app/views/monitors/components/monitorStats.tsx" pos="31:2:2" line-data="function MonitorStats({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorStats`</SwmToken>

The <SwmToken path="static/app/views/monitors/components/monitorStats.tsx" pos="31:2:2" line-data="function MonitorStats({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorStats`</SwmToken> function fetches and displays statistical data for a specific monitor. It calculates the time range for the stats based on the selected date range and uses the <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="1:3:3" line-data="import {useApiQuery} from &#39;sentry/utils/queryClient&#39;;">`useApiQuery`</SwmToken> hook to fetch the data. It then processes the data into chart series for display.

<SwmSnippet path="/static/app/views/monitors/components/monitorStats.tsx" line="31">

---

The <SwmToken path="static/app/views/monitors/components/monitorStats.tsx" pos="31:2:2" line-data="function MonitorStats({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorStats`</SwmToken> function calculates the time range for the stats and uses the <SwmToken path="static/app/views/monitors/components/timeline/hooks/useMonitorStats.tsx" pos="1:3:3" line-data="import {useApiQuery} from &#39;sentry/utils/queryClient&#39;;">`useApiQuery`</SwmToken> hook to fetch the data, which is then processed into chart series for display.

```tsx
function MonitorStats({monitor, monitorEnvs, orgSlug}: Props) {
  const {selection} = usePageFilters();
  const {start, end, period} = selection.datetime;

  const nowRef = useRef(new Date());

  let since: number, until: number;
  if (start && end) {
    until = new Date(end).getTime() / 1000;
    since = new Date(start).getTime() / 1000;
  } else {
    until = Math.floor(nowRef.current.getTime() / 1000);
    const intervalSeconds = intervalToMilliseconds(period ?? '30d') / 1000;
    since = until - intervalSeconds;
  }

  const queryKey = [
    `/projects/${orgSlug}/${monitor.project.slug}/monitors/${monitor.slug}/stats/`,
    {
      query: {
        since: since.toString(),
```

---

</SwmSnippet>

# Monitor Endpoints

Monitor Endpoints are used to interact with the monitor data. Some of the key endpoints include Monitor <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken> and Monitor Header Actions.

### Monitor <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken>

The <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken> component fetches and displays recent <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken> for a monitor. It uses the endpoint `/projects/${orgSlug}/${monitor.project.slug}/monitors/${monitor.slug}/checkins/` to retrieve <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="116:7:9" line-data="                    tooltipTitle={tct(&#39;Check-in Status: [status]&#39;, {">`Check-in`</SwmToken> data. This endpoint is used to monitor the status and performance of scheduled tasks.

<SwmSnippet path="/static/app/views/monitors/components/monitorCheckIns.tsx" line="51">

---

The <SwmToken path="static/app/views/monitors/components/monitorCheckIns.tsx" pos="51:2:2" line-data="function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {">`MonitorCheckIns`</SwmToken> component uses the endpoint `/projects/${orgSlug}/${monitor.project.slug}/monitors/${monitor.slug}/checkins/` to fetch recent <SwmToken path="static/app/views/monitors/overview.tsx" pos="170:12:14" line-data="                  &#39;Errors were encountered while ingesting check-ins for the selected projects&#39;">`check-ins`</SwmToken> for a monitor.

```tsx
function MonitorCheckIns({monitor, monitorEnvs, orgSlug}: Props) {
  const location = useLocation();
  const organization = useOrganization();
  const queryKey = [
    `/projects/${orgSlug}/${monitor.project.slug}/monitors/${monitor.slug}/checkins/`,
    {
      query: {
        per_page: '10',
        environment: monitorEnvs.map(e => e.name),
        expand: 'groups',
        ...location.query,
      },
    },
  ] as const;

  const {
    data: checkInList,
    getResponseHeader,
    isPending,
    isError,
  } = useApiQuery<CheckIn[]>(queryKey, {staleTime: 0});
```

---

</SwmSnippet>

### Monitor Header Actions

The <SwmToken path="static/app/views/monitors/components/monitorHeaderActions.tsx" pos="23:2:2" line-data="function MonitorHeaderActions({monitor, orgSlug, onUpdate}: Props) {">`MonitorHeaderActions`</SwmToken> component provides actions for managing a monitor, such as updating its status or deleting it. It uses endpoints like <SwmPath>[src/sentry/templates/sentry/emails/crons/](src/sentry/templates/sentry/emails/crons/)</SwmPath> for navigation after deletion and `/organizations/${orgSlug}/crons/${monitor.project.slug}/${monitor.slug}/edit/` for editing the monitor.

<SwmSnippet path="/static/app/views/monitors/components/monitorHeaderActions.tsx" line="23">

---

The <SwmToken path="static/app/views/monitors/components/monitorHeaderActions.tsx" pos="23:2:2" line-data="function MonitorHeaderActions({monitor, orgSlug, onUpdate}: Props) {">`MonitorHeaderActions`</SwmToken> component provides actions for managing a monitor and uses various endpoints for navigation and editing.

```tsx
function MonitorHeaderActions({monitor, orgSlug, onUpdate}: Props) {
  const api = useApi();
  const {selection} = usePageFilters();

  const endpointOptions = {
    query: {
      project: selection.projects,
      environment: selection.environments,
    },
  };

  const handleDelete = async () => {
    await deleteMonitor(api, orgSlug, monitor);
    browserHistory.push(
      normalizeUrl({
        pathname: `/organizations/${orgSlug}/crons/`,
        query: endpointOptions.query,
      })
    );
  };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

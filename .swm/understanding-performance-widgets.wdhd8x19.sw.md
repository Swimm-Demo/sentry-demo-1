---
title: Understanding Performance Widgets
---
## Overview

Widgets are components used to display various performance metrics and visualizations on the landing page. Each widget is defined by a set of properties such as data type, fields, title, and optional secondary fields. Widgets are categorized under different settings, which determine the type of data they display, such as histograms, area charts, and vital metrics.

## Widget Properties

Widgets are defined by properties such as data type, fields, title, and optional secondary fields. These properties determine what data the widget will display and how it will be visualized.

<SwmSnippet path="/static/app/views/performance/landing/widgets/widgetDefinitions.tsx" line="12">

---

The <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="12:4:4" line-data="export interface ChartDefinition {">`ChartDefinition`</SwmToken> interface outlines the properties that define a widget, including <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="13:1:1" line-data="  dataType: GenericPerformanceWidgetDataType;">`dataType`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="14:1:1" line-data="  fields: string[];">`fields`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="16:1:1" line-data="  title: string;">`title`</SwmToken>, and optional properties like <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="23:1:1" line-data="  secondaryFields?: string[]; // Optional. Will default to colors depending on placement in list or colors from the chart itself.">`secondaryFields`</SwmToken> and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="25:1:1" line-data="  vitalStops?: {">`vitalStops`</SwmToken>.

```tsx
export interface ChartDefinition {
  dataType: GenericPerformanceWidgetDataType;
  fields: string[];
  // Additional fields to get requested but are not directly used in visualization.
  title: string;

  titleTooltip: string;
  // The first field in the list will be treated as the primary field in most widgets (except for special casing).
  allowsOpenInDiscover?: boolean;

  chartColor?: string;
  secondaryFields?: string[]; // Optional. Will default to colors depending on placement in list or colors from the chart itself.

  vitalStops?: {
    meh: number;
    poor: number;
  };
}
```

---

</SwmSnippet>

## Widget Settings

Widgets are categorized under different settings, which determine the type of data they display. Examples include histograms, area charts, and vital metrics.

<SwmSnippet path="/static/app/views/performance/landing/widgets/widgetDefinitions.tsx" line="31">

---

The <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="31:4:4" line-data="export enum PerformanceWidgetSetting {">`PerformanceWidgetSetting`</SwmToken> enum lists various widget settings, such as <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="32:1:1" line-data="  DURATION_HISTOGRAM = &#39;duration_histogram&#39;,">`DURATION_HISTOGRAM`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="33:1:1" line-data="  LCP_HISTOGRAM = &#39;lcp_histogram&#39;,">`LCP_HISTOGRAM`</SwmToken>, and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="36:1:1" line-data="  APDEX_AREA = &#39;apdex_area&#39;,">`APDEX_AREA`</SwmToken>, which define the type of data each widget will display.

```tsx
export enum PerformanceWidgetSetting {
  DURATION_HISTOGRAM = 'duration_histogram',
  LCP_HISTOGRAM = 'lcp_histogram',
  FCP_HISTOGRAM = 'fcp_histogram',
  FID_HISTOGRAM = 'fid_histogram',
  APDEX_AREA = 'apdex_area',
  P50_DURATION_AREA = 'p50_duration_area',
  P75_DURATION_AREA = 'p75_duration_area',
  P95_DURATION_AREA = 'p95_duration_area',
  P99_DURATION_AREA = 'p99_duration_area',
  P75_LCP_AREA = 'p75_lcp_area',
  TPM_AREA = 'tpm_area',
  FAILURE_RATE_AREA = 'failure_rate_area',
  USER_MISERY_AREA = 'user_misery_area',
  WORST_LCP_VITALS = 'worst_lcp_vitals',
  WORST_FCP_VITALS = 'worst_fcp_vitals',
  WORST_CLS_VITALS = 'worst_cls_vitals',
  WORST_FID_VITALS = 'worst_fid_vitals',
```

---

</SwmSnippet>

## Widget Props

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="132:3:3" line-data="  const widgetProps = {">`widgetProps`</SwmToken> object consolidates the properties and settings of a widget, making it easier to pass them around and use them in different components.

<SwmSnippet path="/static/app/views/performance/landing/widgets/components/widgetContainer.tsx" line="132">

---

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="132:3:3" line-data="  const widgetProps = {">`widgetProps`</SwmToken> object includes properties like <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="133:2:2" line-data="    ...chartDefinition,">`chartDefinition`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="134:1:1" line-data="    chartSetting,">`chartSetting`</SwmToken>, and components like <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="139:2:2" line-data="            &lt;WidgetInteractiveTitle">`WidgetInteractiveTitle`</SwmToken> and <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="151:2:2" line-data="          &lt;WidgetContainerActions">`WidgetContainerActions`</SwmToken>.

```tsx
  const widgetProps = {
    ...chartDefinition,
    chartSetting,
    chartDefinition,
    InteractiveTitle:
      showNewWidgetDesign && allowedCharts.length > 2
        ? containerProps => (
            <WidgetInteractiveTitle
              {...containerProps}
              eventView={widgetEventView}
              allowedCharts={allowedCharts}
              chartSetting={chartSetting}
              setChartSetting={setChartSetting}
              rowChartSettings={rowChartSettings}
            />
          )
        : null,
    ContainerActions: !showNewWidgetDesign
      ? containerProps => (
          <WidgetContainerActions
            {...containerProps}
```

---

</SwmSnippet>

## Interactive Widgets

Widgets can be interactive, allowing users to switch between different chart settings and view detailed performance data. This is achieved through components like <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="139:2:2" line-data="            &lt;WidgetInteractiveTitle">`WidgetInteractiveTitle`</SwmToken>.

## Main Functions

There are several main functions related to Widgets. Some of them are <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="383:2:2" line-data="const WidgetContainer = withOrganization(_WidgetContainer);">`WidgetContainer`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="139:2:2" line-data="            &lt;WidgetInteractiveTitle">`WidgetInteractiveTitle`</SwmToken>, and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="79:4:4" line-data="export const WIDGET_DEFINITIONS: ({">`WIDGET_DEFINITIONS`</SwmToken>. We will dive a little into these functions.

### <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="383:2:2" line-data="const WidgetContainer = withOrganization(_WidgetContainer);">`WidgetContainer`</SwmToken>

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="383:2:2" line-data="const WidgetContainer = withOrganization(_WidgetContainer);">`WidgetContainer`</SwmToken> function is responsible for rendering a widget container with various settings and properties. It uses several helper functions like <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="81:7:7" line-data="  const performanceType = usePerformanceDisplayType();">`usePerformanceDisplayType`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="82:7:7" line-data="  let _chartSetting = getChartSetting(">`getChartSetting`</SwmToken>, and <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="90:7:7" line-data="  const allowedCharts = filterAllowedChartsMetrics(">`filterAllowedChartsMetrics`</SwmToken> to determine the appropriate chart settings and allowed charts for the widget.

<SwmSnippet path="/static/app/views/performance/landing/widgets/components/widgetContainer.tsx" line="72">

---

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="383:2:2" line-data="const WidgetContainer = withOrganization(_WidgetContainer);">`WidgetContainer`</SwmToken> function uses helper functions to determine the appropriate chart settings and allowed charts for the widget.

```tsx
function _WidgetContainer(props: Props) {
  const {
    organization,
    index,
    chartHeight,
    rowChartSettings,
    setRowChartSettings,
    ...rest
  } = props;
  const performanceType = usePerformanceDisplayType();
  let _chartSetting = getChartSetting(
    index,
    chartHeight,
    performanceType,
    rest.defaultChartSetting,
    rest.forceDefaultChartSetting
  );
  const mepSetting = useMEPSettingContext();
  const allowedCharts = filterAllowedChartsMetrics(
    props.organization,
    props.allowedCharts,
```

---

</SwmSnippet>

### <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="139:2:2" line-data="            &lt;WidgetInteractiveTitle">`WidgetInteractiveTitle`</SwmToken>

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="139:2:2" line-data="            &lt;WidgetInteractiveTitle">`WidgetInteractiveTitle`</SwmToken> function provides an interactive title for the widget, allowing users to change the chart setting or open the widget in Discover. It uses the <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="224:7:7" line-data="  const organization = useOrganization();">`useOrganization`</SwmToken> and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="79:4:4" line-data="export const WIDGET_DEFINITIONS: ({">`WIDGET_DEFINITIONS`</SwmToken> functions to get the organization-specific settings and definitions for the widget.

<SwmSnippet path="/static/app/views/performance/landing/widgets/components/widgetContainer.tsx" line="217">

---

The <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="217:4:4" line-data="export function WidgetInteractiveTitle({">`WidgetInteractiveTitle`</SwmToken> function uses the <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="224:7:7" line-data="  const organization = useOrganization();">`useOrganization`</SwmToken> and <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="227:7:7" line-data="  const settingsMap = WIDGET_DEFINITIONS({organization});">`WIDGET_DEFINITIONS`</SwmToken> functions to get the organization-specific settings and definitions for the widget.

```tsx
export function WidgetInteractiveTitle({
  chartSetting,
  eventView,
  setChartSetting,
  allowedCharts,
  rowChartSettings,
}) {
  const organization = useOrganization();
  const menuOptions: SelectOption<string>[] = [];

  const settingsMap = WIDGET_DEFINITIONS({organization});
  for (const setting of allowedCharts) {
    const options = settingsMap[setting];
    menuOptions.push({
      value: setting,
      label: options.title,
      disabled: setting !== chartSetting && rowChartSettings.includes(setting),
    });
  }

  const chartDefinition = WIDGET_DEFINITIONS({organization})[chartSetting];
```

---

</SwmSnippet>

### <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="79:4:4" line-data="export const WIDGET_DEFINITIONS: ({">`WIDGET_DEFINITIONS`</SwmToken>

The <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="79:4:4" line-data="export const WIDGET_DEFINITIONS: ({">`WIDGET_DEFINITIONS`</SwmToken> function returns a record of chart definitions based on the organization. Each chart definition includes properties like title, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="18:1:1" line-data="  titleTooltip: string;">`titleTooltip`</SwmToken>, fields, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="13:1:1" line-data="  dataType: GenericPerformanceWidgetDataType;">`dataType`</SwmToken>, and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="22:1:1" line-data="  chartColor?: string;">`chartColor`</SwmToken>. This function is crucial for defining the various types of widgets and their settings.

<SwmSnippet path="/static/app/views/performance/landing/widgets/widgetDefinitions.tsx" line="79">

---

The <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="79:4:4" line-data="export const WIDGET_DEFINITIONS: ({">`WIDGET_DEFINITIONS`</SwmToken> function returns a record of chart definitions based on the organization, including properties like <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="90:1:1" line-data="      title: t(&#39;Duration Distribution&#39;),">`title`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="91:1:1" line-data="      titleTooltip: getTermHelp(organization, PerformanceTerm.DURATION_DISTRIBUTION),">`titleTooltip`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="92:1:1" line-data="      fields: [&#39;transaction.duration&#39;],">`fields`</SwmToken>, <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="93:1:1" line-data="      dataType: GenericPerformanceWidgetDataType.HISTOGRAM,">`dataType`</SwmToken>, and <SwmToken path="static/app/views/performance/landing/widgets/widgetDefinitions.tsx" pos="94:1:1" line-data="      chartColor: WIDGET_PALETTE[5],">`chartColor`</SwmToken>.

```tsx
export const WIDGET_DEFINITIONS: ({
  organization,
}: {
  organization: Organization;
}) => Record<PerformanceWidgetSetting, ChartDefinition> = ({
  organization,
}: {
  organization: Organization;
}) => {
  return {
    [PerformanceWidgetSetting.DURATION_HISTOGRAM]: {
      title: t('Duration Distribution'),
      titleTooltip: getTermHelp(organization, PerformanceTerm.DURATION_DISTRIBUTION),
      fields: ['transaction.duration'],
      dataType: GenericPerformanceWidgetDataType.HISTOGRAM,
      chartColor: WIDGET_PALETTE[5],
    },
    [PerformanceWidgetSetting.LCP_HISTOGRAM]: {
      title: t('LCP Distribution'),
      titleTooltip: getTermHelp(organization, PerformanceTerm.DURATION_DISTRIBUTION),
      fields: ['measurements.lcp'],
```

---

</SwmSnippet>

## Widgets Endpoints

Widgets Endpoints are used to fetch data for the widgets. Two main endpoints are <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="108:3:3" line-data="  const listQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`listQuery`</SwmToken> and <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="170:3:3" line-data="  const chartQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`chartQuery`</SwmToken>.

### <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="108:3:3" line-data="  const listQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`listQuery`</SwmToken>

The <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="108:3:3" line-data="  const listQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`listQuery`</SwmToken> endpoint is defined within the <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="26:2:2" line-data="import MobileReleaseComparisonListWidget from &#39;sentry/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget&#39;;">`MobileReleaseComparisonListWidget`</SwmToken> component. It constructs a query to fetch a list of data based on the widget's settings and selected filters. The query is transformed using <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="40:3:3" line-data="import {transformDiscoverToList} from &#39;../transforms/transformDiscoverToList&#39;;">`transformDiscoverToList`</SwmToken> before being used in the widget.

<SwmSnippet path="/static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" line="108">

---

The <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="108:3:3" line-data="  const listQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`listQuery`</SwmToken> endpoint constructs a query to fetch a list of data based on the widget's settings and selected filters.

```tsx
  const listQuery = useMemo<QueryDefinition<DataType, WidgetDataResult>>(
    () => ({
      fields: field,
      component: provided => {
        if (isLoadingReleases || (!primaryRelease && !secondaryRelease)) {
          return null;
        }

        const eventView = provided.eventView.clone();
        let extraQueryParams = getMEPParamsIfApplicable(mepSetting, props.chartSetting);

        // Set fields
        const sortField = {
          [PerformanceWidgetSetting.SLOW_SCREENS_BY_TTID]: 'count()',
          [PerformanceWidgetSetting.SLOW_SCREENS_BY_COLD_START]:
            'count_starts(measurements.app_start_cold)',
          [PerformanceWidgetSetting.SLOW_SCREENS_BY_WARM_START]:
            'count_starts(measurements.app_start_warm)',
        }[props.chartSetting];
        eventView.fields = [{field: 'transaction'}, {field}, {field: sortField}];
        eventView.sorts = [
```

---

</SwmSnippet>

### <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="170:3:3" line-data="  const chartQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`chartQuery`</SwmToken>

The <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="170:3:3" line-data="  const chartQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`chartQuery`</SwmToken> endpoint is another query defined in the <SwmToken path="static/app/views/performance/landing/widgets/components/widgetContainer.tsx" pos="26:2:2" line-data="import MobileReleaseComparisonListWidget from &#39;sentry/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget&#39;;">`MobileReleaseComparisonListWidget`</SwmToken> component. It is used to fetch chart data based on the widget's settings and selected filters. The query is transformed using <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="41:5:5" line-data="import type {transformEventsRequestToArea} from &#39;../transforms/transformEventsToArea&#39;;">`transformEventsRequestToArea`</SwmToken> before being used in the widget.

<SwmSnippet path="/static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" line="170">

---

The <SwmToken path="static/app/views/performance/landing/widgets/widgets/mobileReleaseComparisonListWidget.tsx" pos="170:3:3" line-data="  const chartQuery = useMemo&lt;QueryDefinition&lt;DataType, WidgetDataResult&gt;&gt;(">`chartQuery`</SwmToken> endpoint is used to fetch chart data based on the widget's settings and selected filters.

```tsx
  const chartQuery = useMemo<QueryDefinition<DataType, WidgetDataResult>>(
    () => {
      return {
        enabled: widgetData => {
          return !!widgetData?.list?.data?.length;
        },
        fields: field,
        component: provided => {
          if (selectedListIndex < 0) {
            return null;
          }

          const eventView = props.eventView.clone();
          let extraQueryParams = getMEPParamsIfApplicable(mepSetting, props.chartSetting);
          const pageFilterDatetime = {
            start: provided.start,
            end: provided.end,
            period: provided.period,
          };

          // Chart options
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

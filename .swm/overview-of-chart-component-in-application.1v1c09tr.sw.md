---
title: Overview of Chart Component in Application
---
# Overview

Charts are visual representations of data used to display various metrics and trends. They are essential for providing insights and understanding data patterns.

# Chart Class

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> class is a core component that handles the rendering and updating of charts based on the provided data and configuration. It manages the state and determines whether the component should update based on changes in props and state.

# <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="139:1:1" line-data="  getChartComponent(): ChartComponent {">`getChartComponent`</SwmToken> Method

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="139:1:1" line-data="  getChartComponent(): ChartComponent {">`getChartComponent`</SwmToken> method within the <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> class determines the type of chart to render, such as <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="147:3:3" line-data="      return BarChart;">`BarChart`</SwmToken>, <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="153:3:3" line-data="          return LineChart;">`LineChart`</SwmToken>, or <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="155:3:3" line-data="          return AreaChart;">`AreaChart`</SwmToken>, based on the properties like <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="140:4:4" line-data="    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;">`showDaily`</SwmToken> and <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="140:7:7" line-data="    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;">`timeseriesData`</SwmToken>.

<SwmSnippet path="/static/app/components/charts/eventsChart.tsx" line="139">

---

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="139:1:1" line-data="  getChartComponent(): ChartComponent {">`getChartComponent`</SwmToken> method determines the type of chart to render based on the properties like <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="140:4:4" line-data="    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;">`showDaily`</SwmToken> and <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="140:7:7" line-data="    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;">`timeseriesData`</SwmToken>.

```tsx
  getChartComponent(): ChartComponent {
    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;

    if (defined(chartComponent)) {
      return chartComponent;
    }

    if (showDaily) {
      return BarChart;
    }

    if (timeseriesData.length > 1) {
      switch (aggregateMultiPlotType(yAxis)) {
        case 'line':
          return LineChart;
        case 'area':
          return AreaChart;
        default:
          throw new Error(`Unknown multi plot type for ${yAxis}`);
      }
    }
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/charts/eventsChart.tsx" line="344">

---

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:2:2" line-data="const ThemedChart = withTheme(Chart);">`ThemedChart`</SwmToken> constant applies theming to the <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> component using the <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:6:6" line-data="const ThemedChart = withTheme(Chart);">`withTheme`</SwmToken> higher-order component.

```tsx
const ThemedChart = withTheme(Chart);
```

---

</SwmSnippet>

# Chart Integration

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> component integrates with various sub-components located in the <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="16:13:13" line-data="import type {AreaChartProps} from &#39;sentry/components/charts/areaChart&#39;;">`components`</SwmToken> directory, such as <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="140:10:10" line-data="    const {showDaily, timeseriesData, yAxis, chartComponent} = this.props;">`yAxis`</SwmToken>, <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="71:10:10" line-data="  chartOptions?: Omit&lt;EChartsOption, &#39;xAxis&#39; | &#39;yAxis&#39;&gt; &amp; {">`xAxis`</SwmToken>, <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="285:1:1" line-data="      tooltip: {">`tooltip`</SwmToken>, and <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="242:3:3" line-data="    const legend = showLegend">`legend`</SwmToken>, to build a complete chart.

# Chart Usage

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> component is utilized in multiple files, including <SwmPath>[static/app/components/charts/baseChart.tsx](static/app/components/charts/baseChart.tsx)</SwmPath>, <SwmPath>[static/app/components/charts/barChartZoom.tsx](static/app/components/charts/barChartZoom.tsx)</SwmPath>, and <SwmPath>[static/app/components/charts/miniBarChart.tsx](static/app/components/charts/miniBarChart.tsx)</SwmPath>, to provide consistent chart functionality across different parts of the application.

<SwmSnippet path="/static/app/components/charts/eventsChart.tsx" line="1">

---

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="344:8:8" line-data="const ThemedChart = withTheme(Chart);">`Chart`</SwmToken> component is utilized in multiple files to provide consistent chart functionality across different parts of the application.

```tsx
import {Component, isValidElement} from 'react';
import type {InjectedRouter} from 'react-router';
import type {Theme} from '@emotion/react';
import {withTheme} from '@emotion/react';
import type {
  EChartsOption,
  LegendComponentOption,
  LineSeriesOption,
  XAXisComponentOption,
  YAXisComponentOption,
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/charts/eventsChart.tsx" line="560">

---

The <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="560:3:3" line-data="    let chartImplementation = ({">`chartImplementation`</SwmToken> function handles rendering the chart with the appropriate data and configuration.

```tsx
    let chartImplementation = ({
      zoomRenderProps,
      releaseSeries,
      errored,
      loading,
      reloading,
      results,
      timeseriesData,
      previousTimeseriesData,
      timeframe,
      tableData,
      timeseriesResultsTypes,
    }: ChartDataProps) => {
      if (errored) {
        return (
          <ErrorPanel>
            <IconWarning color="gray300" size="lg" />
          </ErrorPanel>
        );
      }
      const seriesData = results ? results : timeseriesData;
```

---

</SwmSnippet>

# Charts Endpoints

Charts endpoints are used to fetch data for rendering charts. Two main endpoints are <SwmToken path="static/app/components/charts/sessionsRequest.tsx" pos="49:2:2" line-data="class SessionsRequest extends Component&lt;Props, State&gt; {">`SessionsRequest`</SwmToken> and <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="267:2:2" line-data="class EventsRequest extends PureComponent&lt;EventsRequestProps, EventsRequestState&gt; {">`EventsRequest`</SwmToken>.

<SwmSnippet path="/static/app/components/charts/sessionsRequest.tsx" line="68">

---

The <SwmToken path="static/app/components/charts/sessionsRequest.tsx" pos="49:2:2" line-data="class SessionsRequest extends Component&lt;Props, State&gt; {">`SessionsRequest`</SwmToken> component defines an endpoint for fetching session data.

```tsx
  get path() {
    const {organization} = this.props;

    return `/organizations/${organization.slug}/sessions/`;
  }
```

---

</SwmSnippet>

## <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="267:2:2" line-data="class EventsRequest extends PureComponent&lt;EventsRequestProps, EventsRequestState&gt; {">`EventsRequest`</SwmToken> Endpoint

The <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="267:2:2" line-data="class EventsRequest extends PureComponent&lt;EventsRequestProps, EventsRequestState&gt; {">`EventsRequest`</SwmToken> component defines an endpoint for fetching event statistics. The endpoint URL is dynamically generated based on the organization and other query parameters. This component handles various props such as <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="358:3:3" line-data="   * Project ids">`Project`</SwmToken>, <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="353:3:3" line-data="   * Environment condition.">`Environment`</SwmToken>, <SwmToken path="static/app/components/charts/eventsChart.tsx" pos="408:1:1" line-data="  field?: string[];">`field`</SwmToken>, <SwmToken path="static/app/components/charts/sessionsRequest.tsx" pos="40:1:1" line-data="  statsPeriod?: string | null;">`statsPeriod`</SwmToken>, <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="270:1:1" line-data="    start: null,">`start`</SwmToken>, <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="271:1:1" line-data="    end: null,">`end`</SwmToken>, and <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="275:1:1" line-data="    query: &#39;&#39;,">`query`</SwmToken> to construct the query parameters for the API request.

<SwmSnippet path="/static/app/components/charts/eventsRequest.tsx" line="267">

---

The <SwmToken path="static/app/components/charts/eventsRequest.tsx" pos="267:2:2" line-data="class EventsRequest extends PureComponent&lt;EventsRequestProps, EventsRequestState&gt; {">`EventsRequest`</SwmToken> component defines an endpoint for fetching event statistics.

```tsx
class EventsRequest extends PureComponent<EventsRequestProps, EventsRequestState> {
  static defaultProps: DefaultProps = {
    period: undefined,
    start: null,
    end: null,
    interval: '1d',
    comparisonDelta: undefined,
    limit: 15,
    query: '',
    includePrevious: true,
    includeTransformedData: true,
  };

  state: EventsRequestState = {
    reloading: !!this.props.loading,
    errored: false,
    timeseriesData: null,
    fetchedWithPrevious: false,
  };

  componentDidMount() {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

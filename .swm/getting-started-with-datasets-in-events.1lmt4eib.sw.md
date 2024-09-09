---
title: Getting started with Datasets in Events
---
# Getting Started with Datasets in Events

Datasets are configurations used to define the structure and behavior of different types of data within the Events module. They are implemented through the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:14:14" line-data="from sentry.search.events.datasets.base import DatasetConfig">`DatasetConfig`</SwmToken> class, which is imported from the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:2:10" line-data="from sentry.search.events.datasets.base import DatasetConfig">`sentry.search.events.datasets.base`</SwmToken> module. These configurations include various aliases for fields and filters, which help in querying and manipulating the data. Different datasets are defined for various purposes, such as metrics, profiles, sessions, and spans, each with its own specific configuration.

## Dataset Configuration

The <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:14:14" line-data="from sentry.search.events.datasets.base import DatasetConfig">`DatasetConfig`</SwmToken> class is used across multiple files within the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="14:8:8" line-data="from sentry.search.events.datasets import field_aliases, filter_aliases">`datasets`</SwmToken> directory, ensuring consistent data handling and querying capabilities. Below is an example of how the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:14:14" line-data="from sentry.search.events.datasets.base import DatasetConfig">`DatasetConfig`</SwmToken> class is imported and used in the <SwmPath>[src/sentry/search/events/datasets/profiles.py](src/sentry/search/events/datasets/profiles.py)</SwmPath> file.

<SwmSnippet path="/src/sentry/search/events/datasets/profiles.py" line="13">

---

This snippet shows the import statements for the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:14:14" line-data="from sentry.search.events.datasets.base import DatasetConfig">`DatasetConfig`</SwmToken> class and other related modules.

```python
from sentry.search.events.constants import PROJECT_ALIAS, PROJECT_NAME_ALIAS
from sentry.search.events.datasets import field_aliases, filter_aliases
from sentry.search.events.datasets.base import DatasetConfig
from sentry.search.events.fields import (
    ColumnArg,
```

---

</SwmSnippet>

## Function Converter

The <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method in the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="15:14:14" line-data="from sentry.search.events.datasets.base import DatasetConfig">`DatasetConfig`</SwmToken> class defines various functions that can be used to query the dataset. These functions include aggregations like <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="202:2:2" line-data="                    &quot;last_seen&quot;,">`last_seen`</SwmToken>, <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="212:2:2" line-data="                    &quot;latest_event&quot;,">`latest_event`</SwmToken>, <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="221:2:2" line-data="                    &quot;count&quot;,">`count`</SwmToken>, and various percentiles. Below is an example of the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/datasets/profiles.py" line="195">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method, which maps function names to their corresponding <SwmToken path="src/sentry/search/events/fields.py" pos="1160:18:18" line-data="        # TODO: These are no longer expressions with SnQL, this should be removed once the">`SnQL`</SwmToken> functions.

```python
    def function_converter(self) -> Mapping[str, SnQLFunction]:
        return {
            function.name: function
            for function in [
                # TODO: A lot of this is duplicated from the discover dataset.
                # Ideally, we refactor it to be shared across datasets.
                SnQLFunction(
                    "last_seen",
                    snql_aggregate=lambda _, alias: Function(
                        "max",
                        [self.builder.column("timestamp")],
                        alias,
                    ),
                    default_result_type="date",
                    redundant_grouping=True,
                ),
                SnQLFunction(
                    "latest_event",
                    snql_aggregate=lambda _, alias: Function(
                        "argMax",
                        [self.builder.column("id"), self.builder.column("timestamp")],
```

---

</SwmSnippet>

## Reflective Result Type

The <SwmToken path="src/sentry/search/events/datasets/base.py" pos="50:3:3" line-data="    def reflective_result_type(">`reflective_result_type`</SwmToken> method is used to determine the type of the metric, defaulting to duration. It is used within the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method to ensure the correct result type is returned for each function. Below is an example of the <SwmToken path="src/sentry/search/events/datasets/base.py" pos="50:3:3" line-data="    def reflective_result_type(">`reflective_result_type`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/datasets/base.py" line="50">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/base.py" pos="50:3:3" line-data="    def reflective_result_type(">`reflective_result_type`</SwmToken> method, which returns the type of the metric based on the provided arguments.

```python
    def reflective_result_type(
        self, index: int = 0
    ) -> Callable[[list[fields.FunctionArg], dict[str, Any]], str]:
        """Return the type of the metric, default to duration

        based on fields.reflective_result_type, but in this config since we need the _custom_measurement_cache
        """

        def result_type_fn(
            function_arguments: list[fields.FunctionArg], parameter_values: dict[str, Any]
        ) -> str:
            argument = function_arguments[index]
            value = parameter_values[argument.name]
            if (field_type := self.builder.get_field_type(value)) is not None:  # type: ignore[attr-defined]
                return field_type
            else:
                return argument.get_type(value)

        return result_type_fn
```

---

</SwmSnippet>

## With Default

The <SwmToken path="src/sentry/search/events/fields.py" pos="1225:2:2" line-data="def with_default(default, argument):">`with_default`</SwmToken> method is used to set default values for arguments in the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method. This ensures that functions have the necessary default values when they are called. Below is an example of the <SwmToken path="src/sentry/search/events/fields.py" pos="1225:2:2" line-data="def with_default(default, argument):">`with_default`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/fields.py" line="1225">

---

This snippet shows the <SwmToken path="src/sentry/search/events/fields.py" pos="1225:2:2" line-data="def with_default(default, argument):">`with_default`</SwmToken> method, which sets default values for function arguments.

```python
def with_default(default, argument):
    argument.has_default = True
    argument.get_default = lambda *_: default
    return argument
```

---

</SwmSnippet>

## Resolve Percentile

The <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="377:3:3" line-data="    def _resolve_percentile(">`_resolve_percentile`</SwmToken> method is used to calculate percentiles for a given column. It is used within the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method to define various percentile functions like <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="247:2:2" line-data="                    &quot;p50&quot;,">`p50`</SwmToken>, <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="257:2:2" line-data="                    &quot;p75&quot;,">`p75`</SwmToken>, <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="267:2:2" line-data="                    &quot;p95&quot;,">`p95`</SwmToken>, and <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="277:2:2" line-data="                    &quot;p99&quot;,">`p99`</SwmToken>. Below is an example of the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="377:3:3" line-data="    def _resolve_percentile(">`_resolve_percentile`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/datasets/profiles.py" line="377">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="377:3:3" line-data="    def _resolve_percentile(">`_resolve_percentile`</SwmToken> method, which calculates percentiles for a given column.

```python
    def _resolve_percentile(
        self,
        args: Mapping[str, str | Column | SelectType | int | float],
        alias: str,
        fixed_percentile: float | None = None,
    ) -> SelectType:
        return (
            Function(
                "max",
                [args["column"]],
                alias,
            )
            if fixed_percentile == 1
            else Function(
                f'quantile({fixed_percentile if fixed_percentile is not None else args["percentile"]})',
                [args["column"]],
                alias,
            )
        )
```

---

</SwmSnippet>

## Main Functions

There are several main functions in this folder. Some of them are <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken>, <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="185:3:3" line-data="    def field_alias_converter(self) -&gt; Mapping[str, Callable[[str], SelectType]]:">`field_alias_converter`</SwmToken>, and <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken>. We will dive a little into <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken> and <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken>.

### <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken>

The <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken> property returns a mapping of search filters to their corresponding converter functions. This allows for the conversion of search filters into conditions that can be used in queries. Below is an example of the <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/datasets/profile_functions.py" line="151">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/profile_functions.py" pos="151:3:3" line-data="    def search_filter_converter(">`search_filter_converter`</SwmToken> method, which maps search filters to their corresponding converter functions.

```python
    def search_filter_converter(
        self,
    ) -> Mapping[str, Callable[[SearchFilter], WhereType | None]]:
        return {
            "fingerprint": self._fingerprint_filter_converter,
            "message": self._message_filter_converter,
            PROJECT_ALIAS: self._project_slug_filter_converter,
            PROJECT_NAME_ALIAS: self._project_slug_filter_converter,
        }
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/search/events/datasets/profiles.py" line="195">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="195:3:3" line-data="    def function_converter(self) -&gt; Mapping[str, SnQLFunction]:">`function_converter`</SwmToken> method, which maps function names to their corresponding <SwmToken path="src/sentry/search/events/fields.py" pos="1160:18:18" line-data="        # TODO: These are no longer expressions with SnQL, this should be removed once the">`SnQL`</SwmToken> functions.

```python
    def function_converter(self) -> Mapping[str, SnQLFunction]:
        return {
            function.name: function
            for function in [
                # TODO: A lot of this is duplicated from the discover dataset.
                # Ideally, we refactor it to be shared across datasets.
                SnQLFunction(
                    "last_seen",
                    snql_aggregate=lambda _, alias: Function(
                        "max",
                        [self.builder.column("timestamp")],
                        alias,
                    ),
                    default_result_type="date",
                    redundant_grouping=True,
                ),
                SnQLFunction(
                    "latest_event",
                    snql_aggregate=lambda _, alias: Function(
                        "argMax",
                        [self.builder.column("id"), self.builder.column("timestamp")],
```

---

</SwmSnippet>

## Dataset Endpoints

Dataset Endpoints provide various functionalities to interact with datasets. We will cover two main endpoints: <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="68:3:3" line-data="    def resolve_metric(self, value: str) -&gt; int:">`resolve_metric`</SwmToken> and `resolve_total_span_duration`.

### <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="68:3:3" line-data="    def resolve_metric(self, value: str) -&gt; int:">`resolve_metric`</SwmToken>

The <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="68:3:3" line-data="    def resolve_metric(self, value: str) -&gt; int:">`resolve_metric`</SwmToken> function is used to resolve a metric ID based on a given value. It utilizes the <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="69:13:13" line-data="        metric_id = self.builder.resolve_metric_index(constants.SPAN_METRICS_MAP.get(value, value))">`SPAN_METRICS_MAP`</SwmToken> to find the corresponding metric index. If the metric ID is not found, it raises an <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="75:3:3" line-data="                raise IncompatibleMetricsQuery(f&quot;Metric: {value} could not be resolved&quot;)">`IncompatibleMetricsQuery`</SwmToken> exception. Below is an example of the <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="68:3:3" line-data="    def resolve_metric(self, value: str) -&gt; int:">`resolve_metric`</SwmToken> method.

<SwmSnippet path="/src/sentry/search/events/datasets/spans_metrics.py" line="68">

---

This snippet shows the <SwmToken path="src/sentry/search/events/datasets/spans_metrics.py" pos="68:3:3" line-data="    def resolve_metric(self, value: str) -&gt; int:">`resolve_metric`</SwmToken> method, which resolves a metric ID based on a given value.

```python
    def resolve_metric(self, value: str) -> int:
        metric_id = self.builder.resolve_metric_index(constants.SPAN_METRICS_MAP.get(value, value))
        # If its still None its not a custom measurement
        if metric_id is None:
            if constants.SPAN_METRICS_MAP.get(value, value) in self.nullable_metrics:
                metric_id = 0
            else:
                raise IncompatibleMetricsQuery(f"Metric: {value} could not be resolved")
        if metric_id != 0:
            self.builder.metric_ids.add(metric_id)
        return metric_id
```

---

</SwmSnippet>

### resolve_total_span_duration

The `resolve_total_span_duration` function calculates the total time based on the provided scope and returns the result. It uses the <SwmToken path="src/sentry/search/events/datasets/profiles.py" pos="197:1:1" line-data="            function.name: function">`function`</SwmToken> class to create the necessary query expressions. Below is an example of the `resolve_total_span_duration` method.

<SwmSnippet path="/src/sentry/search/events/datasets/spans_metrics.py" line="774">

---

This snippet shows the `resolve_total_span_duration` method, which calculates the total time based on the provided scope.

```python
    def _resolve_total_span_duration(self, alias: str, scope: str, column: str) -> SelectType:
        """This calculates the total time, and based on the scope will return
        either the apps total time or whatever other local scope/filters are
        applied.
        This must be cached since it runs another query."""
        self.builder.requires_other_aggregates = True
        if self.total_span_duration is not None:
            return Function("toFloat64", [self.total_span_duration], alias)

        total_query = spans_metrics.SpansMetricsQueryBuilder(
            dataset=self.builder.dataset,
            params={},
            snuba_params=self.builder.params,
            query=self.builder.query if scope == "local" else None,
            selected_columns=[f"sum({column})"],
        )
        sentry_sdk.set_tag("query.resolved_total", scope)

        total_results = total_query.run_query(
            Referrer.API_DISCOVER_TOTAL_SUM_TRANSACTION_DURATION_FIELD.value
        )
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

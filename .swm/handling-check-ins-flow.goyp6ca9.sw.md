---
title: Handling Check-ins Flow
---
In this document, we will explain the process of handling <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken> for a monitoring system. The process involves grouping related <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken>, processing each <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> individually, validating and handling errors, and updating the status of the monitor environment based on the outcome of the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken>.

The flow starts by grouping related <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken> and then processing each <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> one by one. Each <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> is validated and any errors are handled. Depending on whether the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> is successful or not, the status of the monitor environment is updated. If the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> is successful, the status is marked as OK and any active incidents are resolved. If the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> fails, the status is marked as failed and incidents are created.

# Flow drill down

```mermaid
graph TD;
      subgraph src/sentry/monitors/consumers/monitor_consumer.py
8710859a8a1bca4136c65e100e295527355f2f84820cbaf0f098f2633e1dea1e(process_checkin_group):::mainFlowStyle --> faea4b374d72e0357a1d934071b881dc0a57b2a1f9d8d1af2a8604ec76cfb04d(process_checkin):::mainFlowStyle
end

subgraph src/sentry/monitors/consumers/monitor_consumer.py
faea4b374d72e0357a1d934071b881dc0a57b2a1f9d8d1af2a8604ec76cfb04d(process_checkin):::mainFlowStyle --> 49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle
end

subgraph src/sentry/monitors/logic
49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle --> 4b6399e88df466f91c1d2edc7801b7e5fcf29b0902b03ce4a747483f84ea87ca(mark_ok)
end

subgraph src/sentry/monitors/logic
49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle --> 3eb28bc71e091bfc187e6f41f170bb16f6aec3c1dcc8ea6d7fa47af850f677b0(mark_failed):::mainFlowStyle
end

subgraph src/sentry/monitors/logic
4b6399e88df466f91c1d2edc7801b7e5fcf29b0902b03ce4a747483f84ea87ca(mark_ok) --> ca9a9177bd8a826799b1fe7f05b2adc3edf8ab516a117227a8d569644c99be78(resolve_incident_group)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[src/sentry/monitors/consumers/monitor_consumer.py](src/sentry/monitors/consumers/monitor_consumer.py)</SwmPath>
%% 8710859a8a1bca4136c65e100e295527355f2f84820cbaf0f098f2633e1dea1e(process_checkin_group):::mainFlowStyle --> faea4b374d72e0357a1d934071b881dc0a57b2a1f9d8d1af2a8604ec76cfb04d(process_checkin):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/monitors/consumers/monitor_consumer.py](src/sentry/monitors/consumers/monitor_consumer.py)</SwmPath>
%% faea4b374d72e0357a1d934071b881dc0a57b2a1f9d8d1af2a8604ec76cfb04d(process_checkin):::mainFlowStyle --> 49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/monitors/logic/](src/sentry/monitors/logic/)</SwmPath>
%% 49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle --> 4b6399e88df466f91c1d2edc7801b7e5fcf29b0902b03ce4a747483f84ea87ca(mark_ok)
%% end
%% 
%% subgraph <SwmPath>[src/sentry/monitors/logic/](src/sentry/monitors/logic/)</SwmPath>
%% 49e828fe97de0244fbccd6ad74badbb05ce40a22a433f45fb32f24bc5380d52a(_process_checkin):::mainFlowStyle --> 3eb28bc71e091bfc187e6f41f170bb16f6aec3c1dcc8ea6d7fa47af850f677b0(mark_failed):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/monitors/logic/](src/sentry/monitors/logic/)</SwmPath>
%% 4b6399e88df466f91c1d2edc7801b7e5fcf29b0902b03ce4a747483f84ea87ca(mark_ok) --> ca9a9177bd8a826799b1fe7f05b2adc3edf8ab516a117227a8d569644c99be78(resolve_incident_group)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/src/sentry/monitors/consumers/monitor_consumer.py" line="934">

---

## Processing <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> Group

The function <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="934:2:2" line-data="def process_checkin_group(items: list[CheckinItem]):">`process_checkin_group`</SwmToken> processes a group of related <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken> serially by iterating over each item and calling the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="940:1:1" line-data="        process_checkin(item)">`process_checkin`</SwmToken> function.

```python
def process_checkin_group(items: list[CheckinItem]):
    """
    Process a group of related check-ins (all part of the same monitor)
    completely serially.
    """
    for item in items:
        process_checkin(item)
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/monitors/consumers/monitor_consumer.py" line="916">

---

## Processing Individual <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken>

The function <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="916:2:2" line-data="def process_checkin(item: CheckinItem):">`process_checkin`</SwmToken> processes an individual <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken>. It starts a transaction and calls <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="922:4:4" line-data="            op=&quot;_process_checkin&quot;,">`_process_checkin`</SwmToken> with a deep copy of the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> item. If any processing errors occur, they are handled appropriately.

```python
def process_checkin(item: CheckinItem):
    """
    Process an individual check-in
    """
    try:
        with sentry_sdk.start_transaction(
            op="_process_checkin",
            name="monitors.monitor_consumer",
        ) as txn:
            # Deepcopy the checkin here so that it's not modified. We need the original when we get a
            # `ProcessingErrorsException`
            _process_checkin(deepcopy(item), txn)
    except ProcessingErrorsException as e:
        handle_processing_errors(item, e)
    except Exception:
        logger.exception("Failed to process check-in")
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/monitors/consumers/monitor_consumer.py" line="409">

---

### Validating and Handling <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="936:11:13" line-data="    Process a group of related check-ins (all part of the same monitor)">`check-ins`</SwmToken>

The function <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="409:2:2" line-data="def _process_checkin(item: CheckinItem, txn: Transaction | Span):">`_process_checkin`</SwmToken> performs the core logic for processing a <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken>. It validates the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken>, checks for rate limits and quotas, and ensures the monitor and its environment are correctly configured. If any validation or processing errors occur, they are raised as <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="926:4:4" line-data="            # `ProcessingErrorsException`">`ProcessingErrorsException`</SwmToken>.

```python
def _process_checkin(item: CheckinItem, txn: Transaction | Span):
    params = item.payload

    start_time = to_datetime(float(item.message["start_time"]))
    project_id = int(item.message["project_id"])
    source_sdk = item.message["sdk"]

    monitor_slug = item.valid_monitor_slug
    environment = params.get("environment")

    project = Project.objects.get_from_cache(id=project_id)

    # Strip sdk version to reduce metric cardinality
    sdk_platform = source_sdk.split("/")[0] if source_sdk else "none"

    metric_kwargs = {
        "source": "consumer",
        "sdk_platform": sdk_platform,
    }

    if check_killswitch(metric_kwargs, project):
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/monitors/logic/mark_ok.py" line="23">

---

## Marking <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> as OK

The function <SwmToken path="src/sentry/monitors/logic/mark_ok.py" pos="23:2:2" line-data="def mark_ok(checkin: MonitorCheckIn, ts: datetime) -&gt; None:">`mark_ok`</SwmToken> updates the monitor environment status to OK if the <SwmToken path="src/sentry/monitors/consumers/monitor_consumer.py" pos="918:7:9" line-data="    Process an individual check-in">`check-in`</SwmToken> is successful. It also handles resolving any active incidents associated with the monitor.

```python
def mark_ok(checkin: MonitorCheckIn, ts: datetime) -> None:
    monitor_env = checkin.monitor_environment

    if monitor_env is None:
        return None

    next_checkin = monitor_env.monitor.get_next_expected_checkin(ts)
    next_checkin_latest = monitor_env.monitor.get_next_expected_checkin_latest(ts)

    params: _Params = {
        "last_checkin": checkin.date_added,
        "next_checkin": next_checkin,
        "next_checkin_latest": next_checkin_latest,
    }

    if monitor_env.status != MonitorStatus.OK and checkin.status == CheckInStatus.OK:
        recovery_threshold = monitor_env.monitor.config.get("recovery_threshold", 1)
        if not recovery_threshold:
            recovery_threshold = 1

        # Run incident logic if recovery threshold is set
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/monitors/logic/mark_failed.py" line="29">

---

## Marking <SwmToken path="src/sentry/monitors/logic/mark_failed.py" pos="35:7:9" line-data="    Given a failing check-in, mark the monitor environment as failed and trigger">`check-in`</SwmToken> as Failed

The function <SwmToken path="src/sentry/monitors/logic/mark_failed.py" pos="29:2:2" line-data="def mark_failed(">`mark_failed`</SwmToken> updates the monitor environment status to failed if the <SwmToken path="src/sentry/monitors/logic/mark_failed.py" pos="35:7:9" line-data="    Given a failing check-in, mark the monitor environment as failed and trigger">`check-in`</SwmToken> fails. It triggers side effects for creating monitor incidents and issues.

```python
def mark_failed(
    failed_checkin: MonitorCheckIn,
    ts: datetime,
    received: datetime | None = None,
) -> bool:
    """
    Given a failing check-in, mark the monitor environment as failed and trigger
    side effects for creating monitor incidents and issues.

    The provided `ts` is the reference time for when the next check-in time is
    calculated from. This typically would be the failed check-in's `date_added`
    or completion time. Though for the missed and timedout tasks this may be
    computed based on the tasks reference time.
    """
    monitor_env = failed_checkin.monitor_environment

    if monitor_env is None:
        return False

    failure_issue_threshold = monitor_env.monitor.config.get("failure_issue_threshold", 1)
    if not failure_issue_threshold:
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/monitors/logic/mark_ok.py" line="99">

---

## Resolving Incident Group

The function <SwmToken path="src/sentry/monitors/logic/mark_ok.py" pos="99:2:2" line-data="def resolve_incident_group(">`resolve_incident_group`</SwmToken> resolves any open incidents associated with the monitor by producing a status change message to Kafka.

```python
def resolve_incident_group(
    fingerprint: str,
    project_id: int,
):
    from sentry.issues.producer import PayloadType, produce_occurrence_to_kafka
    from sentry.issues.status_change_message import StatusChangeMessage
    from sentry.models.group import GroupStatus

    status_change = StatusChangeMessage(
        fingerprint=[fingerprint],
        project_id=project_id,
        new_status=GroupStatus.RESOLVED,
        new_substatus=None,
    )

    produce_occurrence_to_kafka(
        payload_type=PayloadType.STATUS_CHANGE,
        status_change=status_change,
    )
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

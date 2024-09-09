---
title: Basic Concepts of Actions in Rules
---
# Basic Concepts of Actions in Rules

Actions are specific operations executed when certain conditions in a rule are met. They define what should happen after a rule matches an event. Actions can include operations like sending notifications, creating tickets, or integrating with third-party services.

# <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:10:10" line-data="from sentry.rules.actions import EventAction">`EventAction`</SwmToken> Class

The <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:10:10" line-data="from sentry.rules.actions import EventAction">`EventAction`</SwmToken> class is a base class for defining actions, ensuring they follow a standard structure and behavior. Actions are instantiated and executed as part of the rule evaluation process, ensuring the defined responses are triggered appropriately.

<SwmSnippet path="/src/sentry/rules/actions/integrations/base.py" line="16">

---

The <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:10:10" line-data="from sentry.rules.actions import EventAction">`EventAction`</SwmToken> class is imported from <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:2:6" line-data="from sentry.rules.actions import EventAction">`sentry.rules.actions`</SwmToken>.

```python
from sentry.rules.actions import EventAction
```

---

</SwmSnippet>

# <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="21:2:2" line-data="class IntegrationEventAction(EventAction, abc.ABC):">`IntegrationEventAction`</SwmToken> Class

The <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="21:2:2" line-data="class IntegrationEventAction(EventAction, abc.ABC):">`IntegrationEventAction`</SwmToken> class extends <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:10:10" line-data="from sentry.rules.actions import EventAction">`EventAction`</SwmToken> and provides additional methods and properties to handle integration-specific actions.

<SwmSnippet path="/src/sentry/rules/actions/integrations/base.py" line="21">

---

The <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="21:2:2" line-data="class IntegrationEventAction(EventAction, abc.ABC):">`IntegrationEventAction`</SwmToken> class includes abstract methods like <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="26:3:3" line-data="    def prompt(self) -&gt; str:">`prompt`</SwmToken>, <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="31:3:3" line-data="    def provider(self) -&gt; str:">`provider`</SwmToken>, and <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="36:3:3" line-data="    def integration_key(self) -&gt; str:">`integration_key`</SwmToken>, and a method <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="39:3:3" line-data="    def is_enabled(self) -&gt; bool:">`is_enabled`</SwmToken> to check if the integration is enabled.

```python
class IntegrationEventAction(EventAction, abc.ABC):
    """Intermediate abstract class to help DRY some event actions code."""

    @property
    @abc.abstractmethod
    def prompt(self) -> str:
        pass

    @property
    @abc.abstractmethod
    def provider(self) -> str:
        pass

    @property
    @abc.abstractmethod
    def integration_key(self) -> str:
        pass

    def is_enabled(self) -> bool:
        enabled: bool = bool(self.get_integrations())
        return enabled
```

---

</SwmSnippet>

# Main Functions

Several main functions are involved in the instantiation and execution of actions.

## <SwmToken path="src/sentry/rules/actions/base.py" pos="16:2:2" line-data="def instantiate_action(rule: Rule, action, rule_fire_history: RuleFireHistory | None = None):">`instantiate_action`</SwmToken>

The <SwmToken path="src/sentry/rules/actions/base.py" pos="16:2:2" line-data="def instantiate_action(rule: Rule, action, rule_fire_history: RuleFireHistory | None = None):">`instantiate_action`</SwmToken> function is responsible for creating an instance of an action based on the provided rule and action data. It ensures that the action is registered and valid before instantiation.

<SwmSnippet path="/src/sentry/rules/actions/base.py" line="16">

---

The <SwmToken path="src/sentry/rules/actions/base.py" pos="16:2:2" line-data="def instantiate_action(rule: Rule, action, rule_fire_history: RuleFireHistory | None = None):">`instantiate_action`</SwmToken> function checks if the action is registered and valid, then creates an instance of it.

```python
def instantiate_action(rule: Rule, action, rule_fire_history: RuleFireHistory | None = None):
    from sentry.rules import rules

    action_id = action["id"]
    action_cls = rules.get(action_id)
    if action_cls is None:
        logger.warning("Unregistered action %r", action["id"])
        return None

    action_inst = action_cls(
        rule.project, data=action, rule=rule, rule_fire_history=rule_fire_history
    )
    if not isinstance(action_inst, EventAction):
        logger.warning("Unregistered action %r", action["id"])
        return None

    return action_inst
```

---

</SwmSnippet>

## after

The <SwmToken path="src/sentry/rules/actions/base.py" pos="39:3:3" line-data="    def after(">`after`</SwmToken> method in the <SwmToken path="src/sentry/rules/actions/integrations/base.py" pos="16:10:10" line-data="from sentry.rules.actions import EventAction">`EventAction`</SwmToken> class is an abstract method that must be implemented by subclasses. It defines the operations to be executed after a rule matches an event, yielding <SwmToken path="src/sentry/rules/actions/base.py" pos="41:7:7" line-data="    ) -&gt; Generator[CallbackFuture]:">`CallbackFuture`</SwmToken> instances for further processing.

<SwmSnippet path="/src/sentry/rules/actions/base.py" line="39">

---

The <SwmToken path="src/sentry/rules/actions/base.py" pos="39:3:3" line-data="    def after(">`after`</SwmToken> method should yield <SwmToken path="src/sentry/rules/actions/base.py" pos="41:7:7" line-data="    ) -&gt; Generator[CallbackFuture]:">`CallbackFuture`</SwmToken> instances which will then be passed into the given callback.

```python
    def after(
        self, event: GroupEvent, notification_uuid: str | None = None
    ) -> Generator[CallbackFuture]:
        """
        Executed after a Rule matches.

        Should yield CallBackFuture instances which will then be passed into
        the given callback.

        See the notification implementation for example usage.


        >>> def after(self, state):
        >>>     yield self.future(self.print_results)
        >>>
        >>> def print_results(self, event, futures):
        >>>     print('Got futures for Event {}'.format(event.id))
        >>>     for future in futures:
        >>>         print(future)
        """
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/rules/actions/utils.py" pos="91:2:2" line-data="def get_changed_data(">`get_changed_data`</SwmToken>

The <SwmToken path="src/sentry/rules/actions/utils.py" pos="91:2:2" line-data="def get_changed_data(">`get_changed_data`</SwmToken> function generates a list of changes that occurred when editing an issue alert rule. It compares the current and previous states of the rule data and identifies added, removed, or modified elements.

<SwmSnippet path="/src/sentry/rules/actions/utils.py" line="91">

---

The <SwmToken path="src/sentry/rules/actions/utils.py" pos="91:2:2" line-data="def get_changed_data(">`get_changed_data`</SwmToken> function compares the current and previous states of the rule data to identify changes.

```python
def get_changed_data(
    rule: Rule, rule_data: dict[str, Any], rule_data_before: dict[str, Any]
) -> dict[str, Any]:
    """
    Generate a list per type of issue alert rule data of what changes occurred on edit.
    """
    prior_conditions_data = convert_data(rule_data_before.get("conditions", []))
    present_conditions_data = convert_data(rule_data.get("conditions", []))
    changed_conditions = generate_diff_labels(
        prior_conditions_data, present_conditions_data, rule, "condition"
    )

    prior_actions_data = convert_data(rule_data_before.get("actions", []))
    present_actions_data = convert_data(rule_data.get("actions", []))
    changed_actions = generate_diff_labels(prior_actions_data, present_actions_data, rule, "action")

    changed_conditions_actions = {**changed_conditions, **changed_actions}
    changed_data: DefaultDict[str, list[str]] = defaultdict(list, changed_conditions_actions)

    current_frequency = get_frequency_label(rule_data.get("frequency"))
    previous_frequency = get_frequency_label(rule_data_before.get("frequency"))
```

---

</SwmSnippet>

# Actions Endpoints

Actions endpoints are used to interact with external services or perform specific operations when certain conditions are met.

## <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="53:2:2" line-data="def send_incident_alert_notification(">`send_incident_alert_notification`</SwmToken>

The <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="53:2:2" line-data="def send_incident_alert_notification(">`send_incident_alert_notification`</SwmToken> function is used to send incident data to the <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="61:24:26" line-data="    When a metric alert is triggered, send incident data to the SentryApp&#39;s webhook.">`SentryApp's`</SwmToken> webhook when a metric alert is triggered. It builds the incident attachment and sends the notification using the integration service.

<SwmSnippet path="/src/sentry/rules/actions/notify_event_service.py" line="53">

---

The <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="53:2:2" line-data="def send_incident_alert_notification(">`send_incident_alert_notification`</SwmToken> function sends incident data to the <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="61:24:26" line-data="    When a metric alert is triggered, send incident data to the SentryApp&#39;s webhook.">`SentryApp's`</SwmToken> webhook when a metric alert is triggered.

```python
def send_incident_alert_notification(
    action: AlertRuleTriggerAction,
    incident: Incident,
    new_status: IncidentStatus,
    metric_value: float | None = None,
    notification_uuid: str | None = None,
) -> bool:
    """
    When a metric alert is triggered, send incident data to the SentryApp's webhook.
    :param action: The triggered `AlertRuleTriggerAction`.
    :param incident: The `Incident` for which to build a payload.
    :param metric_value: The value of the metric that triggered this alert to
    fire. If not provided we'll attempt to calculate this ourselves.
    :return:
    """
    organization = serialize_rpc_organization(incident.organization)
    incident_attachment = build_incident_attachment(
        incident, new_status, metric_value, notification_uuid
    )

    success = integration_service.send_incident_alert_notification(
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="85:2:2" line-data="def find_alert_rule_action_ui_component(app_platform_event: AppPlatformEvent) -&gt; bool:">`find_alert_rule_action_ui_component`</SwmToken>

The <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="85:2:2" line-data="def find_alert_rule_action_ui_component(app_platform_event: AppPlatformEvent) -&gt; bool:">`find_alert_rule_action_ui_component`</SwmToken> function loops through the triggers for the alert rule event and checks if an action is an alert rule UI Component. It returns a boolean indicating the presence of such an action.

<SwmSnippet path="/src/sentry/rules/actions/notify_event_service.py" line="85">

---

The <SwmToken path="src/sentry/rules/actions/notify_event_service.py" pos="85:2:2" line-data="def find_alert_rule_action_ui_component(app_platform_event: AppPlatformEvent) -&gt; bool:">`find_alert_rule_action_ui_component`</SwmToken> function checks if an action is an alert rule UI Component.

```python
def find_alert_rule_action_ui_component(app_platform_event: AppPlatformEvent) -> bool:
    """
    Loop through the triggers for the alert rule event. For each trigger, check
    if an action is an alert rule UI Component
    """
    triggers = (
        getattr(app_platform_event, "data", {})
        .get("metric_alert", {})
        .get("alert_rule", {})
        .get("triggers", [])
    )

    actions = [
        action
        for trigger in triggers
        for action in trigger.get("actions", {})
        if (action.get("type") == "sentry_app" and action.get("settings") is not None)
    ]

    return bool(len(actions))
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

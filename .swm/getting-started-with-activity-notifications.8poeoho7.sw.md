---
title: Getting Started with Activity Notifications
---
```mermaid
classDiagram
 ActivityNotification <|-- NoteActivityNotification
 ActivityNotification <|-- ReleaseActivityNotification
 ActivityNotification : +Activity activity
 NoteActivityNotification : +get_description()
 NoteActivityNotification : +get_notification_title()
 ReleaseActivityNotification : +get_context()
 ReleaseActivityNotification : +get_participants_with_group_subscription_reason()

classDiagram
 class ActivityNotification {
 +ActivityNotification(Activity activity)
 +get_base_context() : MutableMapping
 }
 class ResolvedInReleaseActivityNotification {
 +ResolvedInReleaseActivityNotification(Activity activity)
 +get_description() : tuple
 }
 class AssignedActivityNotification {
 +get_assignee_str(Activity activity, Organization organization) : str
 }
 ActivityNotification <|-- ResolvedInReleaseActivityNotification
 ActivityNotification <|-- AssignedActivityNotification

%% Swimm:
%% classDiagram
%%  <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> <|-- NoteActivityNotification
%%  <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> <|-- ReleaseActivityNotification
%%  <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> : +Activity activity
%%  NoteActivityNotification : +get_description()
%%  NoteActivityNotification : +get_notification_title()
%%  ReleaseActivityNotification : +get_context()
%%  ReleaseActivityNotification : +get_participants_with_group_subscription_reason()
%% 
%% classDiagram
%%  class <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> {
%%  +ActivityNotification(Activity activity)
%%  +get_base_context() : <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="4:11:11" line-data="from collections.abc import Mapping, MutableMapping">`MutableMapping`</SwmToken>
%%  }
%%  class <SwmToken path="src/sentry/notifications/notifications/activity/resolved_in_release.py" pos="16:2:2" line-data="class ResolvedInReleaseActivityNotification(GroupActivityNotification):">`ResolvedInReleaseActivityNotification`</SwmToken> {
%%  +ResolvedInReleaseActivityNotification(Activity activity)
%%  +get_description() : tuple
%%  }
%%  class <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="55:2:2" line-data="class AssignedActivityNotification(GroupActivityNotification):">`AssignedActivityNotification`</SwmToken> {
%%  +get_assignee_str(Activity activity, Organization organization) : str
%%  }
%%  <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> <|-- <SwmToken path="src/sentry/notifications/notifications/activity/resolved_in_release.py" pos="16:2:2" line-data="class ResolvedInReleaseActivityNotification(GroupActivityNotification):">`ResolvedInReleaseActivityNotification`</SwmToken>
%%  <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> <|-- <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="55:2:2" line-data="class AssignedActivityNotification(GroupActivityNotification):">`AssignedActivityNotification`</SwmToken>
```

# Overview

Activity refers to various actions or events that occur within the application, such as setting an issue as resolved, assigning an issue, or adding a note. These activities trigger notifications to inform users about the changes or updates related to the issues they are involved with.

# Notification Types

The notifications are categorized by activity types, and each type has a corresponding notification class that handles the specifics of that activity. For example, `NoteActivityNotification` handles notifications for new comments, while `ReleaseActivityNotification` handles notifications for new releases.

# Notification Classes

The notification classes define the content and format of the notifications, including the subject, title, and message description. These notifications are sent via various channels, such as email or Slack, to ensure that users are promptly informed about important activities.

# Class Hierarchy

The <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> class is a base class for different types of activity notifications. It initializes with an <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="29:6:6" line-data="    metrics_key = &quot;activity&quot;">`activity`</SwmToken> object and sets up the basic context for the notification.

<SwmSnippet path="/src/sentry/notifications/notifications/activity/base.py" line="28">

---

The <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> class initializes with an <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="29:6:6" line-data="    metrics_key = &quot;activity&quot;">`activity`</SwmToken> object and sets up the basic context for the notification.

```python
class ActivityNotification(ProjectNotification, abc.ABC):
    metrics_key = "activity"
    notification_setting_type_enum = NotificationSettingEnum.WORKFLOW
    template_path = "sentry/emails/activity/generic"

    def __init__(self, activity: Activity) -> None:
        super().__init__(activity.project)
        self.activity = activity
```

---

</SwmSnippet>

# Handling Specific Activity Types

The <SwmToken path="src/sentry/notifications/notifications/activity/resolved_in_release.py" pos="16:2:2" line-data="class ResolvedInReleaseActivityNotification(GroupActivityNotification):">`ResolvedInReleaseActivityNotification`</SwmToken> class handles notifications for issues resolved in a release. It extends the base <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> class and adds specific details like the release version.

<SwmSnippet path="/src/sentry/notifications/notifications/activity/resolved_in_release.py" line="16">

---

The <SwmToken path="src/sentry/notifications/notifications/activity/resolved_in_release.py" pos="16:2:2" line-data="class ResolvedInReleaseActivityNotification(GroupActivityNotification):">`ResolvedInReleaseActivityNotification`</SwmToken> class extends the base <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="28:2:2" line-data="class ActivityNotification(ProjectNotification, abc.ABC):">`ActivityNotification`</SwmToken> class and adds specific details like the release version.

```python
class ResolvedInReleaseActivityNotification(GroupActivityNotification):
    metrics_key = "resolved_in_release_activity"
    title = "Resolved Issue"

    def __init__(self, activity: Activity) -> None:
        super().__init__(activity)
        self.version = self.activity.data.get("version", "")
        self.version_parsed = parse_release(self.version, json_loads=orjson.loads)["description"]
```

---

</SwmSnippet>

# Generating Notification Content

The <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken> function generates a <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="31:8:10" line-data="    &quot;&quot;&quot;Get a human-readable version of the assignment&#39;s target.&quot;&quot;&quot;">`human-readable`</SwmToken> string for the assignee of an activity. It checks if the assignee is a team or a user and returns the appropriate string.

<SwmSnippet path="/src/sentry/notifications/notifications/activity/assigned.py" line="30">

---

The <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken> function generates a <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="31:8:10" line-data="    &quot;&quot;&quot;Get a human-readable version of the assignment&#39;s target.&quot;&quot;&quot;">`human-readable`</SwmToken> string representing the assignee of an activity. It checks if the assignee is a team or an individual user and returns the appropriate string.

```python
def get_assignee_str(activity: Activity, organization: Organization) -> str:
    """Get a human-readable version of the assignment's target."""

    assignee_id = activity.data.get("assignee")
    assignee_email: str | None = activity.data.get("assigneeEmail")

    if is_team_assignee(activity):
        assignee_team = _get_team_option(assignee_id, organization)
        if assignee_team:
            return f"the {assignee_team.slug} team"
        return "an unknown team"

    # TODO(mgaeta): Refactor GroupAssigneeManager to not make IDs into strings.
    if str(activity.user_id) == str(assignee_id):
        return "themselves"

    assignee_user = _get_user_option(assignee_id)
    if assignee_user:
        assignee: str = assignee_user.get_display_name()
        return assignee
    if assignee_email:
```

---

</SwmSnippet>

# Main Functions

There are several main functions in Activity. Some of them are <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="67:3:3" line-data="    def get_participants_with_group_subscription_reason(self) -&gt; ParticipantMap:">`get_participants_with_group_subscription_reason`</SwmToken>, <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken>, and <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="84:3:3" line-data="    def get_description(self) -&gt; tuple[str, str | None, Mapping[str, Any]]:">`get_description`</SwmToken>. We will dive a little into <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="67:3:3" line-data="    def get_participants_with_group_subscription_reason(self) -&gt; ParticipantMap:">`get_participants_with_group_subscription_reason`</SwmToken> and <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken>.

## <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="67:3:3" line-data="    def get_participants_with_group_subscription_reason(self) -&gt; ParticipantMap:">`get_participants_with_group_subscription_reason`</SwmToken>

The <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="67:3:3" line-data="    def get_participants_with_group_subscription_reason(self) -&gt; ParticipantMap:">`get_participants_with_group_subscription_reason`</SwmToken> function is an abstract method that is overridden by subclasses to return a map of participants for a group activity. This function is crucial for determining who should receive notifications about specific activities.

<SwmSnippet path="/src/sentry/notifications/notifications/activity/base.py" line="67">

---

The <SwmToken path="src/sentry/notifications/notifications/activity/base.py" pos="67:3:3" line-data="    def get_participants_with_group_subscription_reason(self) -&gt; ParticipantMap:">`get_participants_with_group_subscription_reason`</SwmToken> function is an abstract method that is overridden by subclasses to return a map of participants for a group activity.

```python
    def get_participants_with_group_subscription_reason(self) -> ParticipantMap:
        pass
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken>

The <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="30:2:2" line-data="def get_assignee_str(activity: Activity, organization: Organization) -&gt; str:">`get_assignee_str`</SwmToken> function generates a <SwmToken path="src/sentry/notifications/notifications/activity/assigned.py" pos="31:8:10" line-data="    &quot;&quot;&quot;Get a human-readable version of the assignment&#39;s target.&quot;&quot;&quot;">`human-readable`</SwmToken> string representing the assignee of an activity. It checks if the assignee is a team or an individual user and returns the appropriate string. This function is used to personalize notifications by including the assignee's name or team.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

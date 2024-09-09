---
title: Introduction to Notification Actions
---
# Background

Notification Actions are meant to be a generic abstraction of the actions we fire when alert rules go off. The structure of the model for `NotificationAction` was abstracted from `AlertRuleTriggerAction` but decouples it from <SwmPath>[src/sentry/incidents/](src/sentry/incidents/)</SwmPath>. Instead, they are meant to help send notifications to third-party integrations rather than individual channels such as email, or personal notifications settings. These notifications can be configured across the whole <SwmPath>[src/sentry/projects/services/project/](src/sentry/projects/services/project/)</SwmPath>, rather than per recipient. It was originally designed for Spike Protection, but should be generic enough to apply to any other part of Sentry.

# Examples

Some examples of possible notification actions include:

- Receiving audit log entries to a Slack channel
- Creating Jira tickets from new user feedback items
- Triggering a GitHub notification whenever a release is created in Sentry
- Sending quota notifications or billing updates to a specific non-user email
- Project notifications sent to a Slack channel instead of the teams/members

# How They Work

Notification Actions rely on several components:

- **Triggers**: The source of the notification (i.e., what happened in Sentry that caused the notification)
- **Services**: The delivery mechanism (e.g., Slack, PagerDuty, MSTeams, Sentry Notifications, etc.)
- **Targets**: The type of recipient for the notification (i.e., is the recipient a user, a team, or specific to the integration)
- **Registrations**: The `ActionRegistration` subclass which helps set up new actions

# Setting Up New Triggers, Services, or Targets

If you need to set up new types of triggers, services, or targets, you can do so by extending the relevant enums in the <SwmPath>[src/sentry/models/notificationaction.py](src/sentry/models/notificationaction.py)</SwmPath>. These enums are used by Django when validating new Notification Actions before saving, meaning this step cannot be skipped.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

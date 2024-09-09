---
title: Overview of Account Settings
---
# Introduction to Account Settings

Account settings refer to the user-specific configurations within the application. These settings include various sections such as account details, security settings, notification preferences, and email addresses.

# Account Settings Layout

The `AccountSettingsLayout` component is responsible for rendering the account settings page, including navigation and child components. The `AccountSettingsNavigation` function generates the navigation items for the account settings, such as account details, security, notifications, and email addresses.

<SwmSnippet path="/static/app/views/settings/account/accountDetails.tsx" line="42">

---

The <SwmToken path="static/app/views/settings/account/accountDetails.tsx" pos="42:2:2" line-data="function AccountDetails() {">`AccountDetails`</SwmToken> function is responsible for rendering the account details page. It fetches user data and displays a form for updating account details. The form includes fields such as user ID and other account-specific information. The function handles form submission and updates the user data in the Config Store.

```tsx
function AccountDetails() {
  const organization = useOrganization({allowNull: true});
  const queryClient = useQueryClient();
  const {
    data: user,
    isPending,
    isError,
    refetch,
  } = useApiQuery<User>(USER_ENDPOINT_QUERY_KEY, {staleTime: 0});

  if (isPending) {
    return (
      <Fragment>
        <SettingsPageHeader title={t('Account Details')} />
        <LoadingIndicator />
      </Fragment>
    );
  }

  if (isError) {
    return <LoadingError onRetry={refetch} />;
```

---

</SwmSnippet>

# Security Settings

Security settings within the account include options for changing passwords and enabling two-factor authentication.

<SwmSnippet path="/static/app/views/settings/account/accountSecurity/accountSecurityEnroll.tsx" line="467">

---

The <SwmToken path="static/app/views/settings/account/accountSecurity/accountSecurityEnroll.tsx" pos="38:15:15" line-data="import RemoveConfirm from &#39;sentry/views/settings/account/accountSecurity/components/removeConfirm&#39;;">`accountSecurity`</SwmToken> function manages the security settings of the account. It includes functionalities for handling session closures, adding two-factor authentication, and displaying the status of various authentication methods. The function interacts with the API to update security settings and provides feedback to the user.

```tsx
            model={this.formModel}
            apiMethod="POST"
            apiEndpoint={this.authenticatorEndpoint}
```

---

</SwmSnippet>

# Notification Settings

Notification settings allow users to configure their email notification preferences.

<SwmSnippet path="/static/app/views/settings/account/notifications/notificationSettings.tsx" line="116">

---

The <SwmToken path="static/app/views/settings/account/notifications/notificationSettings.tsx" pos="35:2:2" line-data="function NotificationSettings({organizations}: NotificationSettingsProps) {">`NotificationSettings`</SwmToken> function allows users to configure their email notification preferences. It interacts with the API to update the notification settings and provides feedback to the user.

```tsx
            saveOnBlur
            apiMethod="PUT"
            apiEndpoint="/users/me/notifications/"
```

---

</SwmSnippet>

# Managing User Identities

The <SwmToken path="static/app/views/settings/account/accountAuthorizations.tsx" pos="30:2:2" line-data="function AccountAuthorizations() {">`AccountAuthorizations`</SwmToken> function handles the management of user identities, including the display and revocation of authorized applications.

<SwmSnippet path="/static/app/views/settings/account/accountAuthorizations.tsx" line="30">

---

The <SwmToken path="static/app/views/settings/account/accountAuthorizations.tsx" pos="30:2:2" line-data="function AccountAuthorizations() {">`AccountAuthorizations`</SwmToken> function handles the display and management of authorized applications. It fetches the list of authorized applications and allows the user to revoke access to any application. The function interacts with the API to update the list of authorizations and provides feedback to the user.

```tsx
function AccountAuthorizations() {
  const api = useApi();
  const queryClient = useQueryClient();
  const ENDPOINT = '/api-authorizations/';

  const {data, isPending, isError, refetch} = useApiQuery<Authorization[]>([ENDPOINT], {
    staleTime: 0,
  });

  if (isPending) {
    return <LoadingIndicator />;
  }

  if (isError) {
    return <LoadingError onRetry={refetch} />;
  }

  const handleRevoke = async (authorization: Authorization) => {
    const oldData = data;
    setApiQueryData<Authorization[]>(queryClient, [ENDPOINT], prevData =>
      prevData.filter(a => a.id !== authorization.id)
```

---

</SwmSnippet>

# Account APIs

The account settings include several API endpoints for managing user subscriptions and API tokens.

## Subscriptions Endpoint

The <SwmToken path="static/app/views/settings/account/accountSubscriptions.tsx" pos="22:12:12" line-data="const ENDPOINT = &#39;/users/me/subscriptions/&#39;;">`subscriptions`</SwmToken> endpoint is defined at <SwmPath>[src/sentry/uptime/subscriptions/](src/sentry/uptime/subscriptions/)</SwmPath>. This endpoint is used to manage user subscriptions, allowing users to subscribe or unsubscribe from various lists.

<SwmSnippet path="/static/app/views/settings/account/accountSubscriptions.tsx" line="22">

---

The <SwmToken path="static/app/views/settings/account/accountSubscriptions.tsx" pos="22:12:12" line-data="const ENDPOINT = &#39;/users/me/subscriptions/&#39;;">`subscriptions`</SwmToken> endpoint is defined at <SwmPath>[src/sentry/uptime/subscriptions/](src/sentry/uptime/subscriptions/)</SwmPath>. This endpoint is used to manage user subscriptions, allowing users to subscribe or unsubscribe from various lists.

```tsx
const ENDPOINT = '/users/me/subscriptions/';
```

---

</SwmSnippet>

## API Tokens Endpoint

The <SwmToken path="static/app/views/settings/account/apiNewToken.tsx" pos="85:5:7" line-data="                apiEndpoint=&quot;/api-tokens/&quot;">`api-tokens`</SwmToken> endpoint is defined at <SwmToken path="static/app/views/settings/account/apiNewToken.tsx" pos="85:4:8" line-data="                apiEndpoint=&quot;/api-tokens/&quot;">`/api-tokens/`</SwmToken>. This endpoint is used to manage API tokens, allowing users to create, update, and delete tokens for authenticating API requests.

<SwmSnippet path="/static/app/views/settings/account/apiNewToken.tsx" line="21">

---

The <SwmToken path="static/app/views/settings/account/apiNewToken.tsx" pos="85:5:7" line-data="                apiEndpoint=&quot;/api-tokens/&quot;">`api-tokens`</SwmToken> endpoint is defined at <SwmToken path="static/app/views/settings/account/apiNewToken.tsx" pos="85:4:8" line-data="                apiEndpoint=&quot;/api-tokens/&quot;">`/api-tokens/`</SwmToken>. This endpoint is used to manage API tokens, allowing users to create, update, and delete tokens for authenticating API requests.

```tsx
const API_INDEX_ROUTE = '/settings/account/api/auth-tokens/';
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

---
title: Managing Plugins in Static Files
---
```mermaid
classDiagram
 class BasePlugin {
 +plugin: Plugin
 +renderSettings(props: Props)
 }
 class Registry {
 +add(id: string, plugin: Plugin)
 +get(id: string): Plugin
 +isLoaded(id: string): boolean
 +load(id: string)
 }
 class PluginComponentBase {
 +fetchData()
 +onSubmit()
 +onLoad(callback, ...args)
 +onLoadSuccess()
 +onLoadError(callback, ...args)
 +onSave(callback, ...args)
 +onSaveSuccess(callback, ...args)
 +onSaveError(callback, ...args)
 +onSaveComplete(callback, ...args)
 +renderField(props: Omit<GenericFieldProps, 'formState'>): React.ReactNode
 }
 BasePlugin <|-- DefaultPlugin
 BasePlugin <|-- SessionStackPlugin
 BasePlugin <|-- Jira
 Registry <|-- static/app/plugins/index.tsx
 PluginComponentBase <|-- PluginSettings

%% Swimm:
%% classDiagram
%%  class <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> {
%%  +plugin: Plugin
%%  +renderSettings(props: Props)
%%  }
%%  class Registry {
%%  +add(id: string, plugin: Plugin)
%%  +get(id: string): Plugin
%%  +isLoaded(id: string): boolean
%%  +load(id: string)
%%  }
%%  class <SwmToken path="static/app/plugins/components/settings.tsx" pos="40:4:4" line-data="&gt; extends PluginComponentBase&lt;P, S&gt; {">`PluginComponentBase`</SwmToken> {
%%  +fetchData()
%%  +onSubmit()
%%  +onLoad(callback, ...args)
%%  +onLoadSuccess()
%%  +onLoadError(callback, ...args)
%%  +onSave(callback, ...args)
%%  +onSaveSuccess(callback, ...args)
%%  +onSaveError(callback, ...args)
%%  +onSaveComplete(callback, ...args)
%%  +renderField(props: Omit<GenericFieldProps, 'formState'>): <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="389:6:8" line-data="  renderForm(): React.ReactNode {">`React.ReactNode`</SwmToken>
%%  }
%%  <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> <|-- DefaultPlugin
%%  <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> <|-- <SwmToken path="static/app/plugins/index.tsx" pos="15:9:9" line-data="registry.add(&#39;sessionstack&#39;, SessionStackPlugin);">`SessionStackPlugin`</SwmToken>
%%  <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> <|-- Jira
%%  Registry <|-- <SwmPath>[static/app/plugins/index.tsx](static/app/plugins/index.tsx)</SwmPath>
%%  <SwmToken path="static/app/plugins/components/settings.tsx" pos="40:4:4" line-data="&gt; extends PluginComponentBase&lt;P, S&gt; {">`PluginComponentBase`</SwmToken> <|-- <SwmToken path="static/app/plugins/components/settings.tsx" pos="37:2:2" line-data="class PluginSettings&lt;">`PluginSettings`</SwmToken>
```

# Overview

Plugins are used to extend the functionality of the application by integrating with external services or adding custom features. This document explains the core classes and objects involved in managing plugins within static files.

# <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> Class

The <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> class serves as a foundation for creating plugins. It provides methods like <SwmToken path="static/app/plugins/basePlugin.tsx" pos="17:1:1" line-data="  renderSettings(props: Props) {">`renderSettings`</SwmToken> to render plugin-specific settings.

<SwmSnippet path="/static/app/plugins/basePlugin.tsx" line="11">

---

The <SwmToken path="static/app/plugins/basePlugin.tsx" pos="11:2:2" line-data="class BasePlugin {">`BasePlugin`</SwmToken> class is defined here, with a constructor to initialize the plugin and a <SwmToken path="static/app/plugins/basePlugin.tsx" pos="17:1:1" line-data="  renderSettings(props: Props) {">`renderSettings`</SwmToken> method to render the settings.

```tsx
class BasePlugin {
  plugin: Plugin;
  constructor(data: Plugin) {
    this.plugin = data;
  }

  renderSettings(props: Props) {
    return <Settings plugin={this.plugin} {...props} />;
  }
}
```

---

</SwmSnippet>

# Registry Object

The <SwmToken path="static/app/plugins/index.tsx" pos="10:2:2" line-data="const registry = new Registry();">`registry`</SwmToken> object is used to register and manage plugins, allowing the application to dynamically load and interact with them.

<SwmSnippet path="/static/app/plugins/index.tsx" line="10">

---

The <SwmToken path="static/app/plugins/index.tsx" pos="10:2:2" line-data="const registry = new Registry();">`registry`</SwmToken> object is defined and used to register plugins like <SwmToken path="static/app/plugins/index.tsx" pos="15:9:9" line-data="registry.add(&#39;sessionstack&#39;, SessionStackPlugin);">`SessionStackPlugin`</SwmToken> and <SwmToken path="static/app/plugins/index.tsx" pos="18:2:2" line-data="// Jira">`Jira`</SwmToken>.

```tsx
const registry = new Registry();

// Register legacy plugins

// Sessionstack
registry.add('sessionstack', SessionStackPlugin);
contexts.sessionstack = SessionStackContextType;

// Jira
registry.add('jira', Jira);
```

---

</SwmSnippet>

# Registering Plugins

Specific plugins like <SwmToken path="static/app/plugins/index.tsx" pos="15:9:9" line-data="registry.add(&#39;sessionstack&#39;, SessionStackPlugin);">`SessionStackPlugin`</SwmToken> and <SwmToken path="static/app/plugins/index.tsx" pos="18:2:2" line-data="// Jira">`Jira`</SwmToken> are registered in the <SwmPath>[static/app/plugins/index.tsx](static/app/plugins/index.tsx)</SwmPath> file, making them available for use within the application.

<SwmSnippet path="/static/app/plugins/index.tsx" line="14">

---

Plugins are registered here, making them available for use within the application.

```tsx
// Sessionstack
registry.add('sessionstack', SessionStackPlugin);
contexts.sessionstack = SessionStackContextType;

// Jira
registry.add('jira', Jira);
```

---

</SwmSnippet>

# <SwmToken path="static/app/plugins/components/settings.tsx" pos="40:4:4" line-data="&gt; extends PluginComponentBase&lt;P, S&gt; {">`PluginComponentBase`</SwmToken> Class

The <SwmToken path="static/app/plugins/components/settings.tsx" pos="40:4:4" line-data="&gt; extends PluginComponentBase&lt;P, S&gt; {">`PluginComponentBase`</SwmToken> class provides a base for plugin components, handling common tasks like form state management and API interactions.

<SwmSnippet path="/static/app/plugins/components/settings.tsx" line="37">

---

The <SwmToken path="static/app/plugins/components/settings.tsx" pos="40:4:4" line-data="&gt; extends PluginComponentBase&lt;P, S&gt; {">`PluginComponentBase`</SwmToken> class is defined here, with methods to manage form state and API interactions.

```tsx
class PluginSettings<
  P extends Props = Props,
  S extends State = State,
> extends PluginComponentBase<P, S> {
  constructor(props: P, context: any) {
    super(props, context);

    Object.assign(this.state, {
      fieldList: null,
      initialData: null,
      formData: null,
      errors: {},
      rawData: {},
      // override default FormState.READY if api requests are
      // necessary to even load the form
      state: FormState.LOADING,
      wasConfiguredOnPageLoad: false,
    });
  }
```

---

</SwmSnippet>

# Plugin Endpoints

Endpoints for Plugin Actions are defined to interact with external services.

## <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="135:1:1" line-data="  getPluginCreateEndpoint() {">`getPluginCreateEndpoint`</SwmToken>

The <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="135:1:1" line-data="  getPluginCreateEndpoint() {">`getPluginCreateEndpoint`</SwmToken> function constructs the endpoint URL for creating a new issue through the plugin. This URL is used to send a request to create an issue in the external service integrated by the plugin.

<SwmSnippet path="/static/app/plugins/components/issueActions.tsx" line="135">

---

The <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="135:1:1" line-data="  getPluginCreateEndpoint() {">`getPluginCreateEndpoint`</SwmToken> function constructs the endpoint URL for creating a new issue.

```tsx
  getPluginCreateEndpoint() {
    return (
      '/issues/' + this.getGroup().id + '/plugins/' + this.props.plugin.slug + '/create/'
    );
```

---

</SwmSnippet>

## <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="141:1:1" line-data="  getPluginLinkEndpoint() {">`getPluginLinkEndpoint`</SwmToken>

The <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="141:1:1" line-data="  getPluginLinkEndpoint() {">`getPluginLinkEndpoint`</SwmToken> function constructs the endpoint URL for linking an existing issue through the plugin. This URL is used to send a request to link an issue in the external service integrated by the plugin.

<SwmSnippet path="/static/app/plugins/components/issueActions.tsx" line="141">

---

The <SwmToken path="static/app/plugins/components/issueActions.tsx" pos="141:1:1" line-data="  getPluginLinkEndpoint() {">`getPluginLinkEndpoint`</SwmToken> function constructs the endpoint URL for linking an existing issue.

```tsx
  getPluginLinkEndpoint() {
    return (
      '/issues/' + this.getGroup().id + '/plugins/' + this.props.plugin.slug + '/link/'
    );
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

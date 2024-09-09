---
title: Overview of Integration Middleware
---
```mermaid
graph TD;
 A[Request] --> B{Check Classifications};
 B -->|Match| C[Handle by Classification];
 B -->|No Match| D[Pass Along];
 C --> E[Process Request];
 D --> E[Process Request];

 graph TD;
 A[Incoming Webhook] --> B{IntegrationControlMiddleware};
 B -->|No Parser| C[Fall Through];
 B -->|Parser Found| D[Process Request];
 D -->|Control Silo| E[Respond from Control Silo];
 D -->|Region Silo| F[Forward to Region Silo];
```

# What is Integration Middleware

Integration Middleware refers to the mechanisms that allow external services and plugins to interact with the application. They are managed through middleware components that handle requests and responses.

## Integration Control Middleware

The `IntegrationControlMiddleware` class is a key component that determines whether a request should be processed based on the current mode of the application. It uses classifications to decide how to handle different types of requests.

<SwmSnippet path="/src/sentry/middleware/integrations/parsers/vsts.py" line="9">

---

The `IntegrationControlMiddleware` handles incoming webhooks from integration providers. It inspects HTTP requests to `/extensions/*` and identifies the appropriate parser from the provider. If a parser is found, it processes the request accordingly, either responding from the Control Silo or forwarding it to the relevant Region Silos.

```python
from sentry.hybridcloud.outbox.category import WebhookProviderIdentifier
from sentry.integrations.middleware.hybrid_cloud.parser import BaseRequestParser
from sentry.integrations.models.integration import Integration
from sentry.integrations.models.organization_integration import OrganizationIntegration
from sentry.integrations.vsts.webhooks import WorkItemWebhook, get_vsts_external_id
```

---

</SwmSnippet>

## Classifications

Classifications such as <SwmToken path="src/sentry/middleware/integrations/classifications.py" pos="58:2:2" line-data="class IntegrationClassification(BaseClassification):">`IntegrationClassification`</SwmToken> and <SwmToken path="src/sentry/middleware/integrations/classifications.py" pos="38:2:2" line-data="class PluginClassification(BaseClassification):">`PluginClassification`</SwmToken> are used to dynamically parse and handle requests. These classifications can be expanded to include additional types of integrations.

<SwmSnippet path="/src/sentry/middleware/integrations/classifications.py" line="13">

---

The middleware checks each request against the defined classifications and processes it accordingly. If a match is found, the request is handled by the corresponding classification; otherwise, it is passed along.

```python
from sentry.integrations.models.integration import Integration
from sentry.integrations.models.organization_integration import OrganizationIntegration
from sentry.utils import metrics
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/middleware/integrations/parsers/discord.py" line="75">

---

The <SwmToken path="src/sentry/middleware/integrations/classifications.py" pos="67:1:1" line-data="            DiscordRequestParser,">`DiscordRequestParser`</SwmToken> is a specific parser for handling Discord integration requests. It identifies the integration from the request, validates the request, and processes it based on the type of interaction. It can handle asynchronous responses and forward requests to the appropriate regions.

```python
    def get_integration_from_request(self) -> Integration | None:
        if self.view_class in self.control_classes:
            # We don't need to identify an integration since we're handling these on Control
            return None

        discord_request = self.discord_request
        if self.view_class == DiscordInteractionsEndpoint and discord_request:
            if discord_request.guild_id is None:
                return None

            return Integration.objects.filter(
                provider=self.provider,
                external_id=discord_request.guild_id,
            ).first()

        with sentry_sdk.isolation_scope() as scope:
            scope.set_extra("path", self.request.path)
            scope.set_extra("guild_id", str(discord_request.guild_id if discord_request else None))
            sentry_sdk.capture_exception(
                Exception(
                    f"Unexpected view class in {self.provider} request parser: {self.view_class.__name__ if self.view_class else None}"
```

---

</SwmSnippet>

## Flexible and Dynamic Handling

This setup allows for flexible and dynamic handling of various integration requests, ensuring that the application can interact seamlessly with different external services and plugins.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

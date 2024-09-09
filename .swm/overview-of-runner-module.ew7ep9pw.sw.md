---
title: Overview of Runner Module
---
```mermaid
graph TD;
 A[Runner Module] --> B[configure Function];
 A --> C[run Function];
 C --> D[web Command];
 D --> E[Click Options];
 graph TD;
 A[Click Command] --> B[Options: partial, diagnose];
 B --> C[Generate OpenAPI Schema];
 C --> D[Partial Schema Generation];
 C --> E[Error Diagnostics];
 D --> F[Construct API Entry];
 E --> F[Construct API Entry];
 F --> G[Define Request Body Schema];
 F --> H[Define Response Schema];

%% Swimm:
%% graph TD;
%%  A[Runner Module] --> B[configure Function];
%%  A --> C[run Function];
%%  C --> D[web Command];
%%  D --> E[Click Options];
%%  graph TD;
%%  A[Click Command] --> B[Options: partial, diagnose];
%%  B --> C[Generate <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="31:7:7" line-data="        from openapi_pydantic import OpenAPI">`OpenAPI`</SwmToken> Schema];
%%  C --> D[Partial Schema Generation];
%%  C --> E[Error Diagnostics];
%%  D --> F[Construct API Entry];
%%  E --> F[Construct API Entry];
%%  F --> G[Define Request Body Schema];
%%  F --> H[Define Response Schema];
```

# Overview of Runner Module

The Runner module is responsible for initializing and configuring various components and services within the application. It includes functions and commands essential for setting up the environment, managing services, and maintaining consistency across different parts of the application.

# Configuration

The <SwmToken path="src/sentry/runner/commands/cleanup.py" pos="59:9:9" line-data="    from sentry.runner import configure">`configure`</SwmToken> function is a key part of the Runner module. It is imported and executed in multiple files to ensure proper configuration. For example, in <SwmPath>[src/sentry/runner/commands/cleanup.py](src/sentry/runner/commands/cleanup.py)</SwmPath>, the <SwmToken path="src/sentry/runner/commands/cleanup.py" pos="59:9:9" line-data="    from sentry.runner import configure">`configure`</SwmToken> function is called to set up the necessary environment.

<SwmSnippet path="/src/sentry/runner/commands/cleanup.py" line="59">

---

The <SwmToken path="src/sentry/runner/commands/cleanup.py" pos="59:9:9" line-data="    from sentry.runner import configure">`configure`</SwmToken> function is imported and executed to ensure proper configuration.

```python
    from sentry.runner import configure

    configure()
```

---

</SwmSnippet>

# Running Services

The <SwmToken path="src/sentry/runner/commands/run.py" pos="70:2:2" line-data="def run() -&gt; None:">`run`</SwmToken> function is defined to start services and is decorated with Click options to handle command-line arguments. This function is crucial for managing the execution of services within the application.

<SwmSnippet path="/src/sentry/runner/commands/run.py" line="69">

---

The <SwmToken path="src/sentry/runner/commands/run.py" pos="70:2:2" line-data="def run() -&gt; None:">`run`</SwmToken> function is defined to start services.

```python
@click.group()
def run() -> None:
    "Run a service."
```

---

</SwmSnippet>

# Command-Line Options

The <SwmToken path="src/sentry/runner/commands/run.py" pos="95:2:2" line-data="def web(">`web`</SwmToken> command within the <SwmToken path="src/sentry/runner/commands/run.py" pos="70:2:2" line-data="def run() -&gt; None:">`run`</SwmToken> function includes several Click options for binding addresses, setting worker processes, and handling upgrades. These options provide flexibility and control over how services are run.

<SwmSnippet path="/src/sentry/runner/commands/run.py" line="74">

---

The <SwmToken path="src/sentry/runner/commands/run.py" pos="95:2:2" line-data="def web(">`web`</SwmToken> command within the <SwmToken path="src/sentry/runner/commands/run.py" pos="74:1:1" line-data="@run.command()">`run`</SwmToken> function includes several Click options for binding addresses, setting worker processes, and handling upgrades.

```python
@run.command()
@click.option(
    "--bind",
    "-b",
    default=None,
    help="Bind address.",
    metavar="ADDRESS",
    callback=_address_validate,
)
@click.option(
    "--workers", "-w", default=0, help="The number of worker processes for handling requests."
)
@click.option("--upgrade", default=False, is_flag=True, help="Upgrade before starting.")
@click.option(
    "--with-lock", default=False, is_flag=True, help="Use a lock if performing an upgrade."
)
@click.option(
    "--noinput", default=False, is_flag=True, help="Do not prompt the user for input of any kind."
)
@log_options()
@configuration
```

---

</SwmSnippet>

# Runner Endpoints

The Runner module also defines various endpoints for internal RPC <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="86:10:10" line-data="                    title=&quot;Sentry Internal RPC APIs&quot;,">`APIs`</SwmToken>. These endpoints are managed using Click commands and include options for schema generation and error diagnostics.

## rpcschema

The <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="14:6:6" line-data="@click.command(&quot;rpcschema&quot;)">`rpcschema`</SwmToken> command generates an <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="31:7:7" line-data="        from openapi_pydantic import OpenAPI">`OpenAPI`</SwmToken> schema for the internal RPC <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="86:10:10" line-data="                    title=&quot;Sentry Internal RPC APIs&quot;,">`APIs`</SwmToken>. It includes options for partial schema generation and error diagnostics, providing a comprehensive overview of the available RPC methods.

<SwmSnippet path="/src/sentry/runner/commands/rpcschema.py" line="14">

---

The <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="14:6:6" line-data="@click.command(&quot;rpcschema&quot;)">`rpcschema`</SwmToken> command is defined as a Click command that generates an <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="31:7:7" line-data="        from openapi_pydantic import OpenAPI">`OpenAPI`</SwmToken> schema for the internal RPC <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="86:10:10" line-data="                    title=&quot;Sentry Internal RPC APIs&quot;,">`APIs`</SwmToken>.

```python
@click.command("rpcschema")
@click.option(
    "--partial",
    is_flag=True,
    default=False,
    help="Ignore RPC methods that produce errors.",
)
@click.option(
    "--diagnose",
    is_flag=True,
    default=False,
    help="List RPC methods that produce errors and suppress all other output.",
)
@configuration
def rpcschema(diagnose: bool, partial: bool) -> None:
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="54:3:3" line-data="        def build_api_entry(self) -&gt; dict[str, Any]:">`build_api_entry`</SwmToken>

The <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="54:3:3" line-data="        def build_api_entry(self) -&gt; dict[str, Any]:">`build_api_entry`</SwmToken> method constructs the API entry for a given RPC method signature. It defines the request body schema and the response schema for the RPC method, ensuring that the API is well-documented and consistent.

<SwmSnippet path="/src/sentry/runner/commands/rpcschema.py" line="54">

---

The <SwmToken path="src/sentry/runner/commands/rpcschema.py" pos="54:3:3" line-data="        def build_api_entry(self) -&gt; dict[str, Any]:">`build_api_entry`</SwmToken> method constructs the API entry for a given RPC method signature.

```python
        def build_api_entry(self) -> dict[str, Any]:
            param_schema, return_schema = self.sig.get_schemas()
            return {
                "post": {
                    "description": "Execute an RPC",
                    "requestBody": {
                        "content": {
                            "application/json": {
                                "schema": PydanticSchema(schema_class=param_schema)
                            }
                        },
                    },
                    "responses": {
                        "200": {
                            "description": "Success",
                            "content": {
                                "application/json": {
                                    "schema": PydanticSchema(schema_class=return_schema)
                                }
                            },
                        }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

---
title: Authorizing a Request
---
In this document, we will explain the process of authorizing a request. The process involves checking and refreshing the authentication token if necessary, retrieving the access token, preparing the authorization header, and updating the request headers.

The flow starts with checking if the authentication token has expired. If it has, the token is refreshed. Next, the access token is retrieved from the identity data. An authorization header is then prepared using this access token. Finally, the headers of the request are updated with the authorization header to ensure the request is properly authenticated.

Here is a high level diagram of the flow, showing only the most important functions:

```mermaid
graph TD;
      subgraph src/sentry/integrations
f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update)
end

subgraph src/sentry/integrations/vsts
f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle --> fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle --> a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle --> 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle --> 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle
end

subgraph src/sentry/integrations
66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle --> dd6f2c6555a3ad00a0aed3ab34055c7026063e3a2a74b2537fcf2a1223ffa577(sync_group_assignee_inbound):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[src/sentry/integrations/](src/sentry/integrations/)</SwmPath>
%% f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update)
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle --> fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle --> a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle --> 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle --> 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/](src/sentry/integrations/)</SwmPath>
%% 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle --> dd6f2c6555a3ad00a0aed3ab34055c7026063e3a2a74b2537fcf2a1223ffa577(sync_group_assignee_inbound):::mainFlowStyle
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

# Flow drill down

First, we'll zoom into this section of the flow:

```mermaid
graph TD;
      subgraph src/sentry/integrations
f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update)
end

subgraph src/sentry/integrations
f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle
end

subgraph src/sentry/integrations
431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> n1ms3(...)
end

subgraph src/sentry/event_manager.py
c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update) --> 5086692df24257d76a0adf892eba843feac14033d92b4a32022b125d5a725f9b(save)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[src/sentry/integrations/](src/sentry/integrations/)</SwmPath>
%% f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update)
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/](src/sentry/integrations/)</SwmPath>
%% f9d8d02812ff5a585f964b8d9836c8f27ce43708a290e39ff14ba50b6f0b2ea8(authorize_request):::mainFlowStyle --> 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/](src/sentry/integrations/)</SwmPath>
%% 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> n1ms3(...)
%% end
%% 
%% subgraph <SwmPath>[src/sentry/event_manager.py](src/sentry/event_manager.py)</SwmPath>
%% c828ab1860b674ebf5453bcb859f8af0d7c630772d44fd727c57e4fce799a42b(update) --> 5086692df24257d76a0adf892eba843feac14033d92b4a32022b125d5a725f9b(save)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/src/sentry/integrations/vsts/client.py" line="211">

---

## Authorizing the Request

The function <SwmToken path="src/sentry/integrations/vsts/client.py" pos="207:3:3" line-data="    def authorize_request(">`authorize_request`</SwmToken> is responsible for ensuring that the request has a valid authorization token. It first calls <SwmToken path="src/sentry/integrations/vsts/client.py" pos="211:3:3" line-data="        self._refresh_auth_if_expired()">`_refresh_auth_if_expired`</SwmToken> to refresh the token if it has expired. Then, it retrieves the access token from the identity data and prepares the authorization header. Finally, it updates the headers of the prepared request with the authorization header.

```python
        self._refresh_auth_if_expired()
        access_token = self.identity.data["access_token"]
        headers = prepare_auth_header(
            access_token=access_token,
        )
        prepared_request.headers.update(headers)
        return prepared_request
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/integrations/api/bases/external_actor.py" line="109">

---

## Updating the External Actor

The function <SwmToken path="src/sentry/integrations/api/bases/external_actor.py" pos="110:3:3" line-data="            validated_data.update(self.get_actor_params({**validated_data}))">`update`</SwmToken> is used to update the attributes of an <SwmToken path="src/sentry/integrations/api/bases/external_actor.py" pos="115:12:12" line-data="            assert type(self.instance) is ExternalActor, &quot;Instance type must be ExternalActor&quot;">`ExternalActor`</SwmToken> instance. It first removes the <SwmToken path="src/sentry/integrations/vsts/client.py" pos="72:16:16" line-data="    work_items = &quot;{instance}_apis/wit/workitems/{id}&quot;">`id`</SwmToken> from the validated data if it exists. Then, it updates the validated data with actor parameters if the actor key is present. The function iterates over the validated data and sets the corresponding attributes on the instance. Finally, it saves the instance and returns it.

```python
        if self._actor_key in validated_data:
            validated_data.update(self.get_actor_params({**validated_data}))

        for key, value in validated_data.items():
            setattr(self.instance, key, value)
        try:
            assert type(self.instance) is ExternalActor, "Instance type must be ExternalActor"
            self.instance.save()
            return self.instance
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/event_manager.py" line="476">

---

## Saving the Event

The function <SwmToken path="src/sentry/integrations/api/bases/external_actor.py" pos="116:5:5" line-data="            self.instance.save()">`save`</SwmToken> is responsible for normalizing and processing an event before saving it. If the event is not already normalized, it calls the <SwmToken path="src/sentry/event_manager.py" pos="476:3:3" line-data="        # Normalize if needed">`Normalize`</SwmToken> method to normalize it. This step ensures that the event data is in the correct format before proceeding with further processing.

```python
        # Normalize if needed
        if not self._normalized:
            if not assume_normalized:
                self.normalize(project_id=project_id)
            self._normalized = True
```

---

</SwmSnippet>

Now, lets zoom into this section of the flow:

```mermaid
graph TD;
      subgraph src/sentry/integrations/vsts
431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle --> fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle --> a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle --> 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle
end

subgraph src/sentry/integrations/vsts
66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle --> 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle
end

subgraph src/sentry/integrations/utils/sync.py
66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle --> dd6f2c6555a3ad00a0aed3ab34055c7026063e3a2a74b2537fcf2a1223ffa577(sync_group_assignee_inbound):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% 431cdb6c989e379a0b890f28f64acdc253a7a91894b47f35ad4064dee36b11b7(_refresh_auth_if_expired):::mainFlowStyle --> c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% c9f1b6abd5b86b248deafac3aa63eb8d055350bf49cbe100c54a0d94ee13361a(get):::mainFlowStyle --> fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% fc4a2a7e5f1b5a9d6230778920f9b62f4b7f3caa80ebd97c89444e007895b382(search_issues):::mainFlowStyle --> a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% a0445eff32744589c21cfe40b46d7b4346893653994134be4a340aaaf32b3f6d(post):::mainFlowStyle --> 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/vsts/](src/sentry/integrations/vsts/)</SwmPath>
%% 66e049c83c1ca3a7a23933e320651f77196243d817b62c1a401dfd7205f9a929(handle_updated_workitem):::mainFlowStyle --> 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[src/sentry/integrations/utils/sync.py](src/sentry/integrations/utils/sync.py)</SwmPath>
%% 66c307c65db74ab637ed0ed1623cc34d22110f0911938f86a52ccb8f5e8009dd(handle_assign_to):::mainFlowStyle --> dd6f2c6555a3ad00a0aed3ab34055c7026063e3a2a74b2537fcf2a1223ffa577(sync_group_assignee_inbound):::mainFlowStyle
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/src/sentry/integrations/vsts/client.py" line="198">

---

## Refreshing Authentication

The function <SwmToken path="src/sentry/integrations/vsts/client.py" pos="211:3:3" line-data="        self._refresh_auth_if_expired()">`_refresh_auth_if_expired`</SwmToken> checks if the authentication token has expired and refreshes it if necessary. This ensures that subsequent API requests are authenticated properly. If the token is expired, it calls the <SwmToken path="src/sentry/integrations/vsts/client.py" pos="202:9:9" line-data="            self.identity.get_provider().refresh_identity(">`refresh_identity`</SwmToken> method of the identity provider to obtain a new token.

```python
        time_expires = self.identity.data.get("expires")
        if time_expires is None:
            raise InvalidIdentity("VstsApiClient requires identity with specified expired time")
        if int(time_expires) <= int(time()):
            self.identity.get_provider().refresh_identity(
                self.identity, redirect_url=self.oauth_redirect_url
            )
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

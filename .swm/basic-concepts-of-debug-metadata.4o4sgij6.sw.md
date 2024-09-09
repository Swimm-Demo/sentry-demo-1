---
title: Basic Concepts of Debug Metadata
---
# Overview of Debug Metadata

Debug metadata refers to the metadata associated with debugging information in an application. It includes details about images used in the debugging process, such as their status and relevant attributes. This metadata is crucial for identifying and resolving issues within the application.

# <SwmToken path="static/app/components/events/interfaces/debugMeta/index.tsx" pos="12:13:13" line-data="} from &#39;sentry/components/events/interfaces/debugMeta/debugImageDetails&#39;;">`debugMeta`</SwmToken> Component

The <SwmToken path="static/app/components/events/interfaces/debugMeta/index.tsx" pos="12:13:13" line-data="} from &#39;sentry/components/events/interfaces/debugMeta/debugImageDetails&#39;;">`debugMeta`</SwmToken> component processes and filters images to display relevant debugging information to the user. It uses the <SwmToken path="static/app/components/events/interfaces/debugMeta/index.tsx" pos="48:1:1" line-data="  data: {">`data`</SwmToken> property in <SwmToken path="static/app/components/events/interfaces/debugMeta/index.tsx" pos="47:2:2" line-data="interface DebugMetaProps {">`DebugMetaProps`</SwmToken> to filter out irrelevant images, such as proguard images, which are rendered separately.

# Managing State

The component manages the state for filtering options and selections, allowing users to refine the displayed debugging information. This includes setting up filter options based on the status of images and managing the default filter selections.

<SwmSnippet path="/static/app/components/events/interfaces/debugMeta/index.tsx" line="176">

---

The component sets up filter options and default filter selections based on the status of images.

```tsx
    const allImages = [...usedImages, ...unusedImages];

    const filterOptions = [
      {
        label: t('Status'),
        options: [...new Set(allImages.map(image => image.status))].map(status => ({
          value: status,
          textValue: status,
          label: <Status status={status} />,
        })),
      },
    ];

    const defaultFilterSelections = (
      'options' in filterOptions[0] ? filterOptions[0].options : []
    ).filter(opt => opt.value !== ImageStatus.UNUSED);

    setFilterState({
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/debugMeta/index.tsx" line="304">

---

Hooks and callbacks are used to handle updates and reprocessing events, ensuring the component's state is always current.

```tsx
    cache.clearAll();
    getRelevantImages();
    return () => {
      removeListener();
    };
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  useEffect(() => {
    //  componentDidUpdate
    getRelevantImages();
    updateGrid();
  }, [event, getRelevantImages, updateGrid]);
```

---

</SwmSnippet>

# Debug Meta Endpoints

Debug Meta Endpoints are used to interact with the backend to check if events can be reprocessed and to handle other debugging-related tasks.

<SwmSnippet path="/static/app/components/events/interfaces/debugMeta/debugImageDetails/reprocessAlert.tsx" line="40">

---

The <SwmToken path="static/app/components/events/interfaces/debugMeta/debugImageDetails/reprocessAlert.tsx" pos="40:3:3" line-data="  const checkEventReprocessable = useCallback(async () =&gt; {">`checkEventReprocessable`</SwmToken> function makes an API request to check if an event can be reprocessed and updates the state accordingly.

```tsx
  const checkEventReprocessable = useCallback(async () => {
    try {
      const response = await api.requestPromise(
        `/projects/${orgSlug}/${projSlug}/events/${eventId}/reprocessable/`
      );
      setReprocessableEvent(response);
    } catch {
      // do nothing
    }
  }, [api, eventId, orgSlug, projSlug]);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

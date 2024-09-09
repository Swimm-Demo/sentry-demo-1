---
title: Introduction to Frame Component
---
# Introduction to Frame

Frame is a key component in error tracking and performance monitoring functionalities. It represents a single frame in a stack trace, which is a snapshot of the call stack at a specific point in time. Frame contains various properties such as the file name, line number, and function name, which help in identifying the exact location of an error. It is utilized in multiple components and utilities to provide detailed context about errors and their origins, making it essential for debugging and understanding the flow of execution leading to an error.

<SwmSnippet path="/static/app/components/events/interfaces/frame/functionName.tsx" line="7">

---

# Frame in <SwmToken path="static/app/components/events/interfaces/frame/functionName.tsx" pos="14:4:4" line-data="export function FunctionName({">`FunctionName`</SwmToken> Component

The <SwmToken path="static/app/components/events/interfaces/frame/functionName.tsx" pos="7:1:1" line-data="  frame: Frame;">`frame`</SwmToken> prop is used in the <SwmToken path="static/app/components/events/interfaces/frame/functionName.tsx" pos="14:4:4" line-data="export function FunctionName({">`FunctionName`</SwmToken> component to access the function name and other related details of a specific frame in the stack trace.

```tsx
  frame: Frame;
  className?: string;
  hasHiddenDetails?: boolean;
  meta?: Record<any, any>;
  showCompleteFunctionName?: boolean;
};
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/frame/utils.tsx" line="99">

---

# Frame in Utils

The <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="99:1:1" line-data="  frame: Frame;">`frame`</SwmToken> parameter is used in utility functions to check for context sources, variables, and registers associated with a frame.

```tsx
  frame: Frame;
  registers: Record<string, string>;
  emptySourceNotation?: boolean;
  isOnlyFrame?: boolean;
  platform?: string;
}) {
```

---

</SwmSnippet>

# Main Functions

There are several main functions related to Frame. Some of them are <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="23:4:4" line-data="export function getFrameHint(frame: Frame) {">`getFrameHint`</SwmToken>, <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="74:4:4" line-data="export function hasContextSource(frame: Frame) {">`hasContextSource`</SwmToken>, <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="78:4:4" line-data="export function hasContextVars(frame: Frame) {">`hasContextVars`</SwmToken>, and <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="86:4:4" line-data="export function hasAssembly(frame: Frame, platform?: string) {">`hasAssembly`</SwmToken>. We will dive a little into <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="23:4:4" line-data="export function getFrameHint(frame: Frame) {">`getFrameHint`</SwmToken> and <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="74:4:4" line-data="export function hasContextSource(frame: Frame) {">`hasContextSource`</SwmToken>.

<SwmSnippet path="/static/app/components/events/interfaces/frame/utils.tsx" line="23">

---

## <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="23:4:4" line-data="export function getFrameHint(frame: Frame) {">`getFrameHint`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="23:4:4" line-data="export function getFrameHint(frame: Frame) {">`getFrameHint`</SwmToken> function is used to provide hints about the frame, such as the function name and any relevant icons. It checks the function name and symbolicator status to determine the appropriate hint text and icon.

```tsx
export function getFrameHint(frame: Frame) {
  // returning [hintText, hintIcon]
  const {symbolicatorStatus} = frame;
  const func = frame.function || '<unknown>';
  // Custom color used to match adjacent text.
  const warningIcon = <IconQuestion size="xs" color={'#2c45a8' as any} />;
  const errorIcon = <IconWarning size="xs" color="red300" />;

  if (func.match(/^@objc\s/)) {
    return [t('Objective-C -> Swift shim frame'), warningIcon];
  }
  if (func.match(/^__?hidden#\d+/)) {
    return [t('Hidden function from bitcode build'), errorIcon];
  }
  if (!symbolicatorStatus && func === '<unknown>') {
    // Only render this if the event was not symbolicated.
    return [t('No function name was supplied by the client SDK.'), warningIcon];
  }

  if (
    func === '<unknown>' ||
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/frame/utils.tsx" line="74">

---

## <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="74:4:4" line-data="export function hasContextSource(frame: Frame) {">`hasContextSource`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="74:4:4" line-data="export function hasContextSource(frame: Frame) {">`hasContextSource`</SwmToken> function checks if the frame has context source information. It returns true if the frame's context is defined and has a length greater than zero.

```tsx
export function hasContextSource(frame: Frame) {
  return defined(frame.context) && !!frame.context.length;
}
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/frame/utils.tsx" line="78">

---

## <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="78:4:4" line-data="export function hasContextVars(frame: Frame) {">`hasContextVars`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="78:4:4" line-data="export function hasContextVars(frame: Frame) {">`hasContextVars`</SwmToken> function checks if the frame has context variables. It returns true if the frame's vars property is not an empty object.

```tsx
export function hasContextVars(frame: Frame) {
  return !isEmptyObject(frame.vars || {});
}
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/frame/utils.tsx" line="86">

---

## <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="86:4:4" line-data="export function hasAssembly(frame: Frame, platform?: string) {">`hasAssembly`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/utils.tsx" pos="86:4:4" line-data="export function hasAssembly(frame: Frame, platform?: string) {">`hasAssembly`</SwmToken> function checks if the frame is related to .NET assembly. It returns true if the platform is .NET and the frame's package is defined.

```tsx
export function hasAssembly(frame: Frame, platform?: string) {
  return (
    isDotnet(getPlatform(frame.platform, platform ?? 'other')) && defined(frame.package)
  );
```

---

</SwmSnippet>

# Frame Endpoints

Frame endpoints are used to fetch and parse data related to frames in the stack trace. Two important endpoints are <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="58:10:14" line-data="      `/organizations/${organization.slug}/derive-code-mappings/`,">`derive-code-mappings`</SwmToken> and <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="115:22:26" line-data="    const parsingEndpoint = `/projects/${organization.slug}/${project.slug}/repo-path-parsing/`;">`repo-path-parsing`</SwmToken>.

<SwmSnippet path="/static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" line="56">

---

## <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="58:10:14" line-data="      `/organizations/${organization.slug}/derive-code-mappings/`,">`derive-code-mappings`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="58:10:14" line-data="      `/organizations/${organization.slug}/derive-code-mappings/`,">`derive-code-mappings`</SwmToken> endpoint is used to fetch suggested code mappings for a given organization. This endpoint helps in identifying the correct source code files corresponding to the stack trace frames.

```tsx
  const {data: suggestedCodeMappings} = useApiQuery<DerivedCodeMapping[]>(
    [
      `/organizations/${organization.slug}/derive-code-mappings/`,
      {
        query: {
          projectId: project.id,
          stacktraceFilename: filename,
        },
      },
    ],
    {
      staleTime: Infinity,
      refetchOnWindowFocus: false,
      retry: false,
      notifyOnChangeProps: ['data'],
    }
  );
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" line="115">

---

## <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="115:22:26" line-data="    const parsingEndpoint = `/projects/${organization.slug}/${project.slug}/repo-path-parsing/`;">`repo-path-parsing`</SwmToken>

The <SwmToken path="static/app/components/events/interfaces/frame/stacktraceLinkModal.tsx" pos="115:22:26" line-data="    const parsingEndpoint = `/projects/${organization.slug}/${project.slug}/repo-path-parsing/`;">`repo-path-parsing`</SwmToken> endpoint is used to parse repository paths for a given project within an organization. This endpoint assists in configuring the stack trace to point to the correct source code locations.

```tsx
    const parsingEndpoint = `/projects/${organization.slug}/${project.slug}/repo-path-parsing/`;
    try {
      const configData = await api.requestPromise(parsingEndpoint, {
        method: 'POST',
        data: {
          sourceUrl: sourceCodeInput,
          stackPath: filename,
        },
      });
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

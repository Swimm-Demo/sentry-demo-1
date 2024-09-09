---
title: Query Function Flow
---
This document provides an overview of the query function flow. It explains how queries are initiated, batched, processed, and handled within the application. The document includes a high-level diagram and detailed explanations of each step in the flow.

The flow starts with the query function initiating the query process. It calls a function to perform the query, which checks if batching is enabled. If batching is enabled, the query is added to a batch and processed together with other queries. If not, the query is processed directly. The batched queries are then categorized into mergeable and unmergeable queries. Mergeable queries are combined and sent as a single request, while unmergeable queries are handled individually. Finally, the requests are sent, and the responses are processed.

Here is a high level diagram of the flow, showing only the most important functions:

```mermaid
graph TD;
      subgraph static/app/utils
a950191463ab06d0a2281cf5da2d083e2d9597fabda068cdaca057580ebd7169(queryFn):::mainFlowStyle --> 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle
end

subgraph static/app/utils
463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle --> f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle
end

subgraph static/app/utils
f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle --> e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle
end

subgraph static/app/utils
e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle --> 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle
end

subgraph static/app/utils
5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 4828141d547f5f2e5afec5603e540d98fdbd67e4d4c1471cbb0eae026cd0cfbf(_handleUnmergeableQueries)
end

subgraph static/app/utils
5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle
end

subgraph static/app/utils
90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle
end

subgraph static/app/utils
b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle --> c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle
end

subgraph static/app
c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle --> 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle
end

subgraph static/app
1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle --> 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle
end

subgraph static/app
4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler)
end

subgraph static/app/utils
4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle
end

subgraph static/app/utils
4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle --> b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle
end

subgraph static/app/utils
b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle --> 05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle
end

subgraph static/app/utils
05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle --> 635bb507b11255a8fd7c2375dac3b6c46b736470cf89007061c6861fc973e73b(fetchAvailableTags)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% a950191463ab06d0a2281cf5da2d083e2d9597fabda068cdaca057580ebd7169(queryFn):::mainFlowStyle --> 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle --> f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle --> e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle --> 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 4828141d547f5f2e5afec5603e540d98fdbd67e4d4c1471cbb0eae026cd0cfbf(_handleUnmergeableQueries)
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle --> c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle --> 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle --> 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler)
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle --> b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle --> 05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle --> 635bb507b11255a8fd7c2375dac3b6c46b736470cf89007061c6861fc973e73b(fetchAvailableTags)
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
      subgraph static/app/utils
a950191463ab06d0a2281cf5da2d083e2d9597fabda068cdaca057580ebd7169(queryFn):::mainFlowStyle --> 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle
end

subgraph static/app/utils
463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle --> f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle
end

subgraph static/app/utils
f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle --> e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle
end

subgraph static/app/utils
e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle --> 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle
end

subgraph static/app/utils
5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 4828141d547f5f2e5afec5603e540d98fdbd67e4d4c1471cbb0eae026cd0cfbf(_handleUnmergeableQueries)
end

subgraph static/app/utils
5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle
end

subgraph static/app/utils
90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> 6l2rp(...)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% a950191463ab06d0a2281cf5da2d083e2d9597fabda068cdaca057580ebd7169(queryFn):::mainFlowStyle --> 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 463d51dc39a12112043746e2e22b686f610e385941341c222cefe70f866362c5(doDiscoverQuery):::mainFlowStyle --> f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% f38aab9ca512b9d1eac49089af43601b9040aa3aa26250e7f5763d682bb32844(batchRequest):::mainFlowStyle --> e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% e2b67c983350bd142a5aaa1f1017d4bb264a9702d05bb48934bfa23cd89dfb08(addQuery):::mainFlowStyle --> 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 4828141d547f5f2e5afec5603e540d98fdbd67e4d4c1471cbb0eae026cd0cfbf(_handleUnmergeableQueries)
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 5b8c3af4c29605a7099831493304f29e9563c92a87bbc1501f00c37a627ee007(handleBatching):::mainFlowStyle --> 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> 6l2rp(...)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/static/app/utils/discover/genericDiscoverQuery.tsx" line="427">

---

## Query Function

The <SwmToken path="static/app/utils/discover/genericDiscoverQuery.tsx" pos="427:1:1" line-data="    queryFn: ({signal: _signal}) =&gt;">`queryFn`</SwmToken> function initiates the query process by calling <SwmToken path="static/app/utils/discover/genericDiscoverQuery.tsx" pos="428:1:1" line-data="      doDiscoverQuery&lt;T&gt;(api, url, apiPayload, {">`doDiscoverQuery`</SwmToken> with the necessary parameters. It sets up the query with options like <SwmToken path="static/app/utils/discover/genericDiscoverQuery.tsx" pos="429:1:1" line-data="        queryBatching: props.queryBatching,">`queryBatching`</SwmToken> and <SwmToken path="static/app/utils/discover/genericDiscoverQuery.tsx" pos="430:1:1" line-data="        skipAbort: props.skipAbort,">`skipAbort`</SwmToken>.

```tsx
    queryFn: ({signal: _signal}) =>
      doDiscoverQuery<T>(api, url, apiPayload, {
        queryBatching: props.queryBatching,
        skipAbort: props.skipAbort,
      }),
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/discover/genericDiscoverQuery.tsx" line="337">

---

## Discover Query

The <SwmToken path="static/app/utils/discover/genericDiscoverQuery.tsx" pos="337:6:6" line-data="export async function doDiscoverQuery&lt;T&gt;(">`doDiscoverQuery`</SwmToken> function handles the main logic for performing the query. It checks if batching is enabled and either processes the batch request or performs the query directly. It also includes retry logic to handle failures.

```tsx
export async function doDiscoverQuery<T>(
  api: Client,
  url: string,
  params: DiscoverQueryRequestParams,
  options: {
    queryBatching?: QueryBatching;
    retry?: RetryOptions;
    skipAbort?: boolean;
  } = {}
): Promise<[T, string | undefined, ResponseMeta<T> | undefined]> {
  const {queryBatching, retry, skipAbort} = options;
  if (queryBatching?.batchRequest) {
    return queryBatching.batchRequest(api, url, {
      query: params,
      includeAllArgs: true,
    });
  }

  const baseTimeout = retry?.baseTimeout ?? BASE_TIMEOUT;
  const timeoutMultiplier = retry?.timeoutMultiplier ?? TIMEOUT_MULTIPLIER;
  const statusCodes = retry?.statusCodes ?? [];
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="247">

---

## Batch Request

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="247:3:3" line-data="  function batchRequest(">`batchRequest`</SwmToken> function creates a promise for the query and adds it to the batch context using <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="262:3:3" line-data="      batchContext?.addQuery(queryDefinition, id.current);">`addQuery`</SwmToken>. This function is crucial for managing multiple queries efficiently.

```tsx
  function batchRequest(
    _: Client,
    path: string,
    requestQueryObject: QueryObject
  ): Promise<any> {
    const queryPromise = new Promise((resolve, reject) => {
      const queryDefinition: BatchQueryDefinition = {
        resolve,
        reject,
        transform,
        batchProperty,
        path,
        requestQueryObject,
        api,
      };
      batchContext?.addQuery(queryDefinition, id.current);
    });
    return queryPromise;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="188">

---

## Add Query

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="188:3:3" line-data="  const addQuery = (q: BatchQueryDefinition, id: symbol) =&gt; {">`addQuery`</SwmToken> function adds a query to the current batch and sets a timeout to handle batching. This ensures that all queries within a frame are aggregated before being processed.

```tsx
  const addQuery = (q: BatchQueryDefinition, id: symbol) => {
    queries.current[id] = q;

    window.clearTimeout(timeoutRef.current);
    // Put batch function in the next macro task to aggregate all requests in this frame.
    timeoutRef.current = window.setTimeout(() => {
      handleBatching(organization, queries.current);
      timeoutRef.current = undefined;
    }, 0);
  };
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="153">

---

## Handle Batching

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="153:2:2" line-data="function handleBatching(">`handleBatching`</SwmToken> function processes the batched queries by categorizing them into mergeable and unmergeable queries. It tracks the number of queries collected, saved, and sent for analytics purposes.

```tsx
function handleBatching(
  organization: Organization,
  queries: Record<symbol, BatchQueryDefinition>
) {
  const mergeMap = queriesToMap(queries);

  if (!mergeMap) {
    return;
  }

  let queriesSent = 0;
  queriesSent += _handleUnmergeableQueries(mergeMap);
  queriesSent += _handleMergeableQueries(mergeMap);

  const queriesCollected = Object.values(mergeMap).reduce(
    (acc, mergeList) => acc + mergeList.length,
    0
  );

  const queriesSaved = queriesCollected - queriesSent;

```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="80">

---

### Handling Unmergeable Queries

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="80:2:2" line-data="function _handleUnmergeableQueries(mergeMap: MergeMap) {">`_handleUnmergeableQueries`</SwmToken> function processes queries that cannot be merged. It iterates over the merge map and handles each unmergeable query individually.

```tsx
function _handleUnmergeableQueries(mergeMap: MergeMap) {
  let queriesSent = 0;
  Object.keys(mergeMap).forEach(k => {
    // Using async forEach to ensure calls start in parallel.
    const mergeList = mergeMap[k];

    if (mergeList.length === 1) {
      const [queryDefinition] = mergeList;
      queriesSent++;
      _handleUnmergeableQuery(queryDefinition);
    }
  });

  return queriesSent;
}
```

---

</SwmSnippet>

Now, lets zoom into this section of the flow:

```mermaid
graph TD;
      subgraph static/app/utils
90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle
end

subgraph static/app/utils
b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle --> c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle
end

subgraph static/app
c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle --> 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle
end

subgraph static/app
1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle --> 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle
end

subgraph static/app
4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler)
end

subgraph static/app/utils
4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle
end

subgraph static/app/utils
4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle --> b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle
end

subgraph static/app
2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler) --> 559bfddfedaeb6eedd4a2b9c4af59508927a1a6190c13b585781a179d22a07a1(processEvent)
end

subgraph static/app/utils
b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle --> 05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 90ff9374397a0adb357fe4c2249524c2149f81c211a4b8b1f471066ba428f2de(_handleMergeableQueries):::mainFlowStyle --> b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% b06d6a338d77963cde2551f503a2ce3b3530fa37719ed3615534229f27eaf648(_handleUnmergeableQuery):::mainFlowStyle --> c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% c4380a03d42ac0c65470f5ea342d4dce126f01939798968b2931ae3e5837aea5(requestFunction):::mainFlowStyle --> 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% 1025c11ff078741e3a52849e4dc81510d630800b045c60aea951683433a1c993(requestPromise):::mainFlowStyle --> 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler)
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 4f5a67a71dfb71654db327ed24d5e8187187a49b58963a473eec18ecb0aef026(request):::mainFlowStyle --> 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% 4b2faee236c2e651d9932fa234f72966df49f7aa0f85eb9909d65f4b6d8ce1a6(parse):::mainFlowStyle --> b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[static/app/](static/app/)</SwmPath>
%% 2cd409575454572c7b228bde73d6eb55227f3d7b14d37cc7ca5415bbcb81e4e5(handler) --> 559bfddfedaeb6eedd4a2b9c4af59508927a1a6190c13b585781a179d22a07a1(processEvent)
%% end
%% 
%% subgraph <SwmPath>[static/app/utils/](static/app/utils/)</SwmPath>
%% b2b47f6077e96a1ff47606d77c3fe70b18a84edc0ab0fa1349f7face4165d2ea(parseWidget):::mainFlowStyle --> 05bf2ddeab316943d2187e10bc3886949b4b03ae946f68d4f27a5bfc0025e132(mapToMetricsQuery):::mainFlowStyle
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="96">

---

## Handling Mergeable Queries

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="96:2:2" line-data="function _handleMergeableQueries(mergeMap: MergeMap) {">`_handleMergeableQueries`</SwmToken> function processes queries that can be merged together. It iterates over the <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="96:4:4" line-data="function _handleMergeableQueries(mergeMap: MergeMap) {">`mergeMap`</SwmToken>, checks if the queries can be merged based on their properties, and then sends a single batch request. If the queries cannot be merged, it delegates them to <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="71:2:2" line-data="function _handleUnmergeableQuery(queryDefinition: BatchQueryDefinition) {">`_handleUnmergeableQuery`</SwmToken>.

```tsx
function _handleMergeableQueries(mergeMap: MergeMap) {
  let queriesSent = 0;
  Object.keys(mergeMap).forEach(async k => {
    const mergeList = mergeMap[k];

    if (mergeList.length <= 1) {
      return;
    }

    const [exampleDefinition] = mergeList;
    const batchProperty = exampleDefinition.batchProperty;
    const query = {...exampleDefinition.requestQueryObject.query};
    const requestQueryObject = {...exampleDefinition.requestQueryObject, query};

    const batchValues: string[] = [];

    mergeList.forEach(q => {
      const batchFieldValue = q.requestQueryObject.query[batchProperty];
      if (Array.isArray(batchFieldValue)) {
        if (batchFieldValue.length > 1) {
          // Omit multiple requests with multi fields (eg. yAxis) for now and run them as single queries
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="71">

---

## Handling Unmergeable Queries

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="71:2:2" line-data="function _handleUnmergeableQuery(queryDefinition: BatchQueryDefinition) {">`_handleUnmergeableQuery`</SwmToken> function handles queries that cannot be merged. It sends individual requests for each query and resolves them separately.

```tsx
function _handleUnmergeableQuery(queryDefinition: BatchQueryDefinition) {
  const result = requestFunction(
    queryDefinition.api,
    queryDefinition.path,
    queryDefinition.requestQueryObject
  );
  queryDefinition.resolve(result);
}
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/performance/contexts/genericQueryBatcher.tsx" line="67">

---

## Sending Requests

The <SwmToken path="static/app/utils/performance/contexts/genericQueryBatcher.tsx" pos="67:2:2" line-data="function requestFunction(api: Client, path: string, queryObject: QueryObject) {">`requestFunction`</SwmToken> is a helper function that sends a request using the provided API client, path, and query object.

```tsx
function requestFunction(api: Client, path: string, queryObject: QueryObject) {
  return api.requestPromise(path, queryObject);
}
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/api.tsx" line="656">

---

## Request Promise

The <SwmToken path="static/app/api.tsx" pos="656:1:1" line-data="  requestPromise&lt;IncludeAllArgsType extends boolean&gt;(">`requestPromise`</SwmToken> method sends an API request and returns a promise. It handles success and error responses, ensuring that errors are properly logged and managed.

```tsx
  requestPromise<IncludeAllArgsType extends boolean>(
    path: string,
    {
      includeAllArgs,
      ...options
    }: {includeAllArgs?: IncludeAllArgsType} & Readonly<RequestOptions> = {}
  ): Promise<IncludeAllArgsType extends true ? ApiResult : any> {
    // Create an error object here before we make any async calls so that we
    // have a helpful stack trace if it errors
    //
    // This *should* get logged to Sentry only if the promise rejection is not handled
    // (since SDK captures unhandled rejections). Ideally we explicitly ignore rejection
    // or handle with a user friendly error message
    const preservedError = new Error('API Request Error');

    return new Promise((resolve, reject) =>
      this.request(path, {
        ...options,
        preservedError,
        success: (data, textStatus, resp) => {
          if (includeAllArgs) {
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/api.tsx" line="420">

---

## Making the Request

The <SwmToken path="static/app/api.tsx" pos="420:1:1" line-data="  request(path: string, options: Readonly&lt;RequestOptions&gt; = {}): Request {">`request`</SwmToken> method constructs and sends the actual HTTP request. It handles various aspects such as URL building, data serialization, and response handling.

```tsx
  request(path: string, options: Readonly<RequestOptions> = {}): Request {
    const method = options.method || (options.data ? 'POST' : 'GET');

    let fullUrl = buildRequestUrl(this.baseUrl, path, options);

    let data = options.data;

    if (data !== undefined && method !== 'GET' && !(data instanceof FormData)) {
      data = JSON.stringify(data);
    }

    // TODO(epurkhiser): Mimicking the old jQuery API, data could be a string /
    // object for GET requests. jQuery just sticks it onto the URL as query
    // parameters
    if (method === 'GET' && data) {
      const queryString = typeof data === 'string' ? data : qs.stringify(data);

      if (queryString.length > 0) {
        fullUrl = fullUrl + (fullUrl.includes('?') ? '&' : '?') + queryString;
      }
    }
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/replays/canvasReplayerPlugin.tsx" line="300">

---

## Event Handler

The <SwmToken path="static/app/components/replays/canvasReplayerPlugin.tsx" pos="304:1:1" line-data="    handler: (e: eventWithTime, isSync: boolean, {replayer}: {replayer: Replayer}) =&gt; {">`handler`</SwmToken> function processes canvas mutation events. It determines whether the event is a canvas mutation and processes it accordingly, either synchronously or asynchronously.

```tsx
    /**
     * Mutate canvas outside of iframe, then export the canvas as an image, and
     * draw inside of the image el inside of replay canvas.
     */
    handler: (e: eventWithTime, isSync: boolean, {replayer}: {replayer: Replayer}) => {
      const isCanvas = isCanvasMutationEvent(e);

      // isSync = true means it is fast forwarding vs playing
      // nothing to do when fast forwarding since canvas mutations for us are
      // image snapshots and do not depend on past events
      if (isSync) {
        // Set this to -1 to indicate that we will need to search
        // `canvasMutationEvents` for starting point of preloading
        //
        // Only do this when isSync is true, meaning there was a seek, since we
        // don't know where next index is
        nextPreloadIndex = -1;

        if (isCanvas) {
          processEventSync(e, {replayer});
        }
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/metrics/dashboardImport.tsx" line="138">

---

## Parsing Data

The <SwmToken path="static/app/utils/metrics/dashboardImport.tsx" pos="139:5:5" line-data="  public async parse() {">`parse`</SwmToken> method parses the imported widget data. It validates the widget type, parses the widget, and returns a report with the parsing outcome.

```tsx
  // Parsing functions
  public async parse() {
    const {
      id,
      definition: {title, type: widgetType},
    } = this.importedWidget;

    try {
      if (!SUPPORTED_WIDGET_TYPES.has(widgetType)) {
        throw new Error(`widget - unsupported type ${widgetType}`);
      }
      const widget = await this.parseWidget();

      if (!widget || !widget.queries.length) {
        throw new Error('widget - no parseable queries found');
      }

      const outcome: ImportOutcome = this.errors.length ? 'warning' : 'success';

      return {
        report: {
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/metrics/dashboardImport.tsx" line="179">

---

## Parsing Widget

The <SwmToken path="static/app/utils/metrics/dashboardImport.tsx" pos="179:5:5" line-data="  private async parseWidget() {">`parseWidget`</SwmToken> method parses the widget definition and its requests. It maps the parsed queries to metrics queries and constructs the final dashboard widget.

```tsx
  private async parseWidget() {
    this.parseLegendColumns();

    const {title, requests = []} = this.importedWidget.definition as WidgetDefinition;

    const parsedRequests = requests.map(r => this.parseRequest(r));
    const parsedQueries = parsedRequests.flatMap(request => request.queries);

    const metricsQueries = await Promise.all(
      parsedQueries.map(async query => {
        const mapped = await this.mapToMetricsQuery(query);
        return {
          ...mapped,
        };
      })
    );

    const nonEmptyQueries = metricsQueries.filter(query => query.mri) as MetricsQuery[];

    if (!nonEmptyQueries.length) {
      return null;
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/replays/canvasReplayerPlugin.tsx" line="230">

---

## Processing Events

The <SwmToken path="static/app/components/replays/canvasReplayerPlugin.tsx" pos="233:5:5" line-data="  async function processEvent(e: CanvasEventWithTime, {replayer}: {replayer: Replayer}) {">`processEvent`</SwmToken> function processes canvas mutation events asynchronously. It preloads the event, finds the target canvas, applies the mutation, and updates the canvas image.

```tsx
  /**
   * Processes canvas mutation events
   */
  async function processEvent(e: CanvasEventWithTime, {replayer}: {replayer: Replayer}) {
    preload(e);

    const source = replayer.getMirror().getNode(e.data.id);
    const target =
      canvases.get(e.data.id) ||
      (source && cloneCanvas(e.data.id, source as HTMLCanvasElement));

    if (!target) {
      throw new InvalidCanvasNodeError('No canvas found for id');
    }

    await canvasMutation({
      event: e,
      mutation: e.data,
      target,
      imageMap,
      canvasEventMap,
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/utils/metrics/dashboardImport.tsx" line="397">

---

## Mapping to Metrics Query

The <SwmToken path="static/app/utils/metrics/dashboardImport.tsx" pos="398:5:5" line-data="  private async mapToMetricsQuery(widget): Promise&lt;MetricsQuery | null&gt; {">`mapToMetricsQuery`</SwmToken> method maps a widget's query to a metrics query. It fetches the available tags, constructs the query filter and group by, and returns the metrics query.

```tsx
  // Mapping functions
  private async mapToMetricsQuery(widget): Promise<MetricsQuery | null> {
    const {metric, aggregation, filters} = widget;

    // @ts-expect-error name is actually defined on MetricMeta
    const metricMeta = this.availableMetrics.find(m => m.name === metric);

    if (!metricMeta) {
      this.errors.push(`widget.request.query - metric not found: ${metric}`);
      return null;
    }

    const availableTags = await this.fetchAvailableTags(metricMeta.mri);

    const query = this.constructMetricQueryFilter(filters, availableTags);
    const groupBy = this.constructMetricGroupBy(widget.groupBy, availableTags);

    return {
      mri: metricMeta.mri,
      aggregation,
      query,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

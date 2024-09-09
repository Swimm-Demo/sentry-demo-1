---
title: Understanding Dynamic Sampling Tasks
---
```mermaid
graph TD;
 A[Function Call] --> B[dynamic_sampling_task]
 A[Function Call] --> C[dynamic_sampling_task_with_context]
 B --> D[metrics.incr]
 B --> E[metrics.timer]
 C --> D[metrics.incr]
 C --> E[metrics.timer]
 C --> F[TaskContext]

 graph TD;
 A[Function] -->|decorated with dynamic_sampling_task| B[TaskContext];
 B -->|manages| C[Timers];
 B -->|tracks| D[Execution Metrics];
 C -->|creates| E[Named Timers];
 D -->|provides| F[Detailed Metrics];
```

# Decorators

The <SwmToken path="src/sentry/dynamic_sampling/tasks/utils.py" pos="49:2:2" line-data="def dynamic_sampling_task(func):">`dynamic_sampling_task`</SwmToken> decorator wraps the function and uses the <SwmToken path="src/sentry/dynamic_sampling/tasks/utils.py" pos="38:1:3" line-data="            metrics.incr(f&quot;{task_name}.start&quot;, sample_rate=1.0)">`metrics.incr`</SwmToken> method to increment a counter each time the function starts. It also uses a timer to measure the execution duration. The <SwmToken path="src/sentry/dynamic_sampling/tasks/utils.py" pos="30:2:2" line-data="def dynamic_sampling_task_with_context(max_task_execution: int):">`dynamic_sampling_task_with_context`</SwmToken> decorator extends this functionality by also providing a <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="63:2:2" line-data="class TaskContext:">`TaskContext`</SwmToken> object to the function, which can be used to manage task-specific data and execution limits. Both decorators help in monitoring and optimizing the performance of dynamic sampling tasks by providing detailed metrics.

<SwmSnippet path="/src/sentry/dynamic_sampling/tasks/task_context.py" line="63">

---

# <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="63:2:2" line-data="class TaskContext:">`TaskContext`</SwmToken> Class

The <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="63:2:2" line-data="class TaskContext:">`TaskContext`</SwmToken> class keeps information about a running task, including its name, allowed runtime, and stats about its operation. It also manages multiple named timers for tracking execution time of functions.

```python
class TaskContext:
    """
    Keeps information about a running task

    * the name
    * the amount of time is allowed to run (until a TimeoutError should be emitted)
    * stats about the task operation (how many items it has processed) used for logging
    * keeps a Timers object that manages multiple named timers for tracking execution time of functions.
    """

    name: str
    num_seconds: float
    context_data: dict[str, DynamicSamplingLogState] | None = None

    def __post_init__(self):
        # always override
        self.expiration_time = time.monotonic() + self.num_seconds
        if self.context_data is None:
            self.context_data = {}
        self.timers = Timers()
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/dynamic_sampling/tasks/task_context.py" line="146">

---

# Timers Class

The <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="146:2:2" line-data="class Timers:">`Timers`</SwmToken> class keeps the state of many named timers. Individual timers are created at first use, and the <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="152:1:1" line-data="    TaskContext uses this class to keep track of timers.">`TaskContext`</SwmToken> class uses this to keep track of timers.

```python
class Timers:
    """
    Keeps the state of many named timers.

    Individual timers will be created at first use.
    Users should not use this class directly, but use the NamedTimer class instead.
    TaskContext uses this class to keep track of timers.
    For using timers for functions use TaskContext.get_timer("<name>") to get a NamedTimer.

    """

    def __init__(self):
        self.timers: dict[str, TimerState] = {}

    def get_timer(self, name: str) -> "NamedTimer":
        return NamedTimer(name, self)

    def start(self, name: str) -> float:
        state = self.get_timer_state(name)
        if not state.started:
            state.started = time.monotonic()
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/dynamic_sampling/tasks/common.py" line="77">

---

# Wrapped Function

The <SwmToken path="src/sentry/dynamic_sampling/tasks/common.py" pos="77:3:3" line-data="        def wrapped(context: TaskContext, *args, **kwargs):">`wrapped`</SwmToken> function uses the <SwmToken path="src/sentry/dynamic_sampling/tasks/common.py" pos="77:8:8" line-data="        def wrapped(context: TaskContext, *args, **kwargs):">`TaskContext`</SwmToken> to manage the execution state and timing of a function. It raises a <SwmToken path="src/sentry/dynamic_sampling/tasks/common.py" pos="79:3:3" line-data="                raise TimeoutException(context)">`TimeoutException`</SwmToken> if the task exceeds its allowed runtime.

```python
        def wrapped(context: TaskContext, *args, **kwargs):
            if time.monotonic() > context.expiration_time:
                raise TimeoutException(context)
            timer = context.get_timer(func_name)
            with timer:
                state = context.get_function_state(func_name)
                val = inner(state, *args, **kwargs)
                state.execution_time = timer.current()
                context.set_function_state(func_name, state)
                return val
```

---

</SwmSnippet>

<SwmSnippet path="/src/sentry/dynamic_sampling/tasks/utils.py" line="26">

---

# <SwmToken path="src/sentry/dynamic_sampling/tasks/utils.py" pos="26:2:2" line-data="def _compute_task_name(function_name: str) -&gt; str:">`_compute_task_name`</SwmToken> Function

The <SwmToken path="src/sentry/dynamic_sampling/tasks/utils.py" pos="26:2:2" line-data="def _compute_task_name(function_name: str) -&gt; str:">`_compute_task_name`</SwmToken> function generates a task name based on the function name, which is used for tracking and logging purposes.

```python
def _compute_task_name(function_name: str) -> str:
    return f"sentry.tasks.dynamic_sampling.{function_name}"
```

---

</SwmSnippet>

# Example Usage

An example of creating a <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="63:2:2" line-data="class TaskContext:">`TaskContext`</SwmToken> object: <SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="201:1:1" line-data="        task_context = TaskContext(&quot;my_task&quot;, 100)">`task_context`</SwmToken>` = TaskContext('my_task', `<SwmToken path="src/sentry/dynamic_sampling/tasks/task_context.py" pos="201:12:12" line-data="        task_context = TaskContext(&quot;my_task&quot;, 100)">`100`</SwmToken>`)`.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

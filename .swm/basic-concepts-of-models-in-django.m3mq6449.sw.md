---
title: Basic Concepts of Models in Django
---
# Overview of Models in Django

Models are used to define the structure of the database tables and the relationships between them. They are defined using Django's ORM (Object-Relational Mapping) system, which allows for easy interaction with the database using Python code. Models include fields that represent the columns in the database table, and each field is an instance of a specific field class provided by Django. They also include methods that define the behavior of the data, such as custom save methods or query methods.

# Fields in Models

Fields in models represent the columns in the database table. Each field is an instance of a specific field class provided by Django. These fields define the type of data that can be stored in each column and can include options such as <SwmToken path="src/sentry/db/models/base.py" pos="60:13:13" line-data="    # Some models have a globally unique identifier, like a UUID. This should be a set of one or">`unique`</SwmToken>, <SwmToken path="src/sentry/db/models/base.py" pos="180:19:19" line-data="        # whose PK we&#39;ve already exported (or `NULL`, if the FK field is nullable).">`NULL`</SwmToken>, and `blank`.

<SwmSnippet path="/src/sentry/db/models/base.py" line="53">

---

The <SwmToken path="src/sentry/db/models/base.py" pos="53:2:2" line-data="class BaseModel(models.Model):">`BaseModel`</SwmToken> class in <SwmPath>[src/sentry/db/models/base.py](src/sentry/db/models/base.py)</SwmPath> demonstrates how fields are defined in a model. It includes various attributes and methods that help manage the model's data.

```python
class BaseModel(models.Model):
    class Meta:
        abstract = True

    __relocation_scope__: RelocationScope | set[RelocationScope]
    __relocation_dependencies__: set[str]

    # Some models have a globally unique identifier, like a UUID. This should be a set of one or
    # more fields, none of which are foreign keys, that are `unique=True` or `unique_together` for
    # an entire Sentry instance.
    __relocation_custom_ordinal__: list[str] | None = None

    objects: ClassVar[BaseManager[Self]] = BaseManager()

    update = update

    def __getstate__(self) -> dict[str, Any]:
        d = self.__dict__.copy()
        # we can't serialize weakrefs
        d.pop("_Model__data", None)
        return d
```

---

</SwmSnippet>

# Methods in Models

Models also include methods that define the behavior of the data. These methods can be custom save methods, query methods, or any other method that manipulates the model's data.

<SwmSnippet path="/src/sentry/db/models/base.py" line="69">

---

The <SwmToken path="src/sentry/db/models/base.py" pos="53:2:2" line-data="class BaseModel(models.Model):">`BaseModel`</SwmToken> class also includes methods like <SwmToken path="src/sentry/db/models/base.py" pos="69:3:3" line-data="    def __getstate__(self) -&gt; dict[str, Any]:">`__getstate__`</SwmToken>, <SwmToken path="src/sentry/db/models/base.py" pos="75:3:3" line-data="    def __hash__(self) -&gt; int:">`__hash__`</SwmToken>, and <SwmToken path="src/sentry/db/models/base.py" pos="82:3:3" line-data="    def __reduce__(">`__reduce__`</SwmToken> which define how the model's data is serialized, hashed, and reduced.

```python
    def __getstate__(self) -> dict[str, Any]:
        d = self.__dict__.copy()
        # we can't serialize weakrefs
        d.pop("_Model__data", None)
        return d

    def __hash__(self) -> int:
        # Django decided that it shouldn't let us hash objects even though they have
        # memory addresses. We need that behavior, so let's revert.
        if self.pk:
            return models.Model.__hash__(self)
        return id(self)

    def __reduce__(
        self,
    ) -> tuple[Callable[[int], models.Model], tuple[tuple[str, str]], Mapping[str, Any]]:
        reduced = super().__reduce__()
        assert isinstance(reduced, tuple), reduced
        (model_unpickle, stuff, _) = reduced
        return (model_unpickle, stuff, self.__getstate__())
```

---

</SwmSnippet>

# Importing Models

Models are imported from the <SwmToken path="src/sentry/db/models/manager/base.py" pos="13:2:6" line-data="from django.db.models import Model">`django.db.models`</SwmToken> module and are used throughout the codebase to interact with the database. This allows for a consistent and easy-to-use interface for database operations.

<SwmSnippet path="/src/sentry/db/models/manager/base.py" line="11">

---

The import statements in <SwmPath>[src/sentry/db/models/manager/base.py](src/sentry/db/models/manager/base.py)</SwmPath> show how models and related components are imported from Django's ORM.

```python
from django.conf import settings
from django.db import models, router
from django.db.models import Model
from django.db.models.fields import Field
from django.db.models.manager import Manager as DjangoBaseManager
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

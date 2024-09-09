---
title: Fields in Models
---
# What is Fields in Models

Fields in models are attributes that define the type of data that can be stored in a model's attribute. They specify the characteristics and constraints of the data, such as its type, default value, and validation rules. Fields are essential for defining the structure and behavior of data within the application.

## <SwmToken path="src/sentry/db/models/fields/jsonfield.py" pos="39:2:2" line-data="class JSONField(models.TextField):">`JSONField`</SwmToken>

The <SwmToken path="src/sentry/db/models/fields/jsonfield.py" pos="39:2:2" line-data="class JSONField(models.TextField):">`JSONField`</SwmToken> ensures that the data entered is valid JSON and can serialize dates and decimals. It includes validation rules and custom behaviors for handling JSON data.

<SwmSnippet path="/src/sentry/db/models/fields/jsonfield.py" line="39">

---

The <SwmToken path="src/sentry/db/models/fields/jsonfield.py" pos="39:2:2" line-data="class JSONField(models.TextField):">`JSONField`</SwmToken> class in the code ensures that the data entered into it is valid JSON. It can serialize dates and decimals and provides a default value if none is specified. It also includes validation to ensure the data is correct and can handle default values that are callable or strings.

```python
class JSONField(models.TextField):
    """
    A field that will ensure the data entered into it is valid JSON.

    Originally from https://github.com/adamchainz/django-jsonfield/blob/0.9.13/jsonfield/fields.py
    Adapted to fit our requirements of:

    - always using a text field
    - being able to serialize dates/decimals
    - not emitting deprecation warnings

    By default, this field will also invoke the Creator descriptor when setting the attribute.
    This can make it difficult to use json fields that receive raw strings, so optionally setting no_creator_hook=True
    surpresses this behavior.
    """

    default_error_messages = {"invalid": _("'%s' is not a valid JSON string.")}
    description = "JSON object"
    no_creator_hook = False

    def __init__(self, *args, **kwargs):
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/db/models/fields/array.py" pos="15:2:2" line-data="class ArrayField(models.Field):">`ArrayField`</SwmToken>

The <SwmToken path="src/sentry/db/models/fields/array.py" pos="15:2:2" line-data="class ArrayField(models.Field):">`ArrayField`</SwmToken> allows storing arrays of a particular type in <SwmToken path="src/sentry/db/models/fields/array.py" pos="17:7:7" line-data="        # Arrays in PostgreSQL are arrays of a particular type.">`PostgreSQL`</SwmToken>, providing flexibility for handling multiple values within a single field.

<SwmSnippet path="/src/sentry/db/models/fields/array.py" line="13">

---

The <SwmToken path="src/sentry/db/models/fields/array.py" pos="15:2:2" line-data="class ArrayField(models.Field):">`ArrayField`</SwmToken> class allows storing arrays of a particular type in <SwmToken path="src/sentry/db/models/fields/array.py" pos="17:7:7" line-data="        # Arrays in PostgreSQL are arrays of a particular type.">`PostgreSQL`</SwmToken>. It saves the subtype in the field class and ensures that the array elements are appropriately coerced to the correct type. It also includes methods for contributing to the class, determining the database type, and preparing values for the database.

```python
# Adapted from django-pgfields
# https://github.com/lukesneeringer/django-pgfields/blob/master/django_pg/models/fields/array.py
class ArrayField(models.Field):
    def __init__(self, of=models.TextField, **kwargs):
        # Arrays in PostgreSQL are arrays of a particular type.
        # Save the subtype in our field class.
        if isinstance(of, type):
            of = of()
        self.of = of

        # Set "null" to True. Arrays don't have nulls, but null=True
        # in the ORM amounts to nothing in SQL (whereas null=False
        # corresponds to `NOT NULL`)
        kwargs["null"] = True

        super().__init__(**kwargs)

    def contribute_to_class(self, cls: type[models.Model], name: str, private_only: bool = False):
        """
        Add a descriptor for backwards compatibility
        with previous Django behavior.
```

---

</SwmSnippet>

## <SwmToken path="src/sentry/db/models/fields/uuid.py" pos="44:2:2" line-data="class UUIDField(models.Field):">`UUIDField`</SwmToken>

The <SwmToken path="src/sentry/db/models/fields/uuid.py" pos="44:2:2" line-data="class UUIDField(models.Field):">`UUIDField`</SwmToken> can automatically generate <SwmToken path="src/sentry/db/models/fields/uuid.py" pos="45:10:10" line-data="    &quot;&quot;&quot;Field for storing UUIDs.&quot;&quot;&quot;">`UUIDs`</SwmToken> for new records and enforce constraints such as non-editability and nullability.

<SwmSnippet path="/src/sentry/db/models/fields/uuid.py" line="49">

---

The <SwmToken path="src/sentry/db/models/fields/uuid.py" pos="44:2:2" line-data="class UUIDField(models.Field):">`UUIDField`</SwmToken> class can automatically generate <SwmToken path="src/sentry/db/models/fields/uuid.py" pos="45:10:10" line-data="    &quot;&quot;&quot;Field for storing UUIDs.&quot;&quot;&quot;">`UUIDs`</SwmToken> for new records. It enforces constraints such as non-editability and nullability, ensuring that each record has a unique identifier.

```python
    def __init__(self, auto_add=False, coerce_to=UUID, **kwargs):
        """Instantiate the field."""

        # If the `auto_add` argument is specified as True, substitute an
        # appropriate callable which requires no arguments and will return
        # a UUID.
        if auto_add is True:
            auto_add = uuid4

        # If the `auto_add` arguments is specified as a string
        # parse out and import the callable.
        if isinstance(auto_add, str):
            module_name, member = auto_add.split(":")
            module = importlib.import_module(module_name)
            auto_add = getattr(module, member)

        # Save the `auto_add` and `coerce_to` rules.
        self._auto_add = auto_add
        self._coerce_to = coerce_to

        # If `auto_add` is enabled, it should imply that the field
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>

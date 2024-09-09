---
title: Importing Data Flow
---
This document will cover the Importing Data Flow, which includes:

1. Initiating the import task
2. Handling the import within the organization scope
3. Processing the core import logic
4. Saving the imported data.

Technical document: <SwmLink doc-title="Importing Data Flow">[Importing Data Flow](/.swm/importing-data-flow.opos8asp.sw.md)</SwmLink>

# [Initiating the Import Task](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/opos8asp#initiating-the-import-task)

The import process begins by initiating the import task. This involves starting the relocation task and verifying that the relocation file is ready for use. The relocation task ensures that the data to be imported is correctly identified and prepared. This step is crucial for setting up the import process and ensuring that the data is ready for the subsequent steps.

# [Handling the Import in Organization Scope](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/opos8asp#importing-in-organization-scope)

Once the import task is initiated, the next step is to handle the import within the organization scope. This means that only specific models related to the organization or user are imported. This step ensures that the import process is scoped correctly and only relevant data is imported. The organization scope is determined by the models' `RelocationScope`, which can be either `User` or `Organization`.

# [Processing the Core Import Logic](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/opos8asp#handling-the-import-logic)

The core import logic involves processing the data, writing it, and resolving any necessary mappings. This step is where the actual data import happens. The data is read from the source, processed to ensure it is in the correct format, and then written to the appropriate location. Any necessary mappings, such as resolving organization slugs from the primary key map, are also handled in this step. This ensures that the data is correctly integrated into the system.

# [Saving the Imported Data](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/opos8asp#saving-imported-data)

The final step in the import process is saving the imported data. This involves normalizing and processing the event, saving related models to the database, and writing the event into the event stream. Normalizing the data ensures that it is in a consistent format, while processing it involves any necessary transformations. Saving the data to the database ensures that it is stored persistently, and writing it into the event stream allows it to be picked up by other parts of the system for further processing. This step ensures that the imported data is fully integrated and available for use.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

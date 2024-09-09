---
title: Bulk Mutation of Issues
---
This document will cover the Bulk Mutation of Issues feature, which includes:

1. Processing the request
2. Validating project access
3. Identifying issues to be modified
4. Applying changes to issues.

Technical document: <SwmLink doc-title="Bulk Mutation of Issues">[Bulk Mutation of Issues](/.swm/bulk-mutation-of-issues.f6jjyg87.sw.md)</SwmLink>

# [Processing the Request](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/f6jjyg87#handling-bulk-mutation-of-issues)

The process begins with handling the incoming request. This involves receiving the request from the user, which contains the details of the issues to be modified. The request includes query parameters that specify which issues are to be updated and the attributes that need to be changed. This step ensures that the system understands what modifications are being requested.

# [Validating Project Access](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/f6jjyg87#handling-bulk-mutation-of-issues)

Next, the system validates access to the specified project. This is a security measure to ensure that the user making the request has the necessary permissions to modify the issues within the project. If the user does not have the appropriate access rights, the request is denied. This step is crucial for maintaining the integrity and security of the project data.

# [Identifying Issues to Modify](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/f6jjyg87#handling-bulk-mutation-of-issues)

Once access is validated, the system identifies the issues that need to be modified based on the query parameters provided in the request. This involves filtering the issues to match the criteria specified by the user, such as issue IDs or status. This step ensures that only the relevant issues are selected for modification.

# [Applying Changes to Issues](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=/docs/f6jjyg87#updating-group-data)

Finally, the system applies the necessary changes to the identified issues. This is done by calling the `update_groups` function, which updates the attributes of the issues as specified in the request. The changes are applied in bulk to ensure efficiency and consistency. This step ensures that the modifications are executed as requested by the user.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>

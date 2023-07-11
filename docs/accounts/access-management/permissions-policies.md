# Permissions and Policies

Autenticami allows for the creation of `Policies` to ensure that the correct identity has the appropriate access to resources linked to an account.

Policies are implemented as a document listing the actions that can be performed and the resourcers those actions can affect.

In particular policies are `Identity-based policies` as they can be attached only to identities.

!!! info "INFO"
    By default no permission is associated to an identity, hence an identity can't access anythong until permissions are granted.

`Permissions` are a collection of policies that can be associated to identities. There are two types of permissions:

- **Inline**: permissions implemeneted inline to the definition of the identity
- **Managed**: permissions implemeneted and managed outside the identity, so they can be shared across multiple identities.

!!! info "INFO"
    `Resources` are defined within the account, however identities are themselves resources that can be target of `policies` actions.

## Trust Policy for roles

A `Trust Policy` define which principal can assume the role, and under which conditions.

## Policies Access Control

Policies enabled two types of access control:

- **Role-Based access control (RBAC)**: Defines permissions based on role. For each identity, the collections of policies are listed.
- **Attribute-based access control (ABAC)**: Define permissions based on attributes on resources. Each identity is associated with one or more tags and automatically has access to all resources that belong to the same tags.

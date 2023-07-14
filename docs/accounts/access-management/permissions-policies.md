# Permissions and Policies

Autenticami allows for the creation of `Policies` to ensure that the correct identity has the appropriate access to resources.

In particular policies are `Identity-based policies` as they can be attached only to identities.

There are two types of policy documents:

- [Principal Trust Identity Policy](#permissions-policies/#principal-trust-identity-policy)
- [Access Control List Policy](#access-control-list-policy)

## Principal Trust Identity Policy

A `Principal Trust Identit Policy (TRUST)` defines which principal can assume the role, and under which conditions.

## Access Control List Policy

An `Access Control List Policy (ACL)` is implemented as a document listing the actions that can/cannot be performed and the resourcers those actions can affect.

!!! info "INFO"
    Identities are themselves resources that can be target of `policies` actions.

Policies enable two types of access control:

- **Role-Based access control (RBAC)**: Defines permissions based on role. For each identity, the collections of policies are listed.
- **Attribute-based access control (ABAC)**: Define permissions based on attributes on resources. Each identity is associated with one or more tags and automatically has access to all resources that belong to the same tags.

!!! info "INFO"
    Autenticami implements a Least-Privilege Model, hence an identity can't access anything until permissions are granted.

A collection of policies can be referred as `Permissions`. There are two types of permissions:

- **Inline**: permissions implemented inline to the definition of the identity
- **Managed**: permissions implemented and managed outside the identity, so they can be shared across multiple identities.
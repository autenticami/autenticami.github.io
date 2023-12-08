# Policies

Autenticami allows the creation of `Policies` that can be associated with an identity to ensure that it has the proper permissions to access resources.

In particular policies are `Identity-based policies` as they can be attached only to identities.

`Policies` are implemented in the form of documents that define a list of [policy statements](#policy-statement) that can be permitted or fobidden.

It is possible to divide the policies into several documents and these will be aggregated during the evaluation phase

There are two types of policies:

- [Policies](#policies)
  - [Principal Trust Identity Policy](#principal-trust-identity-policy)
  - [Access Control List Policy](#access-control-list-policy)
  - [Policy Statement](#policy-statement)

## Principal Trust Identity Policy

A `Principal Trust Identity Policy (TRUST)` defines which principal can assume the role, and under which conditions.

## Access Control List Policy

An `Access Control List Policy (ACL)` lists the actions that can/cannot be performed and the resourcers those actions can affect.

!!! info "INFO"
    Identities are themselves resources that can be target of `policies` actions.

`Permissions` permit identities to access a resource or execute a specific action and they are granted through the association of policies.

Policies enable two types of permission-based access control:

- **Role-Based access control (RBAC)**: Permission-based on role. For each identity, the collections of policies are listed.
- **Attribute-based access control (ABAC)**: Permission-based on resource attributes. Each identity is associated with one or more tags and automatically has access to all resources that belong to the same tags.

!!! info "INFO"
    Autenticami implements a Least-Privilege Model, hence an identity can't access anything until permissions are granted.

There are two types of policies:

- **Inline**: policies associated inline to the definition of the identity
- **Managed**: policies associated and managed outside the identity, so they can be shared across multiple identities.

## Policy Statement

A policy statement list actions associated to resources.

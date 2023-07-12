# Identities

An `Identity Security` is a solution for securing all identities used in an account.

There are mainly two types of identities:

- [User and Groups](../users-groups)
- [Roles](../roles)

## Principals

A `Principal` is an human user or workload with granted permissions that authenticates and make requests, specifically:

- A user
- A role
- An assumed role (role assumed by a user or a role assumed by a workload).

Autenticami implements `OAuth` and `OpenId` protocols, in particular a `Principal` is issued with an `Access Token`.

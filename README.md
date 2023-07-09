# Autenticami

`Autenticami` is a multi-account `Identity and Access Managment` that provides the foundations for creating an identity-based application access control.

An Account is identified by an `Account Id` and it is responsible for defining `Users, Roles and Permissions`.

`Autenticami` implements OAuth and OpenId protocols, in particular an `Authenticated Identity` is issued with an `Access Token` that can be used by third-party APIs to grant access to its resources.

An `Identity and Access Managment` (IAM or IdAM) is a framework of policies and technologies to ensure that the right users and roles have the appropriate access to resources linked to an account.

`Autenticami` is inspired by AWS IAM and Policies are implemented using an `AWS like definition languange`.

With `Autenticami` you can specify who or what can access resources by the means of fine-grained permissions.

- `Who`: *Users and Roles that can authenticate*
- `Can Access`: *Permission with policies to ensure appropriate access to resources for users and roles*
- `Resources`: *Custom resources defined into the account*

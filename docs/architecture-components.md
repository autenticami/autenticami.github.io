# Architecture and Concepts

`Autenticami` is composed of several components.

- **Identity Service (IDS):** The identitiy service is responsible swapping the third party token with an autenticami token. By the means of this service it is possible to assume a role identity.
- **Policy Decision Point (PDP):** The policy decision point is responsible for evaluating the policies and deciding if a identity is allowed to perform an action. Policies are retrieved by the means of the Policy Administration Point (PAP).
- **Policy Administration Point (PAP):** The policy administration point is responsible for managing the policies.
- **Autenticami Administration Point (AAP):** The autenticami administration point is responsible for managing accounts and projects.
- **Policy Enforcement Point (PEP):** The policy enforcement point is responsible for enforcing the policies.

!!! info "INFO"
    Identity Service has to be configured with a plugin that implements the integration with an external identity provider.

## Applicative Flow

An authentication-based application flow can be summarized with the following steps:

- The Developer configures the Application and its Projects using the AAP.
- The Application autenticates with the external identity provider by the means of the IDS.
- The IDS swaps the external token with an autenticami token.
- Optionally the application can assume a role by the means of the IDS.
- The Application use an Autenticami SDK to act as a PEP and check the permissions with the PDP.
- The PDP retrieves policies and attributes from the PAP.

!!! info "INFO"
    If the application has already been authenticated with the external identity provider it is possible just to swap the token with the Identity Service.

The following diagram shows the applicative flow of an application using `Autenticami`.

![Architectural diagram](assets/images/autenticami-architecture.png)

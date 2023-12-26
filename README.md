# Autenticami

<div style="background-color:#111111;text-align:justify;}">
  <img src="docs/assets/images/autenticami-black-logo.png" width="250px" height="auto"/>
</div>

`Autenticami` A Multi-Account and Multi-Tenant Policy-Based Access Control Platform to enable a modern Identity-Based Access Control.

As an `Autenticami administrator` you can create multiple accounts and create multiple projects within each account.

All you have to do is describe your project's `resources` within your account and create your own access control policies. Resources are organized into project's domains.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions:

- `Who`: *Identities (Users and Roles) authenticated in the application*
- `Can Access`: *Permissions granted by attaching policies*
- `Resources`: *Resources targeted by permissions*

To enforce the access control process, the application implements the Policy Enforcement Point using the available SDKs

Below is a sample policy document for granting access to the Employee and Timesheet resources of an HR project (hr-app):

```json linenums="1"
# Autenticami

<div style="background-color:#111111;text-align:justify;}">
  <img src="assets/images/autenticami-black-logo.png" width="250px" height="auto"/>
</div>


`Autenticami` A Multi-Account and Multi-Tenant Policy-Based Access Control Platform to enable a modern Identity-Based Access Control.

As an `Autenticami administrator` you can create multiple accounts and create multiple projects within each account.

All you have to do is describe your project's `resources` within your account and create your own access control policies. Resources are organized into project's domains.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions:

- `Who`: *Identities (Users and Roles) authenticated in the application*
- `Can Access`: *Permissions granted by attaching policies*
- `Resources`: *Resources targeted by permissions*

To enforce the access control process, the application implements the Policy Enforcement Point using the available SDKs

Below is a sample policy document for granting access to the Employee and Timesheet resources of an HR project (hr-app):

```json linenums="1"
{
  "Syntax": "autenticami1",
  "Name": "person-base-reader",
  "Type": "AC",
  "Permit": [
    {
      "Name": "permit-hr:person:reader:any",
      "Actions": [
        "person:ListEmployee",
        "person:ReadEmployee"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:organisation:person/*"
      ]
    },
    {
      "Name": "permit-hr:timesheet:writer:any",
      "Actions": [
        "person:ReadTimesheet",
        "person:CreateTimesheet",
        "person:UpdateTimesheet",
        "person:DeleteTimesheet"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:time-management:person/*"
      ],
      "Condition": "DateGreaterThan({{.Autenticami.TokenIssueTime}})' && DateLessThan('{{.Autenticami.CurrentTime}}': '2023-12-31T23:59:59Z')"
    }
  ],
  "Forbid": [
    {
      "Name": "forbid-write-hr:timesheet:writer:bc182146-1598-4fde-99aa-b2d4d08bc1e2",
      "Actions": [
        "person:Read"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:time-management:person/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

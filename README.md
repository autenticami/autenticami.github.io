# Autenticami

<div style="background-color:#111111;text-align:justify;}">
  <img src="docs/assets/images/autenticami-black-logo.png" width="250px" height="auto"/>
</div>

`Autenticami` is a multi-account `Identity and Access Management` (IAM or IdAM) solution to enable a modern identity-based project access control for third party projects.

All you have to do is describe your project's resources and create your own access control policies. Resources are organized into project's domains.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions:

- `Who`: *Identities (Users and Roles) that can authenticate*
- `Can Access`: *Permissions to affect resources using actions, those are granted by attaching policies*
- `Resources`: *Resources described into the account*

Below is a sample policy document for granting access to the Employee and Timesheet resources of the HR project (hr-app):

```json linenums="1"
{
  "Syntax": "autenticami1",
  "Name": "person-base-reader",
  "Type": "ACL",
  "Permit": [
    {
      "Name": "permit-hr/person/reader/any",
      "Actions": [
        "person:ListEmployee",
        "person:ReadEmployee"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:organisation:person/*"
      ]
    },
    {
      "Name": "permit-hr/timesheet/writer/any",
      "Actions": [
        "person:ReadTimesheet",
        "person:CreateTimesheet",
        "person:UpdateTimesheet",
        "person:DeleteTimesheet"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:time-management:person/*"
      ]
    }
  ],
  "Forbid": [
    {
      "Name": "forbid-write-hr/timesheet/writer/bc182146-1598-4fde-99aa-b2d4d08bc1e2",
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

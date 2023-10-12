# Autenticami

<div style="background-color:#111111;text-align:justify;}">
  <img src="docs/assets/images/autenticami-black-logo.png" width="250px" height="auto"/>
</div>

`Autenticami` is a multi-account `Identity and Access Management` (IAM or IdAM) solution to enable a modern identity-based application access control for third party applications.

All you have to do is describe your application's resources and create your own access control policies. Resources are organized into hierarchies of Applications and Domains.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions:

- `Who`: *Identities (Users and Roles) that can authenticate*
- `Can Access`: *Permissions to affect resources using actions, those are granted by attaching policies*
- `Resources`: *Resources described into the account*

Below is a sample policy document for granting access to the Employee and Timesheet resources of the HR application (hr-app):

```json linenums="1"
{
  "Version": "2022-07-21",
  "Label": "PeopleBaseReader",
  "Description": "This policy enable List and Read access to employee and timesheet of the domain people.",
  "Type": "ACL",
  "Permit": [
    {
      "Label": "permit-hr/person/reader/any",
      "Actions": [
        "people:ListEmployee",
        "people:ReadEmployee"
      ],
      "Resources": [
        "uur:hr-app:organisation:explore:581616507495:people/*"
      ]
    },
    {
      "Label": "permit-hr/timesheet/writer/any",
      "Actions": [
        "people:ReadTimesheet",
        "people:CreateTimesheet",
        "people:UpdateTimesheet",
        "people:DeleteTimesheet"
      ],
      "Resources": [
        "uur:hr-app:time-management:data-entry:581616507495:people/*"
      ]
    }
  ],
  "Forbid": [
    {
      "Label": "forbid-write-hr/timesheet/writer/bc182146-1598-4fde-99aa-b2d4d08bc1e2",
      "Actions": [
        "people:Read"
      ],
      "Resources": [
        "uur:hr-app:time-management:data-entry:581616507495:people/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

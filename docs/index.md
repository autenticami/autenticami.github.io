# Autenticami

`Autenticami` is a multi-account `Identity and Access Management` (IAM or IdAM) solution to enable a modern identity-based application access control for third party applications.

All you have to do is describe your application's resources and create your own access control policies. Resources are organized into hierarchies of Applications, Domains and Features.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions:

- `Who`: *Identities (Users and Roles) that can authenticate*
- `Can Access`: *Permissions granted by policies to affect resources using actions*
- `Resources`: *Resources described into the account*

Below is a sample policy document for granting access to the Employee and Timesheet resources of the HR application (hr-app):

```json linenums="1"
{
  "Version": "2022-07-21",
  "DisplayName": "PeopleBaseReader",
  "Description": "This policy enable List and Read access to employee and timesheet of the domain people.",
  "Type": "ACL",
  "Allow": [
    {
      "DisplayName": "allow-hr/people/person/reader/any",
      "Actions": [
        "people:ListEmployee",
        "people:ReadEmployee"
      ],
      "Resources": [
        "arn:hr-app:organisation:explore:581616507495:person/*"
      ]
    },
    {
      "DisplayName": "allow-hr/people/timesheet/writer/any",
      "Actions": [
        "people:ReadTimesheet",
        "people:CreateTimesheet",
        "people:UpdateTimesheet",
        "people:DeleteTimesheet"
      ],
      "Resources": [
        "arn:hr-app:time-management:data-entry:581616507495:person/*"
      ]
    }
  ],
  "Deny": [
    {
      "DisplayName": "deny-write-hr/people/timesheet/writer/bc182146-1598-4fde-99aa-b2d4d08bc1e2",
      "Actions": [
        "people:Read"
      ],
      "Resources": [
        "arn:hr-app:time-management:data-entry:581616507495:person/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

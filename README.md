# Autenticami

`Autenticami` is a multi-account `Identity and Access Managment` (IAM or IdAM) solution to enable a modern identity-based application access control for third party applications.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions.

- `Who`: *Identities (Users and Roles) that can authenticate*
- `Can Access`: *Permissions with policies to ensure appropriate access to resources for identities*
- `Resources`: *Resources linked to the account*

Below a sample policy document to grant access to the resources Employee and Timesheet of the HR Application (hr):

```json linenums="1"
{
  "Version": "2022-07-21",
  "DisplayName": "PeopleBaseReader",
  "Description": "This policy enable List and Read access to employee and timesheet of the domain people.",
  "Type": "ACL",
  "Allow": [
    {
      "DisplayName": "allow-hr/people/user/reader/any",
      "Actions": [
        "people:employee:List",
        "people:employee:Read"
      ],
      "Resources": [
        "arn:hr:people::581616507495:user/*"
      ]
    },
    {
      "DisplayName": "allow-hr/people/timesheet/writer/any",
      "Actions": [
        "people:timesheet:Read",
        "people:timesheet:Create",
        "people:timesheet:Update",
        "people:timesheet:Delete"
      ],
      "Resources": [
        "arn:hr:people::581616507495:user/*"
      ]
    }
  ],
  "Deny": [
    {
      "DisplayName": "write-hr/people/timesheet/writer/bc182146-1598-4fde-99aa-b2d4d08bc1e2",
      "Actions": [
        "people:timesheet:Read",
      ],
      "Resources": [
        "arn:hr:people::581616507495:user/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

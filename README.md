# Autenticami

`Autenticami` is a multi-account `Identity and Access Managment` (IAM or IdAM) solution to enable a modern identity-based application access control for third party applications.

Autenticami is inspired by AWS Identity and Access Managment (IAM) therefore policies are implemented using an AWS-like definition language.

`Autenticami` allows to specify who or what can access resources by the means of fine-grained permissions.

- `Who`: *Identities (Users and Roles) that can authenticate*
- `Can Access`: *Permissions with policies to ensure appropriate access to resources for identities*
- `Resources`: *Resources linked to the account*

Below a sample policy document to grant access to the resources Employee and Timesheet of the HR Application (HR-App):

```json
{
  "Version": "2022-07-21",
  "Statement": [
    {
      "Sid": "hr-app/employee/reader",
      "Effect": "Allow",
      "Action": [
        "employee:List"
        "employee:Read"
      ],
      "Resource": "arn:hr-app:people:employee::581616507495:user/*"
    },
    {
      "Sid": "hr-app/employee/reader",
      "Effect": "Allow",
      "Action": [
        "timesheet:Read"
        "timesheet:Create"
        "timesheet:Update"
        "timesheet:Delete"
      ],
      "Resource": "arn:hr-app:people:timesheet::581616507495:user/*"
    }
  ]
}
```

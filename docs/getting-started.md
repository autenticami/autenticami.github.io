# Getting Started

Let's take a third-party HR application as an example. As a developer you need to:

- [Create an account](#create-an-account)
- [Create Apps and Resources](#create-apps-and-resources)
- [Create identities](#create-identities)
- [Create policies and permissions](#create-policies-and-permissions)

## Create an account

The very first step is to create an account.

| ACCOUNT EMAIL    | ACCOUNT NUMBER |
|------------------|----------------|
| john@example.com | 581616507495   |

## Create Apps and Resources

Once the account has been created you can proceed with the creation of applications.

| APPLICATION NAME | CODE   |
|------------------|--------|
| HR Application   | hr-app |

Once done you have to create the resources for each application and for each of them create the actions.

| RESOURCE NAME | CODE             | ACTIONS                      |
|---------------|------------------|------------------------------|
| Employee      | hr-app:employee  | Create, Update, Delete, List |
| Timesheet     | hr-app:timesheet | Create, Update, Delete, List |

## Create identities

Naturally, it is required to create identities to access the application.

| IDENTITY TYPE | ARN                                        |
|---------------|--------------------------------------------|
| USER          | arn:hr-app:iam::470676885481:user/john     |
| ROLE          | arn:hr-app:iam::470676885481:role/manager  |
| ROLE          | arn:hr-app:iam::470676885481:role/employee |

## Create policies and permissions

At this point, all that remains is to create the policies and assign them to the identities as permissions.

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
      "Resource": "arn:hr-app:employee::581616507495:user/*"
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
      "Resource": "arn:hr-app:timesheet::581616507495:user/*"
    }
  ]
}
```

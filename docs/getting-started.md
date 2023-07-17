# Getting Started

Let's take a third-party HR application as an example. As a developer you need to:

- [Create an Account](#create-an-account)
- [Create Applications, Domains and Resources](#create-applications-domains-and-resources)
- [Create Identities](#create-identities)
- [Create Permissions and Policies](#create-permissions-and-policies)
- [Application Integration via SDK](#application-integration-via-sdk)

## Create an Account

The very first step is to create an account.

| ACCOUNT EMAIL    | ACCOUNT NUMBER |
|------------------|----------------|
| john@example.com | 581616507495   |

## Create Applications, Domains and Resources

Once the account has been created you can proceed with the creation of applications.

| APPLICATION NAME | CODE   |
|------------------|--------|
| HR Application   | hr |

Once done you have to create the resources for each application's domain and for each of them create the actions.

|  DOMAIN    | RESOURCE NAME | CODE             | ACTIONS                      |
|------------|---------------|------------------|------------------------------|
|  People    | Employee      | hr:employee  | Create, Update, Delete, List |
|  People    | Timesheet     | hr:timesheet | Create, Update, Delete, List |

## Create Identities

Naturally, it is required to create identities to access the application.

| IDENTITY TYPE | ARN                                        |
|---------------|--------------------------------------------|
| USER          | arn:autenticami:iam-identities::581616507495:user/john     |
| ROLE          | arn:autenticami:iam-identities::581616507495:role/manager  |
| ROLE          | arn:autenticami:iam-identities::581616507495:role/employee |

## Create Permissions and Policies

At this point, all that remains is to create the policies and assign them to the identities as permissions.

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
        "people:ListEmployee",
        "people:ReadEmployee"
      ],
      "Resources": [
        "arn:hr-app:people:explore:581616507495:user/*"
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
        "arn:hr-app:people:data-entry:581616507495:user/*"
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
        "arn:hr-app:people:data-entry:581616507495:user/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

## Application Integration via SDK

Once everything is configured, you can go ahead with the integration into your application. 
This can be done using a Autenticami SDK for your application language.

Below is an example of integration in a python application with fastapi.

```python
@router.get(
    '/employees',
    response_model=list[DTOEmployeeResponse],
    response_description='Get all employees',
    status_code=status.HTTP_200_OK,
    tags=['hr'],
)
async def get_employees(
   
    iam_context: IAMHrContext = Depends(get_current_iam_context)
):
    """
    Retrieve list of the employees
    """
    try:
        iam_profile = iam_context.iam_profile
        if not iam_context.iam_provider.can_list_employees(iam_profile):
            raise IAMUnauthorizedException('User has not been granted permissions to list employees')
        ...
        # Here your code
        ...
        return dto_employees
    except IAMUnauthorizedException as e:
        logger.error(e, exc_info=True, stack_info=True)
        raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail=e.args[0])
    except Exception as e:
        logger.error(e, exc_info=True, stack_info=True)
        raise HTTPException(status_code=status.HTTP_500_INTERNAL_SERVER_ERROR, detail='Internal Server Error')
```

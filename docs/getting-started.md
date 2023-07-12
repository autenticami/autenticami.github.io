# Getting Started

Let's take a third-party HR application as an example. As a developer you need to:

- [Create an Account](#create-an-account)
- [Create Apps and Resources](#create-apps-and-resources)
- [Create Identities](#create-identities)
- [Create Permissions and Policies](#create-permissions-and-policies)
- [Third Party Integration](#third-party-integration)

## Create an Account

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

## Create Identities

Naturally, it is required to create identities to access the application.

| IDENTITY TYPE | ARN                                        |
|---------------|--------------------------------------------|
| USER          | arn:hr-app:iam::581616507495:user/john     |
| ROLE          | arn:hr-app:iam::581616507495:role/manager  |
| ROLE          | arn:hr-app:iam::581616507495:role/employee |

## Create Permissions and Policies

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

## Third Party Integration

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

# Getting Started

Let's take a third-party HR project as an example. As a developer you need to:

- [Create an Account](#create-an-account)
- [Create the Applicative Hierarchy](#create-the-applicative-hierarchy)
- [Create Identities](#create-identities)
- [Create Permissions and Policies](#create-permissions-and-policies)
- [Application Integration via SDK](#project-integration-via-sdk)

## Create an Account

The very first step is to create an account.

| ACCOUNT EMAIL    | ACCOUNT NUMBER |
|------------------|----------------|
| john@example.com | 581616507495   |

## Create the Applicative Hierarchy

Once the account has been created you can proceed with the creation of project and its applicative hierarchy.

| APPLICATION NAME | CODE   |
|------------------|--------|
| HR Application   | hr-app |

At this stage of the development the HR project has two domains:

- **OrganisationManagement**: The corporate organisation management for the employees
- **TimeManagement**: Time managament for the users.

Morever we have a single resource which is `person` that is available on both domains.

### Person actions

Finally for each reasource you need to create actions.

| ACTION                    | ORGANISATION-MANAGEMENT | TIME-MANAGEMENT         |
|---------------------------|-------------------------|-------------------------|
| people:ReadTimesheet      |                         | YES                     |
| people:CreateTimesheet    |                         | YES                     |
| people:UpdateTimesheet    |                         | YES                     |
| people:DeleteTimesheet    |                         | YES                     |
| people:ListEmployee       | YES                     |                         |
| people:ReadEmployee       | YES                     |                         |

## Create Identities

Naturally, it is required to create identities to access the project.

| IDENTITY TYPE | UUR                                                         |
|---------------|-------------------------------------------------------------|
| USER          | uur:581616507495:default:autenticami:iam:user/john    |
| ROLE          | uur:581616507495:default:autenticami:iam:role/manager   |
| ROLE          | uur:581616507495:default:autenticami:iam:role/employee  |

## Create Permissions and Policies

At this point, all that remains is to grant the permissions by creating policies and assigning them to the identities.

```json linenums="1"
{
  "Syntax": "autenticami1",
  "Label": "PeopleBaseReader",
  "Type": "ACL",
  "Permit": [
    {
      "Label": "permit-hr/person/reader/any",
      "Actions": [
        "people:ListEmployee",
        "people:ReadEmployee"
      ],
      "Resources": [
        "uur:581616507495:default:hr-app:organisation:people/*"
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
        "uur:581616507495:default:hr-app:time-management:people/*"
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
        "uur:581616507495:default:hr-app:time-management:people/bc182146-1598-4fde-99aa-b2d4d08bc1e2"
      ]
    }
  ]
}
```

## Application Integration via SDK

Once everything is configured, you can go ahead with the integration into your project.
This can be done using an Autenticami SDK for your project language.

Below is an example of integration in a python project with fastapi.

``` py linenums="1" hl_lines="17 18"
@router.get(
    '/employees',
    response_model=list[DTOEmployeeResponse],
    response_description='Get all employees',
    status_code=status.HTTP_200_OK,
    tags=['hr-app'],
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

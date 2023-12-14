# Getting Started

Let's take an HR project as an example. As a developer you need to:

- [Create an Account](#create-an-account)
- [Create Identities](#create-identities)
- [Configure a Project](#configure-a-project)
- [Create Projects and Domains](#create-projects-and-domains)
- [Create Resources and Actions](#create-resources-and-actions)
- [Create Permissions and Policies](#create-permissions-and-policies)
- [Implement a Policy Enforcement Point via SDK](#implement-a-policy-enforcement-point-via-sdk)

## Create an Account

The very first step is to create an account.

| ACCOUNT EMAIL    | ACCOUNT NUMBER |
|------------------|----------------|
| john@example.com | 581616507495   |

## Create Identities

Naturally, it is required to create identities and associate them with a tenant.

| IDENTITY TYPE | UUR                                                         |
|---------------|-------------------------------------------------------------|
| USER          | uur:581616507495:default:autenticami:iam:user/john    |
| ROLE          | uur:581616507495:default:autenticami:iam:role/manager   |
| ROLE          | uur:581616507495:default:autenticami:iam:role/employee  |

## Configure a Project

### Create Projects and Domains

Once the account has been created you can proceed with the creation of project and its domains.

| PROJECT NAME | CODE   |
|------------------|--------|
| HR Application   | hr-app |

At this stage of the development the HR project has two domains:

- **OrganisationManagement**: The corporate organisation management for the employees
- **TimeManagement**: Time managament for the users.

Morever we have a single resource which is `person` that is available on both domains.

### Create Resources and Actions

Finally for each reasource you need to create actions.

| ACTION                    | ORGANISATION-MANAGEMENT | TIME-MANAGEMENT         |
|---------------------------|-------------------------|-------------------------|
| person:ReadTimesheet      |                         | YES                     |
| person:CreateTimesheet    |                         | YES                     |
| person:UpdateTimesheet    |                         | YES                     |
| person:DeleteTimesheet    |                         | YES                     |
| person:ListEmployee       | YES                     |                         |
| person:ReadEmployee       | YES                     |                         |

### Create Permissions and Policies

At this point, all that remains is to grant the permissions by creating policies and assigning them to the identities.

```json linenums="1"
# Autenticami

<div style="background-color:#111111;text-align:justify;}">
  <img src="assets/images/autenticami-black-logo.png" width="250px" height="auto"/>
</div>


`Autenticami` is a multi-account `Identity and Access Management` (IAM or IdAM) solution to enable a modern identity-based access control.

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
      ],
      "Condition": "DateGreaterThan({{.Autenticami.TokenIssueTime}})' && DateLessThan('{{.Autenticami.CurrentTime}}': '2023-12-31T23:59:59Z')"
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

```

## Implement a Policy Enforcement Point via SDK

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

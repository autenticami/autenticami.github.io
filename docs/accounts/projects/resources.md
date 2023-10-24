# Resources

A resource represents a project's resource.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `UUR` (Universally unique resource) which looks like `uur:581616507495:default:hr-app:time-management:person/*`.

An `UUR` is composed by multiple sections `uur:{account}:{tenant}:{project}:{domain}:{resource}/{resource-filter}`:

- **Account**: an `autenticami` account number
- **Tenant**: an `autenticami` tenant name
- **Project**: name of the project to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Resource**: resource type
- **Resource Filter**: resource filter.

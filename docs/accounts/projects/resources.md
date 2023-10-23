# Resources

A resource represents a resource from a third-party project.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `UUR` (Universally unique resource) which looks like `uur:581616507495:default:hr-app:time-management:people/*`.

An `UUR` is composed by multiple sections `uur:{account}:{tenant}:{project}:{domain}:{resource}/{resource-filter}`:

- **Account**: an `autenticami` account number
- **Tenant**: an `autenticami` tenant number
- **Project**: name of the project to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Resource**: resource type
- **Resource Filter**: resource filter.

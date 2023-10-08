# Resources

A resource represents a resource from a third-party application.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `UUR` (Universally unique resource) which looks like `uur:hr-app:time-management:data-entry:581616507495:people/*`.

An `UUR` is composed by multiple sections `uur:{application}:{domain}:{feature}:{account}:{resource}/{resource-filter}`:

- **Application**: name of the application to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Feature**: applicative feature
- **Account**: an `autenticami` account number
- **Resource**: resource type
- **Resource Filter**: resource filter.

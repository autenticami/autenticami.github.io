# Resources

A resource represents a resource from a third-party application.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `ARN` (Applicative Resource Name) which looks like `arn:hr-app:time-management:data-entry:581616507495:people/*`.

An `ARN` is composed by multiple sections `arn:{application}:{domain}:{feature}:{account}:{resource}/{resource-filter}`:

- **Application**: name of the application to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Feature**: applicative feature
- **Account**: an `autenticami` account number
- **Resource**: resource type
- **Resource Filter**: resource filter.

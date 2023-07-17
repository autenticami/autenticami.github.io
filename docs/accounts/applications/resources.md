# Resources

A resource represents a resource from a third-party application.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `ARN` (Applicative Resource Name) which looks like `arn:hr-app:people:time-management:data-entry:581616507495:person/*`.

An `ARN` is composed by multiple sections `arn:{application}:{domain}:{sub-domain}:{feature}:{account}:{resource}/{resource-id}`:

- **Application**: name of the application to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **SubDomain**: name of the sub-domain to which the resource belongs
- **Feature**: applicative feature
- **Account**: an `autenticami` account number
- **Resource**: resource type
- **ResourceId**: resource identifier

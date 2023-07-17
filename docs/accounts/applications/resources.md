# Resources

A resource represents a resource from a third-party application that are organised into domains.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `ARN` (Applicative Resource Name) which looks like `arn:hr:people::581616507495:user/*`.

An `ARN` is composed by multiple sections (`arn:{application}:{domain}:{epic}:{feature}:{account}}:{resource}/{resourceid}`):

- **Application**: name of the application to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Epic**: applicative epic
- **Feature**: applicative feature
- **Account**: an `autenticami` account number
- **Resource**: resource type
- **ResourceId**: resource identifier

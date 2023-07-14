# Resources

A resource represents a resource from a third-party application that are organised into domains.
For each resource, you can specify a collection of actions and tags.

A resource is uniquely identified with an `ARN` (Applicative Resource Name) which looks like `arn:hr:people::581616507495:user/*`.

An `ARN` is composed by multiple sections (`arn:{application}:{domain}:{device}:{account}}:{resource}`):

- **Application**: name of the application to which the resource belongs
- **Domain**: name of the domain to which the resource belongs
- **Device**: type of device the principal used to connect
- **Account**: an `autenticami` account number
- **Resource**: name of the resource

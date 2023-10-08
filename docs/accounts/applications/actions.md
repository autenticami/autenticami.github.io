# Actions

Actions are operations that can affect more than one resource in the context of one or more features.

Actions must be uniquely identified and they look like `organisation/people:CreateTimesheet`.

An `Action` is composed by two sections `{domain}/{resource}:{action-name}`:

- **Domain**: Resource in which the action can be used
- **Resource**: Resource in which the action can be used
- **ActionName**: Name of the action.

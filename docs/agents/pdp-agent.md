# PDP Agent

A `PDP` is responsible to expose the endpoints to check permissions.

This agent can be run in two modes:

- **LOCAL**: This mode is used in contexts where you need to run a PDP node in close proximity with low latency, one use case is that of a sidecar.
- **REMOTE**: This mode is useful in contexts where you don't need to run the node in proximity.

Here list of the environment variables that can be used to configure any of the pdp agent:

| ENV VARIABLE              | VALUES    | DEFAULT | DESCRIPTION               |
|---------------------------|-----------|---------|---------------------------|
| AUTENTICAMI-AGENT-APPDATA |           | .       | Application data folder   |
| AUTENTICAMI-AGENT-PORT    |           | 9090    | Application data folder   |

## Local configuration

Below is the list of environment variables that can be used to configure a local pdp agent:

| ENV VARIABLE              | VALUES    | DEFAULT | DESCRIPTION               |
|---------------------------|-----------|---------|---------------------------|
| AUTENTICAMI-AGENT-TYPE    | PDP-LOCAL |         | PDP Agent running locally |

## Remote configuration

Below is the list of environment variables that can be used to configure a remote pdp agent:

| ENV VARIABLE              | VALUES     | DEFAULT | DESCRIPTION                |
|---------------------------|------------|---------|----------------------------|
| AUTENTICAMI-AGENT-TYPE    | PDP-REMOTE |         | PDP Agent running remotely |

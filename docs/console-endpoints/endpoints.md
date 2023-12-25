# Endpoints

## Account Management

`Autenticami` implements a console for web access moreover it exposes api for the `Account Management`.

| Name                   |  Type | Endpoint                                                                                                                                      |
|----------------------- |-------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `Management Console`   |  WEB  | [https://console.autenticami.com](https://console.autenticami.com)                                                                            |
| `Management Api`       |  API  | [https://accounts.autenticami.com/v1/management](https://accounts.autenticami.com/v1/management)                                              |

## Identity and Access Management

Autenticami exposes api for `Identity and Access Management`.

### Identities

| Name                   |  Type | Endpoint                                                                                                                                      |
|----------------------- |-------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `OAuth Authorization`  |  API  | [https://accounts.autenticami.com/v1/authorize](https://accounts.autenticami.com/v1/authorize)                                                |
| `Device Authorization` |  API  | [https://accounts.autenticami.com/v1/oauth/device/code](https://accounts.autenticami.com/v1/oauth/device/code)                                |
| `OAuth Token`          |  API  | [https://accounts.autenticami.com/v1/oauth/token](https://accounts.autenticami.com/v1/oauth/token)                                            |
| `OAuth User Info`      |  API  | [https://accounts.autenticami.com/v1/userinfo](https://accounts.autenticami.com/v1/userinfo)                                                  |
| `OpenID Configuration` |  API  | [https://accounts.autenticami.com/v1/.well-known/openid-configuration](https://accounts.autenticami.com/v1/.well-known/openid-configuration)  |
| `JSON Web Key Set`     |  API  | [https://accounts.autenticami.com/v1/.well-known/jwks.json](https://accounts.autenticami.com/v1/.well-known/jwks.json)                        |

### Access Management

| Name                   |  Type | Endpoint                                                                                                                                      |
|----------------------- |-------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `Accessible Apps`      |  API  | [https://accounts.autenticami.com/v1/ac/apps](https://accounts.autenticami.com/v1/ac/apps)                                                  |
| `Permissions`          |  API  | [https://accounts.autenticami.com/v1/ac/permissions](https://accounts.autenticami.com/v1/ac/permissions)                                    |
| `Action Evaluation`    |  API  | [https://accounts.autenticami.com/v1/ac/action](https://accounts.autenticami.com/v1/ac/action)                                              |

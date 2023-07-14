# Endpoints

`Autenticami` can be managed using a web portal or directly via api.

| Name                   |  Type | Endpoint                                                                                                                                      |
|----------------------- |-------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `Management Console`   |  WEB  | [https://console.autenticami.com](https://console.autenticami.com)                                                                            |
| `Management Api`       |  API  | [https://accounts.autenticami.com/v1/management](https://accounts.autenticami.com/v1/management)                                              |

## Auth and Authorization

Autenticami exposes api for Authentication and Authorization.

| Name                   |  Type | Endpoint                                                                                                                                      |
|----------------------- |-------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `OAuth Authorization`  |  API  | [https://accounts.autenticami.com/v1/authorize](https://accounts.autenticami.com/v1/authorize)                                                |
| `Device Authorization` |  API  | [https://accounts.autenticami.com/v1/oauth/device/code](https://accounts.autenticami.com/v1/oauth/device/code)                                |
| `OAuth Token`          |  API  | [https://accounts.autenticami.com/v1/oauth/token](https://accounts.autenticami.com/v1/oauth/token)                                            |
| `OAuth User Info`      |  API  | [https://accounts.autenticami.com/v1/userinfo](https://accounts.autenticami.com/v1/userinfo)                                                  |
| `OpenID Configuration` |  API  | [https://accounts.autenticami.com/v1/.well-known/openid-configuration](https://accounts.autenticami.com/v1/.well-known/openid-configuration)  |
| `JSON Web Key Set`     |  API  | [https://accounts.autenticami.com/v1/.well-known/jwks.json](https://accounts.autenticami.com/v1/.well-known/jwks.json)                        |
| `Accessible Resources` |  API  | [https://accounts.autenticami.com/v1/acl/resources](https://accounts.autenticami.com/v1/acl/resources)                                        |
| `Permissions`          |  API  | [https://accounts.autenticami.com/v1/acl/permissions](https://accounts.autenticami.com/v1/acl/permissions)                                    |
| `Action Evaluation`    |  API  | [https://accounts.autenticami.com/v1/acl/action](https://accounts.autenticami.com/v1/acl/action)                                             |

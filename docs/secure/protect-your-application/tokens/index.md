# Token

`Token based authentication` is a protocol which allows users to verify their identity and in return receive an unique access token.

Autenticami uses `Json Web Tokens (JWTs)` and `Opaque tokens`, the main difference between JWTs and opaque tokens is that an unencrypted JWT can be interpreted by anybody that holds the token, whereas opaque tokens cannot.

Tokens are returned by the token endpoint moreover they should be transmitted to the target endpoint via header or body only.

!!! tip "Token types"

    Tokens are wrapped into an envelope which contains three types of tokens:
    
    - access_token: This token must be used to access private resources
    - id_token: This token represents the Open ID token
    - refresh_token: This token is used to refresh the access token

    ```json
    {
        "access_token": "eyJhbGciOi...L1LAA16KwijpaHg",
        "id_token":     "eyJhbGciOi...l91loffOVwyhXDQ",
        "scope": "openid profile email address phone",
        "expires_in": 86400,
        "token_type": "Bearer"
    }
    ```

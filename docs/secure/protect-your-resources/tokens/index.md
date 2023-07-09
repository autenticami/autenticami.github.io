[JWS]: https://www.rfc-editor.org/rfc/rfc7519.html#ref-JWS
[JWE]: https://www.rfc-editor.org/rfc/rfc7519.html#ref-JWE

# Token Based Authentication

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

## Json Web Tokens (JWTs)

`JSON Web Token (JWT)` is a compact, URL-safe means of representing claims to be transferred between two parties.  The claims in a JWT are encoded as a JSON object that is used as the payload of a `JSON Web Signature (JWS)` structure or as the plaintext of a `JSON Web Encryption (JWE)` structure, enabling the claims to be digitally signed or integrity protected with a `Message Authentication Code (MAC)` and/or encrypted.

!!! Documentation abstract "RFC 7519: JSON Web Token (JWT)"

    The [RFC number 7519](https://www.rfc-editor.org/rfc/rfc7519.html) describes in detail the JSON Web Token.

### Creation

To create a JWT, the following steps are performed. The order of the steps is not significant in cases where there are no dependencies between the inputs and outputs of the steps.

1. Create a JWT Claims Set containing the desired claims. Note that whitespace is explicitly allowed in the representation and no canonicalization need be performed before encoding.
2. Let the Message be the octets of the UTF-8 representation of the JWT Claims Set.
3. Create a JOSE Header containing the desired set of Header Parameters. The JWT MUST conform to either the [JWS] or [JWE] specification. Note that whitespace is explicitly allowed in the representation and no canonicalization need be performed before encoding.
4. Depending upon whether the JWT is a JWS or JWE, there are two cases:
    - If the JWT is a JWS, create a JWS using the Message as the JWS Payload; all steps specified in [JWS] for creating a JWS MUST be followed.
    - Else, if the JWT is a JWE, create a JWE using the Message as the plaintext for the JWE; all steps specified in [JWE] for creating a JWE MUST be followed.
5. If a nested signing or encryption operation will be performed, let the Message be the JWS or JWE, and return to Step 3, using a "cty" (content type) value of "JWT" in the new JOSE Header created in that step.
6. Otherwise, let the resulting JWT be the JWS or JWE.

### Claims

JWTs claims are piece of information asserted about a subject.
Configuration with custom claimns should avoid name collisions.


#### Restricted Claims

You can see a full list of registered claims at the [IANA JSON Web Token Claims Registry](https://www.iana.org/assignments/jwt/jwt.xhtml#claims).

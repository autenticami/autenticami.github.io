[JWS]: https://www.rfc-editor.org/rfc/rfc7519.html#ref-JWS
[JWE]: https://www.rfc-editor.org/rfc/rfc7519.html#ref-JWE
[RFC7159]: https://www.rfc-editor.org/rfc/rfc7159

# JWT Validation

When validating a JWT, the following steps are performed.  The order of the steps is not significant in cases where there are no dependencies between the inputs and outputs of the steps.  If any of the listed steps fail, then the JWT MUST be rejected -- that is, treated by the application as an invalid input.

1. Verify that the JWT contains at least one period ('.') character.
2. Let the Encoded JOSE Header be the portion of the JWT before the first period ('.') character.
3. Base64url decode the Encoded JOSE Header following the restriction that no line breaks, whitespace, or other additional characters have been used.
4. Verify that the resulting octet sequence is a UTF-8-encoded representation of a completely valid JSON object conforming to [RFC7159]; let the JOSE Header be this JSON object.
5. Verify that the resulting JOSE Header includes only parameters and values whose syntax and semantics are both understood and supported or that are specified as being ignored when not understood.
6. Determine whether the JWT is a JWS or a JWE using any of the methods described in Section 9 of [JWE].
7. Depending upon whether the JWT is a JWS or JWE, there are two cases:
      - If the JWT is a JWS, follow the steps specified in [JWS] for validating a JWS.  Let the Message be the result of base64url decoding the JWS Payload.
      - Else, if the JWT is a JWE, follow the steps specified in [JWE] for validating a JWE.  Let the Message be the resulting plaintext.
8. If the JOSE Header contains a "cty" (content type) value of "JWT", then the Message is a JWT that was the subject of nested signing or encryption operations.  In this case, return to Step 1, using the Message as the JWT.
9. Otherwise, base64url decode the Message following the restriction that no line breaks, whitespace, or other additional characters have been used.
10. Verify that the resulting octet sequence is a UTF-8-encoded representation of a completely valid JSON object conforming to [RFC7159]; let the JWT Claims Set be this JSON object. Finally, note that it is an application decision which algorithms may be used in a given context.  Even if a JWT can be successfully validated, unless the algorithms used in the JWT are acceptable to the application, it SHOULD reject the JWT.

!!! tip "Client Validation"

      Below additional required client validation checks:

      1. Verify there are three valid sections
      2. Verify sections are encoded using base64url
      3. Make sure the header is a valid json object
      4. Make sure the payload is a valid json object
      5. Validate header
            - Must only contain well-known values
            - Token is signed using a well-known key
            - Check the signing key belong to the issuer
            - Signing key is intended to be used with the defined algorithm
      6. Validate payload
            - Must only contain well-known values
            - Token is issued by the well-known identity provider
            - Application is the intendend recipient of the token
            - Token is not expired
            - Required claims are well configured
            - Custom required claims are well configured

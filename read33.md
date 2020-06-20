[ HOME ](README.md)
# Read 33 - Authentication & Production Server

# JSON Web Tokens (JWT)

- JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. 
- This information can be verified and trusted because it is digitally signed. 
- JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.
-  Signed tokens can verify the integrity of the claims contained within it.
- Encrypted tokens hide claims from other parties. When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.


### What is the JSON Web Token structure?
- In its compact form, JSON Web Tokens consist of three parts separated by dots (.)
1. Header
    1. type
    1. algorithm
1. Payload (claims)
    1. registered
    1. public
    1. private claims
1. Signature

#### Header
The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

#### Payload
The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

**Public claims**: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

**Private claims**: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

#### Signature
To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

## How do JSON Web Tokens work?
- In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned.
- In general, you should not keep tokens longer than required.
- **You should not store sensitive session data in browser storage due to lack of security.**
- Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema.

```
Authorization: Bearer <token>
```

#### How a JWT is obtained and used to access APIs or resources 
![How a JWT is obtained and used to access APIs or resources](https://cdn2.auth0.com/docs/media/articles/api-auth/client-credentials-grant.png)

# Source
[Source](https://jwt.io/introduction/)
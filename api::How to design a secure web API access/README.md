## [How to design a secure web API access for you website?](https://twitter.com/alexxubyte/status/1514256018187816965)

> When we open web API access to users, we need to make sure each API call is authenticated. This means the user must be who they claim to be.
> 
> There are two common ways:
> 1. Token based authentication
> 2. HMAC (Hash-based Message Authentication Code) authentication
> 
> The diagram below illustrates how they work.

![secure-api](secure_api.jpeg)

### Token based
1. Step 1 - the user enters their password into the client, and the client sends the password to the Authentication Server.
2. Step 2 - the Authentication Server authenticates the credentials and generates a token with an expiry time.
3. Steps 3 and 4 - now the client can send requests to access server resources with the token in the HTTP header. This access is valid until the token expires.

### HMAC based
> This mechanism generates a Message Authentication Code (signature) by using a hash function (SHA256 or MD5).

1. Steps 1 and 2 - the server generates two keys, one is Public APP ID (public key) and the other one is API Key (private key).
2. Step 3 - we now generate a HMAC signature on the client side (hmac A). This signature is generated with a set of attributes listed in the diagram.
3. Step 4 - the client sends requests to access server resources with hmac A in the HTTP header.
4. Step 5 - the server receives the request which contains the request data and the authentication header. It extracts the necessary attributes from the request and uses the API key that’s stored on the server side to generate a signature (hmac B.)
5. Steps 6 and 7 - the server compares hmac A (generated on the client side) and hmac B (generated on the server side). If they are matched, the requested resource will be returned to the client.
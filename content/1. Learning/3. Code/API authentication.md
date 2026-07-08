## 1. Introduction
- The token-based authentication systems allow users to enter their user name and password in order to obtain an access token which allows them to retrieve the resources from the server without having to re-enter the credential information again.
___

## 2. Compare authenticate method
### 2.1. HTTP basic
- In the traditional ways of authentication, we will use session and cookies:
	- The session will be stored on the server side reference to the user’s profile.
	- The cookies stored on the client side contains the access token that can be used to compare with the session ID.
![[Pasted image 20260708151541.png]]

- HTTP Basic authentication flow:
	- User provides username/password as a HTTP Request to the server.
	- Server validate username/password provided with the database. If it is incorrect, server will deny access.
	- If user’s information is correct, the server will create an unique access token to identifies the user's session and attached it to the response.
	- When user make another request, the browser will attached the cookies.The server will then check the data and grant access.

*Note: For small applications this is a viable option, but it contains multiple disadvantages that doesn’t work well with larger applications and require some complicated workaround to solve.*

- Advantage:
	- Easy to implement.
- Disadvantage:
	- Server have to manage the user’s session.
	- Slow performance: sessions require a server side lookup to find and deserialize the session on each request.
	- Scalability: session and cookies can’t be used on multiple backend servers.
	- Difficult to use with non-browser based applications. (Ex: mobile app)
___

### 2.2. JSON web token
- Json Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.
- The JSON object used as a payload for Json Web Signature (JWS - RFC7515) or as a plain text of a Json Web Encryption (JWE - RFC 7516),prevent any tampering from the client side.
![[Pasted image 20260708152433.png]]

![[Pasted image 20260708152504.png]]

- In its compact form, JSON Web Tokens consist of three parts separated by dots “.”, which are:
1. HEADER
2. PAYLOAD
3. SIGNATURE

ex: 
![[Pasted image 20260708152624.png]]

- HEADER: Header consist of two parts:
	- The algorithm.
	- Token type
![[Pasted image 20260708152851.png]]

- PAYLOAD: Contains the claims about the user. (RFC 7519)
	- Registered Claims.
	- Public Claims.
	- Private Claims.
![[Pasted image 20260708153041.png]]

- SIGNATURE: Use to verify the JWT wasn’t tampered with along the way.
- To create this signature, we need the **header**, the **payload**, a **secret key** and running them through the encryption algorithm. For example using HMACSHA256 the signature will be: (jwt.io)
![[Pasted image 20260708153333.png]]
___

- Advantage of a JWT:
	- Scalability: token-based application don’t need to store user session.User can use it to access multiple servers without worrying about logging in.
	- Portability: Can be use with non-browser based applications.
	- Security: using an encrypted digital signature helps prevent any tampering from the client-side.
	- Faster performance: each JWT is a compact and self-contained token including credential, expire time, and any other user defined claims.
___

- Disadvantage of a JWT:
	- JWT is several times the size of session ID due to being a self-contained token with build-in expire time and other user defined claims. Essentially,JWT trade size for latency by keeping data on client side.
	- Can be exposed to CSRF (Cross-site request forgery) or XSS (Cross-siteScripting). JWT should not store any sensitive data.
___

## 3. Oauth

- OAuth, which stand for OpenAuthorization, is an open-standard authorization protocol (RFC 5849, RFC6749) allows user to safely authenticate into third party services without sharing user credential.
![[Pasted image 20260708154007.png]]
___

### 3.1 OAuth 1.0
- OAuth 1.0 Terms:
	- User: a person who want to get access to the protected resources.
	- Consumer: the application uses OAuth to access the Service Provider for the User. 
	- Service Provider: the web application that allows access via OAuth
	- Protected Resources: the data that the user want to access.
- Token:
	- Request Token: used for asking the service for authorization.
	- Access Token: used for accessing protected resources.
![[Pasted image 20260708154159.png]]
___

### 3.2 OAuth 2.0
- OAuth 2.0 is built on OAuth 1.0 deployment experience.
- However, OAuth 2.0 protocol is not backwards compatible with OAuth 1.0.There’re very little similarities between their implementations
- OAuth 2.0 Terms:
	- Resource Owner: An entity capable of granting access to a protected resource.
	- Resource Server: The server hosting the protected resources.
	- Client: An application making protected resource requests on behalf of the resource owner.
	- Authorization Server: The server issuing access tokens to the client.
![[Pasted image 20260708154354.png]]
___

## 3.2 OAuth 2.0 (optional refresh token)
![[Pasted image 20260708154413.png]]



## References
- JSON Web Token: https://tools.ietf.org/html/rfc7519
- JSON Web Signature: https://tools.ietf.org/html/rfc7515
- JSON Web Encryption: https://tools.ietf.org/html/rfc7516
- OAuth 1: https://tools.ietf.org/html/rfc5849
- OAuth 2: https://tools.ietf.org/html/rfc6749

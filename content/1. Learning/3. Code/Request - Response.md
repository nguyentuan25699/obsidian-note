## 1. Request/Response Structure
-   HTTP Method
- Resource names and request URL
- Request structure
- Response structure
___

## 1.1. HTTP Method
- HTTP method is a critical component of a request to REST API service as it determines the type of action being requested.

| HTTP Method | Description                                                |
| ----------- | ---------------------------------------------------------- |
| GET         | Retrieves information about the referenced object.         |
| POST        | Creates a new object.                                      |
| PUT/PATCH   | Updates the properties associated with an existing object. |
| DELETE      | Deletes the referenced object                              |
*Note: Our REST API service may return a 405 Method Not Allowed response for requests submitted with an unsupported HTTP method.*
___

## 1.2. Resource names and request URL
- The APIs act the same object type should be used the same Resource Names.
- Example:-
	- A resource name might be “objects”
	- The path to access that resource might be “/api/objects”
	- Request URL should be:

| HTTP method | Request URL                       | Description                                                 |
| ----------- | --------------------------------- | ----------------------------------------------------------- |
| GET         | /api/objects or /api/objects/{id} | retrieve a list of objects or retrieve a single object byID |
| POST        | /api/objects                      | Add a new object                                            |
| PUT/PATCH   | /api/objects/{id}                 | Update a single object by ID                                |
| DELETE      | /api/objects/{id}                 | Delete an object by ID                                      |
___

## 1.3. Request structure
-  Structure:
```xml
// Request-line
<method><request-URL><http-version>
//(optional)
<header>
// one empty line, mark as end of header

//optional
<body>
```

- **Request-line**
	- method: HTTP method of request
	- request-URL: if request doesn’t request any resource, URL is *
	- http-version
- **Request-header**: provide information about your request to a REST APIservice. This information allows our server to authenticate your request and provides information that allows it to receive and translate the request body.
- Request header values are **case-insensitive**.
___

- Some common fields in request-header:

| Accept              | The format of the response. Ex: application/xml, application/json, text/plain,...       |
| ------------------- | --------------------------------------------------------------------------------------- |
| **Accept-encoding** | Encoding types are accepted. Ex: gzip, xz, br,...                                       |
| **Authorization**   | Token or authorization type of request                                                  |
| **Content-Type**    | The format of the request body. Ex: application/json, application/x-www-form-urlencoded |
| **Cookie**          | HTTP Cookie information on server                                                       |
| **Content-Length**  | The number of bytes is contained in the request body.                                   |
| **Host**            | The host name corresponding to the requested endpoint.                                  |
___

- Request body:
	- PUT and POST requests typically require request body parameters that contains data you send to server. These request body parameters are case-sensitive.
	- Type: an XML element or a JSON message

Example:

```xml
POST <webservice>/Login HTTP/1.1
Host: <host name>
Accept: {application/xml | application/json}
Content-type: application/json

{
	"domain": "",
	"username": "",
	"password": "",
	"commserver": ""
}
```
___

## 1.4. Response structure
- Structure:
```xml
// Status-line
<http-version><status><reason-phrase>
//optional<header>
// one empty line, mark as end of header

//optional
<body>
```

- Status-line:
	- HTTP-version
	- Status-code: HTTP response status code
	- Reason-phrase: status-code description
- Response Headers: provide information about the response to your request to the REST API service, are returned by most endpoints
- Response body: contains data returned by the server.
___

- Some common fields in response-header:

| Cache-Controller   | The cache-control policy for the response body.                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Content-Length** | The number of bytes in the response body.                                                                   |
| **Content-Type**   | The format of the response body. JSON: application/json; charset=utf-8 or XML: application/xml              |
| **Set-Cookie**     | A cookie is sent from the server to the user agent, so the user agent can send it back to the server later. |
| **Date**           | The date and time (UTC) at which your request was processed.                                                |
- Example:
```js
HTTP/1.1 200 OK
Content-Type: application/json

{
	"status":"In progress",
	"link": { 
		"rel":"cancel", 
		"method":"delete",
		"href":"/api/status/12345" 
	}
}
```
___

## 2. Content types
- The Content-Type entity header is used to indicate the media type (MIME type) of the resource.
- In the request, Content-Type specifies the format of the data in the request body so that receiver can parse it into appropriate format.
- In the response, Content-Type specifies the format of the data in the response body.
- MIME type is also used in the Accept header attribute of the request.
- The Accept header attribute can have multiple values.
- In a POST request, resulting from an HTML form submission, theContent-Type of the request is specified by the enctype attribute on the \<form> element.
- Example:
![[Pasted image 20260708133533.png]]

- Request:
```xml
POST /foo HTTP/1.1
Content-Length: 68137
Content-Type: multipart/form-data; boundary=something
```

Some HTML form encoding:
- application/x-www-form-urlencoded
- multipart/form-data
- text/plain

### application/x-www-form-urlencoded
- Represents a URL encoded form. This is the default value if enctype attributeis not set to anything.
![[Pasted image 20260708133942.png]]
- A long string of (name, value) pairs are created. Each (name, value) pair is separated from one another by a & (ampersand) sign, and for each (name, value) pair, the name is separated from the value by an = (equals).

### multipart/form-data
- Multipart forms are generally used in contexts where the user needs files tobe uploaded to the server.
![[Pasted image 20260708134128.png]]

- The boundary value allows the server to understand when and where aparameter value starts and ends.

### text/plain
- Simply sends the data without any encoding.
- Is the default value for textual files. A textual file should be human-readable and must not contain binary data.

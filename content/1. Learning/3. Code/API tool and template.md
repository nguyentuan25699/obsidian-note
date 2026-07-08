## 1. API Design Template
- There are a number of ways to get started with documenting your APIs. It just really depends on which method of API design you've settled on.
- The most traditional method of documenting APIs is to use a regular content creation tools.
- Many projects in Sun Asterisk use the company “API Design” Template.
-   The title of the file should include project ID & project name. (Ex: \[123] ABCSystem - API Design)
- The document should includes:
	- **History of changes**: logs of changes done to the API Design file.
	- **Common Conventions**: list of common conventions to follow when design APIs for the project.
	- **Status code**: list of all available status code use in this project.
	- **API List**: list of all APIs in the system.
	- **API Detail**: each API listed in API List will have a sheet to describe that API detail.
	- **Appendix**: other information such as actions, members, input types & parameter types.
___

## 2. API Documentation Template

![[Pasted image 20260708163338.png]]
___

## 3. Tools
- Another method to document API is to simply use a tool.
- 2 tools are introduced in this lecture:
	- Postman
	- Swagger
___

### 3.1. Postman
- Postman is an API platform for building and using APIs.
- Postman allows you to:
	- Publish documentation quickly and easily.
	- Automatically Update your Documentation
	- Share Easily with the Run in Postman Button
	- Gain Adoption of your API
	- Collaborate with Your Team on Docs
![[Pasted image 20260708163654.png|667]]

#### Send Request:
1. Click on button \[+].
2. Select HTTP method.
3. Input API URL.
4. Fill request variables.
5. Click “Send”

#### View Response:
1. Check status code.
2. View response body.
___

- Document: https://learning.postman.com/docs/getting-started/introduction/
- Installing and updating: https://learning.postman.com/docs/getting-started/installation-and-updates/
- After installing, you can:
	- Making requests
	- Testing APIs
	- Building and managing APIs
	- Publishing APIs
	- Collaborating with your team
	- Developing with Postman
___

### 3.2. Swagger
Swagger is a set of open-source tools built around the OpenAPI Specification that can help you design, build, document and consume RESTful APIs. The majorSwagger tools include:
- **Swagger Editor** – browser-based editor where you can write OpenAPI specs.
- **Swagger UI** – renders OpenAPI specs as interactive API documentation.
- **Swagger Codegen** – generates server stubs and client libraries from anOpenAPI spec.
___ 

OpenAPI Specification (formerly Swagger Specification) is an API description format for RESTful APIs. An OpenAPI file allows you to describe your entire API, including:
- Available endpoints (/users) and operations on each endpoint (GET /users,POST /users)
- Operation parameters Input and output for each operation
- Authentication methods
- Contact information, license, terms of use and other information.

![[Pasted image 20260708165652.png]]

![[Pasted image 20260708165703.png]]


- Swagger Introduction: https://swagger.io/
- Swagger Docs: https://swagger.io/docs/specification/about/
- API documentation: https://swagger.io/resources/articles/documenting-apis-with-swagger/
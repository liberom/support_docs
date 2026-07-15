### Setting up Swagger Editor Repository

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Commands to clone the Swagger Editor repository, checkout the 'next' branch, initialize and update submodules, install dependencies, and start the development server.

```bash
git clone https://github.com/swagger-api/swagger-editor.git
cd swagger-editor
git checkout next
git submodule init
git submodule update
npm i
npm start
```

--------------------------------

### Parameter Examples

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates how to specify a single example value for an API parameter.

```APIDOC
## GET /api/resource

### Description
This endpoint retrieves resources with an optional status filter.

### Method
GET

### Endpoint
/api/resource

### Parameters
#### Query Parameters
- **status** (string) - Optional - Filters resources by their status. Allowed values: approved, pending, closed, new.

### Request Example
```
GET /api/resource?status=approved
```

### Response
#### Success Response (200)
- **data** (array) - A list of resources.
- **status** (string) - The status of the resource.

#### Response Example
```json
{
  "data": [
    {
      "id": 1,
      "name": "Example Resource",
      "status": "approved"
    }
  ]
}
```
```

--------------------------------

### Response Body Multiple Examples (Media Type Child with $ref)

Source: https://swagger.io/docs/specification/adding-examples

Shows how to provide multiple examples for a response body when using a $ref for the schema. The 'examples' keyword is used under the media type, with each example having a 'value' property.

```yaml
responses:
  "200":
    description: A user object.
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User" # Reference to an object
        examples:
          Jessica:
            value:
              id: 10
              name: Jessica Smith
          Ron:
            value:
              id: 20
              name: Ron Stewart
```

--------------------------------

### Multiple Parameter Examples

Source: https://swagger.io/docs/specification/adding-examples

Illustrates how to provide multiple named examples for a single API parameter, including optional summaries.

```APIDOC
## GET /api/items

### Description
This endpoint retrieves a list of items, with an optional limit parameter.

### Method
GET

### Endpoint
/api/items

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return. Maximum value: 50.

### Request Example
```
GET /api/items?limit=50
```

### Response
#### Success Response (200)
- **items** (array) - A list of items.
- **count** (integer) - The number of items returned.

#### Response Example
```json
{
  "items": [
    {
      "id": 1,
      "name": "Item 1"
    },
    {
      "id": 2,
      "name": "Item 2"
    }
  ],
  "count": 2
}
```
```

--------------------------------

### Array Examples

Source: https://swagger.io/docs/specification/adding-examples

Illustrates how to provide examples for arrays, including arrays of integers and arrays of objects.

```APIDOC
## Components Schemas - Array Examples

### Description
This section shows how to define examples for array types in OpenAPI specifications.

### Components
#### Schemas
##### ArrayOfInt (Array of Integers)
- **type**: array
- **items**:
  - **type**: integer
  - **format**: int64
  - **example**: 1

### Array-level Example (Integers)
```json
[1, 2, 3]
```

##### ArrayOfUsers (Array of Objects)
- **type**: array
- **items**:
  - **type**: object
  - **properties**:
    - **id** (integer)
    - **name** (string)

### Array-level Example (Objects)
```json
[
  {
    "id": 10,
    "name": "Jessica Smith"
  },
  {
    "id": 20,
    "name": "Ron Stewart"
  }
]
```
```

--------------------------------

### POST /users - Add New User

Source: https://swagger.io/docs/specification/adding-examples

This endpoint allows for the addition of a new user. It demonstrates how to define request body examples, including single examples and multiple examples using the 'examples' keyword.

```APIDOC
## POST /users

### Description
Adds a new user to the system.

### Method
POST

### Endpoint
/users

### Parameters
#### Request Body
- **id** (integer) - Required - The unique identifier for the user.
- **name** (string) - Required - The name of the user.

### Request Example
```json
{
  "id": 10,
  "name": "Jessica Smith"
}
```

### Response
#### Success Response (200)
- **description** (string) - Indicates that the request was successful.

#### Response Example
```json
{
  "message": "User added successfully"
}
```
```

--------------------------------

### Response Body Example (Media Type Child with $ref)

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates using the 'example' keyword for a response body when the schema is a reference ($ref). The example is placed under the media type.

```yaml
responses:
  "200":
    description: A user object.
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User" # Reference to an object
        example:
          # Properties of the referenced object
          id: 10
          name: Jessica Smith
```

--------------------------------

### Add Multiple Examples to OpenAPI Parameter (YAML)

Source: https://swagger.io/docs/specification/adding-examples

This snippet shows how to specify multiple examples for a single OpenAPI parameter using the `examples` key. Each example is given a distinct key name and can optionally include a `summary` for a brief description. This feature, supported in Swagger UI 3.23.0+ and Swagger Editor 3.6.31+, allows for richer parameter illustration.

```yaml
parameters:
  - in: query
    name: limit
    schema:
      type: integer
      maximum: 50
    examples:
      zero:
        value: 0
        summary: A sample limit value
      max:
        value: 50
        summary: A sample limit value
```

--------------------------------

### Complete OpenAPI Example with Links

Source: https://swagger.io/docs/specification/links

A full OpenAPI 3.0.4 example showcasing the 'links' feature. It defines a 'createUser' POST operation and a 'getUser' GET operation, with a link from the 'createUser' response to 'getUser' using the created user's ID.

```yaml
openapi: 3.0.4
info:
  version: 0.0.0
  title: Links example

paths:
  /users:
    post:
      summary: Creates a user and returns the user ID
      operationId: createUser
      requestBody:
        required: true
        description: A JSON object that contains the user name and age.
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/User"
      responses:
        "201":
          description: Created
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: integer
                    format: int64
                    description: ID of the created user.
          # -----------------------------------------------------
          # Links
          # -----------------------------------------------------
          links:
            GetUserByUserId: # <---- arbitrary name for the link
              operationId: getUser
              # or
              # operationRef: '#/paths/~1users~1{userId}/get'
              parameters:
                userId: "$response.body#/id"

              description: >
                The `id` value returned in the response can be used as
                the `userId` parameter in `GET /users/{userId}`.
          # -----------------------------------------------------

  /users/{userId}:
    get:
      summary: Gets a user by ID
      operationId: getUser
      parameters:
        - in: path
          name: userId
          required: true
          schema:
            type: integer
            format: int64
      responses:
        "200":
          description: A User object
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/User"

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
          format: int64
          readOnly: true
        name:
          type: string

```

--------------------------------

### Request Body Multiple Examples (Media Type Child with $ref)

Source: https://swagger.io/docs/specification/adding-examples

Illustrates providing multiple examples for a request body when using a $ref for the schema. The 'examples' keyword is used, with each example having a 'value' property.

```yaml
paths:
  /users:
    post:
      summary: Adds a new user
      requestBody:
        content:
          application/json: # Media type
            schema: # Request body contents
              $ref: "#/components/schemas/User" # Reference to an object
            examples: # Child of media type
              Jessica: # Example 1
                value:
                  id: 10
                  name: Jessica Smith
              Ron: # Example 2
                value:
                  id: 11
                  name: Ron Stewart
      responses:
        "200":
          description: OK
```

--------------------------------

### Examples for XML and HTML Data

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates how to specify inline examples for XML and HTML content types when they cannot be represented in JSON or YAML.

```APIDOC
## Examples for XML and HTML Data

### Description
To describe an example value that cannot be presented in JSON or YAML format, specify it as a string.

### Method
N/A (This describes a specification structure, not an endpoint)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
content:
  application/xml:
    schema:
      $ref: "#/components/schemas/xml"
    examples:
      xml:
        summary: A sample XML response
        value: "<objects><object><id>1</id><name>new</name></object><object><id>2</id></object></objects>"
  text/html:
    schema:
      type: string
    examples:
      html:
        summary: A list containing two items
        value: "<html><body><ul><li>item 1</li><li>item 2</li></ul></body></html>"
```

### Response
N/A

### Response Example
N/A
```

--------------------------------

### Request Body Example (Media Type Child with $ref)

Source: https://swagger.io/docs/specification/adding-examples

Shows how to use the 'example' keyword as a child of the media type when the schema is a reference ($ref). This is necessary because $ref overwrites sibling keywords.

```yaml
paths:
  /users:
    post:
      summary: Adds a new user
      requestBody:
        content:
          application/json: # Media type
            schema: # Request body contents
              $ref: "#/components/schemas/User" # Reference to an object
            example: # Child of media type because we use $ref above
              # Properties of a referenced object
              id: 10
              name: Jessica Smith
      responses:
        "200":
          description: OK
```

--------------------------------

### User Object Schema Examples

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates how to provide examples for object schemas and individual properties within the components section of an OpenAPI specification.

```APIDOC
## Components Schemas - User Object Examples

### Description
This section details how to define examples for the 'User' object schema and its properties.

### Components
#### Schemas
##### User (Object Schema)
- **type**: object
- **properties**:
  - **id** (integer) - The unique identifier for the user. `example`: 1
  - **name** (string) - The name of the user. `example`: New order

### Object-level Example
```json
{
  "id": 1,
  "name": "Jessica Smith"
}
```

### Property-level Examples
- **id**: `1`
- **name**: `New order`
```

--------------------------------

### Component Schema Object Example

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates providing an example for an entire object schema in the 'components' section. This shows a complete instance of the object being defined.

```yaml
components:
  schemas:
    User: # Schema name
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
      example: # Object-level example
        id: 1
        name: Jessica Smith
```

--------------------------------

### Reusing Examples

Source: https://swagger.io/docs/specification/adding-examples

Explains how to define common examples in the `components/examples` section and reuse them across different parts of the API specification.

```APIDOC
## Reusing Examples

### Description
You can define common examples in the `components/examples` section of your specification and then re-use them in various parameter descriptions, request and response body descriptions, objects and properties.

### Method
N/A (This describes a specification structure, not an endpoint)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
content:
  application/json:
    schema:
      $ref: '#/components/schemas/MyObject'
    examples:
      objectExample:
        $ref: '#/components/examples/objectExample'
...
components:
  examples:
    objectExample:
      value:
        id: 1
        name: new object
      summary: A sample object
```

### Response
N/A

### Response Example
N/A
```

--------------------------------

### Parameter Examples

Source: https://swagger.io/docs/specification/describing-parameters

Illustrates how to provide single or multiple named examples for parameters to clarify their usage.

```APIDOC
## Single Parameter Example

### Description
Specifies a single example value for a parameter that matches its schema.

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return.
  - `minimum: 1`
  - `example: 20`

## Multiple Named Parameter Examples

### Description
Provides multiple, distinctly named examples for a parameter, useful for array types or complex scenarios.

### Parameters
#### Query Parameters
- **ids** (array[integer]) - Required - One or more IDs.
  - `style: form`
  - `explode: false`
  - `examples`:
    - **oneId**:
      - `summary: Example of a single ID`
      - `value: [5]`
    - **multipleIds**:
      - `summary: Example of multiple IDs`
      - `value: [1, 5, 7]`

### Request Example (for multipleIds)
```
GET /resource?ids=1,5,7
```
```

--------------------------------

### Inline XML and HTML Examples in Swagger/OpenAPI

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates how to provide inline examples for XML and HTML content within a Swagger/OpenAPI specification. This is useful when the example data cannot be represented in standard JSON or YAML formats. The 'value' keyword holds the literal example string.

```yaml
content:
  application/xml:
    schema:
      $ref: "#/components/schemas/xml"
    examples:
      xml:
        summary: A sample XML response
        value: "<objects><object><id>1</id><name>new</name></object><object><id>2</id></object></objects>"
  text/html:
    schema:
      type: string
    examples:
      html:
        summary: A list containing two items
        value: "<html><body><ul><li>item 1</li><li>item 2</li></ul></body></html>"
```

--------------------------------

### Detailed OpenAPI Operation with Parameters and Schema

Source: https://swagger.io/docs/specification/paths-and-operations

A comprehensive example of an OpenAPI operation for 'GET /users/{id}'. It includes tags, summary, description, operationId, path parameters, and a response schema referencing a User component.

```yaml
paths:
  /users/{id}:
    get:
      tags:
        - Users
      summary: Gets a user by ID.
      description: |
        A detailed description of the operation.
        Use markdown for rich text representation,
        such as **bold**, *italic*, and [links](https://swagger.io).
      operationId: getUserById
      parameters:
        - name: id
          in: path
          description: User ID
          required: true
          schema:
            type: integer
            format: int64
      responses:
        "200":
          description: Successful operation
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/User"
      externalDocs:
        description: Learn more about user operations provided by this API.
        url: http://api.example.com/docs/user-operations/

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
      required:
        - id
        - name
```

--------------------------------

### Embed Swagger UI Standalone Preset HTML with unpkg

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

This example demonstrates embedding Swagger UI with the StandalonePreset using unpkg. It includes the necessary HTML, CSS, and JavaScript, along with the `swagger-ui-standalone-preset.js` script. This preset enables features like TopBar and ValidatorBadge, offering a more complete UI experience.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content="SwaggerUI" />
    <title>SwaggerUI</title>
    <link rel="stylesheet" href="https://unpkg.com/swagger-ui-dist@5.11.0/swagger-ui.css" />
  </head>
  <body>
  <div id="swagger-ui"></div>
  <script src="https://unpkg.com/swagger-ui-dist@5.11.0/swagger-ui-bundle.js" crossorigin></script>
  <script src="https://unpkg.com/swagger-ui-dist@5.11.0/swagger-ui-standalone-preset.js" crossorigin></script>
  <script>
    window.onload = () => {
      window.ui = SwaggerUIBundle({
        url: 'https://petstore3.swagger.io/api/v3/openapi.json',
        dom_id: '#swagger-ui',
        presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset
        ],
        layout: "StandaloneLayout",
      });
    };
  </script>
  </body>
</html>
```

--------------------------------

### Component Schema Array Item Example

Source: https://swagger.io/docs/specification/adding-examples

Shows how to specify an example for an individual item within an array schema in the 'components' section. This is useful for documenting the structure of elements within the array.

```yaml
components:
  schemas:
    ArrayOfInt:
      type: array
      items:
        type: integer
        format: int64
        example: 1
```

--------------------------------

### Component Schema Array Example (Multiple Items)

Source: https://swagger.io/docs/specification/adding-examples

Illustrates providing an example for an entire array, containing multiple items, within a schema in the 'components' section. This provides a sample of the array's content.

```yaml
components:
  schemas:
    ArrayOfInt:
      type: array
      items:
        type: integer
        format: int64
      example: [1, 2, 3]
```

--------------------------------

### Minimal OpenAPI Operation Definition

Source: https://swagger.io/docs/specification/paths-and-operations

A basic example of an OpenAPI operation defining a 'get' method for the '/ping' path, including a simple '200' response with a description.

```yaml
paths:
  /ping:
    get:
      responses:
        "200":
          description: OK
```

--------------------------------

### Importing Individual Swagger Editor Presets

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Shows how to import presets, which are collections of plugins designed to work together. Presets simplify the setup by providing pre-configured feature sets. Examples include 'textarea' and 'monaco' presets.

```javascript
import TextareaPreset from 'swagger-editor/presets/textarea';
import MonacoPreset from 'swagger-editor/presets/monaco';
```

--------------------------------

### Install Node.js Dependencies for Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/development/setting-up

After cloning the repository, navigate into the directory and run this command to install all necessary Node.js dependencies. Requires Node.js and npm to be installed.

```bash
cd swagger-ui
npm install
```

--------------------------------

### Example: Paginated Item Retrieval (HTTP Request)

Source: https://swagger.io/docs/specification/links

This snippet illustrates an HTTP GET request for retrieving a list of items with a specified limit. It shows how a cursor parameter can be used in subsequent requests to fetch the next set of data, demonstrating pagination.

```http
GET /items?limit=100
```

--------------------------------

### Get Components in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This example demonstrates how to retrieve registered components from the system using the `getComponent` method. This allows you to use components defined elsewhere in your plugin or in the core Swagger UI.

```javascript
// elsewhere
const HelloWorldStateless = system.getComponent("HelloWorldStateless")
const HelloWorldClass = system.getComponent("HelloWorldClass")
```

--------------------------------

### Request Body Example (Schema Child)

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates using the 'example' keyword as a child of 'schema' for a request body. This is suitable when the schema is defined inline.

```yaml
paths:
  /users:
    post:
      summary: Adds a new user
      requestBody:
        content:
          application/json:
            schema: # Request body contents
              type: object
              properties:
                id:
                  type: integer
                name:
                  type: string
              example: # Sample object
                id: 10
                name: Jessica Smith
      responses:
        "200":
          description: OK
```

--------------------------------

### Dictionary Example with Sample Content

Source: https://swagger.io/docs/specification/data-models/dictionaries

This schema defines a string-to-string dictionary and provides sample content using the `example` keyword. The sample shows key-value pairs for English and French greetings.

```yaml
type: object
additionalProperties:
  type: string
example:
  en: Hello!
  fr: Bonjour!
```

--------------------------------

### Reusing Defined Examples in Swagger/OpenAPI

Source: https://swagger.io/docs/specification/adding-examples

Illustrates how to define common examples in the `components/examples` section and then reuse them across different parts of the Swagger/OpenAPI specification using the '$ref' keyword. This promotes consistency and reduces redundancy.

```yaml
content:
  application/json:
    schema:
      $ref: '#/components/schemas/MyObject'
    examples:
      objectExample:
        $ref: '#/components/examples/objectExample'
...
components:
  examples:
    objectExample:
      value:
        id: 1
        name: new object
      summary: A sample object
```

--------------------------------

### API Path and Operation Definition (GET /users)

Source: https://swagger.io/docs/specification/basic-structure

Defines an API endpoint, specifically the 'GET' operation for the '/users' path. It includes a summary, extended description, and details about the expected '200' OK response, including the JSON schema for the response body.

```yaml
paths:
  /users:
    get:
      summary: Returns a list of users.
      description: Optional extended description in CommonMark or HTML
      responses:
        "200":
          description: A JSON array of user names
          content:
            application/json:
              schema:
                type: array
                items:
                  type: string

```

--------------------------------

### Define Multiple Request Body Examples (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This snippet shows how to define multiple examples for a request body using the 'examples' property. It illustrates inline examples with summaries, external referenced examples via 'externalValue', and examples referenced from the 'components.examples' section using '$ref'.

```yaml
requestBody:
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/Pet'
      examples:
        dog:
          summary: An example of a dog
          value:
            name: Fluffy
            petType: dog
        cat:
          summary: An example of a cat
          externalValue: http://api.example.com/examples/cat.json
        hamster:
          $ref: '#/components/examples/hamster'
components:
  examples:
    hamster:
      summary: An example of a hamster
      value:
        name: Ginger
        petType: hamster
```

--------------------------------

### OpenAPI 3.0.4 Basic Structure Example (YAML)

Source: https://swagger.io/docs/specification/basic-structure

A fundamental OpenAPI 3.0.4 definition in YAML format, illustrating the core components of an API specification. This includes the OpenAPI version, API information, server definitions, and path definitions for endpoints.

```yaml
openapi: 3.0.4
info:
  title: Sample API
  description: Optional multiline or single-line description in [CommonMark](http://commonmark.org/help/) or HTML.
  version: 0.1.9

servers:
  - url: http://api.example.com/v1
    description: Optional server description, e.g. Main (production) server
  - url: http://staging-api.example.com
    description: Optional server description, e.g. Internal staging server for testing

paths:
  /users:
    get:
      summary: Returns a list of users.
      description: Optional extended description in CommonMark or HTML.
      responses:
        "200": # status code
          description: A JSON array of user names
          content:
            application/json:
              schema:
                type: array
                items:
                  type: string

```

--------------------------------

### Add Single Example to OpenAPI Parameter (YAML)

Source: https://swagger.io/docs/specification/adding-examples

This snippet demonstrates how to add a single example value to an OpenAPI parameter using the `example` key. It's useful for providing a clear, representative value for a parameter, aiding tools like API mockers. The example value must match the parameter's schema type.

```yaml
parameters:
  - in: query
    name: status
    schema:
      type: string
      enum: [approved, pending, closed, new]
      example: approved
```

--------------------------------

### Component Schema Property Example

Source: https://swagger.io/docs/specification/adding-examples

Illustrates defining an example for an individual property within a schema in the 'components' section. This helps document the expected format or value of a specific field.

```yaml
components:
  schemas:
    User: # Schema name
      type: object
      properties:
        id:
          type: integer
          format: int64
          example: 1 # Property example
        name:
          type: string
          example: New order # Property example
```

--------------------------------

### GET /users

Source: https://swagger.io/docs/specification/basic-structure

Retrieves a list of users. The response contains a JSON array of user names.

```APIDOC
## GET /users

### Description
Returns a list of users. The response contains a JSON array of user names.

### Method
GET

### Endpoint
/users

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **Array of Strings** - A JSON array of user names

#### Response Example
{
  "example": "[\"user1\", \"user2\"]"
}
```

--------------------------------

### Example: Paginated Item Retrieval with Cursor (HTTP Request)

Source: https://swagger.io/docs/specification/links

This snippet demonstrates fetching the next page of items using a cursor obtained from a previous request. It includes the GET request with a 'cursor' and 'limit' parameter, facilitating sequential data retrieval.

```http
GET /items?cursor=Q1MjAwNz&limit=100
```

--------------------------------

### External Examples

Source: https://swagger.io/docs/specification/adding-examples

Shows how to use the `externalValue` keyword to reference example values from external URLs when they cannot be directly embedded in the specification.

```APIDOC
## External Examples

### Description
If a sample value cannot be inserted into your specification for some reason, for instance, it is neither YAML-, nor JSON-conformant, you can use the `externalValue` keyword to specify the URL of the example value. The URL should point to the resource that contains the literal example contents (an object, file or image, for example).

### Method
N/A (This describes a specification structure, not an endpoint)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
content:
  application/json:
    schema:
      $ref: "#/components/schemas/MyObject"
    examples:
      jsonObject:
        summary: A sample object
        externalValue: "http://example.com/examples/object-example.json"
  application/pdf:
    schema:
      type: string
      format: binary
    examples:
      sampleFile:
        summary: A sample file
        externalValue: "http://example.com/examples/example.pdf"
```

### Response
N/A

### Response Example
N/A
```

--------------------------------

### Component Schema Array of Objects Example

Source: https://swagger.io/docs/specification/adding-examples

Demonstrates providing a multi-item example for an array of objects within a schema in the 'components' section. This shows a sample array containing multiple object instances.

```yaml
components:
  schemas:
    ArrayOfUsers:
      type: array
      items:
        type: object
        properties:
          id:
            type: integer
          name:
            type: string
      example:
        - id: 10
          name: Jessica Smith
        - id: 20
          name: Ron Stewart
```

--------------------------------

### Basic Authentication Header Example

Source: https://swagger.io/docs/specification/authentication/basic-authentication

An example of how to format the Authorization header for Basic Authentication.

```APIDOC
## Basic Authentication Header Example

### Description
This section demonstrates the correct format for the `Authorization` header when using Basic Authentication. It includes a base64-encoded string of the username and password.

### Method
N/A (This is a header format example)

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```
Authorization: Basic ZGVtbzpwQDU1dzByZA==
```

### Response
N/A
```

--------------------------------

### Docker Compose Environment Variables (.env file) (Shell)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Provides examples of environment variable configurations for a Docker Compose setup, specifically for the swagger.io project. It shows how to define supported submission methods and a list of URLs with associated names.

```shell
SUPPORTED_SUBMIT_METHODS=['get', 'post']
URLS=[ { url: 'https://petstore.swagger.io/v2/swagger.json', name: 'Petstore' } ]
```

--------------------------------

### Start Swagger UI Development Server

Source: https://swagger.io/docs/open-source-tools/swagger-ui/development/setting-up

This command starts the local development server for Swagger UI. It provides features like hot module reloading and unminified stack traces for easier debugging. Access the UI at http://localhost:3200/.

```bash
npm run dev
```

--------------------------------

### Define Multiple Named Examples for Array Parameter (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This snippet demonstrates defining multiple, named examples for an array-type query parameter. The `examples` object contains key-value pairs, where each key is a name for the example (e.g., `oneId`, `multipleIds`), and the value provides a `summary` and the actual `value` for the example. This is useful for showcasing different valid inputs for complex parameters.

```yaml
parameters:
  - in: query
    name: ids
    description: One or more IDs
    required: true
    schema:
      type: array
      items:
        type: integer
    style: form
    explode: false
    examples:
      oneId:
        summary: Example of a single ID
        value: [5] # ?ids=5
      multipleIds:
        summary: Example of multiple IDs
        value: [1, 5, 7] # ?ids=1,5,7
```

--------------------------------

### External Examples for JSON and PDF in Swagger/OpenAPI

Source: https://swagger.io/docs/specification/adding-examples

Shows how to reference external example values using the 'externalValue' keyword for content types like JSON and PDF. This is beneficial when the example is too large or complex to embed directly, or when it resides in a separate file. The URL should point to the resource containing the example.

```yaml
content:
  application/json:
    schema:
      $ref: "#/components/schemas/MyObject"
    examples:
      jsonObject:
        summary: A sample object
        externalValue: "http://example.com/examples/object-example.json"
  application/pdf:
    schema:
      type: string
      format: binary
    examples:
      sampleFile:
        summary: A sample file
        externalValue: "http://example.com/examples/example.pdf"
```

--------------------------------

### Server Templating Examples

Source: https://swagger.io/docs/specification/api-host-and-base-path

Provides various examples of server templating for different use cases.

```APIDOC
## Server Templating Examples

### Description
Illustrates common use cases for server templating.

#### HTTPS and HTTP
```yaml
servers:
  - url: http://api.example.com
  - url: https://api.example.com
```

Or using templating:
```yaml
servers:
  - url: '{protocol}://api.example.com'
    variables:
      protocol:
        enum:
          - http
          - https
        default: https
```

#### Production, Development, and Staging
```yaml
servers:
  - url: https://{environment}.example.com/v2
    variables:
      environment:
        default: api    # Production server
        enum:
          - api         # Production server
          - api.dev     # Development server
          - api.staging # Staging server
```

#### SaaS and On-Premise
```yaml
servers:
  - url: "{server}/v1"
    variables:
      server:
        default: https://api.example.com # SaaS server
```

#### Regional Endpoints
```yaml
servers:
  - url: https://{region}.api.cognitive.microsoft.com
    variables:
      region:
        default: westus
        enum:
          - westus
          - eastus2
          - westcentralus
          - westeurope
          - southeastasia
```
```

--------------------------------

### Example Query Parameter Usage

Source: https://swagger.io/docs/specification/describing-parameters

Provides examples of API endpoints utilizing query parameters. The first example shows filtering by 'status', while the second demonstrates pagination using 'offset' and 'limit'. These illustrate common use cases for query parameters.

```text
GET /pets/findByStatus?status=available
GET /notes?offset=100&limit=50

```

--------------------------------

### Generate Dynamic HTML API Documentation

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This command generates dynamic HTML API documentation from a Swagger specification using the `-l dynamic-html` flag. After generation, the provided commands install dependencies and start a Node.js server to serve the single-page application documentation.

```bash
cd samples/dynamic-html/
npm install
node .
```

--------------------------------

### Build-Free SwaggerUI with Preview Plugins via unpkg.com (HTML/JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This HTML and JavaScript example shows how to use SwaggerUI with preview plugins for AsyncAPI and API Design Systems without a build process, leveraging unpkg.com. It includes necessary CSS and JS files from CDNs and configures SwaggerUIBundle with the relevant editor plugins.

```html
<!DOCTYPE html>
<html >
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta name="description" content="SwaggerUIMultifold" />
    <link rel="stylesheet" href="//unpkg.com/swagger-editor@5.0.0-alpha.86/dist/swagger-editor.css" />
  </head>
  <body style="margin:0; padding:0;">
    <section id="swagger-ui"></section>

    <script src="//unpkg.com/swagger-ui-dist@5.11.0/swagger-ui-bundle.js"></script>
    <script src="//unpkg.com/swagger-ui-dist@5.11.0/swagger-ui-standalone-preset.js"></script>
    <script>
      ui = SwaggerUIBundle({});
      // expose SwaggerUI React globally for SwaggerEditor to use
      window.React = ui.React;
    </script>
    <script src="//unpkg.com/swagger-editor@5.0.0-alpha.86/dist/umd/swagger-editor.js"></script>
    <script>
      SwaggerUIBundle({
        url: 'https://petstore3.swagger.io/api/v3/openapi.json',
        dom_id: '#swagger-ui',
        presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset,
        ],
        plugins: [
          SwaggerEditor.plugins.EditorContentType,
          SwaggerEditor.plugins.EditorPreviewAsyncAPI,
          SwaggerEditor.plugins.EditorPreviewApiDesignSystems,
          SwaggerEditor.plugins.SwaggerUIAdapter,
          SwaggerUIBundle.plugins.DownloadUrl,
        ],
        layout: 'StandaloneLayout',
      });
    </script>
  </body>
</html>
```

--------------------------------

### Install Swagger Editor via npm

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This command demonstrates how to install the Swagger Editor npm package, specifically the alpha version. Ensure you have Node.js and the necessary prerequisites installed before running this command.

```bash
$ npm install swagger-editor@alpha
```

--------------------------------

### Combine Path and Operation Level Parameters (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML example shows how parameters defined at the path level are inherited by operations, and how additional parameters can be defined at the operation level. The `id` parameter is common to `/users/{id}`, and the `get` operation adds a `metadata` query parameter. This demonstrates a hierarchical approach to parameter definition.

```yaml
paths:
  /users/{id}:
    parameters:
      - in: path
        name: id
        schema:
          type: integer
        required: true
        description: The user ID.
    get:
      summary: Gets a user by ID
      parameters:
        - in: query
          name: metadata
          schema:
            type: boolean
          required: false
          description: If true, the endpoint returns only the user metadata.
      responses:
        "200":
          description: OK
```

--------------------------------

### Define Header Parameter in OpenAPI

Source: https://swagger.io/docs/specification/describing-parameters

Shows how to define a custom request header parameter using `in: header`. This example defines an `X-Request-ID` header for a `GET /ping` operation.

```yaml
paths:
  /ping:
    get:
      summary: Checks if the server is alive
      parameters:
        - in: header
          name: X-Request-ID
          schema:
            type: string
            format: uuid
          required: true
```

--------------------------------

### Define Single Example for Query Parameter (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML code illustrates how to specify a single example value for a query parameter. The `example` property is used, and its value must conform to the parameter's schema. This helps in understanding and testing the expected input for the parameter.

```yaml
parameters:
  - in: query
    name: limit
    schema:
      type: integer
      minimum: 1
    example: 20
```

--------------------------------

### Docker Environment Variable - String Example

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Example of setting string environment variables for Dockerized Swagger UI.

```bash
FILTER="myFilterValue"
LAYOUT="BaseLayout"
```

--------------------------------

### Docker Environment Variable - Number Example

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Example of setting number environment variables for Dockerized Swagger UI.

```bash
DEFAULT_MODELS_EXPAND_DEPTH="5"
DEFAULT_MODEL_EXPAND_DEPTH="7"
```

--------------------------------

### GET /items with Enum Query Parameter

Source: https://swagger.io/docs/specification/data-models/enums

This example demonstrates how to define a query parameter with an enum using OpenAPI 3.0 syntax. The 'sort' parameter accepts either 'asc' or 'desc'.

```APIDOC
## GET /items

### Description
Retrieves a list of items, with an option to specify the sort order.

### Method
GET

### Endpoint
/items

### Parameters
#### Query Parameters
- **sort** (string) - Optional - Sort order. Accepts 'asc' or 'desc'.

### Request Example
```json
{
  "example": "GET /items?sort=asc"
}
```

### Response
#### Success Response (200)
- **items** (array) - A list of items.

#### Response Example
```json
{
  "example": {
    "items": [
      { "id": 1, "name": "Item 1" },
      { "id": 2, "name": "Item 2" }
    ]
  }
}
```
```

--------------------------------

### Example Path Parameter Definitions

Source: https://swagger.io/docs/specification/describing-parameters

Illustrates different ways to define path parameters in URLs. This includes single parameters, multiple parameters in a nested path, and parameters used for file formats. These examples show the flexibility in structuring API endpoints.

```text
GET /users/{id}
GET /cars/{carId}/drivers/{driverId}
GET /report.{format}

```

--------------------------------

### Install Swagger UI Packages via NPM

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Installs the core `swagger-ui`, `swagger-ui-react`, and `swagger-ui-dist` packages from the NPM registry. These packages provide the necessary files for integrating Swagger UI into web applications.

```bash
npm install swagger-ui
```

```bash
npm install swagger-ui-react
```

```bash
npm install swagger-ui-dist
```

--------------------------------

### Server URL Example

Source: https://swagger.io/docs/specification/api-host-and-base-path

Demonstrates a basic API server URL with a base path and query parameters.

```APIDOC
## GET /users

### Description
Retrieves a list of users, optionally filtered by role and status.

### Method
GET

### Endpoint
`/users`

### Query Parameters
- **role** (string) - Optional - Filters users by their role (e.g., 'admin').
- **status** (string) - Optional - Filters users by their status (e.g., 'active').

### Request Example
```
GET https://api.example.com/v1/users?role=admin&status=active
```

### Response
#### Success Response (200)
- **users** (array) - A list of user objects.
  - **id** (string) - The user's unique identifier.
  - **name** (string) - The user's name.
  - **role** (string) - The user's role.
  - **status** (string) - The user's status.

#### Response Example
```json
{
  "users": [
    {
      "id": "user123",
      "name": "John Doe",
      "role": "admin",
      "status": "active"
    }
  ]
}
```
```

--------------------------------

### Get Language-Specific Swagger Codegen Options (CLI)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This command retrieves a list of options specific to a particular language generator within Swagger Codegen. For example, running `config-help -l php` will show options relevant only to PHP client generation.

```shell
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar config-help -l php
```

--------------------------------

### Path and Query Parameter Serialization Example (YAML)

Source: https://swagger.io/docs/specification/serialization

An OpenAPI definition in YAML format demonstrating a path parameter 'id' with 'matrix' style and 'explode: true', and a query parameter 'metadata' with default 'form' style.

```yaml
paths:
  # /users;id=3;id=4?metadata=true
  /users{id}:
    get:
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: array
            items:
              type: integer
            minItems: 1
          style: matrix
          explode: true
        - in: query
          name: metadata
          schema:
            type: boolean
          # Using the default serialization for query parameters:
          # style=form, explode=false, allowReserved=false
      responses:
        '200':
          description: A list of users

```

--------------------------------

### Clone Swagger UI Repository

Source: https://swagger.io/docs/open-source-tools/swagger-ui/development/setting-up

This command clones the Swagger UI repository from GitHub to your local machine. Ensure you have Git installed.

```bash
git clone https://github.com/swagger-api/swagger-ui.git
```

--------------------------------

### Define Single Inline Request Body Example (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This snippet demonstrates how to define a single inline example for a request body using the 'example' property within the 'requestBody.content.<media-type>' object. This overrides schema examples and is useful for providing a specific instance of the request payload.

```yaml
requestBody:
  content:
    application/json:
      schema:
        $ref: "#/components/schemas/Pet"
      example:
        name: Fluffy
        petType: dog
```

--------------------------------

### Docker Environment Variable - Array Example

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Example of setting array environment variables for Dockerized Swagger UI. Ensure proper escaping of characters within the array string.

```bash
SUPPORTED_SUBMIT_METHODS="[\"get\", \"post\"]"
URLS="[ { url: \"https://petstore.swagger.io/v2/swagger.json\", name: \"Petstore\" } ]"
```

--------------------------------

### Header Parameter Serialization Examples

Source: https://swagger.io/docs/specification/serialization

Demonstrates how header parameters are serialized using the 'simple' style, with and without the 'explode' modifier. This covers primitive, array, and object values.

```text
style| explode| URI template| Primitive value X-MyHeader = 5| Array X-MyHeader = [3, 4, 5]| Object X-MyHeader = {“role”: “admin”, “firstName”: “Alex”}  
---|---|---|---|---|---
simple *| false *| {id}| X-MyHeader: 5| X-MyHeader: 3,4,5| X-MyHeader: role,admin,firstName,Alex  
simple| true| {id*}| X-MyHeader: 5| X-MyHeader: 3,4,5| X-MyHeader: role=admin,firstName=Alex  
```

--------------------------------

### Composing Swagger UI with Swagger Editor Plugins

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Illustrates the integration of Swagger UI with a wide array of Swagger Editor plugins. This example shows how to initialize Swagger UI and pass an array of plugins to enable various functionalities, such as different editor types, preview modes, and UI enhancements. It requires importing the 'swagger-ui' package and its CSS.

```javascript
import SwaggerUI from 'swagger-ui';
import 'swagger-ui/dist/swagger-ui.css';
import ModalsPlugin from 'swagger-editor/plugins/modals';
import DialogsPlugin from 'swagger-editor/plugins/dialogs';
import DropdownMenuPlugin from 'swagger-editor/plugins/dropdown-menu';
import DropzonePlugin from 'swagger-editor/plugins/dropzone';
import VersionsPlugin from 'swagger-editor/plugins/versions';
import EditorTextareaPlugin from 'swagger-editor/plugins/editor-textarea';
import EditorMonacoPlugin from 'swagger-editor/plugins/editor-monaco';
import EditorMonacoLanguageApiDOMPlugin from 'swagger-editor/plugins/editor-monaco-language-apidom';
import EditorContentReadOnlyPlugin from 'swagger-editor/plugins/editor-content-read-only';
import EditorContentOriginPlugin from 'swagger-editor/plugins/editor-content-origin';
import EditorContentTypePlugin from 'swagger-editor/plugins/editor-content-type';
import EditorContentPersistencePlugin from 'swagger-editor/plugins/editor-content-persistence';
import EditorContentFixturesPlugin from 'swagger-editor/plugins/editor-content-fixtures';
import EditorPreviewPlugin from 'swagger-editor/plugins/editor-preview';
import EditorPreviewSwaggerUIPlugin from 'swagger-editor/plugins/editor-preview-swagger-ui';
import EditorPreviewAsyncAPIPlugin from 'swagger-editor/plugins/editor-preview-asyncapi';
import EditorPreviewApiDesignSystemsPlugin from 'swagger-editor/plugins/editor-preview-api-design-systems';
import TopBarPlugin from 'swagger-editor/plugins/top-bar';
import SplashScreenPlugin from 'swagger-editor/plugins/splash-screen';
import LayoutPlugin from 'swagger-editor/plugins/layout';
import EditorSafeRenderPlugin from 'swagger-editor/plugins/editor-safe-render';

SwaggerUI({
  url: 'https://petstore.swagger.io/v2/swagger.json',
  dom_id: '#swagger-editor',
  plugins: [
    ModalsPlugin,
    DialogsPlugin,
    DropdownMenuPlugin,
    DropzonePlugin,
    VersionsPlugin,
    EditorTextareaPlugin,
    EditorMonacoPlugin,
    EditorMonacoLanguageApiDOMPlugin,
    EditorContentReadOnlyPlugin,
    EditorContentOriginPlugin,
    EditorContentTypePlugin,
    EditorContentPersistencePlugin,
    EditorContentFixturesPlugin,
    EditorPreviewPlugin,
    EditorPreviewSwaggerUIPlugin,
    EditorPreviewAsyncAPIPlugin,
    EditorPreviewApiDesignSystemsPlugin,
    TopBarPlugin,
    SplashScreenPlugin,
    LayoutPlugin,
    EditorSafeRenderPlugin,
  ],
  layout: 'StandaloneLayout',
});
```

--------------------------------

### Apply Scoped Security to Specific API Operations

Source: https://swagger.io/docs/specification/authentication

This example illustrates how to apply scoped security requirements to individual API operations rather than globally. It shows a scenario where a 'GET /users' operation requires 'read' scope, while a 'POST /users' operation requires 'write' scope, both using OAuth2 authentication.

```yaml
paths:
  /users:
    get:
      summary: Get a list of users
      security:
        - OAuth2: [read]
      ...
    post:
      summary: Add a user
      security:
        - OAuth2: [write]
      ...
```

--------------------------------

### Install Dependencies with npm

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Installs project dependencies using npm, specifically using the `--legacy-peer-deps` flag to bypass peer dependency version conflicts. This is a common step before running development or build commands.

```bash
npm i --legacy-peer-deps
```

--------------------------------

### OpenAPI Server URL Format Examples

Source: https://swagger.io/docs/specification/api-host-and-base-path

Illustrates various valid formats for server URLs in OpenAPI specifications, including scheme, host, port, and path. It also shows examples of relative URLs and WebSocket schemes.

```text
https://api.example.com
https://api.example.com:8443/v1/reports
http://localhost:3025/v1
http://10.0.81.36/v1
ws://api.example.com/v1
wss://api.example.com/v1
/v1/reports
/
//api.example.com
```

--------------------------------

### Install Swagger Codegen using Homebrew

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/prerequisites

Installs Swagger Codegen on macOS using the Homebrew package manager. This is a convenient method for Mac users to install the tool. Requires Homebrew to be installed.

```bash
brew install swagger-codegen
```

--------------------------------

### Example: Create User Operation (HTTP Request)

Source: https://swagger.io/docs/specification/links

This snippet demonstrates an HTTP POST request to create a new user. It includes the request line, host, content type, and a JSON payload with user details. The expected output is a 201 Created status with the user's ID.

```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "Alex",
  "age": 27
}
```

--------------------------------

### HTTP Basic Authentication Header Example

Source: https://swagger.io/docs/specification/authentication/basic-authentication

An example of the Authorization header used in Basic Authentication. It includes the word 'Basic' followed by a base64-encoded string of 'username:password'. This method should be used with HTTPS for security.

```http
Authorization: Basic ZGVtbzpwQDU1dzByZA==
```

--------------------------------

### OpenID Connect Discovery Metadata Example

Source: https://swagger.io/docs/specification/authentication/openid-connect-discovery

An example JSON object representing the metadata returned by an OpenID Connect Discovery endpoint. This data includes URLs for various OIDC endpoints, supported scopes, response types, and token endpoint authentication methods.

```json
{
  "issuer": "https://example.com/",
  "authorization_endpoint": "https://example.com/authorize",
  "token_endpoint": "https://example.com/token",
  "userinfo_endpoint": "https://example.com/userinfo",
  "jwks_uri": "https://example.com/.well-known/jwks.json",
  "scopes_supported": ["pets_read", "pets_write", "admin"],
  "response_types_supported": ["code", "id_token", "token id_token"],
  "token_endpoint_auth_methods_supported": ["client_secret_basic"]
}
```

--------------------------------

### HTML Form Example

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

An example of a simple HTML form with text, number, and submit input fields. This form is configured to POST data to a specified action URL.

```html
<form action="http://example.com/survey" method="post">
  <input type="text" name="name" />
  <input type="number" name="fav_number" />
  <input type="submit" />
</form>
```

--------------------------------

### Docker Environment Variable - Boolean Example

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Example of setting boolean environment variables for Dockerized Swagger UI.

```bash
DISPLAY_OPERATION_ID="true"
DEEP_LINKING="false"
```

--------------------------------

### Example JSON Configuration for Java Client

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

An example JSON configuration file used with Swagger Codegen to customize the generated Java client. It demonstrates setting the 'apiPackage' option.

```json
{
  "apiPackage" : "petstore"
}
```

--------------------------------

### Build Swagger Codegen in Vagrant with Docker

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This sequence outlines the steps to set up a development environment using Vagrant and Docker. It involves cloning the repository, starting the Vagrant environment, SSHing into the virtual machine, navigating to the project directory, and then building the project using `run-in-docker.sh`.

```bash
git clone http://github.com/swagger-api/swagger-codegen.git
cd swagger-codegen
vagrant up
vagrant ssh
cd /vagrant
./run-in-docker.sh mvn package
```

--------------------------------

### Install Webpack 5 Dependencies for Swagger Editor

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

These commands install the necessary npm packages required for webpack@5 to properly build and bundle the Swagger Editor and its dependencies. These include stream-browserify, https-browserify, stream-http, and util.

```bash
$ npm i stream-browserify --save-dev
$ npm i https-browserify --save-dev
$ npm i stream-http --save-dev
$ npm i util --save-dev

```

--------------------------------

### Install Dependencies for Alternative Webpack Config

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This command installs `copy-webpack-plugin` along with other necessary packages like stream-browserify, https-browserify, stream-http, and util. These are required for the alternative webpack configuration that utilizes pre-built Web Worker fragments from the swagger-editor package.

```bash
$ npm i copy-webpack-plugin --save-dev
$ npm i stream-browserify --save-dev
$ npm i https-browserify --save-dev
$ npm i stream-http --save-dev
$ npm i util --save-dev

```

--------------------------------

### Example CORS Headers Configuration

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/cors

This snippet illustrates an example of CORS headers that need to be configured on the server. It specifies the allowed origin, methods, and importantly, the headers that Swagger UI is permitted to send with requests.

```text
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, DELETE, PUT, PATCH, OPTIONS
Access-Control-Allow-Headers: Content-Type, api_key, Authorization
```

--------------------------------

### Implicit Flow Example (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

An example demonstrating the Implicit OAuth 2.0 flow configuration. It specifies the authorization URL and available scopes for obtaining an access token directly from the authorization server.

```yaml
components:
  securitySchemes:
    oAuth2Implicit:
      type: oauth2
      description: For more information, see https://developers.getbase.com/docs/rest/articles/oauth2/requests
      flows:
        implicit:
          authorizationUrl: https://api.getbase.com/oauth2/authorize
          scopes:
            read: Grant read-only access to all your data except for the account and user info
            write: Grant write-only access to all your data except for the account and user info
            profile: Grant read-only access to the account and user info only

```

--------------------------------

### Example Java Client Configuration

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

An example JSON configuration file for generating a Java client with Swagger Codegen. It specifies groupId, artifactId, artifactVersion, and the desired client library (e.g., 'feign').

```json
{
  "groupId":"com.my.company",
  "artifactId":"MyClient",
  "artifactVersion":"1.2.0",
  "library":"feign"
}
```

--------------------------------

### Run Swagger Codegen CLI Help

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/prerequisites

Executes the Swagger Codegen CLI JAR file to display its help information. This command is used to verify the installation and understand available options. Requires Java runtime.

```bash
java -jar swagger-codegen-cli.jar --help
```

--------------------------------

### Serve Swagger UI Assets with Express

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Uses the `swagger-ui-dist` package to serve Swagger UI assets via an Express server. The `absolutePath()` helper function finds the installed module's directory, which is then served statically.

```javascript
const express = require('express')
const pathToSwaggerUi = require('swagger-ui-dist').absolutePath()

const app = express()

app.use(express.static(pathToSwaggerUi))

app.listen(3000)
```

--------------------------------

### Basic $ref Syntax Example

Source: https://swagger.io/docs/specification/using-ref

Demonstrates the fundamental usage of the $ref keyword to reference a definition. This is useful for reusing schema objects across different parts of an API specification.

```yaml
$ref: "reference to definition"
```

--------------------------------

### OpenAPI Runtime Expression Examples

Source: https://swagger.io/docs/specification/links

Illustrates various OpenAPI runtime expressions and their evaluated results based on a sample request and response. This helps understand how to extract specific data points like query parameters, headers, and response body elements.

```text
Expression| Result| Comments  
---|---|---  
`$url`| http://api.example.com/users?limit=2&total=true|   
`$method`| GET|   
`$request.query.total`| true| `total` must be defined as a query parameter.  
`$statusCode`| 200|   
`$response.header.x-total-count`| 37| Assuming `X-Total-Count` is defined as a response header. Header names are case-insensitive.  
`$response.body#/next_offset`| 2|   
`$response.body#/users/0`| `{"id": 1, "name": "Alice"}`| JSON Pointer (the `#/...` part) uses 0-based indexes to access array elements. There is no wildcard syntax though, so `$response.body#/users/*/id` is not valid.  
`$response.body#/users/1`| `{"id": 2, "name": "Bob"}`|   
`$response.body#/users/1/name`| Bob|   
`ID_{$response.body#/users/1/id}`| ID_2|   
```

--------------------------------

### Run Swagger UI Docker Image

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Commands to pull and run the official Swagger UI Docker image. It shows how to expose the UI on port 80 and how to provide a custom `swagger.json` file or URL.

```bash
docker pull docker.swagger.io/swaggerapi/swagger-ui
docker run -p 80:8080 docker.swagger.io/swaggerapi/swagger-ui
```

```bash
docker run -p 80:8080 -e SWAGGER_JSON=/foo/swagger.json -v /bar:/foo docker.swagger.io/swaggerapi/swagger-ui
```

```bash
docker run -p 80:8080 -e SWAGGER_JSON_URL=https://petstore3.swagger.io/api/v3/openapi.json docker.swagger.io/swaggerapi/swagger-ui
```

--------------------------------

### GET /ping

Source: https://swagger.io/docs/specification/describing-responses

A simple GET endpoint that returns a 'pong' string.

```APIDOC
## GET /ping

### Description
This endpoint is used to check the liveness of the API. It returns a simple string response.

### Method
GET

### Endpoint
/ping

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **pong** (string) - The response string indicating the API is alive.

#### Response Example
```
pong
```
```

--------------------------------

### Initialize Swagger UI Bundle Standalone

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Initializes Swagger UI using `SwaggerUIBundle` from `swagger-ui-dist`, suitable for projects that cannot handle traditional npm modules. It configures the UI with a specific OpenAPI URL, DOM ID, presets, and layout.

```javascript
var SwaggerUIBundle = require('swagger-ui-dist').SwaggerUIBundle

const ui = SwaggerUIBundle({
    url: "https://petstore.swagger.io/v2/swagger.json",
    dom_id: '#swagger-ui',
    presets: [
      SwaggerUIBundle.presets.apis,
      SwaggerUIBundle.SwaggerUIStandalonePreset
    ],
    layout: "StandaloneLayout"
  })
```

--------------------------------

### Customizing Safe-Render Plugin with New Components

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

Example of integrating the safe-render plugin with custom components. This demonstrates how to add `MyCustomComponent1` to the list of components protected by error boundaries.

```javascript
const swaggerUI = SwaggerUI({
  url: "https://petstore.swagger.io/v2/swagger.json",
  dom_id: '#swagger-ui',
  plugins: [
    () => ({
      components: {
        MyCustomComponent1: () => 'my custom component',
      },
    }),
    SwaggerUI.plugins.SafeRender({
      fullOverride: true, // only the component list defined here will apply (not the default list)
      componentList: [
        "MyCustomComponent1",
      ],
    }),
  ],
});
```

--------------------------------

### Build and Run Swagger Editor Docker Image Locally

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Builds a Docker image from the local project code and runs it as a container. This process involves installing npm packages, building the application, creating the Docker image, and then running the container. The application will be accessible via `http://localhost`.

```bash
# Install npm packages (if needed)
npm install

# Build the app
npm run build

# Build an image
docker build -t swagger-editor .

# Run the container
docker run -d -p 80:8080 swagger-editor
```

--------------------------------

### Example: Amazon API Gateway Custom Authorizer Extension

Source: https://swagger.io/docs/specification/openapi-extensions

This example demonstrates how to use OpenAPI extensions to configure a custom authorizer for Amazon API Gateway, including details like authorizer type, URI, credentials, and TTL.

```APIDOC
## Example: Amazon API Gateway Custom Authorizer

### Description
An API that uses Amazon API Gateway custom authorizer might include extensions similar to this, specifying authorizer details and configuration.

### Method
N/A (This is a configuration example within an OpenAPI spec)

### Endpoint
N/A (This is a configuration example within an OpenAPI spec)

### Request Body
```yaml
components:
  securitySchemes:
    APIGatewayAuthorizer:
      type: apiKey
      name: Authorization
      in: header
      x-amazon-apigateway-authtype: oauth2
      x-amazon-apigateway-authorizer:
        type: token
        authorizerUri: arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:account-id:function:function-name/invocations
        authorizerCredentials: arn:aws:iam::account-id:role
        identityValidationExpression: "^x-[a-z]+"
        authorizerResultTtlInSeconds: 60
```

### Response
N/A (This is a configuration example within an OpenAPI spec)
```

--------------------------------

### GET /ping

Source: https://swagger.io/docs/specification/paths-and-operations

A simple endpoint to check if the API is responsive.

```APIDOC
## GET /ping

### Description
This endpoint is used to check the liveness of the API. It returns a simple success response.

### Method
GET

### Endpoint
/ping

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **description** (string) - OK
```

--------------------------------

### GET /users

Source: https://swagger.io/docs/specification/paths-and-operations

Retrieves a list of users.

```APIDOC
## GET /users

### Description
Retrieves a list of all users in the system.

### Method
GET

### Endpoint
/users

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **description** (string) - A list of users.
```

--------------------------------

### Understanding oneOf vs anyOf

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Explains the key difference between `oneOf` (matches exactly one schema) and `anyOf` (matches one or more schemas) with examples.

```APIDOC
## Schema Matching Logic

### Description
This section clarifies the distinction between `oneOf` and `anyOf` keywords in OpenAPI schema composition.

### `oneOf`
- Requires the data to be valid against **exactly one** of the subschemas.
- If data matches multiple subschemas, it is considered invalid.

### `anyOf`
- Allows the data to be valid against **one or more** of the subschemas.
- Provides more flexibility as data can satisfy multiple schema conditions simultaneously.

### Example Scenario
Consider a schema using `oneOf` with `PetByAge` and `PetByType`. A request body like `{"nickname": "Fido", "pet_type": "Dog", "age": 4}` would be **invalid** with `oneOf` because it satisfies both schemas.

With `anyOf`, the same request body `{"nickname": "Fido", "pet_type": "Dog", "age": 4}` would be **valid** because it satisfies both schemas.
```

--------------------------------

### GET /users/{userId}

Source: https://swagger.io/docs/specification/links

Gets a user by ID.

```APIDOC
## GET /users/{userId}

### Description
Gets a user by ID.

### Method
GET

### Endpoint
/users/{userId}

### Parameters
#### Path Parameters
- **userId** (integer) - Required - The ID of the user to retrieve.

### Response
#### Success Response (200)
- **User** (User) - A User object.

#### Response Example
```json
{
  "id": 123,
  "name": "John Doe"
}
```
```

--------------------------------

### Cookie Parameter Serialization Examples

Source: https://swagger.io/docs/specification/serialization

Illustrates cookie parameter serialization using the 'form' style, with and without the 'explode' modifier. This shows how primitive, array, and object values are represented in cookie headers.

```text
style| explode| URI template| Primitive value id = 5| Array id = [3, 4, 5]| Object id = {“role”: “admin”, “firstName”: “Alex”}  
---|---|---|---|---|---
form *| true *| | Cookie: id=5| |   
form| false| id={id}| Cookie: id=5| Cookie: id=3,4,5| Cookie: id=role,admin,firstName,Alex  
```

--------------------------------

### Configure Swagger UI Docker Image Environment Variables

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Demonstrates how to configure the Swagger UI Docker container using environment variables. This includes setting the base URL, port, IPv6 port, and embedding options.

```bash
docker run -p 80:8080 -e BASE_URL=/swagger -e SWAGGER_JSON=/foo/swagger.json -v /bar:/foo docker.swagger.io/swaggerapi/swagger-ui
```

```bash
docker run -p 80:80 -e PORT=80 docker.swagger.io/swaggerapi/swagger-ui
```

```bash
docker run -p 80:80 -e PORT_IPV6=8080 docker.swagger.io/swaggerapi/swagger-ui
```

```bash
docker run -p 80:80 -e EMBEDDING=true docker.swagger.io/swaggerapi/swagger-ui
```

--------------------------------

### Authorization Code Flow Example (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

An example of configuring the Authorization Code flow for OAuth 2.0 security. It includes the authorization URL, token URL, and a list of supported scopes for an API, such as Slack.

```yaml
components:
  securitySchemes:
    oAuth2AuthCode:
      type: oauth2
      description: For more information, see https://api.slack.com/docs/oauth
      flows:
        authorizationCode:
          authorizationUrl: https://slack.com/oauth/authorize
          tokenUrl: https://slack.com/api/oauth.access
          scopes:
            users:read: Read user information
            users:write: Modify user information
            im:read: Read messages
            im:write: Write messages
            im:history: Access the message archive
            search:read: Search messages, files, and so on
            # etc.

```

--------------------------------

### Combine Multiple Authentication Types with Logical AND

Source: https://swagger.io/docs/specification/authentication

This example demonstrates how to enforce the simultaneous use of multiple authentication methods using the logical AND operator. Within a single entry in the 'security' array, multiple security schemes are listed, requiring all of them to be present in the request.

```yaml
security:
  - apiKey1: []
    apiKey2: []
```

--------------------------------

### Set-Cookie Header Example

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

An example of the Set-Cookie header used by the server to send authentication cookies to the client. This header includes the cookie name, value, path, and HttpOnly flag.

```http
Set-Cookie: JSESSIONID=abcde12345; Path=/; HttpOnly
```

--------------------------------

### Authorization Code Flow Example (Slack API)

Source: https://swagger.io/docs/specification/authentication/oauth2

An example of defining an OAuth2 security scheme using the 'authorizationCode' flow, including authorization and token URLs, and a list of scopes specific to the Slack API.

```APIDOC
## Authorization Code Flow Example (Slack API)

### Description
This example showcases the 'authorizationCode' flow for OAuth2, detailing the `authorizationUrl`, `tokenUrl`, and various scopes available for the Slack API. It also includes a description for the security scheme.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
```yaml
components:
  securitySchemes:
    oAuth2AuthCode:
      type: oauth2
      description: For more information, see https://api.slack.com/docs/oauth
      flows:
        authorizationCode:
          authorizationUrl: https://slack.com/oauth/authorize
          tokenUrl: https://slack.com/api/oauth.access
          scopes:
            users:read: Read user information
            users:write: Modify user information
            im:read: Read messages
            im:write: Write messages
            im:history: Access the message archive
            search:read: Search messages, files, and so on
```

### Response
N/A (Schema Definition)
```

--------------------------------

### Initialize Husky for Git Hooks (Optional)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/development/setting-up

This command initializes Husky, a tool for managing Git hooks. This step is optional but recommended for maintaining code quality during development.

```bash
npx husky init
```

--------------------------------

### Enum with Descriptions for Items (YAML)

Source: https://swagger.io/docs/specification/data-models/enums

This example demonstrates how to provide detailed descriptions for each enum item within a parameter's definition. This enhances documentation for API consumers.

```yaml
parameters:
  - in: query
    name: sort
    schema:
      type: string
      enum: [asc, desc]
    description: >
      Sort order:
       * `asc` - Ascending, from A to Z
       * `desc` - Descending, from Z to A
```

--------------------------------

### OpenAPI Specification Structure

Source: https://swagger.io/docs/specification/basic-structure

An overview of the basic structure of an OpenAPI definition, including version, info, servers, and paths.

```APIDOC
## OpenAPI Specification Structure

### Overview
OpenAPI definitions can be written in YAML or JSON. The structure includes essential components like `openapi`, `info`, `servers`, and `paths`.

### OpenAPI Version
Specifies the version of the OpenAPI Specification used.
```yaml
openapi: 3.0.4
```

### Info Object
Contains metadata about the API.
```yaml
info:
  title: Sample API
  description: Optional multiline or single-line description in [CommonMark](http://commonmark.org/help/) or HTML.
  version: 0.1.9
```
- **title** (string): The name of the API.
- **description** (string): Extended information about the API, supporting Markdown.
- **version** (string): The version of the API.

### Servers Object
Defines the base URLs for the API.
```yaml
servers:
  - url: http://api.example.com/v1
    description: Optional server description, e.g. Main (production) server
  - url: http://staging-api.example.com
    description: Optional server description, e.g. Internal staging server for testing
```

### Paths Object
Defines the available endpoints and operations.
```yaml
paths:
  /users:
    get:
      summary: Returns a list of users.
      description: Optional extended description in CommonMark or HTML.
      responses:
        "200":
          description: A JSON array of user names
          content:
            application/json:
              schema:
                type: array
                items:
                  type: string
```
```

--------------------------------

### Cookie Header Example

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

An example of the Cookie header that the client must send in subsequent requests to the server to maintain authentication. This header includes the cookie name and value.

```http
Cookie: JSESSIONID=abcde12345
```

--------------------------------

### Generate Go Client with Swagger Codegen Docker

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This snippet demonstrates how to use the Swagger Codegen CLI Docker image to generate a Go client library. It requires Docker to be installed and involves mounting a local directory as a volume to store the generated output. The command specifies the input Swagger definition URL, the language ('go'), and the output directory.

```docker
docker run --rm -v ${PWD}:/local swaggerapi/swagger-codegen-cli-v3 generate \
    -i http://petstore.swagger.io/v2/swagger.json \
    -l go \
    -o /local/out/go
```

--------------------------------

### Implicit Flow Example (Base API)

Source: https://swagger.io/docs/specification/authentication/oauth2

An example of defining an OAuth2 security scheme using the 'implicit' flow, specifying the authorization URL and scopes for accessing data on the Base API.

```APIDOC
## Implicit Flow Example (Base API)

### Description
This example demonstrates the 'implicit' OAuth2 flow, which is used to obtain an access token directly from the authorization server. It includes the `authorizationUrl` and a set of scopes for accessing data on the Base API.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
```yaml
components:
  securitySchemes:
    oAuth2Implicit:
      type: oauth2
      description: For more information, see https://developers.getbase.com/docs/rest/articles/oauth2/requests
      flows:
        implicit:
          authorizationUrl: https://api.getbase.com/oauth2/authorize
          scopes:
            read: Grant read-only access to all your data except for the account and user info
            write: Grant write-only access to all your data except for the account and user info
            profile: Grant read-only access to the account and user info only
```

### Response
N/A (Schema Definition)
```

--------------------------------

### Example HTTP Request with Custom Headers (Multipart)

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

This is an example of an HTTP POST request using multipart/form-data that includes custom headers. It shows how the 'X-Custom-Header' defined in the OpenAPI schema is included in the request for the 'profileImage' part.

```http
POST /upload HTTP/1.1
Content-Length: 428
Content-Type: multipart/form-data; boundary=abcde12345

--abcde12345
Content-Disposition: form-data; name="id"
Content-Type: text/plain

123e4567-e89b-12d3-a456-426655440000
--abcde12345
Content-Disposition: form-data; name="profileImage"; filename="image1.png"
Content-Type: image/png
X-Custom-Header: x-header

{…file content…}
--abcde12345--
```

--------------------------------

### Enum with Descriptions

Source: https://swagger.io/docs/specification/data-models/enums

This example shows how to provide descriptions for individual enum values within a parameter definition.

```APIDOC
## GET /items with Described Enum

### Description
Retrieves a list of items, with a sort parameter that includes descriptions for its enum values.

### Method
GET

### Endpoint
/items

### Parameters
#### Query Parameters
- **sort** (string) - Optional - Sort order: * `asc` - Ascending, from A to Z * `desc` - Descending, from Z to A

### Request Example
```json
{
  "example": "GET /items?sort=desc"
}
```

### Response
#### Success Response (200)
- **items** (array) - A list of items.

#### Response Example
```json
{
  "example": {
    "items": [
      { "id": 2, "name": "Item 2" },
      { "id": 1, "name": "Item 1" }
    ]
  }
}
```
```

--------------------------------

### OpenAPI Server Templating for HTTP/HTTPS

Source: https://swagger.io/docs/specification/api-host-and-base-path

Provides examples of using server templating to specify both HTTP and HTTPS protocols. One example uses an enum for the protocol, while another relies on separate server entries without a default.

```yaml
servers:
  - url: http://api.example.com
  - url: https://api.example.com
```

```yaml
servers:
  - url: '{protocol}://api.example.com'
    variables:
      protocol:
        enum:
          - http
          - https
        default: https
```

--------------------------------

### Initialize Swagger UI in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

Demonstrates how to initialize Swagger UI in a JavaScript project using either ES6 imports or CommonJS `require`. It targets a DOM element with the ID '#myDomId' to render the UI.

```javascript
import SwaggerUI from 'swagger-ui'
// or use require if you prefer
const SwaggerUI = require('swagger-ui')

SwaggerUI({
  dom_id: '#myDomId'
})
```

--------------------------------

### Example HTTP Request for Multipart Data

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

An example of an HTTP POST request demonstrating a multipart/form-data payload. It includes boundaries to separate different data parts like a UUID, a JSON object, and binary file content.

```http
POST /upload HTTP/1.1
Content-Length: 428
Content-Type: multipart/form-data; boundary=abcde12345

--abcde12345
Content-Disposition: form-data; name="id"
Content-Type: text/plain

123e4567-e89b-12d3-a456-426655440000
--abcde12345
Content-Disposition: form-data; name="address"
Content-Type: application/json

{
  "street": "3, Garden St",
  "city": "Hillsbery, UT"
}
--abcde12345
Content-Disposition: form-data; name="profileImage "; filename="image1.png"
Content-Type: application/octet-stream

{…file content…}
--abcde12345--
```

--------------------------------

### Embed Swagger UI Basic HTML with unpkg

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation

This snippet shows how to embed Swagger UI into an HTML page using unpkg. It includes the necessary HTML structure, CSS, and JavaScript to load the Swagger UI bundle and initialize it with a specified OpenAPI URL. No external build tools are required.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="SwaggerUI" />
  <title>SwaggerUI</title>
  <link rel="stylesheet" href="https://unpkg.com/swagger-ui-dist@5.11.0/swagger-ui.css" />
</head>
<body>
<div id="swagger-ui"></div>
<script src="https://unpkg.com/swagger-ui-dist@5.11.0/swagger-ui-bundle.js" crossorigin></script>
<script>
  window.onload = () => {
    window.ui = SwaggerUIBundle({
      url: 'https://petstore3.swagger.io/api/v3/openapi.json',
      dom_id: '#swagger-ui',
    });
  };
</script>
</body>
</html>
```

--------------------------------

### Set JAVA_HOME for Java 11 on OS X

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/prerequisites

Sets the JAVA_HOME environment variable to point to the Java 11 installation and updates the system's PATH. This is necessary for building Swagger Codegen from source or running applications that require a specific Java version on macOS. Requires Java 11 to be installed.

```bash
export JAVA_HOME=`/usr/libexec/java_home -v 11`
export PATH=${JAVA_HOME}/bin:$PATH
```

--------------------------------

### Define a Reducer in a Plugin

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This JavaScript example illustrates how to define a reducer within a Swagger UI plugin. The `MyReducerPlugin` provides a reducer for the `EXAMPLE_SET_FAV_COLOR` action type within the `example` state namespace. The reducer takes the current state and action, and returns a new state by updating the `favColor` property.

```javascript
const MyReducerPlugin = function(system) {
  return {
    statePlugins: {
      example: {
        reducers: {
          "EXAMPLE_SET_FAV_COLOR": (state, action) => {
            // you're only working with the state under the namespace, in this case "example".
            // So you can do what you want, without worrying about /other/ namespaces
            return state.set("favColor", action.payload)
          }
        }
      }
    }
  }
}
```

--------------------------------

### OpenAPI Serialization and RFC 6570

Source: https://swagger.io/docs/specification/serialization

Explains the mapping between OpenAPI serialization keywords (style, explode, allowReserved) and RFC 6570 URI template modifiers, providing an example of path and query parameter construction.

```APIDOC
## OpenAPI Serialization and RFC 6570

### Description
OpenAPI serialization rules are based on RFC 6570 URI templates. This section maps OpenAPI keywords to URI template modifiers and provides an example of constructing a URI template for path and query parameters.

### Method
GET

### Endpoint
`/users{id}`

### Parameters
#### Path Parameters
- **id** (array of integers) - Required - An array of user IDs.
  - `style`: `matrix`
  - `explode`: `true`

#### Query Parameters
- **metadata** (boolean) - Optional - Metadata flag.
  - `style`: `form` (default)
  - `explode`: `false` (default)

### Request Example
```
GET /users;id=3;id=4?metadata=true
```

### Response
#### Success Response (200)
- **description** (string) - Description of the response.

#### Response Example
```json
{
  "description": "A list of users"
}
```
```

--------------------------------

### Generate PHP API Client using Swagger Codegen (Maven)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This example demonstrates how to generate a PHP API client using Swagger Codegen. It involves cloning the repository, checking out a specific version, building the project with Maven, and then executing the codegen CLI tool with the input OpenAPI specification, language, and output directory.

```shell
git clone https://github.com/swagger-api/swagger-codegen
cd swagger-codegen
git checkout 3.0.0
mvn clean package
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
   -i http://petstore.swagger.io/v2/swagger.json \
   -l php \
   -o /var/tmp/php_api_client
```

--------------------------------

### POST /users

Source: https://swagger.io/docs/specification/paths-and-operations

Creates a new user.

```APIDOC
## POST /users

### Description
Creates a new user in the system.

### Method
POST

### Endpoint
/users

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **id** (integer) - Required - The unique identifier for the user.
- **name** (string) - Required - The name of the user.
```

--------------------------------

### Example: Create User Operation (HTTP Response)

Source: https://swagger.io/docs/specification/links

This snippet shows a successful HTTP response (201 Created) after a user creation request. It returns a JSON object containing the ID of the newly created user, which can be used in subsequent operations.

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 305
}
```

--------------------------------

### GET /users

Source: https://swagger.io/docs/specification/describing-parameters

Retrieves a list of users. Supports pagination using offset and limit parameters.

```APIDOC
## GET /users

### Description
Retrieves a list of users. Supports pagination using offset and limit parameters.

### Method
GET

### Endpoint
/users

### Parameters
#### Query Parameters
- **offset** (integer) - Optional - The number of items to skip before starting to collect the result set.
- **limit** (integer) - Optional - The numbers of items to return. (default: 20, maximum: 50)

### Response
#### Success Response (200)
- **description** (string) - OK

#### Response Example
{
  "example": "{\"users\": [{}, {}]}"
}
```

--------------------------------

### Using Relative URLs for Authorization Endpoints

Source: https://swagger.io/docs/specification/authentication/oauth2

This example illustrates how to specify authorization, token, and refresh URLs as relative paths within the `servers` object, which are then resolved against the base API server URL.

```APIDOC
## Using Relative URLs for Authorization Endpoints

### Description
In OpenAPI 3.0, `authorizationUrl`, `tokenUrl`, and `refreshUrl` can be defined as relative paths. These relative URLs are resolved against the server URL defined in the `servers` object, simplifying configuration when these endpoints reside on the same host.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
```yaml
servers:
  - url: https://api.example.com/v2

components:
  securitySchemes:
    oauth2sample:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: /oauth/authorize
          tokenUrl: /oauth/token
          scopes: ...
```

### Response
N/A (Schema Definition)
```

--------------------------------

### Run Swagger Generator Docker Image with Custom Options

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This example demonstrates how to run the official Swagger Generator Docker image, configuring memory, HTTP port, and hidden options. It shows how to pass hidden options directly as an environment variable or via a mounted volume containing a `hiddenOptions.yaml` file. It also illustrates mounting a volume for custom generators.

```bash
docker run -e "HIDDEN_OPTIONS=servers:foo,bar|clientsV3:fgf,sdsd" -e "JAVA_MEM=1024m" -e "HTTP_PORT=80" -p 80:80 --name swagger-generator-v3 -v /tmp:/jetty_home/lib/shared swaggerapi/swagger-generator-v3
docker run -e "HIDDEN_OPTIONS_PATH=/hiddenOptions.yaml" -e "JAVA_MEM=1024m" -e "HTTP_PORT=80" -p 80:80 --name swagger-generator-v3  -v /tmp:/jetty_home/lib/shared swaggerapi/swagger-generator-v3
docker run -e "HIDDEN_OPTIONS_PATH=/hiddenOptions.yaml" -e "JAVA_MEM=1024m" -e "HTTP_PORT=80" -p 80:80 --name swagger-generator-v3 -v /my/custom:/jetty_home/lib/shared swaggerapi/swagger-generator-v3
```

--------------------------------

### Define an Action in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This example defines a basic action, `updateSpec`, within a plugin's `statePlugins`. Actions are functions that typically return an object with a `type` and `payload`, used for updating the system's state.

```javascript
// FYI: in an actual Swagger UI, `updateSpec` is already defined in the core code
// it's just here for clarity on what's behind the scenes
const MySpecPlugin = function(system) {
  return {
    statePlugins: {
      spec: {
        actions: {
          updateSpec: (str) => {
            return {
              type: "SPEC_UPDATE_SPEC",
              payload: str
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### GET /report - Returns a PDF report

Source: https://swagger.io/docs/specification/describing-responses

This endpoint returns a PDF file as a response. The file content is defined as a binary string.

```APIDOC
## GET /report

### Description
Returns the report in the PDF format.

### Method
GET

### Endpoint
/report

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Body
None

### Response
#### Success Response (200)
- **application/pdf** (string, format: binary) - Description: A PDF file

#### Response Example
(Binary file content)
```

--------------------------------

### 401 Unauthorized Response Handling

Source: https://swagger.io/docs/specification/authentication/basic-authentication

Example of defining a 401 Unauthorized response in OpenAPI 3.0 for missing or invalid credentials.

```APIDOC
## 401 Unauthorized Response Handling

### Description
This example illustrates how to define a standard 401 "Unauthorized" response within an OpenAPI 3.0 specification. It includes the `WWW-Authenticate` header and shows how to reference a globally defined response.

### Method
N/A (This is an OpenAPI specification example)

### Endpoint
N/A

### Parameters
None

### Request Example
```yaml
paths:
  /something:
    get:
      ...
      responses:
        ...
        '401':
            $ref: '#/components/responses/UnauthorizedError'
    post:
      ...
      responses:
        ...
        '401':
          $ref: '#/components/responses/UnauthorizedError'
...
components:
  responses:
    UnauthorizedError:
      description: Authentication information is missing or invalid
      headers:
        WWW_Authenticate:
          schema:
            type: string
```

### Response
#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### API Information Metadata (Info Object)

Source: https://swagger.io/docs/specification/basic-structure

Provides essential metadata about the API, including its title, an optional description, and the API version. The description supports CommonMark and HTML for rich text formatting.

```yaml
info:
  title: Sample API
  description: Optional multiline or single-line description in [CommonMark](http://commonmark.org/help/) or HTML.
  version: 0.1.9

```

--------------------------------

### GET /logo

Source: https://swagger.io/docs/specification/describing-responses

Retrieves the API logo in PNG format.

```APIDOC
## GET /logo

### Description
Retrieves the API logo image in PNG format.

### Method
GET

### Endpoint
/logo

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **Logo image** (binary) - The API logo image file in PNG format.

#### Response Example
(Binary image data)
```

--------------------------------

### Applying Security Schemes

Source: https://swagger.io/docs/specification/authentication

After defining security schemes, you can apply them globally to all API operations or individually to specific operations using the `security` keyword. This example shows global application requiring either an API key or OAuth 2.

```APIDOC
## Applying Security Schemes

After defining the security schemes in the `securitySchemes` section, you can apply them to the whole API or individual operations by adding the `security` section on the root level or operation level, respectively. When used on the root level, `security` applies the specified security schemes globally to all API operations, unless overridden on the operation level.

### Example (Global Security):
```yaml
security:
  - ApiKeyAuth: []
  - OAuth2:
      - read
      - write
```

*Note: For schemes like OAuth 2 and OpenID Connect, specify the required scopes. For others like API keys, use an empty array `[]`.*

### Example (Operation-Level Security Override):
```yaml
paths:
  /billing_info:
    get:
      summary: Gets the account billing info
      security:
        - OAuth2: [admin] # Use OAuth with a different scope
      responses:
        "200":
          description: OK
        "401":
          description: Not authenticated
        "403":
          description: Access token does not have the required scope

  /ping:
    get:
      summary: Checks if the server is running
      security: [] # No security
      responses:
        "200":
          description: Server is up and running
        default:
          description: Something is wrong
```
```

--------------------------------

### Applying Scopes at the Root Level

Source: https://swagger.io/docs/specification/authentication/oauth2

This example shows how to apply a security scheme and its scopes to all API operations by defining it at the root level of the OpenAPI document.

```APIDOC
## Applying Scopes at the Root Level

### Description
If all API operations share the same security requirements, you can define the `security` keyword at the root level of your OpenAPI document. This applies the specified security scheme and scopes to every operation.

### Method
N/A (Applies to all methods)

### Endpoint
N/A (Applies to all endpoints)

### Parameters
N/A

### Request Example
```yaml
security:
  - oAuthSample: [write_pets]

# ... rest of the OpenAPI document
```

### Response
N/A
```

--------------------------------

### Defining API Without Scopes

Source: https://swagger.io/docs/specification/authentication/oauth2

This example demonstrates how to configure security schemes when an API does not utilize scopes, by specifying empty objects and lists.

```APIDOC
## Defining API Without Scopes

### Description
This example shows how to configure security schemes for an API that does not employ scopes. This is achieved by defining an empty object `{}` for scopes in the security scheme and an empty list `[]` in the `security` section.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
```yaml
components:
  securitySchemes:
    oAuthNoScopes:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://api.example.com/oauth2/authorize
          scopes: {}

security:
  - oAuthNoScopes: []
```

### Response
N/A (Schema Definition)
```

--------------------------------

### Compile and Run Java Petstore Client

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

After generating the Java client library, these commands navigate to the output directory and use Maven to compile the code and run unit tests. This ensures the generated client is functional.

```bash
cd samples/client/petstore/java
mvn package
```

--------------------------------

### Specify Multiple Response Media Types (YAML)

Source: https://swagger.io/docs/specification/describing-responses

This example demonstrates how to define an API operation that can return responses in multiple media types, such as JSON, XML, and plain text. It uses the `content` keyword to list the available types and their corresponding schemas.

```yaml
paths:
  /users:
    get:
      summary: Get all users
      responses:
        "200":
          description: A list of users
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/ArrayOfUsers"
            application/xml:
              schema:
                $ref: "#/components/schemas/ArrayOfUsers"
            text/plain:
              schema:
                type: string
```

--------------------------------

### Swagger/OpenAPI 'not' Keyword - Valid Example

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This example shows a valid request body according to the schema using the 'not' keyword. The 'pet_type' is a string ('Cat'), which is not an integer, thus satisfying the 'not' condition.

```json
{ "pet_type": "Cat" }
```

--------------------------------

### GET /info/logo - Wildcard Media Type

Source: https://swagger.io/docs/specification/media-types

Retrieves an image logo using a wildcard media type.

```APIDOC
## GET /info/logo

### Description
Retrieves an image logo. The `image/*` placeholder indicates that the server will use a consistent data structure for any image format response.

### Method
GET

### Endpoint
/info/logo

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **schema**: binary (string format)

#### Response Example
(Binary data representing an image, e.g., PNG, JPEG)

**Note**: The `Content-Type` header will specify the actual image format (e.g., `image/png`), not `image/*`.
```

--------------------------------

### GET /employees - Multiple Media Types

Source: https://swagger.io/docs/specification/media-types

Retrieves a list of employees, supporting both JSON and XML formats.

```APIDOC
## GET /employees

### Description
Returns a list of employees, supporting multiple media types like JSON and XML.

### Method
GET

### Endpoint
/employees

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **id** (integer) - Unique identifier for the employee.
- **name** (string) - The name of the employee.
- **fullTime** (boolean) - Indicates if the employee is full-time.

#### Response Example (application/json)
```json
{
  "id": 1,
  "name": "John Doe",
  "fullTime": true
}
```

#### Response Example (application/xml)
```xml
<employee>
  <id>1</id>
  <name>John Doe</name>
  <fullTime>true</fullTime>
</employee>
```
```

--------------------------------

### GET /users

Source: https://swagger.io/docs/specification/describing-responses

Retrieves a list of users, supporting JSON, XML, and plain text formats.

```APIDOC
## GET /users

### Description
Retrieves a list of all users. The response can be in JSON, XML, or plain text format.

### Method
GET

### Endpoint
/users

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **A list of users** - The response contains a list of users, format depends on the `Accept` header.

#### Response Example (JSON)
```json
{
  "users": [
    {
      "id": 1,
      "username": "user1"
    },
    {
      "id": 2,
      "username": "user2"
    }
  ]
}
```

#### Response Example (XML)
```xml
<users>
  <user>
    <id>1</id>
    <username>user1</username>
  </user>
  <user>
    <id>2</id>
    <username>user2</username>
  </user>
</users>
```

#### Response Example (Text)
```
user1,user2
```
```

--------------------------------

### Get General Swagger Codegen Options (CLI)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This command displays a list of general options available for the Swagger Codegen CLI tool. It's useful for understanding the overall capabilities and parameters you can use during code generation.

```shell
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate --help
```

--------------------------------

### GET /teams

Source: https://swagger.io/docs/specification/describing-parameters

Retrieves a list of teams. Supports pagination using offset and limit parameters.

```APIDOC
## GET /teams

### Description
Retrieves a list of teams. Supports pagination using offset and limit parameters.

### Method
GET

### Endpoint
/teams

### Parameters
#### Query Parameters
- **offset** (integer) - Optional - The number of items to skip before starting to collect the result set.
- **limit** (integer) - Optional - The numbers of items to return. (default: 20, maximum: 50)

### Response
#### Success Response (200)
- **description** (string) - OK

#### Response Example
{
  "example": "{\"teams\": [{}, {}]}"
}
```

--------------------------------

### GET /report

Source: https://swagger.io/docs/specification/describing-parameters

Generates a report. Accepts either a relative date range or an exact date range.

```APIDOC
## GET /report

### Description
Generates a report. Accepts either a relative date range or an exact date range.

### Method
GET

### Endpoint
/report

### Parameters
#### Query Parameters
- **rdate** (string) - Optional - A relative date range for the report, such as `Today` or `LastWeek`. For an exact range, use `start_date` and `end_date` instead.
- **start_date** (string) - Optional - The start date for the report. Must be used together with `end_date`. This parameter is incompatible with `rdate`.
- **end_date** (string) - Optional - The end date for the report. Must be used together with `start_date`. This parameter is incompatible with `rdate`.

### Response
#### Error Response (400)
- **description** (string) - Either `rdate` or `start_date`+`end_date` are required.

#### Response Example
{
  "example": "{\"error\": \"Either rdate or start_date+end_date are required.\"}"
}
```

--------------------------------

### Describing Multiple API Keys (AND Logic)

Source: https://swagger.io/docs/specification/authentication/api-keys

Shows how to define and apply multiple API key security schemes that must both be present for authentication (logical AND). This is achieved by listing them in the same array item within the `security` section.

```yaml
components:
  securitySchemes:
    apiKey:
      type: apiKey
      in: header
      name: X-API-KEY
    appId:
      type: apiKey
      in: header
      name: X-APP-ID
security:
  - apiKey: []
    appId: []
```

--------------------------------

### Swagger/OpenAPI 'not' Keyword - Invalid Example

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This example shows an invalid request body according to the schema using the 'not' keyword. The 'pet_type' is an integer (11), which violates the 'not' condition that it should not be an integer.

```json
{ "pet_type": 11 }
```

--------------------------------

### GET /api/options?language={language}&version={codegenVersion}

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

Retrieves the available language-specific options for code generation.

```APIDOC
## GET /api/options

### Description
Retrieves a list of available configuration options for customizing the code generation for a specific language and codegen version.

### Method
GET

### Endpoint
https://generator3.swagger.io/api/options

### Parameters
#### Query Parameters
- **language** (string) - Required - The programming language for which to retrieve options (e.g., "java").
- **version** (string) - Required - The codegen version (e.g., "V3").

### Request Example
```bash
curl https://generator3.swagger.io/api/options?language=java&version=V3
```

### Response
#### Success Response (200)
- **options** (object) - An object where keys are option names and values contain details about each option (e.g., `opt`, `description`, `type`, `default`).

#### Response Example
```json
{
  "sortParamsByRequiredFlag": {
    "opt": "sortParamsByRequiredFlag",
    "description": "Sort method arguments to place required parameters before optional parameters.",
    "type": "boolean",
    "default": "true"
  },
  "ensureUniqueParams": {
    "opt": "ensureUniqueParams",
    "description": "Whether to ensure parameter names are unique in an operation (rename parameters that are not).",
    "type": "boolean",
    "default": "true"
  },
  "allowUnicodeIdentifiers": {
    "opt": "allowUnicodeIdentifiers",
    "description": "boolean, toggles whether unicode identifiers are allowed in names or not, default is false",
    "type": "boolean",
    "default": "false"
  },
  "modelPackage": {
    "opt": "modelPackage",
    "description": "package for generated models",
    "type": "string"
  }
}
```
```

--------------------------------

### OpenAPI Links Section Example

Source: https://swagger.io/docs/specification/links

Demonstrates the 'links' section within an OpenAPI response definition, showing how to associate a link named 'GetUserByUserId' to the 'getUser' operation. It specifies how to extract the 'userId' from the response body using a runtime expression.

```yaml
responses:
  "200":
    description: Created
    content: ...
    links: # <----
      ...
  "400":
    description: Bad request
    content: ...
    links: # <----
      ...
```

--------------------------------

### Override Security for Specific Operations (YAML)

Source: https://swagger.io/docs/specification/authentication

This YAML demonstrates how to override global security settings for individual API operations. The '/billing_info' GET operation uses OAuth2 with an 'admin' scope, while the '/ping' GET operation has no security applied.

```yaml
paths:
  /billing_info:
    get:
      summary: Gets the account billing info
      security:
        - OAuth2: [admin] # Use OAuth with a different scope
      responses:
        "200":
          description: OK
        "401":
          description: Not authenticated
        "403":
          description: Access token does not have the required scope

  /ping:
    get:
      summary: Checks if the server is running
      security: [] # No security
      responses:
        "200":
          description: Server is up and running
        default:
          description: Something is wrong
```

--------------------------------

### Describe Request Body with Wildcard Media Type (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This YAML example shows how to use a wildcard media type (`image/*`) for a request body in OpenAPI 3.0. This allows the API to accept various image formats for an avatar upload, with a schema defining the content as binary data.

```yaml
paths:
  /avatar:
    put:
      summary: Upload an avatar
      requestBody:
        content:
          image/*:
            schema:
              type: string
              format: binary
```

--------------------------------

### Applying Scopes to API Operations

Source: https://swagger.io/docs/specification/authentication/oauth2

This example shows how to apply a defined OAuth2 security scheme and its scopes to a specific API operation using the `security` keyword.

```APIDOC
## Applying Scopes to API Operations

### Description
This example illustrates how to associate a previously defined security scheme (e.g., 'oAuthSample') with specific scopes (e.g., `[write_pets]`) to an individual API operation (e.g., PATCH /pets/{petId}).

### Method
PATCH

### Endpoint
/pets/{petId}

### Parameters
#### Path Parameters
- **petId** (string) - Required - The ID of the pet to update.

#### Query Parameters
N/A

#### Request Body
N/A (Assumed to be handled by the operation's specific schema)

### Request Example
```yaml
paths:
  /pets/{petId}:
    patch:
      summary: Updates a pet in the store
      security:
        - oAuthSample: [write_pets]
      # ... other operation details
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation of the update.

#### Response Example
```json
{
  "message": "Pet updated successfully."
}
```
```

--------------------------------

### fn: Add Helper Functions to System in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

The `fn` interface allows developers to add helper functions to the Swagger.io system for use elsewhere. This example demonstrates adding the `left-pad` function as a helper.

```javascript
import leftPad from "left-pad"

const MyFnPlugin = function(system) {
  return {
    fn: {
      leftPad: leftPad
    }
  }
}
```

--------------------------------

### Download Swagger Codegen CLI using wget

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/prerequisites

Downloads the Swagger Codegen CLI JAR file using the wget command. This is a common method for downloading files from a URL on Linux-like systems. Requires wget to be installed.

```bash
wget https://repo1.maven.org/maven2/io/swagger/codegen/v3/swagger-codegen-cli/3.0.71/swagger-codegen-cli-3.0.71.jar -O swagger-codegen-cli.jar
```

--------------------------------

### GET /users

Source: https://swagger.io/docs/specification/describing-responses

Retrieves a list of users. It can return a successful response with an array of users or an unauthorized response.

```APIDOC
## GET /users

### Description
Retrieves a list of users. This endpoint can return a successful response containing an array of users or an unauthorized response if the request is not properly authenticated.

### Method
GET

### Endpoint
/users

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **ArrayOfUsers** (object) - An array of user objects.

#### Error Response (401)
- **Unauthorized** (object) - Indicates that the request lacks valid authentication credentials.

#### Response Example (200)
```json
{
  "example": "[ { \"id\": \"user123\", \"name\": \"John Doe\" } ]"
}
```

#### Response Example (401)
```json
{
  "example": "{\"code\": \"UNAUTHORIZED\", \"message\": \"Authentication failed\"}"
}
```
```

--------------------------------

### Custom componentDidCatch with Bugsnag

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

An example of overriding the default `componentDidCatch` function to integrate with a third-party error tracking service like Bugsnag. This allows for centralized error reporting.

```javascript
const BugsnagErrorHandlerPlugin = () => {
  // init bugsnag
  return {
    fn: {
      componentDidCatch = (error, info) => {
        Bugsnag.notify(error);
        Bugsnag.notify(info);
      },
    },
  };
};
```

--------------------------------

### GET /users/{id}

Source: https://swagger.io/docs/specification/paths-and-operations

Retrieves a specific user by their ID.

```APIDOC
## GET /users/{id}

### Description
Retrieves a specific user by their unique ID.

### Method
GET

### Endpoint
/users/{id}

### Parameters
#### Path Parameters
- **id** (integer) - Required - The unique identifier for the user.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier for the user.
- **name** (string) - The name of the user.

#### Response Example
```json
{
  "id": 123,
  "name": "John Doe"
}
```
```

--------------------------------

### GET /user/{userId}

Source: https://swagger.io/docs/specification/links

Retrieves a specific user by their ID.

```APIDOC
## GET /user/{userId}

### Description
Retrieves a specific user by their ID.

### Method
GET

### Endpoint
/user/{userId}

### Parameters
#### Path Parameters
- **userId** (integer) - Required - The ID of the user to retrieve.

### Response
#### Success Response (200)
- **(object)** - The user object.

#### Response Example
```json
{
  "id": 123,
  "username": "johndoe",
  "email": "john.doe@example.com"
}
```
```

--------------------------------

### Server URL Definitions

Source: https://swagger.io/docs/specification/basic-structure

Specifies the base URLs for the API servers. Multiple servers can be defined, allowing for different environments like production and staging. All API paths are relative to these base URLs.

```yaml
servers:
  - url: http://api.example.com/v1
    description: Optional server description, e.g. Main (production) server
  - url: http://staging-api.example.com
    description: Optional server description, e.g. Internal staging server for testing

```

--------------------------------

### Execute Swagger Codegen CLI Commands in Docker

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This shows how to use `run-in-docker.sh` as an executable for the `swagger-codegen-cli`. It covers basic commands like 'help' and 'langs', as well as generating a Go client by specifying input OpenAPI specification, language, output directory, and package name.

```bash
./run-in-docker.sh help
./run-in-docker.sh langs
./run-in-docker.sh /gen/bin/go-petstore.sh
./run-in-docker.sh generate -i modules/swagger-codegen/src/test/resources/2_0/petstore.yaml -l go -o /gen/out/go-petstore -DpackageName=petstore
```

--------------------------------

### Defining OAuth2 Security Schemes with Scopes

Source: https://swagger.io/docs/specification/authentication/oauth2

This example demonstrates how to define an OAuth2 security scheme with 'implicit' flow and associated scopes in the `components/securitySchemes` section.

```APIDOC
## Defining OAuth2 Security Schemes with Scopes

### Description
This section shows how to define an OAuth2 security scheme, specifying the flow type (e.g., 'implicit'), the authorization URL, and the available scopes with their descriptions.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
```yaml
components:
  securitySchemes:
    oAuthSample:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://api.example.com/oauth2/authorize
          scopes:
            read_pets: read pets in your account
            write_pets: modify pets in your account
```

### Response
N/A (Schema Definition)

### Response Example
N/A
```

--------------------------------

### GET /employees - Schema Reference

Source: https://swagger.io/docs/specification/media-types

Retrieves a list of employees using a shared schema definition for JSON and XML.

```APIDOC
## GET /employees (Schema Reference)

### Description
Retrieves a list of employees using a shared schema definition, ensuring consistent data structure for JSON and XML responses.

### Method
GET

### Endpoint
/employees

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **id** (integer) - Unique identifier for the employee.
- **name** (string) - The name of the employee.
- **fullTime** (boolean) - Indicates if the employee is full-time.

#### Response Example (application/json)
```json
{
  "id": 1,
  "name": "John Doe",
  "fullTime": true
}
```

#### Response Example (application/xml)
```xml
<employee>
  <id>1</id>
  <name>John Doe</name>
  <fullTime>true</fullTime>
</employee>
```

### Components
#### Schemas
##### Employee
- **type**: object
- **properties**:
  - **id** (integer)
  - **name** (string)
  - **fullTime** (boolean)
```

--------------------------------

### Combine Multiple Authentication Types with Logical OR

Source: https://swagger.io/docs/specification/authentication

This snippet shows how to define alternative authentication methods using the logical OR operator. The 'security' array contains multiple security scheme definitions, where any one of them can be used for authentication. This example uses Basic Authentication and an API Key as alternatives.

```yaml
security:
  - basicAuth: []
  - apiKey: []
```

--------------------------------

### OpenAPI: Response Headers Definition

Source: https://swagger.io/docs/specification/describing-responses

Defines custom response headers for an API operation. This example shows how to specify schemas and descriptions for headers like `X-RateLimit-Limit`, `X-RateLimit-Remaining`, and `X-RateLimit-Reset`.

```yaml
paths:
  /ping:
    get:
      summary: Checks if the server is alive.
      responses:
        "200":
          description: OK
          headers:
            X-RateLimit-Limit:
              schema:
                type: integer
              description: Request limit per hour.
            X-RateLimit-Remaining:
              schema:
                type: integer
              description: The number of requests left for the time window.
            X-RateLimit-Reset:
              schema:
                type: string
                format: date-time
              description: The UTC date/time at which the current rate limit window resets.
```

--------------------------------

### Customize Java API Client Generation with Options using curl

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

This example shows how to customize the generated Java API client by providing language-specific options in the HTTP request body. It includes `additionalProperties` like `useRuntimeException` and `useRxJava` to configure the generated code. The `options` object allows fine-grained control over the generation process.

```bash
curl -X POST \
  https://generator3.swagger.io/api/generate \
  -H 'content-type: application/json' \
  -d '{
  "specURL" : "https://raw.githubusercontent.com/OAI/OpenAPI-Specification/master/examples/v3.0/petstore.yaml",
  "lang" : "java",
  "options" : {
    "additionalProperties" : {
    "useRuntimeException": true,
    "useRxJava" : true
    }
  },
  "type" : "CLIENT",
  "codegenVersion" : "V3"
}'
```

--------------------------------

### Using Links with Parameters and Hard-coded Values (YAML)

Source: https://swagger.io/docs/specification/links

Provides an example of defining a link (`ReportRelDate`) that calls the `getReport` operation. It demonstrates passing a parameter (`rdate`) derived from the response body and providing hard-coded empty strings for other parameters (`start_date`, `end_date`).

```yaml
links:
  ReportRelDate:
    operationId: getReport
    parameters:
      rdate: '$response.body#/1'
      start_date: ''
      end_date: ''
```

--------------------------------

### Define Memoized Selector with Reselect in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This example demonstrates how to define a memoized selector using the Reselect library. Memoization is recommended for frequently used selectors to improve performance by caching results. The `createSelector` function from Reselect is used for this purpose.

```javascript
import { createSelector } from "reselect"

const MySelectorPlugin = function(system) {
  return {
    statePlugins: {
      example: {
        selectors: {
          // this selector will be memoized after it is run once for a
          // value of `state`
          myFavoriteColor: createSelector((state) => state.get("favColor"))
        }
      }
    }
  }
}
```

--------------------------------

### Define Dictionary with Schema Reference

Source: https://swagger.io/docs/specification/data-models/dictionaries

This example demonstrates defining a dictionary where the value type is referenced from another schema using `$ref`. The `Messages` schema uses `additionalProperties` to point to the `Message` schema.

```yaml
components:
  schemas:
    Messages: # <---- dictionary
      type: object
      additionalProperties:
        $ref: "#/components/schemas/Message"

    Message:
      type: object
      properties:
        code:
          type: integer
        text:
          type: string
```

--------------------------------

### Defining a 401 Unauthorized Response

Source: https://swagger.io/docs/specification/authentication/api-keys

Provides an example of how to define a standard 401 Unauthorized response, including the `WWW-Authenticate` header, within the OpenAPI specification. This response can be referenced using `$ref` for consistency across operations.

```yaml
paths:
  /something:
    get:
      ...
      responses:
        ...
        '401':
            $ref: "#/components/responses/UnauthorizedError"
    post:
      ...
      responses:
        ...
        '401':
          $ref: "#/components/responses/UnauthorizedError"
components:
  responses:
    UnauthorizedError:
      description: API key is missing or invalid
      headers:
        WWW_Authenticate:
          schema:
            type: string
```

--------------------------------

### Apply OpenID Connect Security Per Operation in OpenAPI

Source: https://swagger.io/docs/specification/authentication/openid-connect-discovery

This OpenAPI 3.0 snippet illustrates how to apply an OpenID Connect security scheme to specific API operations. It shows how to define security requirements for 'get' and 'delete' operations on the '/pets/{petId}' path, each with different scopes.

```yaml
paths:
  /pets/{petId}:
    get:
      summary: Get a pet by ID
      security:
        - openId:
          - pets_read
      ...
    delete:
      summary: Delete a pet by ID
      security:
        - openId:
          - pets_write
      ...
```

--------------------------------

### Initialize Swagger UI with Configuration Object

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Demonstrates how to initialize Swagger UI by passing a configuration object directly as an argument. This method allows for setting various parameters like 'dom_id', 'url', and 'spec' to customize the UI's behavior and data source.

```javascript
const ui = SwaggerUI({
  dom_id: '#swagger-ui',
  url: "https://petstore.swagger.io/v2/swagger.json",
  spec: { ... } // Optional: Provide OpenAPI definition object directly
});
```

--------------------------------

### GET /employees

Source: https://swagger.io/docs/specification/media-types

This endpoint retrieves a list of employees. The response is in JSON format and includes employee ID, name, and full-time status.

```APIDOC
## GET /employees

### Description
Returns a list of employees.

### Method
GET

### Endpoint
/employees

### Parameters

#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier for the employee.
- **name** (string) - The name of the employee.
- **fullTime** (boolean) - Indicates if the employee is full-time.

#### Response Example
```json
{
  "id": 1,
  "name": "Jessica Right",
  "fullTime": true
}
```
```

--------------------------------

### Generate Code with Minimal Swagger Generator Docker Image via API

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This snippet shows how to use the minimal Swagger Generator Docker image as a self-hosted API for code generation. It details starting the container, retrieving its IP address, sending a POST request with generation parameters (spec URL, language, type, codegen version), and then shutting down the container. The generated code is saved as `result.zip`.

```bash
# Start container and save the container id
CID=$(docker run -d swaggerapi/swagger-generator-v3-minimal)
# allow for startup
sleep 5
# Get the IP of the running container
GEN_IP=$(docker inspect --format '{{.NetworkSettings.IPAddress}}'  $CID)
# Execute an HTTP request and store the download link
curl -X POST \
           http://localhost:8080/api/generate \
           -H 'content-type: application/json' \
           -d '{ \
           "specURL" : "https://raw.githubusercontent.com/OAI/OpenAPI-Specification/master/examples/v3.0/petstore.yaml", \
           "lang" : "jaxrs-jersey", \
           "type" : "SERVER", \
           "codegenVersion" : "V3" \
         }' > result.zip
# Shutdown the swagger generator image
docker stop $CID && docker rm $CID
```

--------------------------------

### Defining 401 Unauthorized Response in OpenAPI

Source: https://swagger.io/docs/specification/authentication/basic-authentication

This OpenAPI 3.0 example illustrates how to define a 401 'Unauthorized' response, including the 'WWW-Authenticate' header. The response is defined in the global 'components/responses' section and referenced using '$ref' in the path operations.

```yaml
paths:
  /something:
    get:
      ...
      responses:
        ...
        '401':
            $ref: '#/components/responses/UnauthorizedError'
    post:
      ...
      responses:
        ...
        '401':
          $ref: '#/components/responses/UnauthorizedError'
...
components:
  responses:
    UnauthorizedError:
      description: Authentication information is missing or invalid
      headers:
        WWW_Authenticate:
          schema:
            type: string
```

--------------------------------

### GET /items

Source: https://swagger.io/docs/specification/links

This endpoint retrieves a list of items, potentially with pagination using cursors. The response includes metadata for navigating through data sets.

```APIDOC
## GET /items

### Description
Retrieves a list of items. Supports pagination using a cursor parameter to fetch subsequent or previous data sets.

### Method
GET

### Endpoint
/items

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return per page.
- **cursor** (string) - Optional - A cursor value used for pagination to retrieve the next or previous set of items.

### Response
#### Success Response (200 OK)
- **metadata** (object) - Contains pagination information.
  - **previous** (string) - Optional - A cursor for the previous page, or null if on the first page.
  - **next** (string) - Optional - A cursor for the next page, or null if on the last page.
  - **count** (integer) - The number of items returned in this response.
- **[items]** (array) - An array of item objects.

#### Response Example
```json
{
  "metadata": {
    "previous": null,
    "next": "Q1MjAwNz",
    "count": 10
  },
  "items": [
    // ... item objects ...
  ]
}
```
```

--------------------------------

### URL Encoded Form Data Example

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Illustrates the raw HTTP POST request payload for `application/x-www-form-urlencoded` data. It shows key-value pairs formatted for submission.

```http
POST /survey HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 28

name=Amy+Smith&fav_number=42
```

--------------------------------

### Download Swagger Codegen CLI using PowerShell

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/prerequisites

Downloads the Swagger Codegen CLI JAR file using PowerShell's Invoke-WebRequest cmdlet. This is the recommended method for Windows users who do not have wget installed. Requires PowerShell 3.0 or later.

```powershell
Invoke-WebRequest -OutFile swagger-codegen-cli.jar https://repo1.maven.org/maven2/io/swagger/codegen/v3/swagger-codegen-cli/3.0.71/swagger-codegen-cli-3.0.71.jar
```

--------------------------------

### Describing Multiple API Keys (OR Logic)

Source: https://swagger.io/docs/specification/authentication/api-keys

Demonstrates how to define multiple API key security schemes where any one of them can be used for authentication (logical OR). This is achieved by listing each scheme as a separate array item in the `security` section.

```yaml
security:
  - apiKey: []
  - appId: []
```

--------------------------------

### Define Cookie Parameter in OpenAPI

Source: https://swagger.io/docs/specification/describing-parameters

Illustrates how to define cookie parameters using `in: cookie`. This example defines `debug` and `csrftoken` as cookie parameters for an API operation.

```yaml
parameters:
  - in: cookie
    name: debug
    schema:
      type: integer
      enum: [0, 1]
      default: 0
  - in: cookie
    name: csrftoken
    schema:
      type: string
```

--------------------------------

### GET /users/{id}

Source: https://swagger.io/docs/specification/describing-responses

Retrieves a specific user by their ID. This endpoint can return the user details, an unauthorized response, or a not found response.

```APIDOC
## GET /users/{id}

### Description
Retrieves a specific user by their unique identifier. This endpoint can return the user's details upon success, an unauthorized response if authentication fails, or a not found response if the user does not exist.

### Method
GET

### Endpoint
/users/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the user to retrieve.

#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **User** (object) - An object containing the user's details.

#### Error Response (401)
- **Unauthorized** (object) - Indicates that the request lacks valid authentication credentials.

#### Error Response (404)
- **NotFound** (object) - Indicates that the specified user resource was not found.

#### Response Example (200)
```json
{
  "example": "{\"id\": \"user123\", \"name\": \"John Doe\", \"email\": \"john.doe@example.com\"}"
}
```

#### Response Example (401)
```json
{
  "example": "{\"code\": \"UNAUTHORIZED\", \"message\": \"Authentication failed\"}"
}
```

#### Response Example (404)
```json
{
  "example": "{\"code\": \"NOT_FOUND\", \"message\": \"User with the specified ID not found\"}"
}
```
```

--------------------------------

### Define Array in Swagger Specification

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet shows the basic structure for defining an array of strings in a Swagger specification, including an example.

```yaml
books:
  type: array
  items:
    type: string
  example:
    - "one"
    - "two"
    - "three"
```

--------------------------------

### GET /ping - Ping endpoint with rate limit headers

Source: https://swagger.io/docs/specification/describing-responses

This endpoint checks server liveness and includes custom response headers for rate limiting information.

```APIDOC
## GET /ping

### Description
Checks if the server is alive and provides rate limit information in the response headers.

### Method
GET

### Endpoint
/ping

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Body
None

### Response
#### Success Response (200)
- **Description**: OK
- **Headers**:
  - **X-RateLimit-Limit** (integer) - Request limit per hour.
  - **X-RateLimit-Remaining** (integer) - The number of requests left for the time window.
  - **X-RateLimit-Reset** (string, format: date-time) - The UTC date/time at which the current rate limit window resets.

#### Response Example
```
HTTP/1.1 200 OK
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 99
X-RateLimit-Reset: 2016-10-12T11:00:00Z

{ ... }
```
```

--------------------------------

### Alternative Webpack 5 Configuration with CopyWebpackPlugin

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This alternative webpack.config.js simplifies the build process by using pre-built Web Worker fragments from the swagger-editor npm package. It configures webpack@5 to bundle the main application entry point and uses `CopyWebpackPlugin` to copy the necessary worker files into the output directory. It maintains similar fallback and alias configurations as the previous example for browser compatibility and dependency management.

```javascript
const path = require('path');
const webpack = require('webpack');
const CopyWebpackPlugin = require('copy-webpack-plugin');


module.exports = {
  mode: 'production',
  entry: {
    app: './index.js',
  },
  output: {
    globalObject: 'self',
    filename: 'static/js/[name].js',
    path: path.resolve(__dirname, 'dist')
  },
  resolve: {
    fallback: {
      path: false,
      fs: false,
      http: require.resolve('stream-http'), // required for asyncapi parser
      https: require.resolve('https-browserify'), // required for asyncapi parser
      stream: require.resolve('stream-browserify'),
      util: require.resolve('util'),
      url: require.resolve('url'),
      zlib: false,

```

--------------------------------

### Conditional Component Wrapping with Wrap-Components (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This example demonstrates wrapping a component conditionally based on its props. The `NumberDisplay` component is wrapped to show a warning message if the `number` prop exceeds 10. Both functional and class-based component wrappers are shown.

```javascript
// Here's our normal, unmodified component.
const MyNumberDisplayPlugin = function(system) {
  return {
    components: {
      NumberDisplay: ({ number }) => <span>{number}</span>
    }
  }
}

// Here's a component wrapper defined as a function.
const MyWrapComponentPlugin = function(system) {
  return {
    wrapComponents: {
      NumberDisplay: (Original, system) => (props) => {
        if(props.number > 10) {
          return <div>
            <h3>Warning! Big number ahead.</h3>
            <Original {...props} />
          </div>
        } else {
          return <Original {...props} />
        }
      }
    }
  }
}

// Alternatively, here's the same component wrapper defined as a class.
const MyWrapComponentPlugin = function(system) {
  return {
    wrapComponents: {
      NumberDisplay: (Original, system) => class WrappedNumberDisplay extends React.component {
        render() {
          if(props.number > 10) {
            return <div>
              <h3>Warning! Big number ahead.</h3>
              <Original {...props} />
            </div>
          } else {
            return <Original {...props} />
          }
        }
      }
    }
  }
}
```

--------------------------------

### POST /survey - Form Data Example

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This section illustrates how form data, specifically application/x-www-form-urlencoded, is submitted via an HTML form and represented in an HTTP POST request.

```APIDOC
## POST /survey

### Description
This endpoint accepts form data submitted via an HTML POST request.

### Method
POST

### Endpoint
/survey

### Parameters
#### Query Parameters
None

#### Request Body
- **name** (string) - Required - The name entered in the form.
- **fav_number** (integer) - Optional - The favorite number entered in the form.

### Request Example
```http
POST /survey HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 28

name=Amy+Smith&fav_number=42
```

### Response
#### Success Response (200)
Details of the success response are not provided in the source text.

#### Response Example
No example provided for the response.
```

--------------------------------

### OpenAPI Integer Multiple Constraint

Source: https://swagger.io/docs/specification/data-models/data-types

Specifies that an integer value must be a multiple of a given number. This example enforces that the integer must be a multiple of 10.

```yaml
type: integer
multipleOf: 10
```

--------------------------------

### Documenting Mutually Exclusive Parameters in OpenAPI

Source: https://swagger.io/docs/specification/describing-parameters

This example shows how to document mutually exclusive parameters for the `/report` endpoint. Since OpenAPI 3.0 doesn't natively support parameter dependencies, this snippet illustrates documenting the restriction in the parameter descriptions and defining a '400 Bad Request' response to indicate the conflict. It covers scenarios where either a relative date (`rdate`) or an exact date range (`start_date` + `end_date`) is accepted.

```yaml
paths:
  /report:
    get:
      parameters:
        - name: rdate
          in: query
          schema:
            type: string
          description: >
            A relative date range for the report, such as `Today` or `LastWeek`.
            For an exact range, use `start_date` and `end_date` instead.
        - name: start_date
          in: query
          schema:
            type: string
            format: date
          description: >
            The start date for the report. Must be used together with `end_date`.
            This parameter is incompatible with `rdate`.
        - name: end_date
          in: query
          schema:
            type: string
            format: date
          description: >
            The end date for the report. Must be used together with `start_date`.
            This parameter is incompatible with `rdate`.
      responses:
        "400":
          description: Either `rdate` or `start_date`+`end_date` are required.
```

--------------------------------

### OpenAPI Specification Version Declaration

Source: https://swagger.io/docs/specification/basic-structure

Declares the version of the OpenAPI Specification used for the API definition. This is a mandatory field and dictates the structure and available keywords for the document.

```yaml
openapi: 3.0.4

```

--------------------------------

### Add Summary and Description to OpenAPI Paths

Source: https://swagger.io/docs/specification/paths-and-operations

Demonstrates how to add optional 'summary' and multi-line 'description' fields to an API path for documentation purposes. The description supports Markdown.

```yaml
paths:
  /users/{id}:
    summary: Represents a user
    description: |
      This resource represents an individual user in the system.
      Each user is identified by a numeric `id`.
    get: ...
    patch: ...
    delete: ...
```

--------------------------------

### Define Nested Array

Source: https://swagger.io/docs/specification/data-models/data-types

Creates a nested array structure, where the `items` schema itself defines another array. This example shows an array of arrays of integers.

```yaml
type: array
items:
  type: array
  items:
    type: integer
```

--------------------------------

### PATCH /user/{userId}

Source: https://swagger.io/docs/specification/links

Updates an existing user. This operation can reuse the link definition to reference the 'Get a user by ID' operation.

```APIDOC
## PATCH /user/{userId}

### Description
Updates an existing user. This operation can reuse the link definition to reference the 'Get a user by ID' operation.

### Method
PATCH

### Endpoint
/user/{userId}

### Parameters
#### Path Parameters
- **userId** (integer) - Required - The ID of the user to update.

#### Request Body
- **(object)** - Required - The updated user data.

### Request Example
```json
{
  "email": "john.doe.updated@example.com"
}
```

### Response
#### Success Response (200)
- **(object)** - The updated user object (referencing `#/components/schemas/User`).

#### Response Example
```json
{
  "id": 123,
  "username": "johndoe",
  "email": "john.doe.updated@example.com"
}
```

### Links
#### GetUserByUserId
- **Description**: The `id` value returned in the response can be used as the `userId` parameter in `GET /users/{userId}`.
- **OperationId**: getUser
- **Parameters**:
  - **userId** (string) - The ID of the user to retrieve. This is dynamically set from the response body's `id` field.
```

--------------------------------

### GET /users/me - Returns user information with embedded avatar

Source: https://swagger.io/docs/specification/describing-responses

This endpoint returns user information, including a base64-encoded avatar image embedded within the JSON response.

```APIDOC
## GET /users/me

### Description
Returns user information including username and a base64-encoded avatar.

### Method
GET

### Endpoint
/users/me

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Body
None

### Response
#### Success Response (200)
- **username** (string) - Description: The user's name.
- **avatar** (string, format: byte) - Description: Base64-encoded contents of the avatar image.

#### Response Example
```json
{
  "username": "johndoe",
  "avatar": "/9j/4AAQSkZJRgABAQEASABIAAD..."
}
```
```

--------------------------------

### OpenAPI Extensions Overview

Source: https://swagger.io/docs/specification/openapi-extensions

Extensions are custom properties starting with 'x-' that allow adding extra information not covered by the OpenAPI standard. They are supported at the root level and within various sections like 'info', 'paths', 'parameters', 'responses', 'tags', and security schemes.

```APIDOC
## OpenAPI Extensions

### Description
Extensions (also referred to as _specification extensions_ or _vendor extensions_) are custom properties that start with `x-`, such as `x-logo`. These are used to add extra information or functionality that the OpenAPI standard doesn’t include by default. For example, many tools including Amazon API Gateway, ReDoc, APIMatic, and Fern use extensions to include details specific to their products.

### Supported Locations
Extensions are supported on the root level of the API spec and in the following places:
  * `info` section
  * `paths` section, individual paths and operations
  * operation parameters
  * `responses`
  * `tags`
  * security schemes

### Value Types
The extension value can be a primitive, an array, an object or `null`. If the value is an object or array of objects, the object’s property names do not need to start with `x-`.
```

--------------------------------

### Define Basic API Response (YAML)

Source: https://swagger.io/docs/specification/describing-responses

This snippet shows a minimal example of defining a response for an API operation. It specifies the HTTP status code ('200'), a description ('OK'), and the content type ('text/plain') with a simple string schema.

```yaml
paths:
  /ping:
    get:
      responses:
        "200":
          description: OK
          content:
            text/plain:
              schema:
                type: string
                example: pong
```

--------------------------------

### Specify Swagger UI Version in NPM

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This snippet shows how to specify a minor version of Swagger UI to use in your application when installing via NPM. This is recommended for custom plugins that wrap, extend, override, or consume internal core APIs, as these APIs can change without a major version bump.

```json
{
  "dependencies": {
    "swagger-ui": "~3.11.0"
  }
}
```

--------------------------------

### Build and Run Swagger Editor Locally (Unprivileged)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This set of commands outlines the process for building and running an unprivileged Swagger Editor Docker image. After building the application, it uses a specific Dockerfile ('Dockerfile.unprivileged') to create the image tagged 'next-v5-unprivileged'. The container is then run, mapping port 8080 to port 8080. Access the editor at http://localhost:8080/.

```bash
$ npm run build:app
$ docker build . -f Dockerfile.unprivileged -t swaggerapi/swagger-editor:next-v5-unprivileged
$ docker run -d -p 8080:8080 swaggerapi/swagger-editor:next-v5-unprivileged

```

--------------------------------

### Applying Basic Authentication to Specific Operations in OpenAPI

Source: https://swagger.io/docs/specification/authentication/basic-authentication

This OpenAPI 3.0 snippet shows how to apply Basic Authentication to a specific API operation (e.g., a GET request to '/something'). The 'security' key is placed within the operation definition, overriding any global security settings for that operation.

```yaml
paths:
  /something:
    get:
      security:
        - basicAuth: []
```

--------------------------------

### Initialize Swagger UI with Plugin System

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Demonstrates how to customize Swagger UI's layout and functionality by providing custom plugins and presets. The 'layout' parameter specifies the top-level component, while 'plugins' and 'presets' allow for injecting custom logic and configurations.

```javascript
import MyCustomLayout from './MyCustomLayout';
import MyCustomPlugin from './MyCustomPlugin';

const ui = SwaggerUI({
  dom_id: '#swagger-ui',
  layout: MyCustomLayout,
  plugins: [
    MyCustomPlugin,
    // Other plugins...
  ],
  presets: [
    SwaggerUI.presets.ApisPreset,
    // Other presets...
  ]
});
```

--------------------------------

### Define Response Body Schema Inline (YAML)

Source: https://swagger.io/docs/specification/describing-responses

This example shows how to define the structure of a response body directly within the operation definition using the `schema` keyword. It specifies an object with `id` (integer) and `username` (string) properties for a 'User' object.

```yaml
responses:
  "200":
    description: A User object
    content:
      application/json:
        schema:
          type: object
          properties:
            id:
              type: integer
              description: The user ID.
            username:
              type: string
              description: The user name.
```

--------------------------------

### Define and Use Custom Presets in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/overview

Demonstrates how to define a custom preset as an array of plugins and then include it in the Swagger UI configuration using the 'presets' option. It also shows how to include the default 'ApisPreset' when defining custom presets.

```javascript
const MyPreset = [FirstPlugin, SecondPlugin, ThirdPlugin]

SwaggerUI({
  presets: [
    MyPreset
  ]
})
```

```javascript
SwaggerUI({
  presets: [
    SwaggerUI.presets.apis,
    MyAmazingCustomPreset
  ]
})
```

--------------------------------

### Extend Existing Plugin Actions

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

An example of a plugin that extends the functionality of an existing plugin. The `ExtendingPlugin` takes the `system` object and defines a new action `doExtendedThings` within the `extending` state namespace. This new action calls the `doStuff` action from the `normal` state namespace provided by another plugin.

```javascript
const ExtendingPlugin = function(system) {
  return {
    statePlugins: {
      extending: {
        actions: {
          doExtendedThings: function(...args) {
            // you can do other things in here if you want
            return system.normalActions.doStuff(...args)
          }
        }
      }
    }
  }
}
```

--------------------------------

### Describe Query Parameter with Complex JSON Content (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This example shows how to define a query parameter for complex serialization scenarios using the 'content' keyword in YAML. It specifies that the 'filter' parameter should be treated as JSON, with a defined schema for its object structure.

```yaml
parameters:
  - in: query
    name: filter
    content:
      application/json:
        schema:
          type: object
          properties:
            type:
              type: string
            color:
              type: string
```

--------------------------------

### Restrict Query Parameter to Enum Values (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This example demonstrates how to restrict a query parameter ('status') to a fixed set of string values ('available', 'pending', 'sold') using the 'enum' keyword within its schema in YAML.

```yaml
parameters:
  - in: query
    name: status
    schema:
      type: string
      enum:
        - available
        - pending
        - sold
```

--------------------------------

### Combine Schemas with OpenAPI allOf

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Demonstrates using the `allOf` keyword in OpenAPI to combine multiple schema definitions into a single object. This is useful for extending base schemas with specific properties, as shown in the `Dog` and `Cat` examples, which inherit from a base `Pet` schema.

```yaml
paths:
  /pets:
    patch:
      requestBody:
        content:
          application/json:
            schema:
              oneOf:
                - $ref: "#/components/schemas/Cat"
                - $ref: "#/components/schemas/Dog"
              discriminator:
                propertyName: pet_type
      responses:
        "200":
          description: Updated

components:
  schemas:
    Pet:
      type: object
      required:
        - pet_type
      properties:
        pet_type:
          type: string
      discriminator:
        propertyName: pet_type

    Dog: # "Dog" is a value for the pet_type property (the discriminator value)
      allOf: # Combines the main `Pet` schema with `Dog`-specific properties
        - $ref: "#/components/schemas/Pet"
        - type: object
          # all other properties specific to a `Dog`
          properties:
            bark:
              type: boolean
            breed:
              type: string
              enum: [Dingo, Husky, Retriever, Shepherd]

    Cat: # "Cat" is a value for the pet_type property (the discriminator value)
      allOf: # Combines the main `Pet` schema with `Cat`-specific properties
        - $ref: "#/components/schemas/Pet"
        - type: object
          # all other properties specific to a `Cat`
          properties:
            hunts:
              type: boolean
            age:
              type: integer

```

--------------------------------

### Model Composition with `allOf`

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Demonstrates how to compose schemas by combining common properties into a base schema and extending it with schema-specific properties using `allOf`.

```APIDOC
## Model Composition with `allOf`

### Description
Use `allOf` to combine multiple schemas into a single schema. This is useful for inheriting properties from a base schema.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A (Schema Definition)

### Request Body
```yaml
components:
  schemas:
    BasicErrorModel:
      type: object
      required:
        - message
        - code
      properties:
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    ExtendedErrorModel:
      allOf:
        - $ref: "#/components/schemas/BasicErrorModel"
        - type: object
          required:
            - rootCause
          properties:
            rootCause:
              type: string
```

### Response
N/A (Schema Definition)

#### Success Response (200)
N/A (Schema Definition)

#### Response Example
N/A (Schema Definition)
```

--------------------------------

### OpenAPI 3.0 Array Serialization

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Demonstrates how to specify custom serialization for array form fields in OpenAPI 3.0 using the `encoding` section. This example shows a comma-separated list for the 'color' array.

```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        properties:
          color:
            type: array
            items:
              type: string
      encoding:
        color: # color=red,green,blue
          style: form
          explode: false
```

--------------------------------

### Define Mixed-Type Array with oneOf

Source: https://swagger.io/docs/specification/data-models/data-types

Allows an array to contain items of different types by using the `oneOf` keyword within the `items` schema. This example permits strings and integers.

```yaml
type: array
items:
  oneOf:
    - type: string
    - type: integer
```

--------------------------------

### Operation-Level Bearer Authentication in OpenAPI

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Applies the 'bearerAuth' security scheme to a specific API operation ('/something' GET). This allows for granular control over which endpoints require bearer authentication.

```yaml
paths:
  /something:
    get:
      security:
        - bearerAuth: []
```

--------------------------------

### Vendor-Specific Media Types for API Definitions

Source: https://swagger.io/docs/specification/media-types

This list provides examples of vendor-specific media types used in API definitions, following RFC 6838 conventions. These types allow for custom data formats tailored to specific applications or services, such as custom JSON or spreadsheet formats.

```text
application/vnd.mycompany.myapp.v2+json
application/vnd.ms-excel
application/vnd.openstreetmap.data+xml
application/vnd.github-issue.text+json
application/vnd.github.v3.diff
image/vnd.djvu
```

--------------------------------

### OpenAPI Polymorphism with oneOf

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Illustrates how to define responses that can be described by multiple alternative schemas using the `oneOf` keyword. This enables a single endpoint to return different data structures based on certain conditions. The response payload can be either `simpleObject` or `complexObject` in this example.

```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
  ...
  schemas:
    simpleObject:
      ...
    complexObject:
      ...
```

--------------------------------

### Specify Local OpenAPI Description File for Generation

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators

This option allows the Swagger Codegen to use a local OpenAPI Description file (JSON or YAML) instead of a URL. This is useful for generating clients from saved specifications, for example, on CI servers or when working offline.

```bash
-i ./modules/swagger-codegen/src/test/resources/2_0/petstore.json
```

--------------------------------

### Server Templating with Variables

Source: https://swagger.io/docs/specification/api-host-and-base-path

Demonstrates how to use server templating with variables for dynamic server URLs.

```APIDOC
## Server Templating

### Description
Allows parameterization of server URL components (scheme, host, port, path) using variables.

### Code Example
```yaml
servers:
  - url: https://{customerId}.saas-app.com:{port}/v2
    variables:
      customerId:
        default: demo
        description: Customer ID assigned by the service provider
      port:
        enum:
          - '443'
          - '8443'
        default: '443'
```

**Note:** Server variables are assumed to be strings and require a `default` value.
```

--------------------------------

### Multiple Servers Configuration

Source: https://swagger.io/docs/specification/api-host-and-base-path

Shows how to define multiple server URLs, such as for production and sandbox environments.

```APIDOC
## Multiple Server Environments

### Description
Configures multiple server URLs for different environments like production and sandbox.

### Code Example
```yaml
servers:
  - url: https://api.example.com/v1
    description: Production server (uses live data)
  - url: https://sandbox-api.example.com:8443/v1
    description: Sandbox server (uses test data)
```
```

--------------------------------

### Define Enum for Request Parameter (YAML)

Source: https://swagger.io/docs/specification/data-models/enums

This snippet shows how to define an enum for a query parameter named 'sort' in an OpenAPI GET request. It specifies that the 'sort' parameter must be either 'asc' or 'desc'.

```yaml
paths:
  /items:
    get:
      parameters:
        - in: query
          name: sort
          description: Sort order
          schema:
            type: string
            enum: [asc, desc]
```

--------------------------------

### Query Swagger Codegen API for Supported Clients (cURL)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This cURL command queries the Swagger Codegen API to retrieve a list of supported API client types. It makes a GET request to the V3 endpoint and expects a JSON response.

```shell
curl -X 'GET' \
  'https://generator3.swagger.io/api/client/V3' \
  -H 'accept: application/json'
```

--------------------------------

### Retrieve Language-Specific Generation Options using curl

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

This command retrieves the available language-specific generation options for a given language and codegen version. It sends a GET request to the `/api/options` endpoint with `language` and `version` query parameters. The response provides details about each option, including its name, description, type, and default value.

```bash
curl https://generator3.swagger.io/api/options?language=java&version=V3
```

--------------------------------

### Generate Other Petstore Client Libraries

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This snippet shows the commands to generate client libraries for Android and Objective-C petstore samples, in addition to Java. These scripts automate the process of invoking the Swagger Codegen CLI for different target platforms.

```bash
./bin/android-petstore.sh
./bin/java-petstore.sh
./bin/objc-petstore.sh
```

--------------------------------

### Push Generated SDK to GitHub using git_push.sh (Shell)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/workflow-integration

This snippet shows the process of navigating to the directory where the SDK was generated and then executing the `git_push.sh` script to push the auto-generated SDK to a GitHub repository. This is a common step after SDK generation for version control and distribution.

```bash
cd /var/tmp/perl/petstore
/bin/sh ./git_push.sh
```

--------------------------------

### Define a New Action in a Plugin

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This JavaScript snippet demonstrates how to define a new action creator within a Swagger UI plugin. The `MyActionPlugin` returns an object with `statePlugins` where the `example` namespace contains an `actions` object. The `updateFavoriteColor` action creator returns a Flux Standard Action object.

```javascript
const MyActionPlugin = () => {
  return {
    statePlugins: {
      example: {
        actions: {
          updateFavoriteColor: (str) => {
            return {
              type: "EXAMPLE_SET_FAV_COLOR",
              payload: str
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Distinguish Between anyOf and oneOf in OpenAPI

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Explains the difference between `anyOf` and `oneOf` in OpenAPI schema validation. `oneOf` requires data to match exactly one subschema, while `anyOf` allows matching one or more. The example shows a case where `oneOf` would invalidate data that `anyOf` would accept.

```yaml
# Example demonstrating the difference between anyOf and oneOf
# Using oneOf instead of anyOf from the previous example would invalidate:
# {
#   "nickname": "Fido",
#   "pet_type": "Dog",
#   "age": 4
# }
# because it matches both PetByAge and PetByType schemas.

```

--------------------------------

### JSON in Form Data Example (Slack Incoming Webhook)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Demonstrates how to send JSON data within a form field named 'payload' for Slack incoming webhooks. This method is useful when the API expects form-urlencoded data but the actual value is a JSON string. URL-encoding is applied before sending.

```text
payload={"text":"Swagger is awesome"}
```

--------------------------------

### Initialize Swagger UI Bundle with Custom Plugin

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This code initializes the SwaggerUIBundle with various configurations, including deep linking, presets, and plugins. Crucially, it includes the custom `SnippedGeneratorNodeJsPlugin` and the `snippetConfig` to enable and customize request snippets.

```javascript
const ui = SwaggerUIBundle({
  "dom_id": "#swagger-ui",
  deepLinking: true,
  presets: [
    SwaggerUIBundle.presets.apis,
    SwaggerUIStandalonePreset
  ],
  plugins: [
    SwaggerUIBundle.plugins.DownloadUrl,
    SnippedGeneratorNodeJsPlugin
  ],
  layout: "StandaloneLayout",
  validatorUrl: "https://validator.swagger.io/validator",
  url: "https://petstore.swagger.io/v2/swagger.json",
  ...snippetConfig,
})
```

--------------------------------

### Define Common Path-Level Parameter (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML snippet illustrates defining a parameter at the path level, making it common to all operations within that path. The `id` parameter is defined under `/user/{id}` and is inherited by `get`, `patch`, and `delete` operations. This promotes reusability for parameters like resource identifiers.

```yaml
paths:
  /user/{id}:
    parameters:
      - in: path
        name: id
        schema:
          type: integer
        required: true
        description: The user ID
    get:
      summary: Gets a user by ID
      ...
    patch:
      summary: Updates an existing user with the specified ID
      ...
    delete:
      summary: Deletes the user with the specified ID
      ...
```

--------------------------------

### OpenAPI 3.0 Login Operation with Set-Cookie Header

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

Documents a login POST operation in OpenAPI 3.0, including its request body, response, and the Set-Cookie header that returns the authentication cookie. The Set-Cookie header is defined in the response headers with its schema and example.

```yaml
paths:
  /login:
    post:
      summary: Logs in and returns the authentication  cookie
      requestBody:
        required: true
        description: A JSON object containing the login and password.
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/LoginRequest"
      security: []
      responses:
        "200":
          description: >
            Successfully authenticated.
            The session ID is returned in a cookie named `JSESSIONID`. You need to include this cookie in subsequent requests.
          headers:
            Set-Cookie:
              schema:
                type: string
                example: JSESSIONID=abcde12345; Path=/; HttpOnly
```

--------------------------------

### Configure Local API Definition in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/development/setting-up

Modify the `dev-helper-initializer.js` file to point to a local API definition file instead of a remote URL. The local file must be in the `dev-helpers` directory or a subdirectory. This is useful for testing local changes to your API specification.

```javascript
url: "./examples/your-local-api-definition.yaml",
```

--------------------------------

### Integrating Swagger Editor via UMD Bundle

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

An HTML file demonstrating how to integrate Swagger Editor into a web page using its UMD bundle. It includes loading React, ReactDOM, the Swagger Editor script, and initializing the editor with a specified URL.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta
    name="description"
    content="SwaggerEditor"
  />
  <title>SwaggerEditor</title>
  <link rel="stylesheet" href="./swagger-editor.css" />
</head>
<body>
  <div id="swagger-editor"></div>
  <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
  <script src="./dist/umd/swagger-editor.js"></script>
  <script>
    const props = {
      url: 'https://raw.githubusercontent.com/asyncapi/spec/v2.2.0/examples/streetlights-kafka.yml',
    };
    const element = React.createElement(SwaggerEditor, props);
    const domContainer = document.querySelector('#swagger-editor');
    ReactDOM.render(element, domContainer);
  </script>
</body>
</html>
```

--------------------------------

### Define JSON Response Schema in Swagger IO

Source: https://swagger.io/docs/specification/media-types

This snippet demonstrates how to define a JSON response schema within a Swagger IO API definition. It specifies the structure and data types for an employee list response, including an example payload. This is crucial for documenting API contracts.

```yaml
paths:
  /employees:
    get:
      summary: Returns a list of employees.
      responses:
        "200":
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: integer
                  name:
                    type: string
                  fullTime:
                    type: boolean
                example:
                  id: 1
                  name: Jessica Right
                  fullTime: true
```

--------------------------------

### Override Path-Level Parameter in Operation (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML snippet demonstrates how a path-level parameter can be overridden at the operation level. For the `/users/{id}` path, the `id` parameter is initially defined as a single integer. However, the `get` operation redefines `id` as an array of integers with specific styling (`explode: false`, `style: simple`), allowing for comma-separated IDs. Path-level parameters cannot be removed but can be redefined.

```yaml
paths:
  /users/{id}:
    parameters:
      - in: path
        name: id
        schema:
          type: integer
        required: true
        description: The user ID.
    delete:
      summary: Deletes the user with the specified ID.
      responses:
        "204":
          description: User was deleted.
    get:
      summary: Gets one or more users by ID.
      parameters:
        - in: path
          name: id
          required: true
          description: A comma-separated list of user IDs.
          schema:
            type: array
            items:
              type: integer
            minItems: 1
          explode: false
          style: simple
      responses:
        "200":
          description: OK
```

--------------------------------

### Define Security Scopes for OAuth2 and OpenID Connect

Source: https://swagger.io/docs/specification/authentication

This snippet demonstrates how to define security scopes for OAuth 2 and OpenID Connect in a Swagger/OpenAPI document. It shows the structure for specifying scopes required for API access, differentiating between authentication schemes. BasicAuth is also included as an example of a scheme that does not use scopes.

```yaml
security:
  - OAuth2:
      - scope1
      - scope2
  - OpenId:
      - scopeA
      - scopeB
  - BasicAuth: []
```

--------------------------------

### Building Swagger Editor Artifacts

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Commands to build different artifacts of Swagger Editor. This includes building the application, serving it locally, creating ESM and UMD bundles for library consumption, and packaging the npm module.

```bash
npm run build
npm run build:app
npm run build:app:serve
npm run build:bundle:esm
npm run build:bundle:umd
npm pack
```

--------------------------------

### Get Swagger UI 3.x Version via Console

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/version-detection

This method retrieves the exact version of Swagger UI 3.x by executing a JavaScript command in the browser's web console. It requires Swagger UI version 3.0.8 or later. The output provides version, git revision, and git dirty status.

```javascript
JSON.stringify(versions)
```

--------------------------------

### Build and Run Swagger Editor Locally (Privileged)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This sequence of commands shows how to build the Swagger Editor Docker image locally and run it. It first builds the application using 'npm run build:app', then builds the Docker image with the tag 'next-v5', and finally runs the container, mapping port 8080 to port 80. Access the editor at http://localhost:8080/.

```bash
$ npm run build:app
$ docker build . -t swaggerapi/swagger-editor:next-v5
$ docker run -d -p 8080:80 swaggerapi/swagger-editor:next-v5

```

--------------------------------

### $ref Syntax for Local, Remote, and URL References

Source: https://swagger.io/docs/specification/using-ref

Illustrates various ways to use the $ref keyword, including local references within the same document, remote references to files on the same or different servers, and URL references.

```yaml
# Local Reference
$ref: '#/definitions/myElement'

# Remote Reference (same folder)
$ref: 'document.json'

# Remote Reference (element in same folder)
$ref: 'document.json#/myElement'

# Remote Reference (parent folder)
$ref: '../document.json#/myElement'

# Remote Reference (another folder)
$ref: '../another-folder/document.json#/myElement'

# URL Reference (whole document)
$ref: 'http://path/to/your/resource'

# URL Reference (specific element)
$ref: 'http://path/to/your/resource.json#/myElement'

# URL Reference (different server, same protocol)
$ref: '//anotherserver.com/files/example.json'
```

--------------------------------

### Access Components via getComponent Helper in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/overview

Illustrates the usage of the `getComponent` helper function within Swagger UI to retrieve references to components managed by the plugin system. It shows how to load a component and optionally map the system as props.

```javascript
getComponent("ComponentNameToLoad")
```

```javascript
getComponent("ContainerComponentName", true)
```

--------------------------------

### OpenAPI Schema Composition with allOf

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Demonstrates how to compose OpenAPI schemas using the `allOf` keyword. This allows for inheriting properties from a base schema into a more specific one. It's useful for reducing redundancy when multiple schemas share common properties. Ensure that combined models are validated against all constituent models to avoid conflicts.

```yaml
components:
  schemas:
    BasicErrorModel:
      type: object
      required:
        - message
        - code
      properties:
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    ExtendedErrorModel:
      allOf:
        - $ref: "#/components/schemas/BasicErrorModel"
        - type: object
          required:
            - rootCause
          properties:
            rootCause:
              type: string
```

--------------------------------

### Using Multiple Authentication Types

Source: https://swagger.io/docs/specification/authentication

Explains how to combine different authentication types (e.g., Basic Auth, API Key, OAuth 2) using logical OR and AND.

```APIDOC
## Using Multiple Authentication Types

### Description
APIs can support multiple authentication types. The `security` section allows combining these using logical OR (array items) and AND (items within a hashmap).

### Method
N/A (Configuration Example)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
# Logical OR: BasicAuth OR ApiKey
security:
  - basicAuth: []
  - apiKey: []
```

```yaml
# Logical AND: ApiKey1 AND ApiKey2
security:
  - apiKey1: []
    apiKey2: []
```

```yaml
# Combined: (OAuth2 with scopes) OR (ApiKey1 AND ApiKey2)
security:
  - oauth2: [scope1, scope2]
  - apiKey1: []
    apiKey2: []
```

### Response
N/A

### Response Example
N/A
```

--------------------------------

### Build Project Assets with npm

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Builds a new set of JavaScript and CSS assets for the Swagger Editor, outputting them to the `/dist` directory. This command is used to create production-ready files.

```bash
npm run build
```

--------------------------------

### Empty-Valued and Nullable Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates how to define query parameters that can be empty and how to specify nullable schema types.

```APIDOC
## Empty-Valued Query Parameters

### Description
Allows query string parameters to have a name but no value.

### Method
GET

### Endpoint
`/foo?metadata`

### Parameters
#### Query Parameters
- **metadata** (boolean) - Required - Used to indicate metadata presence.
  - `allowEmptyValue: true`

### Request Example
```
GET /foo?metadata
```

## Nullable Schema Types

### Description
Supports `nullable: true` in schemas to allow `null` values for parameters, similar to `int?` in C# or `java.lang.Integer` in Java.

### Schema Example
```yaml
schema:
  type: integer
  format: int32
  nullable: true
```

**Note:** `nullable` is distinct from optional or empty-valued parameters. It explicitly permits a `null` value.
```

--------------------------------

### Swagger Codegen CLI Generate Command Help

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This snippet shows the help output for the `swagger-codegen-cli generate` command, detailing various options for customizing code generation. Key options include specifying the input spec file (`-i`), the output directory (`-o`), the target language (`-l`), and configuration file (`-c`).

```bash
swagger-codegen-cli generate \
        [(-a <authorization> | --auth <authorization>)] \
        [--additional-properties <additional properties>...] \
        [--api-package <api package>] [--artifact-id <artifact id>] \
        [--artifact-version <artifact version>] \
        [(-c <configuration file> | --config <configuration file>)] \
        [-D <system properties>...] [--git-repo-id <git repo id>] \
        [--git-user-id <git user id>] [--group-id <group id>] \
        [--http-user-agent <http user agent>] \
        (-i <spec file> | --input-spec <spec file>) \
        [--ignore-file-override <ignore file override location>] \
        [--import-mappings <import mappings>...] \
        [--instantiation-types <instantiation types>...] \
        [--invoker-package <invoker package>] \
        (-l <language> | --lang <language>) \
        [--language-specific-primitives <language specific primitives>...] \
        [--library <library>] [--model-name-prefix <model name prefix>] \
        [--model-name-suffix <model name suffix>] \
        [--model-package <model package>] \
        [(-o <output directory> | --output <output directory>)] \
        [--release-note <release note>] [--remove-operation-id-prefix] \
        [--reserved-words-mappings <reserved word mappings>...] \
        [(-s | --skip-overwrite)] \
        [(-t <template directory> | --template-dir <template directory>)] \
        [--type-mappings <type mappings>...] [(-v | --verbose)]
```

--------------------------------

### Path Templating in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

Illustrates the use of curly braces `{}` to define path parameters, allowing for dynamic segments in API URLs. These parameters must be provided by the API client.

```text
/users/{id}
/organizations/{orgId}/members/{memberId}
/report.{format}
```

--------------------------------

### afterLoad: Access System and Attach Actions in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

The `afterLoad` method provides a reference to the system after a plugin is registered. It allows for executing logic that depends on the plugin being ready, such as fetching initial data or attaching bound actions as top-level methods. The plugin context is bound to `this`.

```javascript
const MyMethodProvidingPlugin = function() {
  return {
    afterLoad(system) {
      // at this point in time, your actions have been bound into the system
      // so you can do things with them
      this.rootInjects = this.rootInjects || {}
      this.rootInjects.myMethod = system.exampleActions.updateFavoriteColor
    },
    statePlugins: {
      example: {
        actions: {
          updateFavoriteColor: (str) => {
            return {
              type: "EXAMPLE_SET_FAV_COLOR",
              payload: str
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Applying API Key Security Scheme to Specific Operations

Source: https://swagger.io/docs/specification/authentication/api-keys

Illustrates how to apply an API key security scheme to individual operations within an API definition, rather than globally. This allows for more granular control over security requirements.

```yaml
paths:
  /something:
    get:
      security:
        - ApiKeyAuth: []
      responses:
        "200":
          description: OK (successfully authenticated)
```

--------------------------------

### Integrate SwaggerEditor Preview Plugins with SwaggerUI (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This snippet demonstrates how to integrate SwaggerEditor's preview plugins (AsyncAPI, API Design Systems) into SwaggerUI using JavaScript. It requires importing necessary SwaggerUI and SwaggerEditor components and plugins, including the SwaggerUIAdapterPlugin to bridge the two.

```javascript
import SwaggerUI from 'swagger-ui';
import SwaggerUIStandalonePreset from 'swagger-ui/dist/swagger-ui-standalone-preset';
import 'swagger-editor/swagger-editor.css';
import EditorContentTypePlugin from 'swagger-editor/plugins/editor-content-type';
import EditorPreviewAsyncAPIPlugin from 'swagger-editor/plugins/editor-preview-asyncapi';
import EditorPreviewAPIDesignSystemsPlugin from 'swagger-editor/plugins/editor-preview-api-design-systems';
import SwaggerUIAdapterPlugin from 'swagger-editor/plugins/swagger-ui-adapter';

SwaggerUI({
  url: 'https://petstore.swagger.io/v2/swagger.json',
  dom_id: '#swagger-ui',
  presets: [SwaggerUI.presets.apis, SwaggerUIStandalonePreset],
  plugins: [
    EditorContentTypePlugin,
    EditorPreviewAsyncAPIPlugin,
    EditorPreviewAPIDesignSystemsPlugin,
    SwaggerUIAdapterPlugin,
    SwaggerUI.plugins.DownloadUrl,
  ],
});
```

--------------------------------

### Schema vs. Content Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Explains the difference between using `schema` and `content` keywords for parameter definition. `schema` is for most cases, while `content` is for complex serialization scenarios like JSON in query strings.

```APIDOC
## Schema vs. Content Parameters

### Description
This section details the usage of `schema` and `content` keywords for defining API parameters. `schema` is generally preferred for describing primitive types, arrays, and objects with standard serialization. `content` is reserved for complex serialization scenarios, such as embedding JSON directly within a query string.

### Method
N/A (Documentation of parameter definition)

### Endpoint
N/A (Documentation of parameter definition)

### Parameters
#### Query Parameters (using `schema`)
- **color** (array[string]) - Optional - Specifies an array of colors. Serialized as `color=blue,black,brown` when `style: form` and `explode: false`.

#### Query Parameters (using `content`)
- **filter** (object) - Optional - Used for complex filtering, allowing JSON objects in the query string. The structure is defined by the schema under `content/application/json`.
  - **type** (string) - Description of the type property within the filter object.
  - **color** (string) - Description of the color property within the filter object.

### Request Example
```json
// Example using schema for array parameter
GET /items?color=blue,black,brown

// Example using content for JSON parameter
GET /items?filter=%7B%22type%22%3A%22t-shirt%22%2C%22color%22%3A%22blue%22%7D
```

### Response
#### Success Response (200)
N/A (Documentation of parameter definition)

#### Response Example
N/A (Documentation of parameter definition)
```

--------------------------------

### Multiple API Key Authentication

Source: https://swagger.io/docs/specification/authentication/api-keys

Explains how to handle APIs that require multiple API keys, specifying whether they are used together (AND) or interchangeably (OR).

```APIDOC
## Multiple API Key Authentication

### Description
This section covers scenarios where an API requires multiple API keys. It demonstrates how to specify if these keys must be used together (logical AND) or if any one of them is sufficient (logical OR).

### Logical AND (Keys used together)
To require both `X-API-KEY` and `X-APP-ID`:
```yaml
components:
  securitySchemes:
    apiKey:
      type: apiKey
      in: header
      name: X-API-KEY
    appId:
      type: apiKey
      in: header
      name: X-APP-ID

security:
  - apiKey: []
    appId: [] # Both keys are required in the same array item
```

### Logical OR (Either key can be used)
To allow either `X-API-KEY` or `X-APP-ID`:
```yaml
security:
  - apiKey: []
  - appId: [] # Each key is in a separate array item
```
```

--------------------------------

### Generate Java Petstore Client Library

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This command generates a Java client library for the Petstore API. It requires the path to the Swagger specification file, the desired language ('java'), and the output directory. The script `java-petstore.sh` (or `java-petstore.bat` on Windows) is used to execute the generation process.

```bash
./bin/java-petstore.sh
```

```bash
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
  -i http://petstore.swagger.io/v2/swagger.json \
  -l java \
  -o samples/client/petstore/java
```

--------------------------------

### Initialize OAuth2 Configuration (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Provides Swagger UI with information about your OAuth server. Accepts a configuration object.

```javascript
initOAuth({
  clientId: 'YOUR_CLIENT_ID',
  clientSecret: 'YOUR_CLIENT_SECRET',
  realm: 'YOUR_REALM',
  appName: 'YOUR_APP_NAME',
  scopeSeparator: ' ',
  additionalQueryStringParams: {}
});
```

--------------------------------

### Define Query Parameters Correctly in OpenAPI Paths

Source: https://swagger.io/docs/specification/paths-and-operations

Demonstrates the correct way to define query parameters in OpenAPI paths, emphasizing that query strings should not be part of the path itself but defined separately. This ensures proper API definition and avoids issues with operation uniqueness.

```yaml
paths:
  /users:
    get:
      parameters:
        - in: query
          name: role
          schema:
            type: string
            enum: [user, poweruser, admin]
          required: true
```

--------------------------------

### Running Swagger Editor Tests

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

npm scripts for running various tests within the Swagger Editor project. Includes commands for linting, unit/integration tests, and End-to-End (E2E) Cypress tests for both development and CI environments.

```bash
npm run lint
npm test
npm run cy:dev
npm run cy:ci
```

--------------------------------

### Run End-to-End Tests with npm

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Executes end-to-end browser tests for the Swagger Editor using Cypress. This script is crucial for verifying the application's behavior in a simulated user environment.

```bash
npm run e2e
```

--------------------------------

### Generate SDK using Swagger Codegen CLI (Java)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/workflow-integration

This snippet demonstrates how to use the Swagger Codegen CLI, packaged as a JAR, to generate an SDK for a given API specification. It specifies the input API definition, the target language (Perl in this case), Git user and repository IDs for GitHub integration, a release note, and the output directory.

```bash
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
 -i modules/swagger-codegen/src/test/resources/2_0/petstore.json -l perl \
 --git-user-id "swaggerapi" \
 --git-repo-id "petstore-perl" \
 --release-note "Github integration demo" \
 -o /var/tmp/perl/petstore
```

--------------------------------

### API Key Authentication Methods

Source: https://swagger.io/docs/specification/authentication/api-keys

Demonstrates various ways an API key can be passed to an API endpoint for authentication.

```APIDOC
## API Key Authentication Methods

### Description
API keys can be used for authorization by including them in requests. They can be sent as a query parameter, a custom request header, or a cookie.

### Query Parameter Example
```
GET /something?api_key=abcdef12345
```

### Request Header Example
```
GET /something HTTP/1.1
X-API-Key: abcdef12345
```

### Cookie Example
```
GET /something HTTP/1.1
Cookie: X-API-KEY=abcdef12345
```

**Note:** API key authentication should be used with HTTPS/SSL for security.
```

--------------------------------

### Server Overriding with Links

Source: https://swagger.io/docs/specification/links

Demonstrates how the `server` keyword within a link definition can override the default servers for a linked operation.

```APIDOC
## Server Overriding with Links

By default, a linked operation is called against its default servers (global `servers` or operation-specific `servers`). However, the `server` keyword within a link definition allows you to override this behavior and specify a different server for the linked operation.

### `server` Keyword

The `server` keyword has the same fields as global servers but defines a single server for the link.

### Example

Consider the following OpenAPI snippet:

```yaml
servers:
  - url: https://api.example.com
---
links:
  GetUserByUserId:
    operationId: getUser
    parameters:
      userId: "$response.body#/id"
    server:
      url: https://new-api.example.com/v2
```

In this example, the `GetUserByUserId` link, when invoked, will target the server defined in its `server` block (`https://new-api.example.com/v2`), overriding the global server definition (`https://api.example.com`). The `userId` parameter for the `getUser` operation will be populated using the runtime expression `$response.body#/id`.
```

--------------------------------

### Complex Serialization with Content Keyword

Source: https://swagger.io/docs/specification/serialization

Describes how to handle complex serialization scenarios, such as JSON-formatted objects in query strings, using the `content` keyword and specifying media types.

```APIDOC
## Complex Serialization with Content Keyword

### Description
For complex serialization needs not covered by `style` and `explode` (e.g., JSON objects in query strings), use the `content` keyword to specify the media type and its serialization format.

### Method
POST (Example)

### Endpoint
`/complex-data

### Parameters
#### Request Body
- **data** (object) - Required - The complex data object.
  - `content`: `application/json`

### Request Example
```json
{
  "data": {
    "key1": "value1",
    "key2": 123
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message.

#### Response Example
```json
{
  "message": "Complex data processed successfully"
}
```
```

--------------------------------

### OpenAPI: Return File Response (binary)

Source: https://swagger.io/docs/specification/describing-responses

Defines an API response that returns a file, such as a PDF. It uses `type: string` with `format: binary` and specifies the `content` with the appropriate media type.

```yaml
paths:
  /report:
    get:
      summary: Returns the report in the PDF format
      responses:
        "200":
          description: A PDF file
          content:
            application/pdf:
              schema:
                type: string
                format: binary
```

--------------------------------

### Build Swagger Codegen with Docker

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/docker

This snippet demonstrates how to clone the Swagger Codegen repository and build it using the `run-in-docker.sh` script. This script maps local directories and the Maven repository into the Docker container for a seamless build process.

```bash
git clone https://github.com/swagger-api/swagger-codegen
cd swagger-codegen
./run-in-docker.sh mvn package
```

--------------------------------

### Path Parameters Serialization

Source: https://swagger.io/docs/specification/serialization

Details the different serialization styles and explode options for path parameters in OpenAPI 3.0.

```APIDOC
## Path Parameters Serialization

Path parameters support the following `style` values:

*   **simple** – (default) comma-separated values. Corresponds to the `{param_name}` URI template.
*   **label** – dot-prefixed values, also known as label expansion. Corresponds to the `{.param_name}` URI template.
*   **matrix** – semicolon-prefixed values, also known as path-style expansion. Corresponds to the `{;param_name}` URI template.

The default serialization method is `style: simple` and `explode: false`. Given the path `/users/{id}`, the path parameter `id` is serialized as follows:

| style      | explode | URI template | Primitive value id = 5 | Array id = [3, 4, 5] | Object id = {"role": "admin", "firstName": "Alex"} |
|------------|---------|--------------|------------------------|----------------------|------------------------------------------------------|
| simple *   | false * | /users/{id}  | /users/5               | /users/3,4,5         | /users/role,admin,firstName,Alex                     |
| simple     | true    | /users/{id*} | /users/5               | /users/3,4,5         | /users/role=admin,firstName=Alex                     |
| label      | false   | /users/{.id} | /users/.5              | /users/.3,4,5        | /users/.role,admin,firstName,Alex                    |
| label      | true    | /users/{.id*}| /users/.5              | /users/.3.4.5        | /users/.role=admin.firstName=Alex                    |
| matrix     | false   | /users/{;id}| /users/;id=5           | /users/;id=3,4,5     | /users/;id=role,admin,firstName,Alex                 |
| matrix     | true    | /users/{;id*}| /users/;id=5           | /users/;id=3;id=4;id=5| /users/;role=admin;firstName=Alex                    |

* Default serialization method

The `label` and `matrix` styles are sometimes used with partial path parameters, such as `/users{id}`, because the parameter values get prefixed.
```

--------------------------------

### Importing Individual Swagger Editor Plugins

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Demonstrates how to import specific plugins from the swagger-editor library. Each plugin is imported as a distinct ES module. These imports are necessary for selectively enabling features within the editor.

```javascript
import EditorContentTypePlugin from 'swagger-editor/plugins/editor-content-type';
import EditorContentReadOnlyPlugin from 'swagger-editor/plugins/editor-content-read-only';
```

--------------------------------

### Customizing Fallback Component

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

Demonstrates how to override the default `Fallback` component with a custom implementation. This allows for a tailored error display that matches the application's look and feel.

```javascript
const CustomFallbackPlugin = () => ({
  components: {
    Fallback: ({ name } ) => `This is my custom fallback. ${name} failed to render`,
  },
});

const swaggerUI = SwaggerUI({
  url: "https://petstore.swagger.io/v2/swagger.json",
  dom_id: '#swagger-ui',
  plugins: [
    CustomFallbackPlugin,
  ]
});
```

--------------------------------

### Initialize OAuth 2.0 Configuration in Swagger UI (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/oauth2

This snippet demonstrates how to initialize OAuth 2.0 configuration for Swagger UI using the `initOAuth` method. It requires the Swagger UI constructor to be called first. The configuration includes client ID, client secret (with a security warning for production), realm, app name, scope separator, scopes, additional query parameters, and flags for basic authentication and PKCE with authorization code grant.

```javascript
const ui = SwaggerUI({...})

// Method can be called in any place after calling constructor SwaggerUIBundle
ui.initOAuth({
    clientId: "your-client-id",
    clientSecret: "your-client-secret-if-required",
    realm: "your-realms",
    appName: "your-app-name",
    scopeSeparator: " ",
    scopes: "openid profile",
    additionalQueryStringParams: {test: "hello"},
    useBasicAuthenticationWithAccessCodeGrant: true,
    usePkceWithAuthorizationCodeGrant: true
  })
```

--------------------------------

### Run Swagger Editor Docker Image

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

These commands demonstrate how to pull and run a pre-built Swagger Editor Docker image. The first command pulls the 'next-v5' tag from the Docker Hub repository. The second command runs the container in detached mode, mapping port 8080 on the host to port 80 in the container.

```bash
docker pull docker.swagger.io/swaggerapi/swagger-editor:next-v5
docker run -d -p 8080:80 docker.swagger.io/swaggerapi/swagger-editor:next-v5

```

--------------------------------

### OpenAPI Server Templating for SaaS/On-Premise

Source: https://swagger.io/docs/specification/api-host-and-base-path

Illustrates server templating for scenarios involving both SaaS (hosted) and on-premise API deployments. A 'server' variable is used to specify the base URL, with a default for the SaaS option.

```yaml
servers:
  - url: "{server}/v1"
    variables:
      server:
        default: https://api.example.com # SaaS server
```

--------------------------------

### Mapping Type Names

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

This section explains how to map property values to schema names using the discriminator mapping.

```APIDOC
## Discriminator Mapping

### Description
This endpoint demonstrates how to map property values to specific schema names when using a discriminator. This is useful when a property's value doesn't directly match a schema name but needs to be associated with one.

### Method
N/A (Configuration Example)

### Endpoint
N/A (Configuration Example)

### Parameters
#### Query Parameters
None

#### Request Body
This is a configuration example, not a direct request body.

### Request Example
```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/Object1'
              - $ref: '#/components/schemas/Object2'
              - $ref: 'sysObject.json#/sysObject'
            discriminator:
              propertyName: objectType
              mapping:
                obj1: '#/components/schemas/Object1'
                obj2: '#/components/schemas/Object2'
                system: 'sysObject.json#/sysObject'
  schemas:
    Object1:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
    Object2:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
```

### Response
#### Success Response (200)
This configuration defines how responses are structured based on the `objectType` property. The actual response content will vary depending on the mapped schema.

#### Response Example
Example response for `obj1` mapping:
```json
{
  "objectType": "obj1",
  "property1": "value1"
}
```

Example response for `system` mapping:
```json
{
  "objectType": "system",
  "externalProperty": "externalValue"
}
```
```

--------------------------------

### Polymorphism with `oneOf` and `anyOf`

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Explains how to define schemas that can be one of several alternatives using `oneOf` or `anyOf`, allowing for flexible request and response structures.

```APIDOC
## Polymorphism with `oneOf` and `anyOf`

### Description
Use `oneOf` or `anyOf` to specify that a schema can match one or more of the subschemas provided. `oneOf` requires exactly one schema to match, while `anyOf` requires at least one schema to match.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A (Schema Definition)

### Request Body
```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
  schemas:
    simpleObject:
      # ... schema definition ...
    complexObject:
      # ... schema definition ...
```

### Response
N/A (Schema Definition)

#### Success Response (200)
N/A (Schema Definition)

#### Response Example
N/A (Schema Definition)
```

--------------------------------

### Parameter Location Prefixes (YAML)

Source: https://swagger.io/docs/specification/links

Explains how to prefix parameter names with their location (path, query, header, cookie) when multiple parameters share the same name in the target operation.

```yaml
parameters:
  path.id: ...
  query.id: ...
```

--------------------------------

### Define and Reference Common Parameters in OpenAPI

Source: https://swagger.io/docs/specification/describing-parameters

This snippet demonstrates how to define common query parameters like 'offset' and 'limit' in the `components.parameters` section and reference them using `$ref` in different API paths (`/users`, `/teams`). This promotes reusability and consistency in API definitions.

```yaml
components:
  parameters:
    offsetParam:
      in: query
      name: offset
      required: false
      schema:
        type: integer
        minimum: 0
      description: The number of items to skip before starting to collect the result set.
    limitParam:
      in: query
      name: limit
      required: false
      schema:
        type: integer
        minimum: 1
        maximum: 50
        default: 20
      description: The numbers of items to return.

paths:
  /users:
    get:
      summary: Gets a list of users.
      parameters:
        - $ref: "#/components/parameters/offsetParam"
        - $ref: "#/components/parameters/limitParam"
      responses:
        "200":
          description: OK
  /teams:
    get:
      summary: Gets a list of teams.
      parameters:
        - $ref: "#/components/parameters/offsetParam"
        - $ref: "#/components/parameters/limitParam"
      responses:
        "200":
          description: OK
```

--------------------------------

### Use Wildcard Media Type Placeholder in OpenAPI

Source: https://swagger.io/docs/specification/media-types

This snippet shows how to use a wildcard media type placeholder, such as `image/*`, to define a response format that applies to a range of related media types (e.g., image/png, image/jpeg). This is useful for generic binary data responses.

```yaml
paths:
  /info/logo:
    get:
      responses:
        "200": # Response
          description: OK
          content: # Response body
            image/*: # Media type
              schema:
                type: string
                format: binary
```

--------------------------------

### Multiple File Upload

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Explains how to upload an arbitrary number of files in a single multipart request.

```APIDOC
## POST /upload

### Description
Uploads multiple files in a single multipart request.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **fileName** (array of strings, format: binary) - Required - An array of files to be uploaded.

### Request Example
```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          fileName:
            type: array
            items:
              type: string
              format: binary
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of successful upload.

#### Response Example
```json
{
  "message": "Multiple files uploaded successfully"
}
```
```

--------------------------------

### Default Server URL in OpenAPI

Source: https://swagger.io/docs/specification/api-host-and-base-path

Demonstrates how the server URL defaults to '/' if the 'servers' array is not provided or is empty in an OpenAPI definition.

```yaml
servers:
  - url: /
```

--------------------------------

### Run Unit Tests with npm

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Executes various tests for the Swagger Editor project, including unit tests in Node.js (Mocha and Jest), Cypress end-to-end tests, and ESLint style checks. This command ensures code quality and functionality.

```bash
npm run test
```

--------------------------------

### Default Server URL

Source: https://swagger.io/docs/specification/api-host-and-base-path

Explains the default server URL behavior when the 'servers' array is not provided or is empty.

```APIDOC
## Default Server URL

### Description
If the `servers` array is not provided or is empty, the server URL defaults to `/`.

### Code Example
```yaml
servers:
  - url: /
```
```

--------------------------------

### Server Templating with Variables in OpenAPI

Source: https://swagger.io/docs/specification/api-host-and-base-path

Shows how to use variables within the server URL to create dynamic configurations. Variables are enclosed in curly braces and defined in a 'variables' object, each requiring a 'default' value.

```yaml
servers:
  - url: https://{customerId}.saas-app.com:{port}/v2
    variables:
      customerId:
        default: demo
        description: Customer ID assigned by the service provider
      port:
        enum:
          - '443'
          - '8443'
        default: '443'
```

--------------------------------

### OpenAPI Server Templating for Environments

Source: https://swagger.io/docs/specification/api-host-and-base-path

Demonstrates using server templating to define different environments (production, development, staging) for an API. The 'environment' variable uses an enum to specify distinct hostnames.

```yaml
servers:
  - url: https://{environment}.example.com/v2
    variables:
      environment:
        default: api    # Production server
        enum:
          - api         # Production server
          - api.dev     # Development server
          - api.staging # Staging server
```

--------------------------------

### POST /users

Source: https://swagger.io/docs/specification/links

Creates a new user. The response includes the ID of the created user, which can be used to retrieve the user's details.

```APIDOC
## POST /users

### Description
Creates a new user. The response includes the ID of the created user, which can be used to retrieve the user's details.

### Method
POST

### Endpoint
/users

### Parameters
#### Request Body
- **(object)** - Required - User data for creation.

### Request Example
```json
{
  "username": "johndoe",
  "email": "john.doe@example.com"
}
```

### Response
#### Success Response (201)
- **id** (integer) - The ID of the created user.

#### Response Example
```json
{
  "id": 123
}
```

### Links
#### GetUserByUserId
- **Description**: The `id` value returned in the response can be used as the `userId` parameter in `GET /users/{userId}`.
- **OperationId**: getUser
- **Parameters**:
  - **userId** (string) - The ID of the user to retrieve. This is dynamically set from the response body's `id` field.
```

--------------------------------

### Using Unique Paths for Differentiated Operations

Source: https://swagger.io/docs/specification/paths-and-operations

Illustrates how to handle operations that differ only by query parameters by creating distinct paths. This approach aligns with OpenAPI's definition of a unique operation as a combination of path and HTTP method.

```http
GET /users/findByName?firstName=value&lastName=value
GET /users/findByRole?role=value
```

--------------------------------

### Specify Multiple Import Mappings

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

Demonstrates how to specify multiple import mappings for different models using the `--import-mappings` argument. This allows for mapping several generated models to existing classes.

```bash
--import-mappings Pet=my.models.MyPet,Order=my.models.MyOrder
```

--------------------------------

### Scopes in Security

Source: https://swagger.io/docs/specification/authentication

Demonstrates how to define and use scopes for OAuth 2 and OpenID Connect security schemes.

```APIDOC
## Scopes in Security

### Description
Scopes are used in OAuth 2 and OpenID Connect to control permissions to user resources. They must be defined in `securitySchemes` and can be applied globally or per operation.

### Method
N/A (Configuration Example)

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
# Global Security with Scopes
security:
  - OAuth2:
      - scope1
      - scope2
  - OpenId:
      - scopeA
      - scopeB
  - BasicAuth: []
```

```yaml
# Scoped Security per Operation
paths:
  /users:
    get:
      summary: Get a list of users
      security:
        - OAuth2: [read]
    post:
      summary: Add a user
      security:
        - OAuth2: [write]
```

### Response
N/A

### Response Example
N/A
```

--------------------------------

### Load Multiple API Definitions with Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Illustrates how to configure Swagger UI to load and display multiple API definitions using the 'urls' parameter. Each definition in the array can have a 'url' and a 'name'. The 'urls.primaryName' option allows specifying which definition to load by default.

```javascript
const ui = SwaggerUI({
  dom_id: '#swagger-ui',
  urls: [
    { url: "/v2/swagger.json", name: "Petstore API" },
    { url: "/v3/swagger.json", name: "Another API" }
  ],
  urls.primaryName: "Petstore API" // Optional: Set default API to load
});
```

--------------------------------

### Run Swagger Editor Docker Image from DockerHub

Source: https://swagger.io/docs/open-source-tools/swagger-editor

Pulls and runs the Swagger Editor Docker image. It can be configured with environment variables to specify an API definition URL, a local definition file, a custom base URL, a different port, a Google Tag Manager ID, or custom generator/converter endpoints. The `URL` variable takes precedence over `SWAGGER_FILE` if both are set.

```docker
docker pull docker.swagger.io/swaggerapi/swagger-editor
docker run -d -p 80:8080 docker.swagger.io/swaggerapi/swagger-editor
```

```docker
docker run -d -p 80:8080 -e URL="https://petstore3.swagger.io/api/v3/openapi.json" docker.swagger.io/swaggerapi/swagger-editor
```

```docker
docker run -d -p 80:8080 -v $(pwd):/tmp -e SWAGGER_FILE=/tmp/swagger.json docker.swagger.io/swaggerapi/swagger-editor
```

```docker
docker run -d -p 80:8080 -e BASE_URL=/swagger-editor docker.swagger.io/swaggerapi/swagger-editor
```

```docker
docker run -d -p 80:80 -e PORT=80 docker.swagger.io/swaggerapi/swagger-editor
```

```docker
docker run -d -p 80:8080 -e GTM=GTM-XXXXXX docker.swagger.io/swaggerapi/swagger-editor
```

--------------------------------

### Use Defined Action

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This code shows how to invoke a previously defined action creator from anywhere a Swagger UI system reference is available. The `system.exampleActions.updateFavoriteColor("blue")` call executes the action defined in `MyActionPlugin`.

```javascript
// elsewhere
system.exampleActions.updateFavoriteColor("blue")
```

--------------------------------

### Programmatically Set Basic Authorization (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Sets values for a Basic authorization scheme programmatically. Returns an action.

```javascript
preauthorizeBasic('basicAuth', 'username', 'password');
```

--------------------------------

### Query Parameters Serialization

Source: https://swagger.io/docs/specification/serialization

Details the different serialization styles and explode options for query parameters in OpenAPI 3.0.

```APIDOC
## Query Parameters Serialization

Query parameters support the following `style` values:

*   **form** – (default) ampersand-separated values, also known as form-style query expansion. Corresponds to the `{?param_name}` URI template.
*   **spaceDelimited** – space-separated array values. Same as `collectionFormat: ssv` in OpenAPI 2.0. Has effect only for non-exploded arrays (`explode: false`), that is, the space separates the array values if the array is a _single parameter_ , as in `arr=a b c`.
*   **pipeDelimited** – pipeline-separated array values. Same as `collectionFormat: pipes` in OpenAPI 2.0. Has effect only for non-exploded arrays (`explode: false`), that is, the pipe separates the array values if the array is a _single parameter_ , as in `arr=a|b|c`.
*   **deepObject** – simple non-nested objects are serialized as `paramName[prop1]=value1&paramName[prop2]=value2&...`. The behavior for nested objects and arrays is undefined.

The default serialization method is `style: form` and `explode: true`. This corresponds to `collectionFormat: multi` from OpenAPI 2.0. Given the path `/users` with a query parameter `id`, the query string is serialized as follows:

| style          | explode | URI template     | Primitive value id = 5 | Array id = [3, 4, 5] | Object id = {"role": "admin", "firstName": "Alex"} |
|----------------|---------|------------------|------------------------|----------------------|------------------------------------------------------|
| form *         | true *  | /users{?id*}     | /users?id=5            | /users?id=3&id=4&id=5| /users?role=admin&firstName=Alex                     |
| form           | false   | /users{?id}      | /users?id=5            | /users?id=3,4,5      | /users?id=role,admin,firstName,Alex                  |
| spaceDelimited | true    | /users{?id*}     | n/a                    | /users?id=3&id=4&id=5| n/a                                                  |
| spaceDelimited | false   | n/a              | n/a                    | /users?id=3%204%205  | n/a                                                  |
| pipeDelimited  | true    | /users{?id*}     | n/a                    | /users?id=3&id=4&id=5| n/a                                                  |
| pipeDelimited  | false   | n/a              | n/a                    | /users?id=3|4|5      | n/a                                                  |
| deepObject     | true    | n/a              | n/a                    | n/a                  | /users?id[role]=admin&id[firstName]=Alex             |

* Default serialization method

Additionally, the `allowReserved` keyword specifies whether the reserved characters `:/?#[]@!$&'()*+,;=` in parameter values are allowed to be sent as they are, or should be percent-encoded. By default, `allowReserved` is `false`, and reserved characters are percent-encoded. For example, `/` is encoded as `%2F` (or `%2f`), so that the parameter value `quotes/h2g2.txt` will be sent as `quotes%2Fh2g2.txt`.
```

--------------------------------

### OpenAPI to RFC 6570 URI Template Mapping

Source: https://swagger.io/docs/specification/serialization

Shows the mapping between OpenAPI serialization keywords and RFC 6570 URI template modifiers. This helps in understanding how OpenAPI parameters translate into URI templates.

```text
Keyword| URI Template Modifier  
---|---
`style: simple`| none  
`style: label`| `.` prefix  
`style: matrix`| `;` prefix  
`style: form`| `?` or `&` prefix (depending on the parameter position in the query string)  
`style: pipeDelimited`| `?` or `&` prefix (depending on the parameter position in the query string) – but using pipes `                                              |`instead of commas`,` to join the array values  
`style: spaceDelimited`| `?` or `&` prefix (depending on the parameter position in the query string) – but using spaces instead of commas `,` to join the array values  
`explode: false`| none  
`explode: true`| `*` suffix  
`allowReserved: false`| none  
`allowReserved: true`| `+` prefix  
```

--------------------------------

### Default Parameter Values

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates how to set default values for optional parameters using the `default` keyword within the parameter's schema. This is useful for parameters like pagination offsets and limits.

```APIDOC
## Default Parameter Values

### Description
This section explains how to specify default values for optional API parameters using the `default` keyword. This ensures a parameter has a value even if the client does not provide one, commonly used for pagination controls.

### Method
GET

### Endpoint
/users

### Parameters
#### Query Parameters
- **offset** (integer) - Optional - The number of items to skip before starting to collect the result set. Defaults to 0.
- **limit** (integer) - Optional - The number of items to return. Defaults to 20. Ranges from 1 to 100.

### Request Example
```http
GET /users
GET /users?offset=30&limit=10
```

### Response
#### Success Response (200)
- **items** (array) - The list of user items.
- **total** (integer) - The total number of available items.

#### Response Example
```json
{
  "items": [
    { "id": 1, "name": "Alice" },
    { "id": 2, "name": "Bob" }
  ],
  "total": 50
}
```
```

--------------------------------

### Defining Parameters and Request Body for Links (YAML)

Source: https://swagger.io/docs/specification/links

Illustrates how to use `parameters` and `requestBody` keywords within a link definition to specify how input values are computed for the target operation. It shows referencing response bodies and using hard-coded values.

```yaml
links:
  GetUserByUserId:
    operationId: getUser
    parameters:
      userId: "$response.body#/id"
  SetManagerId:
    operationId: setUserManager
    requestBody: "$response.body#/id"
```

--------------------------------

### Define React Components in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This code shows how to provide React components to be integrated into the Swagger UI system. Components are defined within the `components` key of a plugin. Both class-based and stateless functional components can be provided.

```javascript
class HelloWorldClass extends React.Component {
  render() {
    return <h1>Hello World!</h1>
  }
}

const MyComponentPlugin = function(system) {
  return {
    components: {
      HelloWorldClass: HelloWorldClass,
      // components can just be functions, these are called "stateless components"
      HelloWorldStateless: () => <h1>Hello World!</h1>,
    }
  }
}
```

--------------------------------

### Required and Optional Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Explains how to mark parameters as required or optional, noting that path parameters are always required.

```APIDOC
## GET /users/{userId}

### Description
Retrieves a specific user by their ID.

### Method
GET

### Endpoint
/users/{userId}

### Path Parameters
- **userId** (integer) - Required - Numeric ID of the user to retrieve.

### Response
#### Success Response (200)
- **id** (integer) - The user's ID.
- **name** (string) - The user's name.

#### Response Example
```json
{
  "id": 123,
  "name": "John Doe"
}
```
```

--------------------------------

### Common Parameters (Path Level)

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates defining parameters at the path level, which are inherited by all operations under that path.

```APIDOC
## Path-Level Common Parameters

### Description
Parameters defined at the path level are shared across all operations (GET, POST, PUT, DELETE, etc.) within that path.

### Paths
#### /user/{id}
- **Parameters**:
  - **id** (integer) - Required - The user ID.

#### Operations under /user/{id}
- **GET**
  - `summary: Gets a user by ID`
- **PATCH**
  - `summary: Updates an existing user with the specified ID`
- **DELETE**
  - `summary: Deletes the user with the specified ID`

## Combined Path and Operation Level Parameters

### Description
Parameters can be defined at both the path and operation levels. Operation-level parameters supplement path-level parameters.

### Paths
#### /users/{id}
- **Parameters**:
  - **id** (integer) - Required - The user ID.

#### Operations under /users/{id}
- **GET**
  - `summary: Gets a user by ID`
  - **Parameters**:
    - **metadata** (boolean) - Optional - If true, returns only user metadata.
  - **Responses**:
    - "200":
      - `description: OK`

### Request Example (GET /users/{id}?metadata=true)
```
GET /users/123?metadata=true
```

## Overriding Path-Level Parameters

### Description
Path-level parameters can be redefined at the operation level, allowing for different configurations for the same parameter name across operations.

### Paths
#### /users/{id}
- **Parameters**:
  - **id** (integer) - Required - The user ID.

#### Operations under /users/{id}
- **DELETE**
  - `summary: Deletes the user with the specified ID.`
  - **Responses**:
    - "204":
      - `description: User was deleted.`

- **GET**
  - `summary: Gets one or more users by ID.`
  - **Parameters**:
    - **id** (array[integer]) - Required - A comma-separated list of user IDs.
      - `minItems: 1`
      - `explode: false`
      - `style: simple`
  - **Responses**:
    - "200":
      - `description: OK`

### Request Example (GET /users/1,5,7)
```
GET /users/1,5,7
```
```

--------------------------------

### OpenAPI 3.0 Basic Authentication Description

Source: https://swagger.io/docs/specification/authentication/basic-authentication

How to describe Basic Authentication using OpenAPI 3.0 specification.

```APIDOC
## OpenAPI 3.0 Basic Authentication Description

### Description
This example shows how to define Basic Authentication as a security scheme in OpenAPI 3.0. It includes global application of the scheme and operation-level application.

### Method
N/A (This is an OpenAPI specification example)

### Endpoint
N/A

### Parameters
None

### Request Example
```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    basicAuth: # <-- arbitrary name for the security scheme
      type: http
      scheme: basic

security:
  - basicAuth: [] # <-- use the same name here

paths:
  /something:
    get:
      security:
        - basicAuth: []
```

### Response
N/A
```

--------------------------------

### React App with Swagger Editor Integration (index.js)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This JavaScript code demonstrates how to integrate the SwaggerEditor component into a React application. It imports React, ReactDOM, SwaggerEditor, and its CSS. It defines a React component that renders a SwaggerEditor instance, loading a specification from a given URL. The Monaco editor environment is also configured to correctly load worker files.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import SwaggerEditor from 'swagger-editor';
import 'swagger-editor/swagger-editor.css';


const url = "https://raw.githubusercontent.com/asyncapi/spec/v2.2.0/examples/streetlights-kafka.yml";


const MyApp = () => (
  <div>
    <h1>SwaggerEditor Integration</h1>
    <SwaggerEditor url={url} />
  </div>
);


self.MonacoEnvironment = {
  /**
   * We're building into the dist/ folder. When application starts on
   * URL=https://example.com then SwaggerEditor will look for
   * `apidom.worker.js` on https://example.com/dist/apidom.worker.js and
   * `editor.worker` on https://example.com/dist/editor.worker.js.
   */
  baseUrl: `${document.baseURI || location.href}dist/`,
}

ReactDOM.render(<MyApp />, document.getElementById('swagger-editor'));

```

--------------------------------

### Specifying XML Prefixes and Namespaces

Source: https://swagger.io/docs/specification/data-models/representing-xml

Demonstrates how to define XML namespaces and prefixes for elements to prevent naming conflicts and adhere to XML schema standards. The `xml/prefix` and `xml/namespace` properties are used for this purpose.

```yaml
xml:
  prefix: "smp"
  namespace: "http://example.com/schema"
```

```yaml
book:
  type: object
  properties:
    id:
      type: integer
    title:
      type: string
    author:
      type: string
  xml:
    prefix: "smp"
    namespace: "http://example.com/schema"
```

```xml
<smp:book xmlns:smp="http://example.com/schema">
  <id>0</id>
  <title>string</title>
  <author>string</author>
</smp:book>
```

--------------------------------

### Define Multiple API Servers in OpenAPI

Source: https://swagger.io/docs/specification/api-host-and-base-path

Allows defining multiple base URLs for an API, such as production and sandbox environments. Each server entry includes a 'url' and an optional 'description' to clarify its purpose.

```yaml
servers:
  - url: https://api.example.com/v1
    description: Production server (uses live data)
  - url: https://sandbox-api.example.com:8443/v1
    description: Sandbox server (uses test data)
```

--------------------------------

### POST /users

Source: https://swagger.io/docs/specification/links

Creates a user and returns the user ID. The response includes a link to retrieve the created user by their ID.

```APIDOC
## POST /users

### Description
Creates a user and returns the user ID. The response includes a link to retrieve the created user by their ID.

### Method
POST

### Endpoint
/users

### Parameters
#### Request Body
- **user** (User) - Required - A JSON object that contains the user name and age.

### Request Example
```json
{
  "name": "John Doe",
  "age": 30
}
```

### Response
#### Success Response (201)
- **id** (integer) - ID of the created user.

#### Response Example
```json
{
  "id": 123
}
```

### Links
#### GetUserByUserId
- **Description**: The `id` value returned in the response can be used as the `userId` parameter in `GET /users/{userId}`.
- **Operation**: `getUser` (defined by `operationId`)
- **Parameters**: `userId` = `$response.body#/id`
```

--------------------------------

### Retrieve Java Configuration Options

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

This command retrieves a list of available configuration options for the Java language generator in Swagger Codegen. This helps in understanding what can be customized.

```bash
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar config-help -l java
```

--------------------------------

### Path Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Details on how to define and use path parameters, which are variable parts of a URL path used to identify specific resources.

```APIDOC
## GET /users/{userId}

### Description
Retrieves a specific user resource using their unique ID provided in the URL path.

### Method
GET

### Endpoint
/users/{userId}

### Parameters
#### Path Parameters
- **userId** (integer) - Required - The unique identifier for the user.

### Request Example
```
GET /users/123
```

### Response
#### Success Response (200)
- **id** (integer) - The user's ID.
- **name** (string) - The user's name.

#### Response Example
```json
{
  "example": "{\"id\": 123, \"name\": \"John Doe\"}"
}
```
```

--------------------------------

### PATCH /pets - Using anyOf for Flexible Schema Matching

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This endpoint illustrates the use of `anyOf` to allow the request body to be valid against one or more schemas. It provides flexibility by accepting properties from `PetByAge` or `PetByType` or both.

```APIDOC
## PATCH /pets (anyOf Example)

### Description
Updates a pet item, allowing the request body to conform to either `PetByAge` schema, `PetByType` schema, or both. This provides flexible data submission.

### Method
PATCH

### Endpoint
/pets

### Parameters
#### Request Body
- **age** (integer) - Optional - The age of the pet. Required for `PetByAge`.
- **nickname** (string) - Optional - A nickname for the pet. Part of `PetByAge`.
- **pet_type** (string) - Optional - The type of pet (e.g., 'Cat', 'Dog'). Required for `PetByType`. Enum: [Cat, Dog].
- **hunts** (boolean) - Optional - Specific to 'Cat' type. Indicates if the cat hunts. Part of `PetByType`.

### Request Example
```json
{
  "age": 1
}
```

```json
{
  "pet_type": "Cat",
  "hunts": true
}
```

```json
{
  "nickname": "Fido",
  "pet_type": "Dog",
  "age": 4
}
```

### Response
#### Success Response (200)
- **description** (string) - Indicates the operation was successful.

#### Response Example
```json
{
  "message": "Pet update request processed"
}
```
```

--------------------------------

### Apply OpenID Connect Security Globally in OpenAPI

Source: https://swagger.io/docs/specification/authentication/openid-connect-discovery

This OpenAPI 3.0 snippet shows how to apply a defined OpenID Connect security scheme globally to all operations in an API. It references the 'openId' security scheme defined in 'components/securitySchemes' and lists the required scopes.

```yaml
security:
  - openId:
      - pets_read
      - pets_write
      - admin
```

--------------------------------

### Use a Selector in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This snippet illustrates how to access a defined selector from anywhere within the system that has access to the `system` reference. The selector is called like a function to retrieve the corresponding state value.

```javascript
system.exampleSelectors.myFavoriteColor() // gets `favColor` in state for you
```

--------------------------------

### Defining Security Schemes

Source: https://swagger.io/docs/specification/authentication

This section details how to define various security schemes like BasicAuth, BearerAuth, ApiKeyAuth, OpenID Connect, and OAuth2 within the `components/securitySchemes` section of your OpenAPI specification.

```APIDOC
## Defining Security Schemes

All security schemes used by the API must be defined in the global `components/securitySchemes` section. This section contains a list of named security schemes, where each scheme can be of `type`:
  * `http` – for Basic, Bearer and other HTTP authentications schemes
  * `apiKey` – for API keys and cookie authentication
  * `oauth2` – for OAuth 2
  * `openIdConnect` – for OpenID Connect Discovery

### Example:
```yaml
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic

    BearerAuth:
      type: http
      scheme: bearer

    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key

    OpenID:
      type: openIdConnect
      openIdConnectUrl: https://example.com/.well-known/openid-configuration

    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://example.com/oauth/authorize
          tokenUrl: https://example.com/oauth/token
          scopes:
            read: Grants read access
            write: Grants write access
            admin: Grants access to admin operations
```
```

--------------------------------

### Server URL Format

Source: https://swagger.io/docs/specification/api-host-and-base-path

Explains the standard format for server URLs according to RFC 3986.

```APIDOC
## Server URL Format

### Description
Details the structure of a server URL, which follows RFC 3986.

### Format
```
scheme://host[:port][/path]
```

### Examples
```
https://api.example.com
https://api.example.com:8443/v1/reports
http://localhost:3025/v1
ws://api.example.com/v1
/v1/reports
```

**Note:** Server URLs must not include query string parameters.
```

--------------------------------

### Compose Swagger UI with React Components

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This React code snippet demonstrates how to compose Swagger UI within a React application. It imports necessary components and plugins from 'swagger-ui-react' and 'swagger-editor'. The 'SwaggerUI' component is configured with a URL and various plugins to customize its functionality and appearance. The component is then rendered into the DOM.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import SwaggerUI from 'swagger-ui-react';
import 'swagger-ui-react/swagger-ui.css';
import ModalsPlugin from 'swagger-editor/plugins/modals';
import DialogsPlugin from 'swagger-editor/plugins/dialogs';
import DropdownMenuPlugin from 'swagger-editor/plugins/dropdown-menu';
import DropzonePlugin from 'swagger-editor/plugins/dropzone';
import VersionsPlugin from 'swagger-editor/plugins/versions';
import EditorTextareaPlugin from 'swagger-editor/plugins/editor-textarea';
import EditorMonacoPlugin from 'swagger-editor/plugins/editor-monaco';
import EditorMonacoLanguageApiDOMPlugin from 'swagger-editor/plugins/editor-monaco-language-apidom';
import EditorContentReadOnlyPlugin from 'swagger-editor/plugins/editor-content-read-only';
import EditorContentOriginPlugin from 'swagger-editor/plugins/editor-content-origin';
import EditorContentTypePlugin from 'swagger-editor/plugins/editor-content-type';
import EditorContentPersistencePlugin from 'swagger-editor/plugins/editor-content-persistence';
import EditorContentFixturesPlugin from 'swagger-editor/plugins/editor-content-fixtures';
import EditorPreviewPlugin from 'swagger-editor/plugins/editor-preview';
import EditorPreviewSwaggerUIPlugin from 'swagger-editor/plugins/editor-preview-swagger-ui';
import EditorPreviewAsyncAPIPlugin from 'swagger-editor/plugins/editor-preview-asyncapi';
import EditorPreviewApiDesignSystemsPlugin from 'swagger-editor/plugins/editor-preview-api-design-systems';
import TopBarPlugin from 'swagger-editor/plugins/top-bar';
import SplashScreenPlugin from 'swagger-editor/plugins/splash-screen';
import LayoutPlugin from 'swagger-editor/plugins/layout';
import EditorSafeRenderPlugin from 'swagger-editor/plugins/editor-safe-render';

const SwaggerEditor = () => {
  return (
    <SwaggerUI
      url={url}
      plugins={[
        ModalsPlugin,
        DialogsPlugin,
        DropdownMenuPlugin,
        DropzonePlugin,
        VersionsPlugin,
        EditorTextareaPlugin,
        EditorMonacoPlugin,
        EditorMonacoLanguageApiDOMPlugin,
        EditorContentReadOnlyPlugin,
        EditorContentOriginPlugin,
        EditorContentTypePlugin,
        EditorContentPersistencePlugin,
        EditorContentFixturesPlugin,
        EditorPreviewPlugin,
        EditorPreviewSwaggerUIPlugin,
        EditorPreviewAsyncAPIPlugin,
        EditorPreviewApiDesignSystemsPlugin,
        TopBarPlugin,
        SplashScreenPlugin,
        LayoutPlugin,
        EditorSafeRenderPlugin,
      ]}
      layout="StandaloneLayout"
    />
  );
};

ReactDOM.render(<SwaggerEditor />, document.getElementById('swagger-editor'));

```

--------------------------------

### Describe OpenID Connect Discovery in OpenAPI 3.0

Source: https://swagger.io/docs/specification/authentication/openid-connect-discovery

This OpenAPI 3.0 snippet demonstrates how to define an OpenID Connect security scheme. It specifies the 'openIdConnect' type and the URL for the discovery endpoint.

```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    openId:
      type: openIdConnect
      openIdConnectUrl: https://example.com/.well-known/openid-configuration
```

--------------------------------

### SwaggerUI Standalone Mode with Preview Plugins (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This JavaScript code configures SwaggerUI in standalone mode, enabling the use of preview plugins for AsyncAPI and API Design Systems. It includes the necessary imports and sets the 'StandaloneLayout' to provide a top bar for URL input.

```javascript
import SwaggerUI from 'swagger-ui';
import SwaggerUIStandalonePreset from 'swagger-ui/dist/swagger-ui-standalone-preset';
import 'swagger-ui/dist/swagger-ui.css';
import 'swagger-editor/swagger-editor.css';
import EditorContentTypePlugin from 'swagger-editor/plugins/editor-content-type';
import EditorPreviewAsyncAPIPlugin from 'swagger-editor/plugins/editor-preview-asyncapi';
import EditorPreviewAPIDesignSystemsPlugin from 'swagger-editor/plugins/editor-preview-api-design-systems';
import SwaggerUIAdapterPlugin from 'swagger-editor/plugins/swagger-ui-adapter';

SwaggerUI({
  url: 'https://petstore.swagger.io/v2/swagger.json',
  dom_id: '#swagger-ui',
  presets: [SwaggerUI.presets.apis, SwaggerUIStandalonePreset],
  plugins: [
    EditorContentTypePlugin,
    EditorPreviewAsyncAPIPlugin,
    EditorPreviewAPIDesignSystemsPlugin,
    SwaggerUIAdapterPlugin,
    SwaggerUI.plugins.DownloadUrl,
  ],
  layout: 'StandaloneLayout',
});
```

--------------------------------

### Defining 401 Unauthorized Response

Source: https://swagger.io/docs/specification/authentication/api-keys

Illustrates how to define a standard 401 Unauthorized response for missing or invalid API keys, including the WWW-Authenticate header.

```APIDOC
## Defining 401 Unauthorized Response

### Description
This example shows how to define a `401 Unauthorized` response that is returned when an API key is missing or invalid. It includes the `WWW-Authenticate` header and demonstrates referencing a common response definition.

### Example with 401 Response Definition
```yaml
paths:
  /something:
    get:
      # ... other operation details ...
      responses:
        "200":
          description: OK (successfully authenticated)
        '401':
          $ref: "#/components/responses/UnauthorizedError"
    post:
      # ... other operation details ...
      responses:
        '401':
          $ref: "#/components/responses/UnauthorizedError"

components:
  responses:
    UnauthorizedError:
      description: API key is missing or invalid
      headers:
        WWW_Authenticate:
          schema:
            type: string
```

**Note:** The `UnauthorizedError` response can be defined once in `components/responses` and then referenced using `$ref` throughout the OpenAPI document.
```

--------------------------------

### Runtime Expression Syntax

Source: https://swagger.io/docs/specification/links

Details the syntax and usage of runtime expressions in OpenAPI, which allow dynamic extraction of values from API requests and responses.

```APIDOC
## Runtime Expression Syntax

OpenAPI runtime expressions are syntax for extracting various values from an operation’s request and response. Links use runtime expressions to specify the parameter values to be passed to the linked operation. The expressions are called “runtime” because the values are extracted from the actual request and response of the API call and not, say, the example values provided in the API specification.

### Expression Syntax

| Expression                    | Description                                                                                                |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `$url`                        | The full request URL, including the query string.                                                          |
| `$method`                     | Request HTTP method, such as GET or POST.                                                                  |
| `$request.query._param_name_` | The value of the specified query parameter. Must be defined in the operation’s `parameters` section.       |
| `$request.path._param_name_`  | The value of the specified path parameter. Must be defined in the operation’s `parameters` section.        |
| `$request.header._header_name_`| The value of the specified request header. Must be defined in the operation’s `parameters` section.      |
| `$request.body`               | The entire request body.                                                                                   |
| `$request.body_#/foo/bar_`    | A portion of the request body specified by a JSON Pointer.                                                 |
| `$statusCode`                 | HTTP status code of the response. For example, 200 or 404.                                                 |
| `$response.header._header_name_`| The complete value of the specified response header, as a string. Header names are case-insensitive.       |
| `$response.body`              | The entire response body.                                                                                  |
| `$response.body_#/foo/bar_`   | A portion of the response body specified by a JSON Pointer.                                                |
| `foo{$request.path.id}bar`    | Enclose an expression into `{}` curly braces to embed it into a string.                                    |

**Notes:**
* The evaluated expression has the same type as the referenced value, unless noted otherwise.
* If a runtime expression cannot be evaluated, no parameter value is passed to the target operation.

### Example Request and Response

**Request:**
```http
GET /users?limit=2&total=true
Host: api.example.com
Accept: application/json
```

**Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json
X-Total-Count: 37

{
  "prev_offset": 0,
  "next_offset": 2,
  "users": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ]
}
```

### Runtime Expression Evaluation Examples

| Expression                      | Result                                  | Comments                                                                        |
| ------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------- |
| `$url`                          | `http://api.example.com/users?limit=2&total=true` |                                                                                 |
| `$method`                       | `GET`                                   |                                                                                 |
| `$request.query.total`          | `true`                                  | `total` must be defined as a query parameter.                                   |
| `$statusCode`                   | `200`                                   |                                                                                 |
| `$response.header.x-total-count`| `37`                                    | Assuming `X-Total-Count` is defined as a response header. Case-insensitive.     |
| `$response.body#/next_offset`   | `2`                                     |                                                                                 |
| `$response.body#/users/0`       | `{"id": 1, "name": "Alice"}`        | JSON Pointer uses 0-based indexes. No wildcard syntax (e.g., `$response.body#/users/*/id` is invalid). |
| `$response.body#/users/1`       | `{"id": 2, "name": "Bob"}`          |                                                                                 |
| `$response.body#/users/1/name`  | `Bob`                                   |                                                                                 |
| `ID_{$response.body#/users/1/id}`| `ID_2`                                  | Embedded expression within a string.                                            |
```

--------------------------------

### Default componentDidCatch Implementation

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

The default implementation of the `componentDidCatch` function within the safe-render plugin. It uses `console.error` to log any errors caught by the error boundaries.

```javascript
export const componentDidCatch = console.error;
```

--------------------------------

### Header Parameters Serialization

Source: https://swagger.io/docs/specification/serialization

Explains the 'simple' style for header parameters, including how array and object values are serialized with and without the 'explode' modifier.

```APIDOC
## Header Parameters Serialization

### Description
Header parameters always use the `simple` style, which means comma-separated values. The `explode` keyword controls object serialization.

### Method
GET (Example)

### Endpoint
`/example

### Parameters
#### Header Parameters
- **X-MyHeader** (string) - Required - The header name.

### Request Example
```
GET /example HTTP/1.1
Host: example.com
X-MyHeader: 5
```

### Response
#### Success Response (200)
- **message** (string) - A success message.

#### Response Example
```json
{
  "message": "Header processed successfully"
}
```
```

--------------------------------

### Multipart File Upload with Additional Data

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Details how to upload a file along with other form data using multipart/form-data requests.

```APIDOC
## POST /upload

### Description
Uploads a file along with other data fields using a multipart request.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **orderId** (integer) - Required - The ID of the order associated with the upload.
- **userId** (integer) - Required - The ID of the user performing the upload.
- **fileName** (string, format: binary) - Required - The file to be uploaded.

### Request Example
```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          orderId:
            type: integer
          userId:
            type: integer
          fileName:
            type: string
            format: binary
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of successful upload.

#### Response Example
```json
{
  "message": "File and data uploaded successfully"
}
```
```

--------------------------------

### Customizing Wrapper and Item Names

Source: https://swagger.io/docs/specification/data-models/representing-xml

Illustrates how to specify distinct names for the wrapping element and individual array items using `xml/wrapped: true` and `xml/name`.

```APIDOC
## Customizing Wrapper and Item Names

### Description
Allows different names for the wrapping element and array items using `xml/wrapped: true` and `xml/name`.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
- **books-array** (array[string]) - An array of strings, with a custom wrapper and item name.

#### Response Example
```xml
<books-array>
  <item>one</item>
  <item>two</item>
  <item>three</item>
</books-array>
```
```

--------------------------------

### PATCH /pets - Using allOf for Schema Combination

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This endpoint demonstrates how to use `allOf` to combine a base schema with specific subschemas. It utilizes `oneOf` and `discriminator` to select the appropriate schema based on the `pet_type` property.

```APIDOC
## PATCH /pets

### Description
Updates a pet item by combining a base schema with specific properties based on the pet type. Uses `oneOf` and `discriminator` for schema selection.

### Method
PATCH

### Endpoint
/pets

### Parameters
#### Request Body
- **pet_type** (string) - Required - Specifies the type of pet (e.g., 'Cat', 'Dog'). Used as a discriminator.
- **bark** (boolean) - Optional - Specific to 'Dog' type. Indicates if the dog barks.
- **breed** (string) - Optional - Specific to 'Dog' type. Enum: [Dingo, Husky, Retriever, Shepherd].
- **hunts** (boolean) - Optional - Specific to 'Cat' type. Indicates if the cat hunts.
- **age** (integer) - Optional - Specific to 'Cat' type. The age of the cat.

### Request Example
```json
{
  "pet_type": "Cat",
  "age": 3
}
```

```json
{
  "pet_type": "Dog",
  "bark": true
}
```

```json
{
  "pet_type": "Dog",
  "bark": false,
  "breed": "Dingo"
}
```

### Response
#### Success Response (200)
- **description** (string) - Indicates the operation was successful.

#### Response Example
```json
{
  "message": "Pet updated successfully"
}
```
```

--------------------------------

### Describe Multiple File Uploads in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Defines the upload of an arbitrary number of files using `multipart/form-data`. The `fileName` property is defined as an array of strings, where each string item represents a file with `format: binary`.

```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          filename:
            type: array
            items:
              type: string
              format: binary
```

--------------------------------

### Reusing Responses

Source: https://swagger.io/docs/specification/describing-responses

Demonstrates how to define common responses (like errors) in the `components.responses` section and reference them using `$ref` in multiple operations.

```APIDOC
## Reusing Responses

### Description
Common responses, such as error messages for 'Unauthorized' or 'NotFound' status codes, can be defined once in the `components.responses` section of your OpenAPI document. These definitions can then be reused across multiple operations by referencing them using the `$ref` keyword. This promotes consistency and reduces redundancy in your API documentation.

### Example Usage

**Defining a reusable response:**
```yaml
components:
  responses:
    Unauthorized:
      description: Unauthorized
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/Error"
    NotFound:
      description: The specified resource was not found
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/Error"
```

**Referencing the reusable response in an operation:**
```yaml
paths:
  /users/{id}:
    get:
      summary: Gets a user by ID.
      responses:
        "200":
          description: OK
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/User"
        "401":
          $ref: "#/components/responses/Unauthorized"
        "404":
          $ref: "#/components/responses/NotFound"
```
```

--------------------------------

### Specify Multiple Import Mappings Separately

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

An alternative way to specify multiple import mappings by using the `--import-mappings` argument multiple times, once for each model mapping.

```bash
--import-mappings Pet=my.models.MyPet --import-mappings Order=my.models.MyOrder
```

--------------------------------

### Referencing a Schema Object with $ref

Source: https://swagger.io/docs/specification/using-ref

Shows how to define a schema object ('user') and then reference it within a response definition using the $ref keyword. This promotes DRY principles in API documentation.

```yaml
"components":
2
  {
3
    "schemas":
4
      {
5
        "user":
6
          {
7
            "properties":
8
              {
                "id": { "type": "integer" },
                "name": { "type": "string" }
              }
          }
      }
  }

"responses":
2
  {
3
    "200":
4
      {
5
        "description": "The response",
6
        "schema": { "$ref": "#/components/schemas/user" }
      }
  }
```

```yaml
components:
2
  schemas:
3
    User:
4
      properties:
5
        id:
6
          type: integer
7
        name:
8
          type: string

responses:
2
  "200":
3
    description: The response
4
    schema:
5
      $ref: "#/components/schemas/User"
```

--------------------------------

### Generated URI Template from OpenAPI Definition

Source: https://swagger.io/docs/specification/serialization

The resulting RFC 6570 URI template generated from the provided OpenAPI path and parameter definitions. This template can be used by client libraries for URL construction.

```text
/users{;id*}{?metadata}
```

--------------------------------

### Generate Client with Custom Codegen Module (Windows)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators

This command generates a client library using a custom codegen module on Windows. It's similar to the Linux/macOS version but uses a semicolon (;) instead of a colon (:) to separate JARs in the classpath.

```java
java -cp output/myLibrary/target/myClientCodegen-swagger-codegen-1.0.0.jar;modules/swagger-codegen-cli/target/swagger-codegen-cli.jar io.swagger.codegen.v3.cli.SwaggerCodegen
```

--------------------------------

### Query Parameters with Reserved Characters

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates how to handle reserved characters in query parameters by either percent-encoding them or using `allowReserved: true`.

```APIDOC
## GET /file

### Description
Retrieves a file, with the file path specified in the query parameter. Reserved characters in the path must be percent-encoded.

### Method
GET

### Endpoint
/file

### Query Parameters
- **path** (string) - Required - The path to the file, with reserved characters percent-encoded.

### Request Example
```
GET /file?path=quotes%2Fh2g2.txt
```

### Response
#### Success Response (200)
- **fileContent** (string) - The content of the requested file.

#### Response Example
```json
{
  "fileContent": "This is the content of the file."
}
```

## GET /file (Allow Reserved)

### Description
Retrieves a file, allowing reserved characters in the query parameter to be sent without percent-encoding.

### Method
GET

### Endpoint
/file

### Query Parameters
- **path** (string) - Required - The path to the file, allowing reserved characters.
  * **allowReserved**: true

### Request Example
```
GET /file?path=quotes/h2g2.txt
```

### Response
#### Success Response (200)
- **fileContent** (string) - The content of the requested file.

#### Response Example
```json
{
  "fileContent": "This is the content of the file."
}
```
```

--------------------------------

### Response with Alternate Schemas (oneOf/anyOf)

Source: https://swagger.io/docs/specification/describing-responses

Demonstrates how to define a response that can conform to one of several different schemas, such as different pet types.

```APIDOC
## Response with Alternate Schemas

### Description
This response can be one of several defined schemas (e.g., Cat, Dog, Hamster).

### Method
(Not specified in example, applies to any method)

### Endpoint
(Not specified in example)

### Parameters
None

### Response
#### Success Response (200)
- **Schema**: oneOf (Cat, Dog, Hamster)

#### Response Example
(Example depends on which schema is returned, e.g., a Cat object, a Dog object, or a Hamster object)
```

--------------------------------

### Configure Swagger UI via URL Query Parameters

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Shows how to enable and use URL query parameters to override Swagger UI configuration. When 'queryConfigEnabled' is true, parameters like 'configUrl', 'url', and 'dom_id' can be set directly in the URL.

```javascript
const ui = SwaggerUI({
  dom_id: '#swagger-ui',
  queryConfigEnabled: true
});

// Example URL: ?url=https://petstore.swagger.io/v2/swagger.json&dom_id=my-swagger-container
```

--------------------------------

### Reference Shared Schema for Multiple Media Types in OpenAPI

Source: https://swagger.io/docs/specification/media-types

This snippet illustrates how to define a common schema in the `components/schemas` section and reference it for multiple media types (application/json and application/xml) within an API response. This promotes reusability and reduces redundancy in the OpenAPI specification.

```yaml
paths:
  /employees:
    get:
      responses:
        "200": # Response
          description: OK
          content: # Response body
            application/json: # Media type
              schema:
                $ref: "#/components/schemas/Employee" # Reference to object definition
            application/xml: # Media type
              schema:
                $ref: "#/components/schemas/Employee" # Reference to object definition
components:
  schemas:
    Employee: # Object definition
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
        fullTime:
          type: boolean
```

--------------------------------

### API Key Transmission Methods

Source: https://swagger.io/docs/specification/authentication/api-keys

Demonstrates the three primary ways an API key can be transmitted: as a query string parameter, as a custom request header, or as a cookie.

```http
GET /something?api_key=abcdef12345
```

```http
GET /something HTTP/1.1
X-API-Key: abcdef12345
```

```http
GET /something HTTP/1.1
Cookie: X-API-KEY=abcdef12345
```

--------------------------------

### Configuring Wrapped XML Array

Source: https://swagger.io/docs/specification/data-models/representing-xml

Shows how to use the `xml/wrapped: true` property to add a single wrapping element around the array items.

```APIDOC
## Configuring Wrapped XML Array

### Description
Adds a wrapping element around array items using `xml/wrapped: true`.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
- **books** (array[string]) - An array of strings, wrapped in a parent element.

#### Response Example
```xml
<books>
  <books>one</books>
  <books>two</books>
  <books>three</books>
</books>
```
```

--------------------------------

### Create Custom Codegen Module with Swagger Codegen CLI

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators

This command initializes a new project for creating custom Swagger client codegen modules. It specifies the output directory, the name of the new codegen library, and the Java package for the generated code.

```java
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar meta \
  -o output/myLibrary -n myClientCodegen -p com.my.company.codegen
```

--------------------------------

### Apply Global Security Schemes (YAML)

Source: https://swagger.io/docs/specification/authentication

This YAML snippet shows how to apply defined security schemes globally to an entire API using the 'security' keyword at the root level. It illustrates applying ApiKeyAuth and OAuth2 schemes, with scopes for OAuth2.

```yaml
security:
  - ApiKeyAuth: []
  - OAuth2:
      - read
      - write
# The syntax is:
# - scheme name:
#     - scope 1
#     - scope 2
```

--------------------------------

### PATCH /pets

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Updates a pet's information. The `pet_type` field cannot be an integer.

```APIDOC
## PATCH /pets

### Description
Updates a pet's information. The `pet_type` field is restricted to exclude integer types.

### Method
PATCH

### Endpoint
/pets

### Parameters
#### Request Body
- **pet_type** (string | array | boolean | number | object) - Required - The type of the pet. Must not be an integer.

### Request Example
```json
{
  "pet_type": "Cat"
}
```

### Response
#### Success Response (200)
- **description** (string) - Indicates that the pet information was updated successfully.

#### Response Example
```json
{
  "message": "Pet updated successfully"
}
```
```

--------------------------------

### Escaping Special Characters in JSON Pointers

Source: https://swagger.io/docs/specification/using-ref

Demonstrates how to escape the special characters '~' and '/' when they appear literally within a path in a JSON Pointer used with $ref. This ensures correct parsing of complex paths.

```yaml
$ref: "#/paths/~1blogs~1{blog_id}~1new~0posts"
```

--------------------------------

### POST /users

Source: https://swagger.io/docs/specification/links

This endpoint creates a new user and returns the ID of the created user. This ID can then be used in subsequent operations.

```APIDOC
## POST /users

### Description
Creates a new user with the provided name and age. The response includes the unique identifier for the newly created user.

### Method
POST

### Endpoint
/users

### Parameters
#### Request Body
- **name** (string) - Required - The name of the user.
- **age** (integer) - Required - The age of the user.

### Request Example
```json
{
  "name": "Alex",
  "age": 27
}
```

### Response
#### Success Response (201 Created)
- **id** (integer) - The unique identifier of the created user.

#### Response Example
```json
{
  "id": 305
}
```
```

--------------------------------

### Increase Node.js Heap Limit for Bundling

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This command sets the Node.js environment variable 'NODE_OPTIONS' to '--max_old_space_size=4096'. This is used to resolve 'JavaScript heap out of memory' errors that can occur when bundling large projects using swagger-editor@5.

```bash
export NODE_OPTIONS="--max_old_space_size=4096"
```

--------------------------------

### Define Basic Selector in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This snippet shows how to define a simple selector within a plugin. Selectors retrieve data from the system's state. They are defined under the `selectors` key within a plugin's `statePlugins` configuration.

```javascript
const MySelectorPlugin = function(system) {
  return {
    statePlugins: {
      example: {
        selectors: {
          myFavoriteColor: (state) => state.get("favColor")
        }
      }
    }
  }
}
```

--------------------------------

### Define Multiple Media Types in OpenAPI Response

Source: https://swagger.io/docs/specification/media-types

This snippet demonstrates how to define multiple media types (e.g., application/json and application/xml) for a single API response in an OpenAPI specification. It shows the structure for specifying the schema for each media type directly within the response content.

```yaml
paths:
  /employees:
    get:
      summary: Returns a list of employees.
      responses:
        "200": # Response
          description: OK
          content: # Response body
            application/json: # One of media types
              schema:
                type: object
                properties:
                  id:
                    type: integer
                  name:
                    type: string
                  fullTime:
                    type: boolean
            application/xml: # Another media types
              schema:
                type: object
                properties:
                  id:
                    type: integer
                  name:
                    type: string
                  fullTime:
                    type: boolean
```

--------------------------------

### Reusing Link Definitions in OpenAPI (YAML)

Source: https://swagger.io/docs/specification/links

This YAML snippet demonstrates how to define a link in the 'components/links' section and reference it from multiple operations ('createUser' and 'updateUser') using '$ref'. This promotes code reuse by defining the link once and referencing it where needed.

```yaml
paths:
  /users:
    post:
      summary: Create a user
      operationId: createUser
      responses:
        '201':
          description: Created
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: integer
                    format: int64
                    description: ID of the created user.
          links:
            GetUserByUserId:
              $ref: '#/components/links/GetUserByUserId'
  /user/{userId}:
    patch:
      summary: Update user
      operationId: updateUser
      responses:
        '200':
          description: The updated user object
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
          links:
            GetUserByUserId:
              $ref: '#/components/links/GetUserByUserId'
    get:
      summary: Get a user by ID
      operationId: getUser
components:
  links:
    GetUserByUserId:
      description: >
        The `id` value returned in the response can be used as
        the `userId` parameter in `GET /users/{userId}`.
      operationId: getUser
      parameters:
        userId: '$response.body#/id'
```

--------------------------------

### Relative OpenID Connect Discovery URL in OpenAPI

Source: https://swagger.io/docs/specification/authentication/openid-connect-discovery

This OpenAPI 3.0 snippet demonstrates using a relative URL for the 'openIdConnectUrl' within a security scheme definition. When combined with a server URL, this allows for more flexible endpoint configuration.

```yaml
servers:
  - url: https://api.example.com/v2

components:
  securitySchemes:
    openId:
      type: openIdConnect
      openIdConnectUrl: /.well-known/openid-configuration
```

--------------------------------

### Query Parameter with Reserved Characters

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates how to handle reserved characters in query parameters by percent-encoding them. If `allowReserved: true` is set, these characters are sent literally.

```yaml
parameters:
  - in: query
    name: path
    required: true
    schema:
      type: string
    allowReserved: true
```

--------------------------------

### OpenAPI 3.0 Servers Array

Source: https://swagger.io/docs/specification/api-host-and-base-path

Illustrates the use of the 'servers' array in OpenAPI 3.0 to define API base URLs.

```APIDOC
## OpenAPI Servers Configuration

### Description
Defines the base URLs for the API using the `servers` array in OpenAPI 3.0.

### Code Example
```yaml
servers:
  - url: https://api.example.com/v1    # The "url: " prefix is required
```
```

--------------------------------

### Configure npm for Older React Versions with Swagger Editor

Source: https://swagger.io/docs/open-source-tools/swagger-editor

This JSON configuration demonstrates how to use npm `overrides` to ensure that the `swagger-editor` npm package uses a specific version of React (e.g., React 17.0.2) instead of the default React 18. It also shows how to manage `react-redux` version compatibility.

```json
{
  "dependencies": {
    "react": "=17.0.2",
    "react-dom": "=17.0.2"
  },
  "overrides": {
    "swagger-editor": {
      "react": "$react",
      "react": "$react-dom",
      "react-redux": "^8"
    }
  }
}
```

--------------------------------

### OpenAPI 3.0 API Key Security Scheme

Source: https://swagger.io/docs/specification/authentication/api-keys

Shows how to define an API key security scheme in OpenAPI 3.0, specifying its type, location, and name.

```APIDOC
## OpenAPI 3.0 API Key Security Scheme

### Description
This section details how to define an API key security scheme in OpenAPI 3.0. It includes defining the key's name and where it is located (header, query, or cookie), and then applying it globally or to specific operations.

### Defining the Security Scheme
```yaml
components:
  securitySchemes:
    ApiKeyAuth: # Arbitrary name for the security scheme
      type: apiKey
      in: header # Location: 'header', 'query', or 'cookie'
      name: X-API-KEY # Name of the header, query parameter, or cookie
```

### Applying Security Globally
To apply the defined API key scheme to all operations:
```yaml
security:
  - ApiKeyAuth: [] # Use the name defined in securitySchemes
```

### Applying Security to Specific Operations
To apply the API key scheme only to a particular operation:
```yaml
paths:
  /something:
    get:
      # Operation-specific security:
      security:
        - ApiKeyAuth: []
      responses:
        "200":
          description: OK (successfully authenticated)
```

**Note:** The `securitySchemes` section alone is not sufficient; the `security` key must also be used for the API key to take effect.
```

--------------------------------

### Generate Client with JSON Configuration

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

This command generates a Java client using Swagger Codegen, specifying an input Swagger definition, output directory, and a JSON configuration file for custom options.

```bash
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
  -i http://petstore.swagger.io/v2/swagger.json \
  -l java \
  -o samples/client/petstore/java \
  -c path/to/config.json
```

--------------------------------

### Webpack Configuration for Swagger Editor

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This snippet shows a partial Webpack configuration for Swagger Editor. It includes module aliases for 'monaco-editor' and '@stoplight/ordered-object-literal', and configures plugins like ProvidePlugin and CopyWebpackPlugin for assets. It also defines rules for CSS files.

```javascript
{
    resolve: {
      alias: {
        'monaco-editor': '/node_modules/monaco-editor',
        '@stoplight/ordered-object-literal$': '/node_modules/@stoplight/ordered-object-literal/src/index.mjs'
      }
    },
    plugins: [
      new webpack.ProvidePlugin({
        Buffer: ['buffer', 'Buffer'],
      }),
      new CopyWebpackPlugin({
        patterns: [
          {
            from: 'node_modules/swagger-editor/dist/umd/apidom.worker.js',
            to: 'static/js'
          },
          {
            from: 'node_modules/swagger-editor/dist/umd/editor.worker.js',
            to: 'static/js'
          }
        ]
      }),
    ],
    module: {
      rules: [
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader']
        },
      ]
    }
  }
```

--------------------------------

### Cookie Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Illustrates how to define and use cookie parameters for API requests, such as `debug` and `csrftoken`.

```APIDOC
## GET /api/users

### Description
Retrieves a list of users. This endpoint uses cookie parameters for debugging and CSRF protection.

### Method
GET

### Endpoint
/api/users

### Cookie Parameters
- **debug** (integer) - Optional - Debug mode flag (0 or 1). Defaults to 0.
- **csrftoken** (string) - Optional - CSRF protection token.

### Request Example
```http
GET /api/users HTTP/1.1
Host: example.com
Cookie: debug=0; csrftoken=BUSe35dohU3O1MZvDCUOJ
```

### Response
#### Success Response (200)
- **users** (array) - A list of user objects.
  - **id** (integer) - The user's ID.
  - **name** (string) - The user's name.

#### Response Example
```json
{
  "users": [
    {
      "id": 1,
      "name": "Alice"
    },
    {
      "id": 2,
      "name": "Bob"
    }
  ]
}
```
```

--------------------------------

### Define and Reuse Responses in OpenAPI

Source: https://swagger.io/docs/specification/describing-responses

This snippet demonstrates how to define common responses (e.g., 'Unauthorized', 'NotFound') in the global 'components.responses' section and then reference them in multiple operations using '$ref'. This promotes DRY principles for consistent error handling.

```yaml
paths:
  /users:
    get:
      summary: Gets a list of users.
      response:
        "200":
          description: OK
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/ArrayOfUsers"
        "401":
          $ref: "#/components/responses/Unauthorized" # <-----
  /users/{id}:
    get:
      summary: Gets a user by ID.
      response:
        "200":
          description: OK
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/User"
        "401":
          $ref: "#/components/responses/Unauthorized" # <-----
        "404":
          $ref: "#/components/responses/NotFound" # <-----

components:
  responses:
    NotFound:
      description: The specified resource was not found
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/Error"
    Unauthorized:
      description: Unauthorized
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/Error"

  schemas:
    # Schema for error response body
    Error:
      type: object
      properties:
        code:
          type: string
        message:
          type: string
      required:
        - code
        - message
```

--------------------------------

### Default Components Protected by Safe-Render Plugin

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

The default list of UI components that the safe-render plugin automatically protects with error boundaries. This ensures stability by catching errors within these core components.

```javascript
[
  "App",
  "BaseLayout",
  "VersionPragmaFilter",
  "InfoContainer",
  "ServersContainer",
  "SchemesContainer",
  "AuthorizeBtnContainer",
  "FilterContainer",
  "Operations",
  "OperationContainer",
  "parameters",
  "responses",
  "OperationServers",
  "Models",
  "ModelWrapper",
  "Topbar",
  "StandaloneLayout",
  "onlineValidatorBadge"
]
```

--------------------------------

### Generate Client with Custom Codegen Module (Linux/macOS)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators

This command generates a client library using a custom codegen module. It requires specifying the path to the custom library JAR, the swagger-codegen-cli JAR, the codegen class, the custom generator name, the OpenAPI spec location, and the output directory.

```java
java -cp output/myLibrary/target/myClientCodegen-swagger-codegen-1.0.0.jar:modules/swagger-codegen-cli/target/swagger-codegen-cli.jar \
  io.swagger.codegen.v3.cli.SwaggerCodegen generate -l myClientCodegen\
  -i http://petstore.swagger.io/v2/swagger.json \
  -o myClient
```

--------------------------------

### OpenAPI Server Override with Link

Source: https://swagger.io/docs/specification/links

Demonstrates how to override the default server for a linked operation using the `server` keyword within the link definition. This allows specifying a different base URL for the target operation.

```yaml
servers:
  - url: https://api.example.com
---
links:
  GetUserByUserId:
    operationId: getUser
    parameters:
      userId: "$response.body#/id"
    server:
      url: https://new-api.example.com/v2
```

--------------------------------

### Configure Parameter Macro (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

A function to set default values for parameters. It accepts two arguments: 'operation' and 'parameter', both of which are immutable objects passed for context.

```javascript
function parameterMacro(operation, parameter) {
  // Example: Set a default value for a query parameter
  if (parameter.in === 'query' && parameter.name === 'limit') {
    parameter.default = 10;
  }
  return parameter;
}
```

--------------------------------

### Direct File Upload

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Describes how to upload a file directly in the request body with a specified media type.

```APIDOC
## POST /upload

### Description
Uploads a file directly in the request body.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **file** (string, format: binary) - Required - The file content to be uploaded.

### Request Example
```yaml
requestBody:
  content:
    image/png:
      schema:
        type: string
        format: binary
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of successful upload.

#### Response Example
```json
{
  "message": "File uploaded successfully"
}
```
```

--------------------------------

### Swagger Editor Package.json Mapping

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

Defines how Swagger Editor's build artifacts are mapped within the package.json file, specifying entry points for different module systems like unpkg, module, browser, and exports.

```json
{
  "unpkg": "./dist/umd/swagger-editor.js",
  "module": "./dist/esm/swagger-editor.js",
  "browser": "./dist/esm/swagger-editor.js",
  "jsnext:main": "./dist/esm/swagger-editor.js",
  "exports": {
    "./package.json": "./package.json",
    "./swagger-editor.css": "./dist/swagger-editor.css",
    ".": {
      "browser": "./dist/esm/swagger-editor.js"
    },
    "./plugins/*": {
      "browser": "./dist/esm/plugins/*/index.js"
    },
    "./presets/*": {
      "browser": "./dist/esm/presets/*/index.js"
    },
    "./apidom.worker": {
      "browser": "./dist/esm/apidom.worker.js"
    },
    "./editor.worker": {
      "browser": "./dist/esm/editor.worker.js"
    }
  }
}
```

--------------------------------

### Handling Different Responses Based on Request Parameter

Source: https://swagger.io/docs/specification/describing-responses

Explains the limitation in OpenAPI 3.0 regarding directly linking specific response schemas to request parameter combinations, suggesting `oneOf` and descriptive text as workarounds.

```APIDOC
## Handling Different Responses Based on Request Parameter

### Description
OpenAPI 3.0 does not provide a direct mechanism to link specific response schemas to particular combinations of request parameters (e.g., different schemas based on query parameters like `?foo=bar`).

### Workaround
To document scenarios where responses might vary based on request parameters, you can:
1.  **Use `oneOf`**: Define multiple possible response schemas within the `oneOf` keyword for a given status code. This indicates that the response could conform to any of the listed schemas.
2.  **Provide Descriptive Text**: Clearly document the conditions under which each response schema applies within the `description` field of the response object.

### Example Scenario
Consider an endpoint that returns different data structures based on a query parameter:

**GET /something**
- Returns `{200, schema_1}`
**GET /something?foo=bar**
- Returns `{200, schema_2}`

**Documentation Approach:**
```yaml
paths:
  /something:
    get:
      summary: Retrieves something.
      parameters:
        - name: foo
          in: query
          schema:
            type: string
          required: false
      responses:
        "200":
          description: |-
            Returns schema_1 by default. If the 'foo' query parameter is set to 'bar', returns schema_2.
          content:
            application/json:
              schema:
                oneOf:
                  - $ref: "#/components/schemas/Schema1"
                  - $ref: "#/components/schemas/Schema2"
```

*Note: This approach documents the possibility of different responses but does not programmatically enforce the linkage between specific parameter values and response schemas.*
```

--------------------------------

### Webpack 5 Configuration for Swagger Editor (webpack.config.js)

Source: https://swagger.io/docs/open-source-tools/swagger-editor-next

This webpack.config.js file configures webpack@5 for a project using Swagger Editor. It sets the mode to 'production', defines entry points for the application and worker files, and configures the output path and filename. Crucially, it includes fallback configurations for Node.js core modules like 'http', 'https', 'stream', and 'util' to work in a browser environment, and aliases to manage specific package versions. It also includes a plugin to provide 'Buffer' and rules for handling CSS and WASM files.

```javascript
const path = require('path');
const webpack = require('webpack');


module.exports = {
  mode: 'production',
  entry: {
    app: './index.js',
    'apidom.worker': 'swagger-editor/apidom.worker',
    'editor.worker': 'swagger-editor/editor.worker',
  },
  output: {
    globalObject: 'self',
    filename: '[name].js',
    path: path.resolve(__dirname, 'dist')
  },
  resolve: {
    fallback: {
      path: false,
      fs: false,
      http: require.resolve('stream-http'), // required for asyncapi parser
      https: require.resolve('https-browserify'), // required for asyncapi parser
      stream: require.resolve('stream-browserify'),
      util: require.resolve('util'),
      url: require.resolve('url'),
      zlib: false,
    },
    alias: {
      // This alias make sure we don't pull two different versions of monaco-editor
      'monaco-editor': '/node_modules/monaco-editor',
      // This alias makes sure we're avoiding a runtime error related to this package
      '@stoplight/ordered-object-literal$': '/node_modules/@stoplight/ordered-object-literal/src/index.mjs',
    },
  },
  plugins: [
    new webpack.ProvidePlugin({
      Buffer: ['buffer', 'Buffer'],
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
      /**
       * The default way in which webpack loads wasm files won’t work in a worker,
       * so we will have to disable webpack’s default handling of wasm files and
       * then fetch the wasm file by using the file path that we get using file-loader.
       *
       * Resource: https://pspdfkit.com/blog/2020/webassembly-in-a-web-worker/
       *
       * Alternatively, WASM file can be bundled directly into JavaScript bundle as data URLs.
       * This configuration reduces the complexity of WASM file loading
       * but increases the overal bundle size:
       *
       * {
       *   test: /\.wasm$/,
       *   type: 'asset/inline',
       * }
       */
      {
        test: /\.wasm$/,
        loader: 'file-loader',
        type: 'javascript/auto', // this disables webpacks default handling of wasm
      },
    ]
  }
};

```

--------------------------------

### Marking Path Parameter as Required

Source: https://swagger.io/docs/specification/describing-parameters

Demonstrates how to explicitly mark a path parameter as required using `required: true`. Path parameters must always be required.

```yaml
parameters:
  - in: path
    name: userId
    schema:
      type: integer
    required: true
    description: Numeric ID of the user to get.
```

--------------------------------

### Response Body Schema

Source: https://swagger.io/docs/specification/describing-responses

Demonstrates how to define the structure of a response body using schemas.

```APIDOC
## Response Body Schema

### Description
This section explains how to define the structure of the response body using the `schema` keyword, supporting objects, arrays, primitive types, and files.

### Inline Schema Example
```
responses:
  "200":
    description: A User object
    content:
      application/json:
        schema:
          type: object
          properties:
            id:
              type: integer
              description: The user ID.
            username:
              type: string
              description: The user name.
```

### Referenced Schema Example
```
responses:
  "200":
    description: A User object
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User"
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
          description: The user ID.
        username:
          type: string
          description: The user name.
```
```

--------------------------------

### Swagger UI JSON Schema Component Mapping Rules

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This section outlines the internal mapping rules Swagger UI uses to find JSON Schema components for rendering inputs. It prioritizes components based on schema type and format, providing fallback and default options when specific components are not found.

```text
If format defined:
`JsonSchema_${type}_${format}`

Fallback if`JsonSchema_${type}_${format}` component does not exist or format not defined:
`JsonSchema_${type}`

Default:
`JsonSchema_string`
```

--------------------------------

### Understanding $ref in OpenAPI

Source: https://swagger.io/docs/specification/using-ref

This section explains the fundamental concept of using $ref to reference reusable schema objects within an OpenAPI 3.0 specification.

```APIDOC
## Using $ref in OpenAPI

### Description
The `$ref` keyword in OpenAPI 3.0 allows you to reference definitions that are used across multiple API resources. This promotes reusability and consistency in your API documentation. You can reference definitions within the same file or from external files.

### Method
N/A (Conceptual Documentation)

### Endpoint
N/A (Conceptual Documentation)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Example: Referencing a Schema Object

### Description
This example demonstrates how to define a reusable schema object (`User`) and then reference it within a response definition.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier for the user.
- **name** (string) - The name of the user.

#### Response Example
```json
{
  "id": 1,
  "name": "John Doe"
}
```

## $ref Syntax and Types

### Description
This section details the syntax for `$ref` and the different types of references you can create, including local, remote, and URL references.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Local Reference
`$ref: '#/definitions/myElement'`

#### Remote Reference (Same Server)
`$ref: 'document.json'`
`$ref: 'document.json#/myElement'`
`$ref: '../document.json#/myElement'`
`$ref: '../another-folder/document.json#/myElement'`

#### URL Reference
`$ref: 'http://path/to/your/resource'`
`$ref: 'http://path/to/your/resource.json#/myElement'`
`$ref: '//anotherserver.com/files/example.json'`

## Escape Characters in JSON Pointers

### Description
Explains how to escape special characters (`~` and `/`) when they appear in path names within JSON Pointers used in `$ref`.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
```json
{
  "$ref": "#/paths/~1blogs~1{blog_id}~1new~0posts"
}
```

### Response
N/A

## Considerations for $ref Usage

### Description
Highlights important considerations, such as where `$ref` can and cannot be used within an OpenAPI specification, and provides examples of correct and incorrect usage.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
# Incorrect usage:
openapi: 3.0.4
info:
  $ref: info.yaml
paths:
  $ref: paths.yaml

# Correct usage:
paths:
  /users:
    $ref: "../resources/users.yaml"
  /users/{userId}:
    $ref: "../resources/users-by-id.yaml"
```

### Response
N/A
```

--------------------------------

### Define Default Values for Optional Query Parameters (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This snippet illustrates how to set default values for optional query parameters like 'offset' and 'limit' using the 'default' keyword within their schemas in YAML. It also includes constraints like minimum and maximum values.

```yaml
parameters:
  - in: query
    name: offset
    schema:
      type: integer
      minimum: 0
      default: 0
    required: false
    description: The number of items to skip before starting to collect the result set.
  - in: query
    name: limit
    schema:
      type: integer
      minimum: 1
      maximum: 100
      default: 20
    required: false
    description: The number of items to return.
```

--------------------------------

### PATCH /pets - Using oneOf for Request Body Validation

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This endpoint demonstrates how to use the `oneOf` keyword to validate the request body, ensuring it conforms to exactly one of the specified schemas (Cat or Dog).

```APIDOC
## PATCH /pets

### Description
Updates a pet's information. The request body must be valid against either the Cat schema or the Dog schema, but not both or neither.

### Method
PATCH

### Endpoint
/pets

### Parameters
#### Request Body
- **(schema)** - Required - The pet object to update. Must conform to one of the following schemas:
  - `#/components/schemas/Cat`
  - `#/components/schemas/Dog`

### Request Example
```json
{
  "bark": true,
  "breed": "Dingo"
}
```

### Response
#### Success Response (200)
- **description** (string) - Indicates the pet was successfully updated.

#### Response Example
```json
{
  "message": "Pet updated successfully"
}
```

### Components
#### Schemas
##### Dog
- **bark** (boolean) - Indicates if the dog barks.
- **breed** (string) - The breed of the dog. Must be one of: Dingo, Husky, Retriever, Shepherd.

##### Cat
- **hunts** (boolean) - Indicates if the cat hunts.
- **age** (integer) - The age of the cat.
```

--------------------------------

### Mark Operations as Deprecated in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

Demonstrates how to mark specific operations as `deprecated` in the OpenAPI specification. This signals to users and tools that the operation should be phased out of use.

```yaml
/pet/findByTags:
  get:
    deprecated: true
```

--------------------------------

### Apply OAuth 2.0 Security Globally in OpenAPI

Source: https://swagger.io/docs/specification/authentication/oauth2

This code shows how to apply the previously defined OAuth 2.0 security scheme ('oAuthSample') globally to all operations in an OpenAPI specification. It lists the required scopes ('write_pets' and 'read_pets') that clients must provide.

```yaml
security:
  - oAuthSample:
    - write_pets
    - read_pets
```

--------------------------------

### Define and Reference Reusable Enum (YAML)

Source: https://swagger.io/docs/specification/data-models/enums

Shows how to define a reusable enum ('Color') in the `components/schemas` section and reference it using `$ref` for a query parameter. This promotes DRY principles in OpenAPI definitions.

```yaml
paths:
  /products:
    get:
      parameters:
        - in: query
          name: color
          required: true
          schema:
            $ref: "#/components/schemas/Color"
      responses:
        "200":
          description: OK
components:
  schemas:
    Color:
      type: string
      enum:
        - black
        - white
        - red
        - green
        - blue
```

--------------------------------

### SwaggerUI Safe-Render Plugin API

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

The public API of the safe-render plugin, exposing functions and components for error handling customization. It includes `componentDidCatch`, `withErrorBoundary`, `ErrorBoundary`, and `Fallback`.

```javascript
{
  fn: {
    componentDidCatch,
    withErrorBoundary: withErrorBoundary(getSystem),
  },
  components: {
    ErrorBoundary,
    Fallback,
  },
}
```

--------------------------------

### Configure Network Response Interceptor (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Intercepts remote definition, 'Try it out', and OAuth 2.0 responses. Accepts one argument (response) and must return the modified response or a Promise resolving to it.

```javascript
function responseInterceptor(response) {
  // Modify the response here if needed
  return response;
}
```

--------------------------------

### Wrap an Existing Action in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This snippet demonstrates how to override or augment an existing action using `wrapActions`. The `oriAction` parameter represents the original action, which must be called if you want its behavior to execute. This is useful for logging or conditional logic.

```javascript
// this plugin allows you to watch changes to the spec that is in memory
const MyWrapActionPlugin = function(system) {
  return {
    statePlugins: {
      spec: {
        wrapActions: {
          updateSpec: (oriAction, system) => (str) => {
            // here, you can hand the value to some function that exists outside of Swagger UI
            console.log("Here is my API definition", str)
            return oriAction(str) // don't forget! otherwise, Swagger UI won't update
          }
        }
      }
    }
  }
}
```

--------------------------------

### Using Relative URLs for Servers and Other References - YAML

Source: https://swagger.io/docs/specification/api-host-and-base-path

Illustrates the use of relative URLs within the 'servers' array, 'termsOfService', 'externalDocs', and OAuth2 'components' in an OpenAPI specification. These relative URLs are resolved against the server hosting the OpenAPI definition.

```yaml
servers:
  - url: https://api.example.com
  - url: https://sandbox-api.example.com

# Relative URL to Terms of Service
info:
  version: 0.0.0
  title: test
  termsOfService: /terms-of-use

# Relative URL to external documentation
externalDocs:
  url: /docs
  description: Find more info here

# Relative URLs to OAuth2 authorization and token URLs
components:
  securitySchemes:
    oauth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: /oauth/dialog
          tokenUrl: /oauth/token
```

--------------------------------

### Cookie Parameters Serialization

Source: https://swagger.io/docs/specification/serialization

Details the 'form' style for cookie parameters, illustrating serialization for primitive, array, and object values, with and without the 'explode' modifier.

```APIDOC
## Cookie Parameters Serialization

### Description
Cookie parameters always use the `form` style. The `explode` keyword controls array and object serialization.

### Method
GET (Example)

### Endpoint
`/example

### Parameters
#### Cookie Parameters
- **id** (string) - Required - The cookie name.

### Request Example
```
GET /example HTTP/1.1
Host: example.com
Cookie: id=5
```

### Response
#### Success Response (200)
- **message** (string) - A success message.

#### Response Example
```json
{
  "message": "Cookie processed successfully"
}
```
```

--------------------------------

### Define API Paths in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

This snippet shows the basic structure for defining API paths within the global 'paths' section of an OpenAPI specification. Paths are relative to the server URL.

```yaml
paths:
  /ping: ...
  /users: ...
  /users/{id}: ...
```

--------------------------------

### Basic XML and JSON Representation of a Schema

Source: https://swagger.io/docs/specification/data-models/representing-xml

Demonstrates the fundamental mapping between a schema defined in an API specification and its equivalent JSON and XML representations. This serves as a baseline for understanding data structure translation.

```yaml
components:
  schemas:
    book:
      type: object
      properties:
        id:
          type: integer
        title:
          type: string
        author:
          type: string
```

```json
{ "id": 0, "title": "string", "author": "string" }
```

```xml
<book>
  <id>0</id>
  <title>string</title>
  <author>string</author>
</book>
```

--------------------------------

### Define Global Tags with Descriptions and External Docs

Source: https://swagger.io/docs/specification/grouping-operations-with-tags

This YAML snippet illustrates how to define global tags at the root level, including descriptions and external documentation URLs. These global definitions provide more context for the tags used in API operations and influence the default sorting in tools like Swagger UI.

```yaml
tags:
  - name: pets
    description: Everything about your Pets
    externalDocs:
      url: http://docs.my-api.com/pet-operations.htm
  - name: store
    description: Access to Petstore orders
    externalDocs:
      url: http://docs.my-api.com/store-orders.htm
```

--------------------------------

### Describe Array Query Parameter with Schema and Style (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This snippet demonstrates how to describe an array query parameter using the 'schema' keyword in YAML. It specifies the type as an array of strings and uses 'style: form' with 'explode: false' to serialize it as 'key=value1,value2'.

```yaml
parameters:
  - in: query
    name: color
    schema:
      type: array
      items:
        type: string
    style: form
    explode: false
```

--------------------------------

### Generate PHP API Client using Swagger Codegen (Windows)

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/about

This is a Windows-specific variation for generating a PHP API client using Swagger Codegen. The primary difference from the Linux/macOS version is the path separator used in the `java -jar` command.

```shell
java -jar modules\swagger-codegen-cli\target\swagger-codegen-cli.jar generate -i http://petstore.swagger.io/v2/swagger.json -l php -o c:\temp\php_api_client
```

--------------------------------

### Define String-to-Object Dictionary Schema

Source: https://swagger.io/docs/specification/data-models/dictionaries

This schema defines a dictionary where keys are strings and values are objects. The `additionalProperties` keyword references a schema for the object values, which include `code` (integer) and `text` (string) properties.

```yaml
type: object
additionalProperties:
  type: object
  properties:
    code:
      type: integer
    text:
      type: string
```

--------------------------------

### Replace Swagger UI Logo Component with Custom Image

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This React code demonstrates how to create a custom plugin to replace the default Swagger UI logo. The `MyLogoPlugin` overrides the `Logo` component, allowing you to display a custom image, such as a company logo, in the Top Bar when using the Standalone Preset.

```javascript
import React from "react";
const MyLogoPlugin = {
  components: {
    Logo: () => (
      <img alt="My Logo" height="40" src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNTM3IiBoZWlnaHQ9IjEzNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCiA8Zz4KICA8dGl0bGU+TGF5ZXIgMTwvdGl0bGU+CiAgPHRleHQgdHJhbnNmb3JtPSJtYXRyaXgoMy40Nzc2OSAwIDAgMy4yNjA2NyAtNjczLjEyOCAtNjkxLjk5MykiIHN0cm9rZT0iIzAwMCIgZm9udC1zdHlsZT0ibm9ybWFsIiBmb250LXdlaWdodD0ibm9ybWFsIiB4bWw6c3BhY2U9InByZXNlcnZlIiB0ZXh0LWFuY2hvcj0ic3RhcnQiIGZvbnQtZmFtaWx5PSInT3BlbiBTYW5zIEV4dHJhQm9sZCciIGZvbnQtc2l6ZT0iMjQiIGlkPSJzdmdfMSIgeT0iMjQxLjIyMTkyIiB4PSIxOTYuOTY5MjEiIHN0cm9rZS13aWR0aD0iMCIgZmlsbD0iIzYyYTAzZiI+TXkgTG9nbzwvdGV4dD4KICA8cGF0aCBpZD0ic3ZnXzIiIGQ9Im0zOTUuNjAyNSw1MS4xODM1OWw1My44Nzc3MSwwbDE2LjY0ODYzLC01MS4xODM1OGwxNi42NDg2NCw1MS4xODM1OGw1My44Nzc3LDBsLTQzLjU4NzksMzEuNjMyODNsMTYuNjQ5NDksNTEuMTgzNThsLTQzLjU4NzkyLC0zMS42MzM2OWwtNDM1ODc5MSwzMS42MzM2OWwxNi42NDk0OSwtNTEuMTgzNThsLTQzLjU4NzkyLC0zMS42MzI4M3oiIHN0cm9rZS13aWR0aD0iMCIgc3Ryb2tlPSIjMDAwIiBmaWxsPSIjNjJhMDNmIi8+CiA8L2c+Cjwvc3ZnPg=="/>
    )
  }
}
```

--------------------------------

### Reference Response Body Schema from Components (YAML)

Source: https://swagger.io/docs/specification/describing-responses

This snippet demonstrates how to define a response body schema in the global `components.schemas` section and then reference it using `$ref` within the operation's response definition. This promotes reusability for common schemas.

```yaml
responses:
  "200":
    description: A User object
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User"
    components:
      schemas:
        User:
          type: object
          properties:
            id:
              type: integer
              description: The user ID.
            username:
              type: string
              description: The user name.
```

--------------------------------

### Constant Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Explains how to define a constant parameter, which is a required parameter with only one possible value. This ensures the parameter is always sent with a specific value.

```APIDOC
## Constant Parameters

### Description
This section defines a constant parameter, characterized as a required parameter with a single, fixed value. Unlike default parameters, constant parameters must always be provided by the client.

### Method
GET

### Endpoint
/events

### Parameters
#### Query Parameters
- **rel_date** (string) - Required - Specifies the relative date. The only allowed value is `now`.

### Request Example
```http
GET /events?rel_date=now
```

### Response
#### Success Response (200)
- **events** (array) - A list of events occurring now.

#### Response Example
```json
{
  "events": [
    { "id": 501, "name": "Concert", "time": "2023-10-27T20:00:00Z" }
  ]
}
```
```

--------------------------------

### Deprecated Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Shows how to mark parameters as deprecated, indicating they should no longer be used.

```APIDOC
## Deprecated Query Parameter

### Description
Marks a query parameter as deprecated, suggesting an alternative method for achieving the same result.

### Parameters
#### Query Parameters
- **format** (string) - Required - Specifies the response format.
  - `enum: [json, xml, yaml]`
  - `deprecated: true`
  - `description: Deprecated, use the appropriate `Accept` header instead.`
```

--------------------------------

### Describing Parameters in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-parameters

This section explains how to define parameters within an OpenAPI 3.0 specification, covering their name, location, data type, and other attributes.

```APIDOC
## POST /api/users

### Description
This endpoint demonstrates the basic structure for defining parameters in OpenAPI 3.0.

### Method
POST

### Endpoint
/api/users

### Parameters
#### Path Parameters
- **userId** (integer) - Required - Numeric ID of the user to get

#### Query Parameters
- **status** (string) - Optional - Status of the user to filter by

#### Header Parameters
- **X-Request-ID** (string) - Optional - Unique identifier for the request

#### Cookie Parameters
- **session_id** (string) - Required - The session identifier for the user

### Request Example
```json
{
  "example": "{\"userId\": 123, \"status\": \"active\", \"X-Request-ID\": \"abc-123\", \"session_id\": \"xyz-789\"}"
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message

#### Response Example
```json
{
  "example": "{\"message\": \"User processed successfully\"}"
}
```
```

--------------------------------

### Define Path Parameter with Schema Details

Source: https://swagger.io/docs/specification/describing-parameters

Shows a detailed definition for a path parameter named 'id' in OpenAPI 3.0. It specifies the parameter as required, defines its schema as an integer with a minimum value, and provides a descriptive text. This ensures robust validation for path parameters.

```yaml
paths:
  /users/{id}:
    get:
      parameters:
        - in: path
          name: id # Note the name is the same as in the path
          required: true
          schema:
            type: integer
            minimum: 1
          description: The user ID

```

--------------------------------

### Testing CORS with Curl

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/cors

This snippet demonstrates how to use the curl command to inspect the CORS headers returned by a Swagger API endpoint. It helps verify if the necessary 'Access-Control-Allow-Origin' and other related headers are present.

```shell
curl -I "https://petstore.swagger.io/v2/swagger.json"
```

--------------------------------

### Request Body with Alternate Schemas (oneOf)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Demonstrates how to define a request body that can conform to one of several different schemas, such as Cat, Dog, or Hamster.

```APIDOC
## Request Body with Alternate Schemas

### Description
Defines a request body that can be one of several different types (e.g., Cat, Dog, or Hamster).

### Parameters
#### Request Body
- **description** (string) - A JSON object containing pet information
- **content** (object) - Maps media types to their schemas.
  - **application/json** (object) - Schema for JSON request body.
    - **schema** (object) - Specifies alternate schemas for the request body.
      - **oneOf** (array) - An array of schemas, where the request body must validate against exactly one of them.
        - **$ref** (string) - Reference to the Cat schema.
        - **$ref** (string) - Reference to the Dog schema.
        - **$ref** (string) - Reference to the Hamster schema.

### Request Example
```json
{
  "description": "A JSON object containing pet information",
  "content": {
    "application/json": {
      "schema": {
        "oneOf": [
          { "$ref": "#/components/schemas/Cat" },
          { "$ref": "#/components/schemas/Dog" },
          { "$ref": "#/components/schemas/Hamster" }
        ]
      }
    }
  }
}
```
```

--------------------------------

### Define Query Parameters in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-parameters

This snippet illustrates how to define query parameters in an OpenAPI 3.0 specification. It shows two parameters, 'offset' and 'limit', both of type integer, with descriptions explaining their purpose. Query parameters are commonly used for filtering and pagination.

```yaml
parameters:
  - in: query
    name: offset
    schema:
      type: integer
    description: The number of items to skip before starting to collect the result set
  - in: query
    name: limit
    schema:
      type: integer
    description: The numbers of items to return

```

--------------------------------

### Enable and Configure Request Snippets in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This configuration object enables request snippets and defines a custom generator for Node.js native HTTP requests. It specifies the title and syntax for the custom generator.

```javascript
const snippetConfig = {
  requestSnippetsEnabled: true,
  requestSnippets: {
    generators: {
      "node_native": {
        title: "NodeJs Native",
        syntax: "javascript"
      }
    }
  }
}
```

--------------------------------

### OpenAPI 3.0 Schema for Free-Form Form Data

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Demonstrates how to model arbitrary key-value pairs in form data using `additionalProperties: true` in OpenAPI 3.0.

```APIDOC
## OpenAPI 3.0 Schema for Free-Form Form Data

### Description
This OpenAPI 3.0 snippet shows how to define a schema for `application/x-www-form-urlencoded` data that allows for arbitrary key-value pairs using `additionalProperties: true`.

### Method
POST

### Endpoint
[Endpoint not specified in source text]

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **content** (object)
  - **application/x-www-form-urlencoded** (object)
    - **schema** (object)
      - **type** (string) - "object"
      - **additionalProperties** (boolean) - true (optional)

### Request Example
```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        additionalProperties: true
```

### Response
#### Success Response (200)
Details of the success response are not provided in the source text.

#### Response Example
No example provided for the response.
```

--------------------------------

### Referencing Operations with operationRef (YAML)

Source: https://swagger.io/docs/specification/links

Demonstrates how to use `operationRef` to reference API operations when `operationId` is not available. It covers both local and external references, including escaping special characters in path names.

```yaml
operationRef: "#/paths/~1users~1{userId}/get"
```

```yaml
operationRef: 'https://anotherapi.com/openapi.yaml#/paths/~1users~1{userId}/get'
```

```yaml
operationRef: './operations/getUser.yaml'
```

--------------------------------

### OpenAPI 3.0 Schema for Form Data

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Demonstrates how to define form data parameters in OpenAPI 3.0 using a schema with properties for each form field.

```APIDOC
## OpenAPI 3.0 Schema for Form Data

### Description
This OpenAPI 3.0 snippet shows how to model `application/x-www-form-urlencoded` data using a schema with object properties representing form fields.

### Method
POST

### Endpoint
/survey

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **content** (object) - Required - Defines the content type and schema for the request body.
  - **application/x-www-form-urlencoded** (object)
    - **schema** (object)
      - **type** (string) - "object"
      - **properties** (object)
        - **name** (object)
          - **type** (string) - "string"
        - **fav_number** (object)
          - **type** (integer)
      - **required** (array)
        - "name"
        - "email"

### Request Example
```yaml
paths:
  /survey:
    post:
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                name:
                  type: string
                fav_number:
                  type: integer
              required:
                - name
                - email
```

### Response
#### Success Response (200)
Details of the success response are not provided in the source text.

#### Response Example
No example provided for the response.
```

--------------------------------

### Override Global Servers at Path Level in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

Illustrates how to override the global `servers` array at the path level. This is useful when a specific path or set of operations requires a different base URL than the rest of the API.

```yaml
paths:
  /files:
    description: File upload and download operations
    servers:
      - url: https://files.example.com
        description: Override base path for all operations with the /files path
```

--------------------------------

### Cancel Component Rendering in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This plugin demonstrates how to prevent a specific component from rendering. By providing a stateless component that returns `null` for a component key (e.g., 'info'), you effectively 'cancel out' its default behavior.

```javascript
const NeverShowInfoPlugin = function(system) {
  return {
    components: {
      info: () => null
    }
  }
}
```

--------------------------------

### Validate Against Multiple Schemas with OpenAPI anyOf

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Illustrates the use of `anyOf` in OpenAPI to validate data against one or more subschemas simultaneously. The `PetByAge` and `PetByType` schemas can both be matched, allowing for flexible request body validation.

```yaml
paths:
  /pets:
    patch:
      requestBody:
        content:
          application/json:
            schema:
              anyOf:
                - $ref: "#/components/schemas/PetByAge"
                - $ref: "#/components/schemas/PetByType"
      responses:
        "200":
          description: Updated

components:
  schemas:
    PetByAge:
      type: object
      properties:
        age:
          type: integer
        nickname:
          type: string
      required:
        - age

    PetByType:
      type: object
      properties:
        pet_type:
          type: string
          enum: [Cat, Dog]
        hunts:
          type: boolean
      required:
        - pet_type

```

--------------------------------

### Query Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Information on defining query parameters, which are appended to the URL after a question mark and used for filtering or pagination.

```APIDOC
## GET /pets/findByStatus

### Description
Finds pets based on their status, allowing for filtering of results.

### Method
GET

### Endpoint
/pets/findByStatus

### Parameters
#### Query Parameters
- **status** (string) - Required - The status to filter pets by (e.g., 'available', 'pending', 'sold').
- **limit** (integer) - Optional - The maximum number of pets to return.
- **offset** (integer) - Optional - The number of pets to skip before returning results.

### Request Example
```
GET /pets/findByStatus?status=available&limit=10&offset=20
```

### Response
#### Success Response (200)
- **pets** (array) - A list of pet objects matching the criteria.
  - **id** (integer) - The pet's ID.
  - **name** (string) - The pet's name.
  - **status** (string) - The pet's current status.

#### Response Example
```json
{
  "example": "{\"pets\": [{\"id\": 1, \"name\": \"Buddy\", \"status\": \"available\"}, {\"id\": 2, \"name\": \"Lucy\", \"status\": \"available\"}]}"
}
```
```

--------------------------------

### Discriminator for Polymorphic Types

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Details how to use the `discriminator` keyword with `oneOf` or `anyOf` to help consumers identify the specific type of a polymorphic object based on a property value.

```APIDOC
## Discriminator for Polymorphic Types

### Description
The `discriminator` keyword, used with `oneOf` or `anyOf`, specifies a property name that determines the data type of the object. This aids consumers in typecasting.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A (Schema Definition)

### Request Body
```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
            discriminator:
              propertyName: objectType
  schemas:
    simpleObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      # ... other properties ...
    complexObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      # ... other properties ...
```

### Response
N/A (Schema Definition)

#### Success Response (200)
N/A (Schema Definition)

#### Response Example
N/A (Schema Definition)
```

--------------------------------

### Override Global Servers at Operation Level in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

Shows how to override the global `servers` array for a specific operation. This provides granular control over server configurations for individual endpoints.

```yaml
/ping:
  get:
    servers:
      - url: https://echo.example.com
        description: Override base path for the GET /ping operation
```

--------------------------------

### Describing API Key Security Scheme in OpenAPI 3.0

Source: https://swagger.io/docs/specification/authentication/api-keys

Defines an API key security scheme in OpenAPI 3.0, specifying its type, location (header, query, or cookie), and name. It also shows how to apply this scheme globally to all API operations.

```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-KEY
security:
  - ApiKeyAuth: []
```

--------------------------------

### Configure Network Request Interceptor (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Intercepts remote definition, 'Try it out', and OAuth 2.0 requests. Accepts one argument (request) and must return the modified request or a Promise resolving to it. Can be used to set curl options.

```javascript
function requestInterceptor(request) {
  // Example: Set curl options
  request.curlOptions = ["-g", "--limit-rate 20k"];
  return request;
}
```

--------------------------------

### Apply OAuth 2.0 Security to Individual Operation in OpenAPI

Source: https://swagger.io/docs/specification/authentication/oauth2

This snippet illustrates how to apply a specific OAuth 2.0 security scheme ('oAuthSample') to an individual API operation (e.g., the 'patch' operation on the '/pets' path). It specifies the required scopes for that particular operation.

```yaml
paths:
  /pets:
    patch:
      summary: Add a new pet
      security:
        - oAuthSample:
          - write_pets
          - read_pets
      ...
```

--------------------------------

### Configure Model Property Macro (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

A function to set default values for each property in a model. It accepts one argument, 'property', which is immutable.

```javascript
function modelPropertyMacro(property) {
  // Example: Set a default value for a specific property
  if (property.name === 'status') {
    property.default = 'active';
  }
  return property;
}
```

--------------------------------

### Define Path Parameter in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-parameters

This snippet demonstrates how to define a path parameter in an OpenAPI 3.0 specification. It includes the parameter's location (`in: path`), name, schema type, whether it's required, and a description. Path parameters are essential for identifying specific resources in a URL.

```yaml
paths:
  /users/{userId}:
    get:
      summary: Get a user by ID
      parameters:
        - in: path
          name: userId
          schema:
            type: integer
          required: true
          description: Numeric ID of the user to get

```

--------------------------------

### Link Definition Components

Source: https://swagger.io/docs/specification/links

Details the components of a link definition in OpenAPI, including 'operationId' or 'operationRef' to specify the target operation, 'parameters' and 'requestBody' for passing values using runtime expressions, and optional 'server' and 'description' fields.

```text
* `operationId` or `operationRef` that specifies the target operation. It can be the same operation or a different operation in the current or external API specification. `operationId` is used for local links only, and `operationRef` can link to both local and external operations.
* `parameters` and/or `requestBody` sections that specify the values to pass to the target operation. Runtime expression syntax is used to extract these values from the parent operation.
* (Optional) The `server` that the target operation should use, if it is different from the default servers.
* (Optional) A `description` of this link. CommonMark syntax can be used for rich text representation.
```

--------------------------------

### OpenAPI Polymorphism with Discriminator

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Shows how to use the `discriminator` keyword in conjunction with `oneOf` or `anyOf` to help API consumers detect the object type. The `propertyName` points to a property within the schemas that specifies the data type name. All schemas referenced by `oneOf` or `anyOf` must include this discriminator property.

```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
            discriminator:
              propertyName: objectType
  ...
  schemas:
    simpleObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
    complexObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
```

--------------------------------

### Reusable Enum in Components

Source: https://swagger.io/docs/specification/data-models/enums

Shows how to define an enum in the global `components/schemas` section and reference it in an operation parameter using `$ref`.

```APIDOC
## GET /products with Reusable Enum

### Description
Retrieves a list of products, with a required 'color' query parameter defined as a reusable enum.

### Method
GET

### Endpoint
/products

### Parameters
#### Query Parameters
- **color** (string) - Required - The color of the product. Possible values are black, white, red, green, blue.

### Request Example
```json
{
  "example": "GET /products?color=red"
}
```

### Response
#### Success Response (200)
- **products** (array) - A list of products.

#### Response Example
```json
{
  "example": {
    "products": [
      { "id": 1, "name": "Product A", "color": "red" },
      { "id": 2, "name": "Product B", "color": "blue" }
    ]
  }
}
```

### Components
#### Schemas
##### Color
- **type** (string)
- **enum**
  - black
  - white
  - red
  - green
  - blue
```

--------------------------------

### Define String-to-String Dictionary Schema

Source: https://swagger.io/docs/specification/data-models/dictionaries

This schema defines a dictionary where keys are strings and values are also strings. It uses `type: object` and `additionalProperties` to specify the value type.

```yaml
type: object
additionalProperties:
  type: string
```

--------------------------------

### Describing Basic Authentication in OpenAPI 3.0

Source: https://swagger.io/docs/specification/authentication/basic-authentication

This OpenAPI 3.0 snippet demonstrates how to define a Basic Authentication security scheme named 'basicAuth'. It specifies the type as 'http' and the scheme as 'basic'. The 'security' section then applies this scheme globally to the API.

```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    basicAuth: # <-- arbitrary name for the security scheme
      type: http
      scheme: basic

security:
  - basicAuth: [] # <-- use the same name here
```

--------------------------------

### Generate Java API Client using curl

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

This snippet demonstrates how to generate a Java API client using the `curl` command. It sends a POST request to the Swagger Codegen API with the OpenAPI specification URL, target language ('java'), generation type ('CLIENT'), and codegen version ('V3'). The response contains a zipped file with the generated code.

```bash
curl -X POST \
  https://generator3.swagger.io/api/generate \
  -H 'content-type: application/json' \
  -d '{
  "specURL" : "https://raw.githubusercontent.com/OAI/OpenAPI-Specification/master/examples/v3.0/petstore.yaml",
  "lang" : "java",
  "type" : "CLIENT",
  "codegenVersion" : "V3"
}'
```

--------------------------------

### Describe Direct File Upload in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Defines a file upload directly within the request body. It uses the `requestBody` keyword with a content type (e.g., `image/png`) and specifies the file schema as `type: string` with `format: binary` or `base64`.

```yaml
requestBody:
  content:
    image/png:
      schema:
        type: string
        format: binary
```

--------------------------------

### Configure Request Snippets in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

This snippet demonstrates the default configuration for the `requestSnippets` plugin in Swagger UI. It allows customization of snippet generators, default expansion state, and specific language inclusions. The `generators` object defines available snippet types like cURL for bash, PowerShell, and CMD, each with a title and syntax highlighting language.

```javascript
{
  generators: {
    curl_bash: {
      title: "cURL (bash)",
      syntax: "bash"
    },
    curl_powershell: {
      title: "cURL (PowerShell)",
      syntax: "powershell"
    },
    curl_cmd: {
      title: "cURL (CMD)",
      syntax: "bash"
    },
  },
  defaultExpanded: true,
  languages: null
}
```

--------------------------------

### Define OpenAPI Security Schemes (YAML)

Source: https://swagger.io/docs/specification/authentication

This snippet demonstrates how to define various security schemes (BasicAuth, BearerAuth, ApiKeyAuth, OpenID, OAuth2) within the 'components/securitySchemes' section of an OpenAPI specification.

```yaml
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic

    BearerAuth:
      type: http
      scheme: bearer

    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key

    OpenID:
      type: openIdConnect
      openIdConnectUrl: https://example.com/.well-known/openid-configuration

    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://example.com/oauth/authorize
          tokenUrl: https://example.com/oauth/token
          scopes:
            read: Grants read access
            write: Grants write access
            admin: Grants access to admin operations
```

--------------------------------

### Mark Parameter as Deprecated (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML code shows how to mark a parameter as deprecated using the `deprecated: true` property. This indicates that the parameter is no longer recommended for use and may be removed in future versions. It's good practice to include a `description` explaining why it's deprecated and suggesting alternatives.

```yaml
- in: query
  name: format
  required: true
  schema:
    type: string
    enum: [json, xml, yaml]
  deprecated: true
  description: Deprecated, use the appropriate `Accept` header instead.
```

--------------------------------

### Define Array Length Constraints

Source: https://swagger.io/docs/specification/data-models/data-types

Sets minimum and maximum length constraints for an array using `minItems` and `maxItems`. An empty array is valid if `minItems` is not specified or is 0.

```yaml
type: array
items:
  type: integer
minItems: 1
maxItems: 10
```

--------------------------------

### Define Nullable Integer Schema (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This YAML snippet shows how to define a schema for an integer parameter that can accept a `null` value. The `nullable: true` property in the schema allows for explicit nullability, similar to `int?` in C# or `java.lang.Integer` in Java. Note that `nullable` is distinct from optional or empty-valued parameters.

```yaml
schema:
  type: integer
  format: int32
  nullable: true
```

--------------------------------

### Define Basic Object Structure

Source: https://swagger.io/docs/specification/data-models/data-types

Defines an object with properties, where each property has a name and an associated schema. Commonly defined in `components/schemas` for reusability.

```yaml
type: object
properties:
  id:
    type: integer
  name:
    type: string
```

--------------------------------

### Define Reusable Request Body (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This snippet demonstrates how to define a request body in the global 'components.requestBodies' section and reference it using '$ref' in multiple path operations. This promotes reusability and consistency for common request body structures.

```yaml
paths:
  /pets:
    post:
      summary: Add a new pet
      requestBody:
        $ref: '#/components/requestBodies/PetBody'
  /pets/{petId}:
    put:
      summary: Update a pet
      parameters: [ ... ]
      requestBody:
        $ref: '#/components/requestBodies/PetBody'
components:
  requestBodies:
    PetBody:
      description: A JSON object containing pet information
      required: true
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Pet'
```

--------------------------------

### Extend Objective-C Codegen Class

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

This Java code demonstrates how to extend the default Objective-C client generator (`ObjcClientCodegen`) to override specific properties, such as the file prefix. The subclass is then specified using the '-l' argument.

```java
package com.mycompany.swagger.codegen;

import io.swagger.codegen.languages.*;

public class MyObjcCodegen extends ObjcClientCodegen {
    static {
        PREFIX = "HELO";
    }
}
```

--------------------------------

### Extract Swagger UI 2.x Version from File Comment

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/version-detection

This method involves locating the `swagger-ui.js` file and extracting the version number from a comment at the top of the file. This is applicable for Swagger UI 2.x and older versions. The comment typically includes the version, link, and license.

```javascript
/**
 * swagger-ui - Swagger UI is a dependency-free collection of HTML, JavaScript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API
 * @version v2.2.9
 * @link https://swagger.io
 * @license Apache-2.0
 */
```

--------------------------------

### POST /pets - Add a new pet

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This endpoint allows for adding a new pet to the system. It supports JSON, XML, form-urlencoded, and plain text request bodies, with specific schemas for each.

```APIDOC
## POST /pets

### Description
Adds a new pet to the system. The request body can be in JSON, XML, form-urlencoded, or plain text format.

### Method
POST

### Endpoint
/pets

### Parameters
#### Request Body
- **description** (string) - Optional - Optional description in *Markdown*
- **required** (boolean) - Optional - Indicates if the request body is required (defaults to false)
- **content** (object) - Required - Maps media types to their schemas.
  - **application/json** (object) - Schema for JSON request body.
    - **schema** ($ref) - Reference to the Pet schema.
  - **application/xml** (object) - Schema for XML request body.
    - **schema** ($ref) - Reference to the Pet schema.
  - **application/x-www-form-urlencoded** (object) - Schema for form-urlencoded request body.
    - **schema** ($ref) - Reference to the PetForm schema.
  - **text/plain** (object) - Schema for plain text request body.
    - **schema** (string) - Schema for plain text content.

### Request Example
```json
{
  "description": "Optional description in *Markdown*",
  "required": true,
  "content": {
    "application/json": {
      "schema": {
        "$ref": "#/components/schemas/Pet"
      }
    },
    "application/xml": {
      "schema": {
        "$ref": "#/components/schemas/Pet"
      }
    },
    "application/x-www-form-urlencoded": {
      "schema": {
        "$ref": "#/components/schemas/PetForm"
      }
    },
    "text/plain": {
      "schema": {
        "type": "string"
      }
    }
  }
}
```

### Response
#### Success Response (201)
- **description** (string) - Indicates that the pet was created successfully.
```

--------------------------------

### Define Response Status Codes and Descriptions (YAML)

Source: https://swagger.io/docs/specification/describing-responses

This snippet illustrates how to define various HTTP status codes for responses, including success codes (e.g., '200') and error codes (e.g., '400', '404'). It also shows how to define response ranges (e.g., '5XX') and provides descriptions for each status.

```yaml
responses:
  "200":
    description: OK
  "400":
    description: Bad request. User ID must be an integer and larger than 0.
  "401":
    description: Authorization information is missing or invalid.
  "404":
    description: A user with the specified ID was not found.
  "5XX":
    description: Unexpected error.
```

--------------------------------

### OpenAPI 3.0 Schema Validation with oneOf

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

Demonstrates how to use the 'oneOf' keyword in OpenAPI 3.0 to validate that a request body conforms to exactly one of the specified subschemas. This is useful for polymorphic data structures where an object can be one of several types.

```yaml
paths:
  /pets:
    patch:
      requestBody:
        content:
          application/json:
            schema:
              oneOf:
                - $ref: "#/components/schemas/Cat"
                - $ref: "#/components/schemas/Dog"
      responses:
        "200":
          description: Updated

components:
  schemas:
    Dog:
      type: object
      properties:
        bark:
          type: boolean
        breed:
          type: string
          enum: [Dingo, Husky, Retriever, Shepherd]
    Cat:
      type: object
      properties:
        hunts:
          type: boolean
        age:
          type: integer
```

--------------------------------

### Common Media Types for API Definitions

Source: https://swagger.io/docs/specification/media-types

This list outlines common media types that can be used in API request and response definitions according to RFC 6838. It includes standard formats like JSON, XML, and form data, as well as plain text and HTML.

```text
application/json
application/xml
application/x-www-form-urlencoded
multipart/form-data
text/plain; charset=utf-8
text/html
application/pdf
image/png
```

--------------------------------

### Nullable Enum

Source: https://swagger.io/docs/specification/data-models/enums

Demonstrates how to define an enum that can accept null values in addition to specified string values.

```APIDOC
## GET /items with Nullable Enum

### Description
Retrieves a list of items, where a parameter can accept 'asc', 'desc', or null.

### Method
GET

### Endpoint
/items

### Parameters
#### Query Parameters
- **sort** (string) - Optional - Sort order. Accepts 'asc', 'desc', or null.

### Request Example
```json
{
  "example": "GET /items?sort=null"
}
```

### Response
#### Success Response (200)
- **items** (array) - A list of items.

#### Response Example
```json
{
  "example": {
    "items": [
      { "id": 1, "name": "Item 1" },
      { "id": 2, "name": "Item 2" }
    ]
  }
}
```
```

--------------------------------

### Store API

Source: https://swagger.io/docs/specification/grouping-operations-with-tags

Endpoints related to store operations, specifically retrieving pet inventories.

```APIDOC
## GET /store/inventory

### Description
Returns pet inventories by status. This endpoint provides a summary of the number of pets available in the store, categorized by their status.

### Method
GET

### Endpoint
/store/inventory

### Response
#### Success Response (200)
- **Map of status codes to quantities** - A dictionary where keys are pet statuses and values are the counts of pets with that status.

#### Response Example
{
  "example": "{\"available\": 5, \"pending\": 2, \"sold\": 3}"
}
```

--------------------------------

### Define API Server Base URL in OpenAPI

Source: https://swagger.io/docs/specification/api-host-and-base-path

Specifies the base URL for API endpoints using the 'servers' array in OpenAPI 3.0. Each server object requires a 'url' property and can optionally include a 'description'. This replaces older keywords like 'host' and 'basePath'.

```yaml
servers:
  - url: https://api.example.com/v1
```

--------------------------------

### Augment Default BaseLayout with Custom Header in React for Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/custom-layout

Demonstrates how to create a custom layout 'AugmentingLayout' that includes a custom header above the default Swagger UI 'BaseLayout'. It pulls the 'BaseLayout' component using 'getComponent' and renders it within a custom structure. A plugin registers this layout, and Swagger UI is configured to use it.

```javascript
import React from "react"

// Create the layout component
class AugmentingLayout extends React.Component {
  render() {
    const {
      getComponent
    } = this.props

    const BaseLayout = getComponent("BaseLayout", true)

    return (
      <div>
        <div className="myCustomHeader">
          <h1>I have a custom header above Swagger-UI!</h1>
        </div>
        <BaseLayout />
      </div>
    )
  }
}

// Create the plugin that provides our layout component
const AugmentingLayoutPlugin = () => {
  return {
    components: {
      AugmentingLayout: AugmentingLayout
    }
  }
}

// Provide the plugin to Swagger-UI, and select AugmentingLayout
// as the layout for Swagger-UI
SwaggerUI({
  url: "https://petstore.swagger.io/v2/swagger.json",
  plugins: [ AugmentingLayoutPlugin ],
  layout: "AugmentingLayout"
})
```

--------------------------------

### Combine Authentication Types with AND and OR Logic

Source: https://swagger.io/docs/specification/authentication

This snippet illustrates a more complex security requirement combining both AND and OR logic. It defines a scenario where either (A AND B) or (C AND D) must be satisfied for authentication. This allows for flexible authentication strategies, such as requiring a specific OAuth 2 scope OR a pair of API keys.

```yaml
security:
  - oauth2: [scope1, scope2]
  - apiKey1: []
    apiKey2: []
```

--------------------------------

### Configure Yarn for Older React Versions with Swagger Editor

Source: https://swagger.io/docs/open-source-tools/swagger-editor

This JSON configuration illustrates how to use `resolutions` in Yarn to specify that the `swagger-editor` package should use a particular version of React (e.g., 17.0.2) and `react-dom`. It also addresses the `react-redux` version requirement.

```json
{
  "dependencies": {
    "react": "17.0.2",
    "react-dom": "17.0.2"
  },
  "resolutions": {
    "swagger-editor/react": "17.0.2",
    "swagger-editor/react-dom": "17.0.2",
    "swagger-editor/react-redux": "^8"
  }
}
```

--------------------------------

### Valid $ref Usage for Individual Paths

Source: https://swagger.io/docs/specification/using-ref

Shows the correct way to use $ref for individual path items within the 'paths' object in an OpenAPI 3.0 specification. This allows for modular definition of API endpoints.

```yaml
paths:
2
  /users:
3
    $ref: "../resources/users.yaml"
  /users/{userId}:
4
    $ref: "../resources/users-by-id.yaml"
```

--------------------------------

### Header Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Defines how to include custom header parameters in API requests, such as an `X-Request-ID` for tracking requests.

```APIDOC
## GET /ping

### Description
Checks if the server is alive and responsive.

### Method
GET

### Endpoint
/ping

### Header Parameters
- **X-Request-ID** (string, format: uuid) - Required - A unique identifier for the request.

### Request Example
```http
GET /ping HTTP/1.1
Host: example.com
X-Request-ID: 77e1c83b-7bb0-437b-bc50-a7a58e5660ac
```

### Response
#### Success Response (200)
- **status** (string) - The status of the server (e.g., "alive").

#### Response Example
```json
{
  "status": "alive"
}
```
```

--------------------------------

### Enum Parameters

Source: https://swagger.io/docs/specification/describing-parameters

Illustrates how to restrict a parameter to a predefined set of values using the `enum` keyword in the parameter's schema. All enum values must match the parameter's data type.

```APIDOC
## Enum Parameters

### Description
This section covers the use of the `enum` keyword to restrict a parameter's possible values to a specific, fixed set. The values provided in the enum must match the data type of the parameter.

### Method
GET

### Endpoint
/products

### Parameters
#### Query Parameters
- **status** (string) - Optional - The status of the product. Allowed values are: `available`, `pending`, `sold`.

### Request Example
```http
GET /products?status=available
GET /products?status=pending
```

### Response
#### Success Response (200)
- **products** (array) - A list of products matching the specified status.

#### Response Example
```json
{
  "products": [
    { "id": 101, "name": "T-Shirt", "status": "available" }
  ]
}
```
```

--------------------------------

### Describe Multipart File Upload in OpenAPI 3.0

Source: https://swagger.io/docs/specification/describing-request-body/file-upload

Defines a file upload as part of a `multipart/form-data` request. This allows sending files along with other form data, such as `orderId` and `userId`. The file is defined within the `properties` of the multipart schema.

```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          orderId:
            type: integer
          userId:
            type: integer
          fileName:
            type: string
            format: binary
```

--------------------------------

### React Date Picker Plugin for Swagger UI (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This JavaScript code provides a custom plugin for Swagger UI to integrate react-datepicker. It includes two components: `JsonSchema_string_date` for handling date inputs and `JsonSchema_string_date_time` for date-time inputs. The date component strips time information, while the date-time component includes time selection. Both components parse and format date values using `Date.parse` and `toISOString`.

```javascript
import React from "react";
import DatePicker from "react-datepicker";
import "react-datepicker/dist/react-datepicker.css";


const JsonSchema_string_date = (props) => {
  const dateNumber = Date.parse(props.value);
  const date = dateNumber
    ? new Date(dateNumber)
    : new Date();


  return (
    <DatePicker
      selected={date}
      onChange={d => props.onChange(d.toISOString().substring(0, 10))}
    />
  );
}

const JsonSchema_string_date_time = (props) => {
  const dateNumber = Date.parse(props.value);
  const date = dateNumber
    ? new Date(dateNumber)
    : new Date();


  return (
    <DatePicker
      selected={date}
      onChange={d => props.onChange(d.toISOString())}
      showTimeSelect
      timeFormat="p"
      dateFormat="Pp"
    />
  );
}


export const DateTimeSwaggerPlugin = {
  components: {
    JsonSchema_string_date: JsonSchema_string_date,
    "JsonSchema_string_date-time": JsonSchema_string_date_time
  }
};

```

--------------------------------

### Define Dictionary with Fixed Keys

Source: https://swagger.io/docs/specification/data-models/dictionaries

This schema defines a dictionary with a required fixed key named `default` (string) and allows additional string properties. It combines explicit property definitions with `additionalProperties`.

```yaml
type: object
properties:
  default:
    type: string
required:
  - default
additionalProperties:
  type: string
```

--------------------------------

### Swagger UI Plugin Structure

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

Defines the structure of the object returned by a Swagger UI plugin. It can include state plugins, components, wrapped components, root injections, afterLoad functions, and custom functions. The statePlugins key allows for defining actions, reducers, selectors, and wrapping functions for specific state namespaces.

```json
{
  statePlugins: {
    [stateKey]: {
      actions,
      reducers,
      selectors,
      wrapActions,
      wrapSelectors
    }
  },
  components: {},
  wrapComponents: {},
  rootInjects: {},
  afterLoad: (system) => {},
  fn: {},
}
```

--------------------------------

### Describe Request Body with Multiple Content Types (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This snippet demonstrates how to define a request body in OpenAPI 3.0 using YAML. It specifies different schemas for JSON, XML, form data, and plain text, illustrating the flexibility of the `requestBody.content` object.

```yaml
paths:
  /pets:
    post:
      summary: Add a new pet
      requestBody:
        description: Optional description in *Markdown*
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Pet"
          application/xml:
            schema:
              $ref: "#/components/schemas/Pet"
          application/x-www-form-urlencoded:
            schema:
              $ref: "#/components/schemas/PetForm"
          text/plain:
            schema:
              type: string
      responses:
        "201":
          description: Created
```

--------------------------------

### Default Fallback Component

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

The default React component used as a fallback UI when an error boundary catches an error. It displays a generic error message indicating that a component could not be rendered.

```javascript
import React from "react"
import PropTypes from "prop-types"

const Fallback = ({ name }) => (
  <div className="fallback">
    😱 <i>Could not render { name === "t" ? "this component" : name }, see the console.</i>
  </div>
)
Fallback.propTypes = {
  name: PropTypes.string.isRequired,
}
export default Fallback
```

--------------------------------

### Inject Values at Root Level with rootInjects (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

The `rootInjects` interface allows injecting values at the top level of the system. It takes an object that will be merged with the top-level system object at runtime, enabling the addition of constants or methods accessible throughout the system.

```javascript
const MyRootInjectsPlugin = function(system) {
  return {
    rootInjects: {
      myConstant: 123,
      myMethod: (...params) => console.log(...params)
    }
  }
}
```

--------------------------------

### PATCH /users/{id}

Source: https://swagger.io/docs/specification/paths-and-operations

Updates an existing user by their ID.

```APIDOC
## PATCH /users/{id}

### Description
Updates an existing user identified by their ID.

### Method
PATCH

### Endpoint
/users/{id}

### Parameters
#### Path Parameters
- **id** (integer) - Required - The unique identifier for the user.

#### Query Parameters
None

#### Request Body
- **name** (string) - Optional - The updated name of the user.
```

--------------------------------

### Define Any Type Schema in OpenAPI

Source: https://swagger.io/docs/specification/data-models/data-types

A schema without a `type` specified matches any data type. The shorthand `{}` can be used for an arbitrary-type schema. Descriptions can be added for clarity. Allowing `null` requires setting `nullable: true`.

```yaml
components:
  schemas:
    AnyValue: {}
```

```yaml
components:
  schemas:
    AnyValue:
      description: Can be any value - string, number, boolean, array or object.
```

```yaml
components:
  schemas:
    AnyValue:
      anyOf:
        - type: string
        - type: number
        - type: integer
        - type: boolean
        - type: array
          items: {}
        - type: object
```

```yaml
components:
  schemas:
    AnyValue:
      nullable: true
      description: Can be any value, including `null`.
```

--------------------------------

### OpenAPI: Empty Response Body (204 No Content)

Source: https://swagger.io/docs/specification/describing-responses

Indicates that a response, such as a '204 No Content' status, has no body. This is achieved by omitting the `content` property for that specific response.

```yaml
responses:
  "204":
    description: The resource was deleted successfully.
```

--------------------------------

### Generate API Client with Inline OpenAPI Specification using JSON

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

This JSON payload demonstrates how to generate an API client by including the OpenAPI specification directly within the request body using the `spec` field, instead of providing a `specURL`. This is useful for generating code from local or dynamically created specifications.

```json
{
  "options": {},
  "spec": {
    "swagger": "2.0",
    "info": {
      "version": "1.0.0",
      "title": "Test API"
    },
    ...
  }
}
```

--------------------------------

### Set Object Variable with Escaped Characters (Shell)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Demonstrates how to set a shell variable with a JSON object literal, ensuring that special characters within the JSON are properly escaped. This is useful for passing structured data as environment variables.

```shell
SPEC="{ \"openapi\": \"3.0.4\" }"
```

--------------------------------

### OpenAPI: Return File Response (base64)

Source: https://swagger.io/docs/specification/describing-responses

Defines an API response where a file (like an image) is embedded as a base64-encoded string within a JSON object. It uses `type: string` with `format: byte` for the base64 encoded field.

```yaml
paths:
  /users/me:
    get:
      summary: Returns user information
      responses:
        "200":
          description: A JSON object containing user name and avatar
          content:
            application/json:
              schema:
                type: object
                properties:
                  username:
                    type: string
                  avatar: # <-- image embedded into JSON
                    type: string
                    format: byte
                    description: Base64-encoded contents of the avatar image
```

--------------------------------

### OpenAPI 3.0 Schema with Reserved Character Handling

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Illustrates how to control percent-encoding of reserved characters in form data values using the `allowReserved` keyword in OpenAPI 3.0.

```APIDOC
## OpenAPI 3.0 Schema with Reserved Character Handling

### Description
This OpenAPI 3.0 snippet shows how to use the `allowReserved` keyword within the `encoding` object to prevent percent-encoding of reserved characters in specific form field values.

### Method
POST

### Endpoint
[Endpoint not specified in source text]

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **content** (object)
  - **application/x-www-form-urlencoded** (object)
    - **schema** (object)
      - **type** (string) - "object"
      - **properties** (object)
        - **foo** (object)
          - **type** (string)
        - **bar** (object)
          - **type** (string)
        - **baz** (object)
          - **type** (string)
    - **encoding** (object)
      - **bar** (object)
        - **allowReserved** (boolean) - true
      - **baz** (object)
        - **allowReserved** (boolean) - true

### Request Example
```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        properties:
          foo:
            type: string
          bar:
            type: string
          baz:
            type: string
      encoding:
        bar:
          allowReserved: true
        baz:
          allowReserved: true
```

### Response
#### Success Response (200)
Details of the success response are not provided in the source text.

#### Response Example
No example provided for the response.
```

--------------------------------

### Default XML Array Wrapping

Source: https://swagger.io/docs/specification/data-models/representing-xml

Demonstrates the default translation of arrays in XML, where each item is represented by an element with the same name.

```APIDOC
## Default XML Array Wrapping

### Description
Arrays are translated as a sequence of elements of the same name.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
- **books** (array[string]) - An array of strings.

#### Response Example
```xml
<books>one</books>
<books>two</books>
<books>three</books>
```
```

--------------------------------

### OpenAPI 3.0 Schema with Array Serialization

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Shows how to define array serialization strategies within form data using the `encoding` object in OpenAPI 3.0.

```APIDOC
## OpenAPI 3.0 Schema with Array Serialization

### Description
This OpenAPI 3.0 snippet demonstrates how to specify array serialization for form data, using the `encoding` object to control the `style` and `explode` behavior.

### Method
POST

### Endpoint
[Endpoint not specified in source text]

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **content** (object)
  - **application/x-www-form-urlencoded** (object)
    - **schema** (object)
      - **type** (string) - "object"
      - **properties** (object)
        - **color** (object)
          - **type** (array)
          - **items** (object)
            - **type** (string)
    - **encoding** (object)
      - **color** (object)
        - **style** (string) - "form"
        - **explode** (boolean) - false

### Request Example
```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        properties:
          color:
            type: array
            items:
              type: string
      encoding:
        color:
          style: form
          explode: false
```

### Response
#### Success Response (200)
Details of the success response are not provided in the source text.

#### Response Example
No example provided for the response.
```

--------------------------------

### Suppress Missing Component Warnings in JavaScript

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

This snippet shows how to use the `failSilently` option with `getComponent` to suppress warnings when a requested component is not found in the system. The arguments to `getComponent` include a boolean for container presence and a config object.

```javascript
const thisVariableWillBeNull = getComponent("not_real", false, { failSilently: true })
```

--------------------------------

### OpenAPI Server Templating for Regional Endpoints

Source: https://swagger.io/docs/specification/api-host-and-base-path

Shows how to use server templating to configure API endpoints for different geographical regions. The 'region' variable uses an enum to list available regional endpoints, with a default region specified.

```yaml
servers:
  - url: https://{region}.api.cognitive.microsoft.com
    variables:
      region:
        default: westus
        enum:
          - westus
          - eastus2
          - westcentralus
          - westeurope
          - southeastasia
```

--------------------------------

### Specify Custom Codegen Class

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

This command-line argument specifies a custom Java class to be used as the code generator. This allows for deep customization by extending existing language generators.

```bash
-l com.mycompany.swagger.codegen.MyObjcCodegen
```

--------------------------------

### OpenAPI: Response with Alternate Schemas (oneOf)

Source: https://swagger.io/docs/specification/describing-responses

Specifies that a response body can conform to one of several alternative schemas using the `oneOf` keyword. This is useful when a response can be one of several distinct types.

```yaml
responses:
  "200":
    description: A JSON object containing pet information
    content:
      application/json:
        schema:
          oneOf:
            - $ref: "#/components/schemas/Cat"
            - $ref: "#/components/schemas/Dog"
            - $ref: "#/components/schemas/Hamster"
```

--------------------------------

### OpenAPI: Default Response for Errors

Source: https://swagger.io/docs/specification/describing-responses

Uses the `default` response to collectively describe error responses that share the same schema, rather than defining each error status code individually. This simplifies the specification for common error structures.

```yaml
responses:
  "200":
    description: Success
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User"

  # Definition of all error statuses
  default:
    description: Unexpected error
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/Error"
```

--------------------------------

### Describe Request Body with Alternate Schemas (YAML)

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This YAML snippet illustrates the use of `oneOf` to specify alternate schemas for a JSON request body in OpenAPI 3.0. It allows the request body to conform to the schema of a Cat, Dog, or Hamster, providing flexibility in data structure.

```yaml
requestBody:
  description: A JSON object containing pet information
  content:
    application/json:
      schema:
        oneOf:
          - $ref: "#/components/schemas/Cat"
          - $ref: "#/components/schemas/Dog"
          - $ref: "#/components/schemas/Hamster"
```

--------------------------------

### Define API Operations with Tags

Source: https://swagger.io/docs/specification/grouping-operations-with-tags

This YAML snippet shows how to assign tags to individual API operations like finding pets by status, adding a new pet, and retrieving store inventory. Tags are used to categorize operations, which can be handled differently by various tools and libraries.

```yaml
paths:
  /pet/findByStatus:
    get:
      summary: Finds pets by Status
      tags:
        - pets
      ...
  /pet:
    post:
      summary: Adds a new pet to the store
      tags:
        - pets
      ...
  /store/inventory:
    get:
      summary: Returns pet inventories
      tags:
        - store
      ...
```

--------------------------------

### Override Component Rendering with Wrap-Components (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

Wrap-Components allow overriding registered components. They are function factories that take the original component and the system as arguments, returning a new component. This enables customization of how components are rendered, such as adding elements before or after the original component.

```javascript
const MyWrapBuiltinComponentPlugin = function(system) {
  return {
    wrapComponents: {
      info: (Original, system) => (props) => {
        return <div>
          <h3>Hello world! I am above the Info component.</h3>
          <Original {...props} />
        </div>
      }
    }
  }
}
```

--------------------------------

### DELETE /users/{id}

Source: https://swagger.io/docs/specification/paths-and-operations

Deletes a user by their ID.

```APIDOC
## DELETE /users/{id}

### Description
Deletes a user from the system using their unique ID.

### Method
DELETE

### Endpoint
/users/{id}

### Parameters
#### Path Parameters
- **id** (integer) - Required - The unique identifier for the user.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **description** (string) - User deleted successfully.
```

--------------------------------

### POST /api/generate

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/online-generators

Generates an API client based on the provided OpenAPI specification URL, language, and generation type.

```APIDOC
## POST /api/generate

### Description
Generates an API client in a specified language from an OpenAPI specification. The specification can be provided via a URL or directly in the request body. Supports both V2 and V3 OpenAPI specifications.

### Method
POST

### Endpoint
https://generator3.swagger.io/api/generate

### Parameters
#### Request Body
- **specURL** (string) - Required - URL to the OpenAPI/Swagger specification.
- **lang** (string) - Required - The programming language for the client (e.g., "java", "python").
- **type** (string) - Required - The type of generation (e.g., "CLIENT", "SERVER").
- **codegenVersion** (string) - Optional - Specifies the codegen version to use (e.g., "V2", "V3"). Defaults to V3.
- **options** (object) - Optional - Language-specific options for customization.
- **spec** (object) - Optional - The OpenAPI/Swagger specification as a JSON object. Use this instead of `specURL`.

### Request Example
```json
{
  "specURL" : "https://raw.githubusercontent.com/OAI/OpenAPI-Specification/master/examples/v3.0/petstore.yaml",
  "lang" : "java",
  "type" : "CLIENT",
  "codegenVersion" : "V3"
}
```

### Response
#### Success Response (200)
- **zipped file** (binary) - A zipped file containing the generated code.

#### Response Example
(Binary data representing a zipped file)
```

--------------------------------

### OpenAPI Specification for Slack Incoming Webhook with JSON Payload

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

An OpenAPI 3.0.4 specification illustrating how to define a POST request for a Slack incoming webhook. It shows how to accept `application/json` directly or `application/x-www-form-urlencoded` where the `payload` field contains JSON data, specified by `contentType: application/json`.

```yaml
openapi: 3.0.4
info:
  version: 1.0.0
  title: Slack Incoming Webhook
externalDocs:
  url: https://api.slack.com/incoming-webhooks

servers:
  - url: https://hooks.slack.com

paths:
  /services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX:
    post:
      summary: Post a message to Slack
      requestBody:
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Message"

          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                payload: # <--- form field that contains the JSON message
                  $ref: "#/components/schemas/Message"
            encoding:
              payload:
                contentType: application/json

      responses:
        "200":
          description: OK

components:
  schemas:
    Message:
      title: A Slack message
      type: object
      properties:
        text:
          type: string
          description: Message text
      required:
        - text

```

--------------------------------

### Default Response Handling

Source: https://swagger.io/docs/specification/describing-responses

Defines a common schema for all error responses that are not individually specified for an operation.

```APIDOC
## Default Response Handling

### Description
Provides a common schema for all unspecified error responses (e.g., 400, 404, 500).

### Method
(Not specified in example, applies to any method)

### Endpoint
(Not specified in example)

### Parameters
None

### Response
#### Success Response (200)
- **Schema**: User

#### Default Response (Error Handling)
- **Description**: Unexpected error
- **Content**: application/json
  - **Schema**: Error

#### Response Example (Success)
```json
{
  "user_id": 123,
  "username": "testuser"
}
```

#### Response Example (Error)
```json
{
  "error_code": "INVALID_INPUT",
  "message": "The provided input is invalid."
}
```
```

--------------------------------

### Define Free-Form Object Dictionary Schema

Source: https://swagger.io/docs/specification/data-models/dictionaries

This schema defines a dictionary where the values can be of any type. It uses `additionalProperties: true` or `additionalProperties: {}` to indicate free-form values.

```yaml
type: object
additionalProperties: true
```

```yaml
type: object
additionalProperties: {}
```

--------------------------------

### Override Servers at Path and Operation Levels - YAML

Source: https://swagger.io/docs/specification/api-host-and-base-path

Demonstrates overriding the global 'servers' array at both the path level ('/files') and the operation level ('/ping') in an OpenAPI definition. This allows specific endpoints or groups of endpoints to use different base URLs.

```yaml
servers:
  - url: https://api.example.com/v1

paths:
  /files:
    description: File upload and download operations
    servers:
      - url: https://files.example.com
        description: Override base path for all operations with the /files path
    ...

  /ping:
    get:
      servers:
        - url: https://echo.example.com
          description: Override base path for the GET /ping operation
```

--------------------------------

### Enable Array Wrapping in Swagger Specification

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet demonstrates how to enable wrapping for an array in a Swagger specification using the `xml/wrapped: true` property.

```yaml
books:
  type: array
  items:
    type: string
  xml:
    wrapped: true
  example:
    - "one"
    - "two"
    - "three"
```

--------------------------------

### PUT /avatar - Upload an avatar

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

This endpoint allows users to upload an avatar. It accepts any image media type and expects binary data for the avatar.

```APIDOC
## PUT /avatar

### Description
Uploads an avatar for the user. Accepts any image format.

### Method
PUT

### Endpoint
/avatar

### Parameters
#### Request Body
- **content** (object) - Required - Maps media types to their schemas.
  - **image/* ** (object) - Schema for any image media type.
    - **schema** (object) - Schema for the image data.
      - **type** (string) - Specifies the data type, should be 'string'.
      - **format** (string) - Specifies the format, should be 'binary'.
```

--------------------------------

### XML Representation with Custom Wrapped Element Names

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet illustrates the XML output when custom names are specified for the wrapping element and array items, providing better control over naming.

```xml
<books-array>
  <item>one</item>
  <item>two</item>
  <item>three</item>
</books-array>
```

--------------------------------

### Implement Custom Node.js Native Request Snippet Generator Plugin

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This JavaScript plugin provides a function to generate Node.js native HTTP request snippets. It handles different request methods, headers, and body types, including JSON and multipart/form-data (though the latter is currently unsupported). The generated snippet includes options for method, hostname, port, path, headers, and request body.

```javascript
const SnippedGeneratorNodeJsPlugin = {
  fn: {
    requestSnippetGenerator_node_native: (request) => {
      const url = new Url(request.get("url"))
      let isMultipartFormDataRequest = false
      const headers = request.get("headers")
      if(headers && headers.size) {
        request.get("headers").map((val, key) => {
          isMultipartFormDataRequest = isMultipartFormDataRequest || /^content-type$/i.test(key) && /^multipart\/form-data$/i.test(val)
        })
      }
      const packageStr = url.protocol === "https:" ? "https" : "http"
      let reqBody = request.get("body")
      if (request.get("body")) {
        if (isMultipartFormDataRequest && ["POST", "PUT", "PATCH"].includes(request.get("method"))) {
          return "throw new Error(\"Currently unsupported content-type: /^multipart\/form-data$/i\");"
        } else {
          if (!Map.isMap(reqBody)) {
            if (typeof reqBody !== "string") {
              reqBody = JSON.stringify(reqBody)
            }
          } else {
            reqBody = getStringBodyOfMap(request)
          }
        }
      } else if (!request.get("body") && request.get("method") === "POST") {
        reqBody = ""
      }

      const stringBody = "`" + (reqBody || "")
          .replace(/\\n/g, "\n")
          .replace(/`/g, "\\`")
        + "`"

      return `const http = require("${packageStr}");
const options = {
  "method": "${request.get("method")}",
  "hostname": "${url.host}",
  "port": ${url.port || "null"},
  "path": "${url.pathname}"${headers && headers.size ? `, 
  "headers": {
    ${request.get("headers").map((val, key) => `"${key}": "${val}"`).valueSeq().join(",\n    ")} 
  }` : ""}
};
const req = http.request(options, function (res) {
  const chunks = [];
  res.on("data", function (chunk) {
    chunks.push(chunk);
  });
  res.on("end", function () {
    const body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});
${reqBody ? `\nreq.write(${stringBody});` : ""}
req.end();`
    }
  }
}
```

--------------------------------

### Define a Constant Required Query Parameter (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This snippet shows how to define a constant parameter ('rel_date') that is required and has only one possible value ('now') using the 'required: true' and 'enum' keywords in YAML. This ensures the client must always send this specific value.

```yaml
parameters:
  - in: query
    name: rel_date
    required: true
    schema:
      type: string
      enum:
        - now
```

--------------------------------

### Specifying Content-Type for Multipart Parts

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

Demonstrates how to explicitly set the Content-Type for individual parts within a multipart request using the `encoding` field.

```APIDOC
## POST /upload

### Description
This endpoint handles multipart requests, allowing for the upload of files and other data in a single request body. This example shows how to specify custom Content-Types for request parts.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **id** (string, uuid) - Required - A unique identifier for the request.
- **address** (object) - Required - An object containing address details.
  - **street** (string) - Required - The street name and number.
  - **city** (string) - Required - The city name.
- **profileImage** (string, base64) - Optional - The profile image file to upload, specified with a custom content type.

#### Request Body Encoding
- **profileImage**:
  - **contentType**: `image/png, image/jpeg`

### Request Example
```json
{
  "requestBody": {
    "content": {
      "multipart/form-data": {
        "schema": {
          "type": "object",
          "properties": {
            "id": {
              "type": "string",
              "format": "uuid"
            },
            "address": {
              "type": "object",
              "properties": {
                "street": {
                  "type": "string"
                },
                "city": {
                  "type": "string"
                }
              }
            },
            "profileImage": {
              "type": "string",
              "format": "base64"
            }
          }
        },
        "encoding": {
          "profileImage": {
            "contentType": "image/png, image/jpeg"
          }
        }
      }
    }
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating successful upload.
```

--------------------------------

### Define String Pattern with Regex

Source: https://swagger.io/docs/specification/data-models/data-types

Uses the `pattern` keyword to enforce a regular expression for string values. The regex syntax is based on JavaScript (ECMA 262) and is case-sensitive. Enclosing the regex in `^...$` ensures an exact match.

```yaml
ssn:
  type: string
  pattern: '^\d{3}-\d{2}-\d{4}$'
```

--------------------------------

### Applying Bearer Authentication Globally

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Applies the defined Bearer Authentication scheme to all operations within the API globally.

```APIDOC
## Applying Bearer Authentication Globally

### Description
Applies the defined Bearer Authentication scheme globally to all API operations. This ensures that all requests must include a valid bearer token.

### Method
N/A (Schema Configuration)

### Endpoint
N/A (Schema Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

```yaml
security:
  - bearerAuth: []
```
```

--------------------------------

### Documenting 401 Unauthorized Response in OpenAPI

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Documents a 401 'Unauthorized' response for an API operation using a reference to a globally defined response. This standardizes error handling for missing or invalid tokens.

```yaml
paths:
  /something:
    get:
      responses:
        '401':
          $ref: '#/components/responses/UnauthorizedError'
components:
  responses:
    UnauthorizedError:
      description: Access token is missing or invalid
```

--------------------------------

### Programmatically Set API Key Authorization (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration

Sets values for an API key or Bearer authorization scheme programmatically. For OpenAPI 3.0 Bearer scheme, apiKeyValue must be the token itself without the 'Bearer' prefix.

```javascript
preauthorizeApiKey('apiKeyAuth', 'YOUR_API_KEY');
```

--------------------------------

### Mapping Schema Property to XML Attribute

Source: https://swagger.io/docs/specification/data-models/representing-xml

Shows how to designate a schema property to be represented as an XML attribute instead of a child element using the `xml/attribute: true` setting. This is useful for properties that logically function as metadata.

```yaml
book:
  type: object
  properties:
    id:
      type: integer
      xml:
        attribute: true
    title:
      type: string
    author:
      type: string
```

```xml
<book id="0">
  <title>string</title>
  <author>string</author>
</book>
```

--------------------------------

### Define Nullable Enum (YAML)

Source: https://swagger.io/docs/specification/data-models/enums

Illustrates how to define an enum that can accept null values. Both `nullable: true` and explicitly including `null` in the enum list are required.

```yaml
type: string
nullable: true
enum:
  - asc
  - desc
  - null
```

--------------------------------

### Changing XML Element Names with 'xml/name'

Source: https://swagger.io/docs/specification/data-models/representing-xml

Illustrates how to override the default XML element naming convention by specifying a custom name using the `xml/name` property within the schema definition. This allows for more control over the generated XML structure.

```yaml
components:
  schemas:
    book:
      type: object
      properties:
        id:
          type: integer
        title:
          type: string
        author:
          type: string
      xml:
        name: "xml-book"
```

```xml
<xml-book>
  <id>0</id>
  <title>string</title>
  <author>string</author>
</xml-book>
```

--------------------------------

### Swagger/OpenAPI 'not' Keyword Schema Definition

Source: https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not

This snippet demonstrates the usage of the 'not' keyword within a Swagger/OpenAPI schema definition. It specifies that the 'pet_type' property should not be of type 'integer'. This is useful for enforcing specific data types or excluding certain types.

```yaml
components:
  schemas:
    PetByType:
      type: object
      properties:
        pet_type:
          not:
            type: integer
      required:
        - pet_type
```

--------------------------------

### Define Empty-Valued Query Parameter (YAML)

Source: https://swagger.io/docs/specification/describing-parameters

This snippet demonstrates how to define a query parameter that is allowed to have an empty value. It uses the `allowEmptyValue` property set to `true` within the parameter definition. This is useful for parameters that do not require a value but should still be present in the query string.

```yaml
parameters:
  - in: query
    name: metadata
    schema:
      type: boolean
    allowEmptyValue: true
```

--------------------------------

### Define File Types in OpenAPI Schema

Source: https://swagger.io/docs/specification/data-models/data-types

In OpenAPI 3.0, files are represented as strings with specific formats. Use `format: binary` for raw binary file contents or `format: byte` for base64-encoded file contents.

```yaml
type: string
format: binary
```

```yaml
type: string
format: byte
```

--------------------------------

### Pets API

Source: https://swagger.io/docs/specification/grouping-operations-with-tags

Endpoints related to pet operations, including finding pets by status and adding new pets.

```APIDOC
## GET /pet/findByStatus

### Description
Finds pets by Status. This endpoint allows you to retrieve a list of pets based on their available status (e.g., available, pending, sold).

### Method
GET

### Endpoint
/pet/findByStatus

### Parameters
#### Query Parameters
- **status** (string) - Required - The status values that need to be considered for filter

### Response
#### Success Response (200)
- **Array of Pet objects** - Description of the pet objects returned

#### Response Example
{
  "example": "[{"id": 1, "name": "Buddy", "status": "available"}]"
}

## POST /pet

### Description
Adds a new pet to the store. This endpoint allows you to create a new pet record in the system.

### Method
POST

### Endpoint
/pet

### Parameters
#### Request Body
- **Pet object** (object) - Required - The pet object to add to the store

### Request Example
{
  "example": "{\"id\": 1, \"name\": \"Buddy\", \"status\": \"available\"}"
}

### Response
#### Success Response (200)
- **Pet object** - Description of the pet object that was added

#### Response Example
{
  "example": "{\"id\": 1, \"name\": \"Buddy\", \"status\": \"available\"}"
}
```

--------------------------------

### Specify Import Mapping for Models

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/generators-configuration

This argument tells Swagger Codegen to use a specified external class for a particular model instead of generating a new one. This is useful for integrating with existing model definitions.

```bash
--import-mappings Pet=my.models.MyPet
```

--------------------------------

### POST /upload - Custom Headers for Multipart

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

This endpoint demonstrates how to define and use custom headers for specific parts within a multipart/form-data request. It utilizes the `encoding` property in the OpenAPI schema to specify headers like `X-Custom-Header` for the `profileImage` part.

```APIDOC
## POST /upload

### Description
This endpoint allows file uploads using `multipart/form-data`. It shows how to specify custom headers for individual parts of the request, such as a custom header for the `profileImage` part.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **id** (string, uuid) - Required - The unique identifier for the upload.
- **profileImage** (string, binary) - Required - The image file to be uploaded.
  - **encoding**:
    - **profileImage**:
      - **contentType** (string) - Optional - Specifies allowed content types (e.g., `image/png, image/jpeg`).
      - **headers**:
        - **X-Custom-Header** (string) - Optional - A custom header for this part.

### Request Example
```
POST /upload HTTP/1.1
Content-Length: 428
Content-Type: multipart/form-data; boundary=abcde12345

--abcde12345
Content-Disposition: form-data; name="id"
Content-Type: text/plain

123e4567-e89b-12d3-a456-426655440000
--abcde12345
Content-Disposition: form-data; name="profileImage"; filename="image1.png"
Content-Type: image/png
X-Custom-Header: x-header

{…file content…}
--abcde12345--
```

### Response
#### Success Response (200)
- **message** (string) - Description of the upload status.

#### Response Example
```json
{
  "message": "File uploaded successfully"
}
```
```

--------------------------------

### OpenAPI Floating-Point Range Definition with Exclusive Minimum

Source: https://swagger.io/docs/specification/data-models/data-types

Illustrates how to define a floating-point number range where the minimum boundary is excluded. This is achieved using 'exclusiveMinimum: true'.

```yaml
type: number
minimum: 0
exclusiveMinimum: true
maximum: 50
```

--------------------------------

### Define Basic Array

Source: https://swagger.io/docs/specification/data-models/data-types

Defines an array where all items are of a specified type, such as string. The `items` keyword is mandatory and describes the schema for array elements.

```yaml
type: array
items:
  type: string
```

--------------------------------

### YAML Discriminator Mapping for Schema Resolution

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

This YAML snippet illustrates how to configure a discriminator with a mapping in an OpenAPI specification. It defines how a property's value (e.g., 'objectType') should be used to resolve to a specific schema (e.g., 'Object1', 'Object2', or an external 'sysObject'). This is useful for polymorphism where a single property determines the actual data structure.

```yaml
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/Object1'
              - $ref: '#/components/schemas/Object2'
              - $ref: 'sysObject.json#/sysObject'
            discriminator:
              propertyName: objectType
              mapping:
                obj1: '#/components/schemas/Object1'
                obj2: '#/components/schemas/Object2'
                system: 'sysObject.json#/sysObject'
  ...
  schemas:
    Object1:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
    Object2:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
```

--------------------------------

### OpenAPI 3.0 Free-Form Schema

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Models arbitrary key-value pairs for `application/x-www-form-urlencoded` data in OpenAPI 3.0 using `additionalProperties: true`. This allows for flexible, undefined form fields.

```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        additionalProperties: true # this line is optional
```

--------------------------------

### XML Representation of Unwrapped Array

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet illustrates the default XML output for an unwrapped array of strings, where each item is a separate element with the same name.

```xml
<books>one</books>
<books>two</books>
<books>three</books>
```

--------------------------------

### Define Array with Schema Reference

Source: https://swagger.io/docs/specification/data-models/data-types

Defines an array where the schema for its items is referenced from elsewhere using `$ref`. This promotes reusability and modularity in OpenAPI definitions.

```yaml
type: array
items:
  $ref: "#/components/schemas/Pet"
```

--------------------------------

### Valid Link Name Characters

Source: https://swagger.io/docs/specification/links

Specifies the allowed characters for naming links in OpenAPI. Link names can only contain uppercase letters (A-Z), lowercase letters (a-z), digits (0-9), period (.), underscore (_), and hyphen (-).

```text
A..Z a..z 0..9 . _ -
```

--------------------------------

### Define Array of Objects

Source: https://swagger.io/docs/specification/data-models/data-types

Defines an array where each element is an object with a specific schema. The `items` keyword specifies the object schema, including its properties.

```yaml
type: array
items:
  type: object
  properties:
    id:
      type: integer
```

--------------------------------

### Define Array of Any Type

Source: https://swagger.io/docs/specification/data-models/data-types

Specifies an array that can contain items of any type. This is achieved by using an empty schema `{}` for the `items` keyword, representing the 'any-type' schema.

```yaml
type: array
items: {}
```

--------------------------------

### Apply Scopes Globally (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

Applies a set of OAuth scopes to all API operations by defining them at the root level of the API definition in the `security` section.

```yaml
security:
  - oAuthSample: [write_pets]

```

--------------------------------

### Define Enum with One Value Per Line (YAML)

Source: https://swagger.io/docs/specification/data-models/enums

An alternative YAML syntax for defining an enum where each possible value is listed on a new line. This can improve readability for longer enum lists.

```yaml
enum:
  - asc
  - desc
```

--------------------------------

### Create Custom Operations Layout in React for Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/custom-layout

Defines a custom React component 'OperationsLayout' that displays only the operations section of the Swagger UI. It uses a plugin to register this layout and then configures Swagger UI to use it. This allows for high-level control over the UI's root component.

```javascript
import React from "react"

// Create the layout component
class OperationsLayout extends React.Component {
  render() {
    const {
      getComponent
    } = this.props

    const Operations = getComponent("operations", true)

    return (
      <div className="swagger-ui">
        <Operations />
      </div>
    )
  }
}

// Create the plugin that provides our layout component
const OperationsLayoutPlugin = () => {
  return {
    components: {
      OperationsLayout: OperationsLayout
    }
  }
}

// Provide the plugin to Swagger-UI, and select OperationsLayout
// as the layout for Swagger-UI
SwaggerUI({
  url: "https://petstore.swagger.io/v2/swagger.json",
  plugins: [ OperationsLayoutPlugin ],
  layout: "OperationsLayout"
})
```

--------------------------------

### Implement Custom Multiple-Phrase Operation Filter in Swagger UI

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plug-points

This JavaScript code defines a custom plugin, `MultiplePhraseFilterPlugin`, that overrides the default `opsFilter` function in Swagger UI. It allows filtering operations based on multiple comma-separated phrases provided by the user, enhancing the filtering capabilities beyond a single phrase.

```javascript
const MultiplePhraseFilterPlugin = function() {
  return {
    fn: {
      opsFilter: (taggedOps, phrase) => {
        const phrases = phrase.split(", ")

        return taggedOps.filter((val, key) => {
          return phrases.some(item => key.indexOf(item) > -1)
        })
      }
    }
  }
}
```

--------------------------------

### HTTP Header for Bearer Token

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

This snippet shows the standard HTTP header format for sending a bearer token. The client must include this header in requests to protected resources.

```http
Authorization: Bearer <token>
```

--------------------------------

### OpenAPI 3: Specify Content-Type for Multipart Part

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

Demonstrates how to explicitly set the `Content-Type` for a specific part within a multipart request in OpenAPI 3. This is achieved using the `encoding` keyword at the same level as the `schema`.

```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties: # Request parts
          id:
            type: string
            format: uuid
          address:
            type: object
            properties:
              street:
                type: string
              city:
                type: string
          profileImage:
            type: string
            format: base64
      encoding: # The same level as schema
        profileImage: # Property name (see above)
          contentType: image/png, image/jpeg
```

--------------------------------

### Define OAuth 2.0 Security Scheme in OpenAPI

Source: https://swagger.io/docs/specification/authentication/oauth2

This snippet demonstrates how to define an OAuth 2.0 security scheme named 'oAuthSample' within the 'components/securitySchemes' section of an OpenAPI document. It specifies the 'oauth2' type, provides a description, and configures the 'implicit' grant flow with its authorization URL and available scopes.

```yaml
components:
  securitySchemes:
    oAuthSample:
      type: oauth2
      description: This API uses OAuth 2 with the implicit grant flow. [More info](https://api.example.com/docs/auth)
      flows:
        implicit:
          authorizationUrl: https://api.example.com/oauth2/authorize
          scopes:
            read_pets: read your pets
            write_pets: modify pets in your account
```

--------------------------------

### Customizing Wrapped Array Element Names in Swagger

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet shows how to customize the names of the wrapping element and individual array items in a Swagger specification using `xml/name`.

```yaml
books:
  type: array
  items:
    type: string
    xml:
      name: "item"
  xml:
    wrapped: true
    name: books-array
  example:
    - "one"
    - "two"
    - "three"
```

--------------------------------

### Use Relative URLs for OAuth Endpoints (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

Specifies OAuth authorization and token URLs relative to the API server URL. This simplifies configuration when these endpoints reside on the same host as the API.

```yaml
servers:
  - url: https://api.example.com/v2

components:
  securitySchemes:
    oauth2sample:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: /oauth/authorize # <-----
          tokenUrl: /oauth/token # <-----
          scopes: ...

```

--------------------------------

### OpenAPI 3.0 Reserved Character Handling

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Shows how to control percent-encoding of reserved characters in form field values using the `allowReserved` keyword in OpenAPI 3.0. This allows specific characters to be sent as-is.

```yaml
requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        properties:
          foo:
            type: string
          bar:
            type: string
          baz:
            type: string
      encoding:
        # Don't percent-encode reserved characters in the values of "bar" and "baz" fields
        bar:
          allowReserved: true
        baz:
          allowReserved: true
```

--------------------------------

### Define Unique Operation IDs in OpenAPI

Source: https://swagger.io/docs/specification/paths-and-operations

Shows how to use the `operationId` field in OpenAPI to uniquely identify operations. This is useful for code generation and linking between operations. IDs must be unique across all operations within the API.

```yaml
/users:
  get:
    operationId: getUsers
    summary: Gets all users
  post:
    operationId: addUser
    summary: Adds a new user
/user/{id}:
  get:
    operationId: getUserById
    summary: Gets a user by user ID
```

--------------------------------

### Response Status Codes

Source: https://swagger.io/docs/specification/describing-responses

Defines common HTTP status codes and their descriptions for API responses.

```APIDOC
## Response Status Codes

### Description
This section outlines the standard HTTP status codes used in API responses, including success and error codes.

### Status Codes
- **200 OK**: The request was successful.
- **400 Bad Request**: The request was invalid. For example, a user ID must be an integer and larger than 0.
- **401 Unauthorized**: Authorization information is missing or invalid.
- **404 Not Found**: A resource with the specified ID was not found.
- **5XX Server Error**: An unexpected error occurred on the server.
```

--------------------------------

### Allow Null Values

Source: https://swagger.io/docs/specification/data-models/data-types

Indicates that a value can be `null` using `nullable: true`. This is distinct from an empty string. This maps to nullable types in languages like C# (`int?`) and Java (`java.lang.Integer`).

```yaml
type: integer
nullable: true
```

--------------------------------

### Multipart Request Definition

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

Defines a multipart request with various data types including strings, JSON objects, and binary files.

```APIDOC
## POST /upload

### Description
This endpoint handles multipart requests, allowing for the upload of files and other data in a single request body.

### Method
POST

### Endpoint
/upload

### Parameters
#### Request Body
- **id** (string, uuid) - Required - A unique identifier for the request.
- **address** (object) - Required - An object containing address details.
  - **street** (string) - Required - The street name and number.
  - **city** (string) - Required - The city name.
- **profileImage** (string, binary) - Optional - The profile image file to upload.

### Request Example
```http
POST /upload HTTP/1.1
Content-Length: 428
Content-Type: multipart/form-data; boundary=abcde12345

--abcde12345
Content-Disposition: form-data; name="id"
Content-Type: text/plain

123e4567-e89b-12d3-a456-426655440000
--abcde12345
Content-Disposition: form-data; name="address"
Content-Type: application/json

{
  "street": "3, Garden St",
  "city": "Hillsbery, UT"
}
--abcde12345
Content-Disposition: form-data; name="profileImage "; filename="image1.png"
Content-Type: application/octet-stream

{…file content…}
--abcde12345--
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating successful upload.
```

--------------------------------

### POST /services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Posts a message to a Slack channel using an incoming webhook. Supports both direct JSON payloads and JSON embedded within a form data field named 'payload'.

```APIDOC
## POST /services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX

### Description
Posts a message to a Slack channel using an incoming webhook. This endpoint can accept the message content either as a direct JSON payload or as a JSON string within the `payload` form field.

### Method
POST

### Endpoint
/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX

### Parameters

#### Request Body

##### `application/json`
- **text** (string) - Required - The text content of the message.

##### `application/x-www-form-urlencoded`
- **payload** (object) - Required - An object containing the message details. The `contentType` for this field is `application/json`, meaning the value should be a JSON string representing the message.
  - **text** (string) - Required - The text content of the message.

### Request Example

#### Using `application/json`
```json
{
  "text": "Swagger is awesome"
}
```

#### Using `application/x-www-form-urlencoded` with `payload` field
```
payload=%7B%22text%22%3A%22Swagger%20is%20awesome%22%7D
```

### Response

#### Success Response (200)
- **description** (string) - Indicates that the message was successfully posted.

#### Response Example
```json
{
  "description": "OK"
}
```
```

--------------------------------

### OpenAPI Correct Mixed Type Definition using oneOf

Source: https://swagger.io/docs/specification/data-models/data-types

Shows the correct method for defining mixed types in OpenAPI by utilizing the 'oneOf' keyword to specify a list of alternative valid types.

```yaml
oneOf:
  - type: string
  - type: integer
```

--------------------------------

### Disable Scarf Analytics in package.json

Source: https://swagger.io/docs/open-source-tools/swagger-editor

This code snippet demonstrates how to disable Scarf analytics by setting the 'enabled' field to 'false' within the 'scarfSettings' object in your project's package.json file. This is a project-specific configuration.

```json
{
  // ...
  "scarfSettings": {
    "enabled": false
  }
  // ...
}
```

--------------------------------

### Restrict Number of Properties in OpenAPI Schema

Source: https://swagger.io/docs/specification/data-models/data-types

Use `minProperties` and `maxProperties` to enforce a minimum or maximum number of properties in an object. This is particularly useful for free-form objects or when specific property counts are required.

```yaml
type: object
minProperties: 2
maxProperties: 10
```

--------------------------------

### Swagger Codegen 2.X Maven Dependency

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/versioning

This snippet shows the Maven dependency configuration for integrating Swagger Codegen version 2.X into a project. It specifies the group ID, artifact ID, and version required for the swagger-codegen-maven-plugin.

```xml
<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-codegen-maven-plugin</artifactId>
    <version>2.4.46</version>
</dependency>
```

--------------------------------

### Apply Scopes to API Operations (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

Applies defined OAuth scopes to specific API operations. This is achieved by listing the security scheme name and the required scopes within the `security` section of an operation.

```yaml
paths:
  /pets/{petId}:
    patch:
      summary: Updates a pet in the store
      security:
        - oAuthSample: [write_pets]
      ...

```

--------------------------------

### Handling 401 Unauthorized Response

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Defines a reusable 401 Unauthorized response for API operations that require authentication but receive an invalid or missing token.

```APIDOC
## Handling 401 Unauthorized Response

### Description
Defines a standard 401 "Unauthorized" response that can be referenced by multiple operations. This response is returned when a request lacks a proper bearer token.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
components:
  responses:
    UnauthorizedError:
      description: Access token is missing or invalid

paths:
  /something:
    get:
      responses:
        '401':
          $ref: '#/components/responses/UnauthorizedError'
```
```

--------------------------------

### OpenAPI 3.0 Global Cookie Authentication

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

Applies cookie authentication globally to all operations in an OpenAPI 3.0 specification. This is done by defining the 'security' key at the root level.

```yaml
security:
  - cookieAuth: []
```

--------------------------------

### Client Credentials Flow - OpenAPI Security Scheme

Source: https://swagger.io/docs/specification/authentication/oauth2

Defines the OAuth 2.0 Client Credentials flow for machine-to-machine authentication within an OpenAPI security scheme. It specifies the token URL, and notes that Getty Images API does not utilize scopes for this flow. This flow is ideal for non-interactive clients.

```yaml
components:
  securitySchemes:
    oAuth2ClientCredentials:
      type: oauth2
      description: See http://developers.gettyimages.com/api/docs/v3/oauth2.html
      flows:
        clientCredentials:
          tokenUrl: https://api.gettyimages.com/oauth2/token/
          scopes: {} # Getty Images does not use scopes
```

--------------------------------

### Define Custom Headers for Multipart Request Part (OpenAPI YAML)

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

This OpenAPI YAML snippet demonstrates how to define custom headers for a specific part ('profileImage') of a multipart request. It specifies the content type and includes a custom header 'X-Custom-Header' with its description and schema.

```yaml
requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          id:
            type: string
            format: uuid
          profileImage:
            type: string
            format: binary
      encoding:
        profileImage: # Property name
          contentType: image/png, image/jpeg
          headers: # Custom headers
            X-Custom-Header:
              description: This is a custom header
              schema:
                type: string
```

--------------------------------

### Override Selector Behavior with Wrap-Selectors (JavaScript)

Source: https://swagger.io/docs/open-source-tools/swagger-ui/customization/plugin-api

Wrap-Selectors allow overriding selector behavior. They are function factories that take the original selector and the system as arguments, returning a new selector. This is useful for controlling data flow into components, such as disabling selectors based on API definition versions.

```javascript
import { createSelector } from 'reselect'

const MySpecPlugin = function(system) {
  return {
    statePlugins: {
      spec: {
        selectors: {
          url: createSelector(
            state => state.get("url")
          )
        }
      }
    }
  }
}

const MyWrapSelectorsPlugin = function(system) {
  return {
    statePlugins: {
      spec: {
        wrapSelectors: {
          url: (oriSelector, system) => (state, ...args) => {
            console.log('someone asked for the spec url!!! it is', state.get('url'))
            // you can return other values here...
            // but let's just enable the default behavior
            return oriSelector(state, ...args)
          }
        }
      }
    }
  }
}
```

--------------------------------

### Define API Without Scopes (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

Configures an OAuth 2.0 security scheme when no scopes are used. This involves defining an empty object for `scopes` in the security scheme and an empty list for scopes in the `security` section.

```yaml
components:
  securitySchemes:
    oAuthNoScopes:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://api.example.com/oauth2/authorize
          scopes: {} # <-----

security:
  - oAuthNoScopes: [] # <-----

```

--------------------------------

### XML Representation of Wrapped Array

Source: https://swagger.io/docs/specification/data-models/representing-xml

This snippet shows the XML output when array wrapping is enabled, resulting in a single parent element containing the array items.

```xml
<books>
  <books>one</books>
  <books>two</books>
  <books>three</books>
</books>
```

--------------------------------

### OpenAPI 3.0 Cookie Authentication Scheme

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

Defines a cookie-based security scheme in OpenAPI 3.0. This involves specifying the type as 'apiKey', the location as 'cookie', and the name of the cookie.

```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    cookieAuth:
      type: apiKey
      in: cookie
      name: JSESSIONID
```

--------------------------------

### Applying Bearer Authentication to Specific Operations

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Applies the Bearer Authentication scheme to individual API operations rather than globally.

```APIDOC
## Applying Bearer Authentication to Specific Operations

### Description
Applies the Bearer Authentication scheme to specific API operations. This allows for more granular control over which endpoints require token authentication.

### Method
N/A (Schema Configuration)

### Endpoint
N/A (Schema Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

```yaml
paths:
  /something:
    get:
      security:
        - bearerAuth: []
```
```

--------------------------------

### Define Read-Only and Write-Only Properties in OpenAPI Schema

Source: https://swagger.io/docs/specification/data-models/data-types

Use `readOnly` and `writeOnly` keywords to control property visibility in requests and responses. `readOnly` properties are included in responses but not requests, while `writeOnly` properties are the opposite. This is useful for managing sensitive data or properties generated by the server.

```yaml
type: object
properties:
  id:
    type: integer
    readOnly: true
  username:
    type: string
  password:
    type: string
    writeOnly: true
```

--------------------------------

### Add Amazon API Gateway Extensions in OpenAPI Spec

Source: https://swagger.io/docs/specification/openapi-extensions

This YAML snippet demonstrates how to add custom extensions for Amazon API Gateway within an OpenAPI specification. It includes extensions for authentication type and authorizer configuration under the `securitySchemes` component.

```yaml
components:
  securitySchemes:
    APIGatewayAuthorizer:
      type: apiKey
      name: Authorization
      in: header
      x-amazon-apigateway-authtype: oauth2
      x-amazon-apigateway-authorizer:
        type: token
        authorizerUri: arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:account-id:function:function-name/invocations
        authorizerCredentials: arn:aws:iam::account-id:role
        identityValidationExpression: "^x-[a-z]+"
        authorizerResultTtlInSeconds: 60
```

--------------------------------

### Invalid $ref Usage in OpenAPI Specification

Source: https://swagger.io/docs/specification/using-ref

Highlights incorrect placements of the $ref keyword within an OpenAPI 3.0 specification, such as directly under 'info' or 'paths'. The $ref can only be used where the specification explicitly allows it.

```yaml
openapi: 3.0.4

# Incorrect!
info:
  $ref: info.yaml
paths:
  $ref: paths.yaml
```

--------------------------------

### Bearer Authentication Scheme

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Defines the Bearer Authentication security scheme in OpenAPI 3.0, specifying the type, scheme, and optional bearer format.

```APIDOC
## Bearer Authentication Scheme

### Description
Defines the Bearer Authentication security scheme in OpenAPI 3.0. This scheme uses HTTP bearer tokens for authentication.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
```

--------------------------------

### OpenAPI String Length Constraints

Source: https://swagger.io/docs/specification/data-models/data-types

Defines a string data type with constraints on its minimum and maximum length. This ensures that the string falls within a specified character count.

```yaml
type: string
minLength: 3
maxLength: 20
```

--------------------------------

### Swagger/OpenAPI $ref with Ignored Siblings (YAML)

Source: https://swagger.io/docs/specification/using-ref

This YAML snippet illustrates how sibling properties ('description', 'default') to a '$ref' in an OpenAPI schema are ignored. The '$ref' effectively replaces the entire schema definition with the content of the referenced schema.

```yaml
components:
  schemas:
    Date:
      type: string
      format: date

    DateWithExample:
      $ref: "#/components/schemas/Date"
      description: Date schema extended with a `default` value... Or not?
      default: 2000-01-01
```

--------------------------------

### OpenAPI Discriminator Property Requirement

Source: https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism

Highlights the requirement for schemas used with a `discriminator` to include the specified discriminator property. This ensures that API consumers, such as code generation tools, can correctly identify and typecast data. Both `simpleObject` and `complexObject` must have the `objectType` property.

```yaml
schemas:
    simpleObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
    complexObject:
      type: object
      required:
        - objectType
      properties:
        objectType:
          type: string
      ...
```

--------------------------------

### Swagger Codegen 3.X Maven Dependency

Source: https://swagger.io/docs/open-source-tools/swagger-codegen/codegen-v3/versioning

This snippet provides the Maven dependency configuration for Swagger Codegen version 3.X. It includes the specific group ID 'io.swagger.codegen.v3', artifact ID, and version for the swagger-codegen-maven-plugin.

```xml
<dependency>
    <groupId>io.swagger.codegen.v3</groupId>
    <artifactId>swagger-codegen-maven-plugin</artifactId>
    <version>3.0.71</version>
</dependency>
```

--------------------------------

### OpenAPI 3.0 Operation-Level Cookie Authentication

Source: https://swagger.io/docs/specification/authentication/cookie-authentication

Applies cookie authentication to a specific operation in an OpenAPI 3.0 specification. This is achieved by defining the 'security' key within the operation object.

```yaml
paths:
  /users:
    get:
      security:
        - cookieAuth: []
      description: Returns a list of users.
      responses:
        "200":
          description: OK
```

--------------------------------

### OpenAPI 3.0 Form Data Schema

Source: https://swagger.io/docs/specification/describing-request-body/describing-request-body

Defines form data using an OpenAPI 3.0 schema with `type: object`. Properties within the schema correspond to the form fields, specifying their types and required status.

```yaml
paths:
  /survey:
    post:
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                name: # <!--- form field name
                  type: string
                fav_number: # <!--- form field name
                  type: integer
              required:
                - name
                - email
```

--------------------------------

### Global Application of Bearer Authentication in OpenAPI

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Applies the defined 'bearerAuth' security scheme globally to all operations in the OpenAPI specification. This ensures all API endpoints require a valid bearer token.

```yaml
security:
  - bearerAuth: []
```

--------------------------------

### OpenAPI 3: Define Multipart Request Body

Source: https://swagger.io/docs/specification/describing-request-body/multipart-requests

Defines a multipart request body in OpenAPI 3, specifying different parts including a string, a JSON object, and a binary file. This structure is commonly used for file uploads.

```yaml
requestBody:
  content:
    multipart/form-data: # Media type
      schema: # Request payload
        type: object
        properties: # Request parts
          id: # Part 1 (string value)
            type: string
            format: uuid
          address: # Part2 (object)
            type: object
            properties:
              street:
                type: string
              city:
                type: string
          profileImage: # Part 3 (an image)
            type: string
            format: binary
```

--------------------------------

### OpenAPI Incorrect Mixed Type Definition

Source: https://swagger.io/docs/specification/data-models/data-types

Demonstrates an invalid way to define mixed types in OpenAPI using a list for the 'type' keyword. This approach is not supported and will result in an error.

```yaml
type:
  - string
  - integer
```

--------------------------------

### OpenAPI Integer Range Definition

Source: https://swagger.io/docs/specification/data-models/data-types

Defines an integer data type with a specified minimum and maximum value, inclusive of the boundaries. This is useful for setting constraints on numerical data.

```yaml
type: integer
minimum: 1
maximum: 20
```

--------------------------------

### Define Free-Form Objects in OpenAPI Schema

Source: https://swagger.io/docs/specification/data-models/data-types

A free-form object allows for arbitrary property-value pairs. This is achieved by setting `type: object` with `additionalProperties: true`, `additionalProperties: {}`, or simply `type: object`.

```yaml
type: object
```

```yaml
type: object
additionalProperties: true
```

```yaml
type: object
additionalProperties: {}
```

--------------------------------

### Enforce Unique Array Items

Source: https://swagger.io/docs/specification/data-models/data-types

Ensures that all items within an array are unique by setting `uniqueItems: true`. Duplicate values are not permitted in the array.

```yaml
type: array
items:
  type: integer
uniqueItems: true
```

--------------------------------

### OpenAPI 3.0 Bearer Authentication Scheme

Source: https://swagger.io/docs/specification/authentication/bearer-authentication

Defines a Bearer authentication security scheme in OpenAPI 3.0. It specifies the type as 'http' and the scheme as 'bearer', with an optional 'bearerFormat' for documentation.

```yaml
openapi: 3.0.4
---
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

--------------------------------

### CORS Error Message in Browser Console

Source: https://swagger.io/docs/open-source-tools/swagger-ui/usage/cors

This snippet shows a typical error message observed in a browser's developer console when CORS is not enabled for a requested resource. It indicates the absence of the 'Access-Control-Allow-Origin' header, preventing cross-origin access.

```text
XMLHttpRequest cannot load http://sad.server.com/v2/api-docs. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'null' is therefore not allowed access.
```

--------------------------------

### Define Required Object Properties

Source: https://swagger.io/docs/specification/data-models/data-types

Specifies which properties of an object are mandatory using the `required` array. Properties not listed are considered optional. The `required` keyword is an object-level attribute.

```yaml
type: object
properties:
  id:
    type: integer
  username:
    type: string
  name:
    type: string
required:
  - id
  - username
```

--------------------------------

### Define OAuth Scopes in OpenAPI 3.0 (YAML)

Source: https://swagger.io/docs/specification/authentication/oauth2

Defines OAuth 2.0 security schemes with scopes for API access control. This is done in the `components/securitySchemes` section, specifying the flow type (e.g., `implicit`) and the available scopes with descriptions.

```yaml
components:
  securitySchemes:
    oAuthSample:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://api.example.com/oauth2/authorize
          scopes:
            read_pets: read pets in your account
            write_pets: modify pets in your account
```

--------------------------------

### Multiple OAuth 2.0 Flows - OpenAPI Security Scheme

Source: https://swagger.io/docs/specification/authentication/oauth2

Defines an OpenAPI security scheme that supports multiple OAuth 2.0 flows, including implicit and resource owner password flows. This allows clients to choose the most appropriate authentication method. It specifies authorization and token URLs along with their respective scopes.

```yaml
components:
  securitySchemes:
    oAuth2:
      type: oauth2
      description: For more information, see https://developers.getbase.com/docs/rest/articles/oauth2/requests
      flows:
        implicit:
          authorizationUrl: https://api.getbase.com/oauth2/authorize
          scopes:
            read: Grant read-only access to all your data except for the account and user info
            write: Grant write-only access to all your data except for the account and user info
            profile: Grant read-only access to the account and user info only
        password:
          tokenUrl: https://api.gettyimages.com/oauth2/token/
          scopes:
            read: Grant read-only access to all your data except for the account and user info
            write: Grant write-only access to all your data except for the account and user info
            profile: Grant read-only access to the account and user info only
```

--------------------------------

### Define Boolean Type

Source: https://swagger.io/docs/specification/data-models/data-types

Specifies a boolean type, accepting only `true` or `false`. Other truthy or falsy values like "true", 0, or `null` are not considered valid boolean types.

```yaml
type: boolean
```

--------------------------------

### Define Array of Referenced Types with oneOf

Source: https://swagger.io/docs/specification/data-models/data-types

Defines a mixed-type array where the possible item types are specified using `$ref` within a `oneOf` construct. This allows for arrays containing objects defined elsewhere.

```yaml
type: array
items:
  oneOf:
    - $ref: "#/components/schemas/Cat"
    - $ref: "#/components/schemas/Dog"
```

--------------------------------

### Define Nested Objects in OpenAPI Schema

Source: https://swagger.io/docs/specification/data-models/data-types

Objects can contain nested objects directly within their properties. For better organization and reusability, nested objects can be defined as separate schemas and referenced using `$ref`.

```yaml
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
        contact_info:
          type: object
          properties:
            email:
              type: string
              format: email
            phone:
              type: string
```

```yaml
components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
        contact_info:
          $ref: "#/components/schemas/ContactInfo"
    ContactInfo:
      type: object
      properties:
        email:
          type: string
          format: email
        phone:
          type: string
```

--------------------------------

### Resource Owner Password Flow - OpenAPI Security Scheme

Source: https://swagger.io/docs/specification/authentication/oauth2

Defines the OAuth 2.0 Resource Owner Password Credentials flow within an OpenAPI security scheme. It specifies the token URL and available scopes for authentication. This flow is suitable when the client application can securely obtain the user's username and password.

```yaml
components:
  securitySchemes:
    oAuth2Password:
      type: oauth2
      description: See https://developers.getbase.com/docs/rest/articles/oauth2/requests
      flows:
        password:
          tokenUrl: https://api.getbase.com/oauth2/token
          scopes:
            read: Grant read-only access to all your data except for the account and user info
            write: Grant write-only access to all your data except for the account and user info
            profile: Grant read-only access to the account and user info only
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.
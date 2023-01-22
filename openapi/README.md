# OpenAPI

- [OpenAPI](#openapi)
  - [OpenAPI Document](#openapi-document)
  - [API Endpoints](#api-endpoints)
    - [Path Item Object](#path-item-object)
    - [Operation Object](#operation-object)
    - [Responses Object](#responses-object)
    - [Response Object](#response-object)
  - [Content of Message Bodies](#content-of-message-bodies)
    - [```content``` Field](#content-field)
  - [Parameters and Payload of an Operation](#parameters-and-payload-of-an-operation)
    - [Parameter Object](#parameter-object)
    - [Location](#location)
    - [Parameter Type](#parameter-type)
    - [Parameter Serialization Control](#parameter-serialization-control)
      - [Primitive Types](#primitive-types)
      - [Array Types](#array-types)
      - [Object Types](#object-types)
  - [Request Bodsy Object](#request-bodsy-object)

```yaml
# OpenAPI Object
openapi: 3.1.0
info: 
  title: Tic Tac Toe
  description: |
    This API allows writing down marks on a Tic Tac Toe board
    and requesting the state of the board or of individual squares.
  version: 1.0.0
paths:
  # Whole board Operations
  /board:
    get:
      summary: Get the whole board
      description: Retrieves the current state of the board and the winner.
      responses:
        "200":
          description: "OK"
          content:
            application/json:
              schema:
                type: object
                properties:
                    winner:
                      type: string
                      enum: [".", "X", "O"]
                      description: |
                        Winner of the game. `.` means nobody has won yet.
                    board:
                      type: array
                      maxItems: 3
                      minItems: 3
                      items: 
                        type: array
                        minItems: 3
                        maxItems: 3
                        items:
                          type: string
                          enum: [".", "X", "O"]
                          description: |
                            Possible values for a board square.
                            `.` means empty square.
...
```

## OpenAPI Document

OpenAPI document describes an HTTP-like API in one or more machine-readable files.

- commonly called ```openapi.json``` or ```openapi.yaml```
- An object (also called a Map) is a collection of name-value pairs 
- The names (also called Keys or Field) are unique within the object
- The names can support numbers, strings, boolean, null, arras and objects.

```json
{
    "anObject": {
        "aNumber": 52,
        "aString": "this is a string",
        "aBoolean": true,
        "nothing": null,
        "arrayOfNumbers": [
            1,
            2,
            3
        ]
    }
}
```

```yaml
# Anything after a hash sign is a comment
anObject:
  aNumber: 42
  aString: This is a string
  aBoolean: true
  nothing: null
  arrayOfNumbers:
    - 1
    - 2
    - 3
```

An OpenAPI document is a single JSON object containing fields adhering to the structure defined in the OpenAPI Specification.

The root object of any OpenAPI Document is the OpenAPI Object:

- ```openapi``` and ```info``` are mandatory
- at least one of ```paths```,  ```components``` and ```webhooks``` is required

- ```openapi```: (**string**) 
  - Version of the OAS this document is using
  - ej "3.1.0"
- ```info```: (**Info Object**)
  - General information about the API
  - ```title:``` name of the API
  - ```version:``` version of the API document
- ```paths```: (**Paths** **Object**) describes all the **endpoints** of the API, including parameters and all possible server responses

```yaml
openapi: 3.1.0
info:
  title: A minimal OpenAPI document
  version: 0.0.1
paths: {} # No endpoints defined
```

## API Endpoints

```yaml
#OpenAPI Object
openapi:
info:
paths: # Path Object
  /endpoint1: #Path Item Object
  /endpoint2: #Path Item Object
  /endpoint3: #Path Item Object
    get: # Operation Object 
    put: # Operation Object
    post: # Operation Object
    delete: # Operation Object
      summary:
      description:
      requestBody:
      responses: # Responses Object
        code1: # Response Object
        code2: # Responses Object
          description:
          content:
```

- OpenAPI Object
  - openapi
  - info
  - paths (Path Object)
    - /endpoint1..N (Path Item Object)
      - get, put, post, delete (Operation Object)
        - summary
        - description
        - requestBody
        - operationID
        - responses (Responses Object)
          - HTTP code1..N (Response Object)
            - description
            - content

- API Endpoints are called **Paths**
- Every field in the Paths Object is a Path Item Object, describing one API endpoint
  - Use field instead of an Array to enforce endpoint uniqueness at syntax level
- **Paths must start with a forward slash**

```yaml
openapi: 3.1.0
info:
  title: Tic Tac Toe
  description: |
    This API allows writing down marks on a Tic Tac Toe board
    and requesting the state of the board or of individual squares.
  version: 1.0.0
paths:
  /board:
    ...
```

### Path Item Object

- Path Item Object describes HTTP operations that can be performed on a path with a separate Operation Object
- Operations match HTTP methods names like ```get```, ```put``` or ```delete```
- Also accepts common properties for all operations on the path like ```summary``` or ```description```

```yaml
paths:
  /board:
    get: 
      ...
    put:
      ...
```

### Operation Object

- operation's parameters
- payload
- possible server responses

```yaml
paths:
  /board:
    get:
      sumary: Get the Whole Board
      description: Retrieves the current state of the board and the winner.
      parameters:
        ...
      responses:
        ...
```

### Responses Object

- expected answers to the request
- each field is an HTTP response
- **enclosed in quotation marks**
- At least one response must be given

```yaml
  /board
    get:
      responses:
      "200":
        ...
      "404":
        ...
```

### Response Object

- description of the meaning of the response
- Compementing the HTTP response codes

```yaml
  /board
    get:
      responses:
      "200":
        description: Everything went fine.
        content:
          ...
```

## Content of Message Bodies

How 

### ```content``` Field

- Can be found in Response Objects and Request Body Objects.
- Map pairing standard Media Types [RFC6838] with Open Api **```
- Allows to returning/accept content in **diferent formats**
- **Wildcards A are accepted**

```yaml
content:
  # Media Type Objects: describes the structure of the content
  application/json:
    schema: # defines the type and possible values (minimum, maximum, enums, etc)
      type: integer
      minimum: 1
      maximum: 1000
  text/html:
    ...
  text/*:
    ...
```

- ```integer```: accept ```minumum``` and ```maximum``` values
- ```string```: can be limited with ```minLength``` and ```maxLength```
- (No matter the type): a set of options can be specified with ```enum``` array

```yaml
content:
  application/json:
    schema:
      type: string
      enum:
      - Alice
      - Bob
      - Carl
```

- ```array``` must have an ```items``` field, and defines the type for each element of the array.
- The size of the array can be limited with ```minItems``` and ```maxItems```

```yaml
contet:
  application/json:
    schema:
      type: array
      minItems: 1
      maxItems: 10
      items:
        type: integer
```

- Object types must have a ```properties``` field listing the properties of the object.

```yaml
content:
  application/json:
    schema:
      type: object
      properties:
        productName:
          type: string
        productPrice:
          type: number
```

## Parameters and Payload of an Operation

- OpenAPI provides two mechanism to specify **input** data.
  - parameters: typically used to identify a resource
  - request body: provides the content for that resource 

### Parameter Object

- ```parameters``` field in **Path Item** and **Operation Objects** is an **array** containing **Parameter Objects**.
- When provided in Path Item the parameters are **shared by all operations**
- Each parameter Object describes one parameter with the following fields:
  - **mandatory**
    - ```in``` (string): Location of the parameter
    - ```name``` (string): Must be unique in each location 
  - **additional**
    - ```description``` (string): for documentation
    - ```required``` (boolean): Whether this parameter must be present or not. By default is false

### Location

- path
- query
- header
  
```in: path```: The parameter is part of the route of this operation. The parameter's name **must** appear in the path as a template expression

```yaml
paths:
  /users/{id}:
    get:
      parameters:
      - name: id
        in: path
        required: true
```

```in: query```: Appended to the **query string** part of the operation's URL

```yaml
# For example URL "/users?id=1234"
paths:
  /users:
    get:
      parameters:
      - name: id
        in: query
```

- ```in: header```: Parameter is sent in a custom HTTP header as part of the request. Case-insensitive.

### Parameter Type

```yaml
parameters:
- name: id
  in: query
  schema:
    type: integer
    minimum: 1
    maximum: 100
```

For Media Type Objects single-entry map in more advanced scenarios the ```content``` field can be used instead of ```schema```. They cannot appear at the same time.

### Parameter Serialization Control

```style``` field defines how a parameter is to be serialized and its effect depends on the **type** of the parameter.

#### Primitive Types

Example: integer named **```id```** with **value** *```1234```*

| style | ```simple``` | ```form``` | ```label``` | ```matrix``` |
| --- | --- | --- | --- | --- |
| | ```1234``` | ```id=1234``` | ```.1234```| ```;id=1234``` |


#### Array Types

Example: array named ```ids``` containing the integeres 1, 2 and 3 

| style | ```simple``` | ```form``` | ```label``` | ```matrix``` |
| --- | --- | --- | --- | --- |
| ```explode=false```| ```1,2,3```| ```ids=1,2,3```|```.1.2.3``` | ```;ids=1,2,3``` |
| ```explode=true```| ```1,2,3```| ```ids=1&ids=2&ids=3```| ```.1.2.3```| ```;ids=1;ids=2;ids=3```|

#### Object Types

Example: object named ```color``` containing integer fields R, G and B with values 1, 2 and 3.

| style| ```simple``` | ```form``` | ```label``` | ```matrix``` |
| --- | --- | --- | --- | --- |
| ```explode=false```| ```R,1,G,2,B,3```|```color=R,1,G,2,B,3``` | ```.R.1.G.2.B.3```| ```;ids=1;ids=2;ids=3```|
|```explode=true``` | ```R=1,G=2,B=3```| ```R=1&G=2&B=3```| ```.R=1.G=2.B=3```| ```;R=1;G=2;B=3``` |

## Request Bodsy Object

>  **UPDATING A DATABASE RECORD**
>  - Parameters: identify the record
>  - Body: provides new content

```yaml
# operation with a JSONJ request body 
# containing a single integer with values between 1 and 100

paths:
  /board:
    put: 
      requestBody:
        content:
          application/json:
            schema: 
              type: integer
              minimum: 1
              maximum: 100
```
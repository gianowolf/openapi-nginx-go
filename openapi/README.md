# OpenAPI


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
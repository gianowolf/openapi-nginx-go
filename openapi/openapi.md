# OpenAPI

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

Endpoints (also called Operations or Routes) are called **Paths** in the OAS. the **Paths Object** is accessible ghrough the **paths** field in the root **OpenAPI Object**

Every field in the **Paths Object** is a **Path Item Object** describing one API endpint.

Paths **must start with a forward slash**.

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
  ...
```



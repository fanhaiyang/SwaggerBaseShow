# SwaggerBaseShow
Basic Swagger Example

复制以下swagger json示例代码,粘贴进 swagger edit 在线编辑器

在 https://swagger.io/tools/swagger-editor/download/ 下安装swagger编辑工具

```js
swagger: "2.0"
info:
  description: "This is a sample server Petstore server.  "
  version: "1.0.0"
  title: "Swagger Petstore"
  termsOfService: "http://swagger.io/terms/"
host: "petstore.swagger.io"
basePath: "/v2"

schemes:
- "http"


# 方法接口声明
tags:
- name: "pet"
  description: "Everything about your Pets"

# 具体方法实现
paths:
  /pet:
  
    post:
      tags:
      - "pet"
      summary: "Add a new pet to the store"
      description: ""
      operationId: "addPet"
      consumes:
      - "application/json"
      - "application/xml"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        description: "Pet object that needs to be added to the store"
        required: true
        schema:
          $ref: "#/definitions/Pet"
      responses:
        405:
          description: "Invalid input"

    put:
      tags:
      - "pet"
      summary: "Update an existing pet"
      description: ""
      operationId: "updatePet"
      consumes:
      - "application/json"
      - "application/xml"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - in: "body"
        name: "body"
        description: "Pet object that needs to be added to the store"
        required: true
        schema:
          $ref: "#/definitions/Pet"
      responses:
        400:
          description: "Invalid ID supplied"
        404:
          description: "Pet not found"
        405:
          description: "Validation exception"
          

  /pet/findByStatus:
    get:
      tags:
      - "pet"
      summary: "Finds Pets by status"
      description: "Multiple status values can be provided with comma separated strings"
      operationId: "findPetsByStatus"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - name: "status"
        in: "query"
        description: "Status values that need to be considered for filter"
        required: true
        type: "array"
        items:
          type: "string"
          enum:
          - "available"
          - "pending"
          - "sold"
          default: "available"
        collectionFormat: "multi"
      responses:
        200:
          description: "successful operation"
          schema:
            type: "array"
            items:
              $ref: "#/definitions/Pet"
        400:
          description: "Invalid status value"


  /pet/{petId}:
    get:
      tags:
      - "pet"
      summary: "Find pet by ID"
      description: "Returns a single pet"
      operationId: "getPetById"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - name: "petId"
        in: "path"
        description: "ID of pet to return"
        required: true
        type: "integer"
        format: "int64"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/Pet"
        400:
          description: "Invalid ID supplied"
        404:
          description: "Pet not found"


    post:
      tags:
      - "pet"
      summary: "Updates a pet in the store with form data"
      description: ""
      operationId: "updatePetWithForm"
      consumes:
      - "application/x-www-form-urlencoded"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - name: "petId"
        in: "path"
        description: "ID of pet that needs to be updated"
        required: true
        type: "integer"
        format: "int64"
      - name: "name"
        in: "formData"
        description: "Updated name of the pet"
        required: false
        type: "string"
      - name: "status"
        in: "formData"
        description: "Updated status of the pet"
        required: false
        type: "string"
      responses:
        405:
          description: "Invalid input"


    delete:
      tags:
      - "pet"
      summary: "Deletes a pet"
      description: ""
      operationId: "deletePet"
      produces:
      - "application/xml"
      - "application/json"
      parameters:
      - name: "api_key"
        in: "header"
        required: false
        type: "string"
      - name: "petId"
        in: "path"
        description: "Pet id to delete"
        required: true
        type: "integer"
        format: "int64"
      responses:
        400:
          description: "Invalid ID supplied"
        404:
          description: "Pet not found"


  /pet/{petId}/uploadImage:
    post:
      tags:
      - "pet"
      summary: "uploads an image"
      description: ""
      operationId: "uploadFile"
      consumes:
      - "multipart/form-data"
      produces:
      - "application/json"
      parameters:
      - name: "petId"
        in: "path"
        description: "ID of pet to update"
        required: true
        type: "integer"
        format: "int64"
      - name: "additionalMetadata"
        in: "formData"
        description: "Additional data to pass to server"
        required: false
        type: "string"
      - name: "file"
        in: "formData"
        description: "file to upload"
        required: false
        type: "file"
      responses:
        200:
          description: "successful operation"
          schema:
            $ref: "#/definitions/ApiResponse"
            
  
# Modle开始
definitions:

  Category:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int64"
      name:
        type: "string"
    xml:
      name: "Category"
  
  Tag:
    type: "object"
    properties:
      id:
        type: "integer"
        format: "int64"
      name:
        type: "string"
    xml:
      name: "Tag"
      
  Pet:
    type: "object"
    required:
    - "name"
    - "photoUrls"
    properties:
      id:
        type: "integer"
        format: "int64"
      category:
        $ref: "#/definitions/Category"
      name:
        type: "string"
        example: "doggie"
      photoUrls:
        type: "array"
        xml:
          name: "photoUrl"
          wrapped: true
        items:
          type: "string"
      tags:
        type: "array"
        xml:
          name: "tag"
          wrapped: true
        items:
          $ref: "#/definitions/Tag"
      status:
        type: "string"
        description: "pet status in the store"
        enum:
        - "available"
        - "pending"
        - "sold"
    xml:
      name: "Pet"
      
  ApiResponse:
    type: "object"
    properties:
      code:
        type: "integer"
        format: "int32"
      type:
        type: "string"
      message:
        type: "string"

 ```

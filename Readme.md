# Solución 💪

En nuestro navegador nos dirigimos a la página de swagger editor, a través de este link 👉 [**Swagger Editor**](https://editor.swagger.io/) 👈

Y por defecto nos da una plantilla de cómo se vería nuestra documentación api

![image](https://github.com/Splinnk/Solucion-Swagger/assets/114356147/c8bd9df2-7a96-454a-a125-18f476d8b96e)
 

Comenzamos borrado la plantilla por defecto

![image](https://github.com/Splinnk/Solucion-Swagger/assets/114356147/3b9eb8ef-240e-4738-bc8c-37336fe20605)

# Ahora habrá un ejemplo de las propiedades básicas en los métodos HTTP
## **Información General** ☝️

### **openapi: 3.0.0**: 
Es esencial y debe incluirse al comienzo de tu documento OpenAPI. Esta línea indica la versión de la especificación OpenAPI que estás utilizando, en este caso, la versión 3.0.0

### **info**: 
En esta sección se proporciona información general sobre nuestro API:

### **title**: 
Es el título de tu API (Estudiantes API en este caso), que describe brevemente qué hace nuestro API.

### **version**: 
Indica la versión actual de tu API (1.0.0 en este caso). Esto ayuda a gestionar cambios y versiones de tu API de manera controlada.

### **description**: 
Proporciona una descripción más detallada de nuestro  API (API para gestionar estudiantes), explicando su propósito y funcionalidad principal.

![image](https://github.com/Splinnk/Solucion-Swagger/assets/114356147/d39e5601-7784-4810-80f3-0a12accc411d)


## **Servidores** 📃

En la sección **servers**  se define el servidor base de donde se encuentra alojado la API, en este caso pegamos el url de nuestro api.

![image](https://github.com/Splinnk/Solucion-Swagger/assets/114356147/31224f52-ac15-4718-a1a8-5d04f9abd40b)


## **Paths** 🚶

### **Método Get**

Los endpoints de la API se definen en la sección paths. Aquí, se define una serie de operaciones CRUD (Crear, Leer, Actualizar, Eliminar) para la entidad "estudiante".

### **paths**: 
Define los endpoints (rutas) disponibles en nuestra  API. En este caso, /estudiantes es el endpoint que se está describiendo.

/estudiantes: Especifica el path para las operaciones relacionadas con los estudiantes.

### **get**: 
Indica que esta es una operación HTTP GET para obtener recursos.

### **tags**: 
Asocia esta operación al tag Estudiantes, que ayuda a organizar y categorizar las operaciones en grupos lógicos.

### **summary**: 
Proporciona un resumen breve de la operación (Obtener todos los estudiantes). Es una descripción concisa de lo que hace esta operación.

### **description**: 
Ofrece una descripción más detallada de lo que hace la operación GET (Devuelve una lista de todos los estudiantes). Esto es útil para proporcionar contexto adicional sobre el propósito de la operación.

### **responses**: 
Define las respuestas posibles que puede devolver esta operación GET:

### **'200'**: 
Indica una respuesta exitosa con código de estado HTTP 200.

### **description**: 
Descripción de la respuesta (Lista de estudiantes). Es un mensaje breve que indica qué se espera recibir en la respuesta.

### **content**: 
Especifica el tipo de contenido que se enviará en la respuesta.

### **application/json**: 
Indica que el cuerpo de la respuesta está en formato JSON, que es común en las APIs RESTful.

### **schema**: 
Define el esquema del cuerpo de la respuesta.

### **type**: array: 
Indica que se espera un array (arreglo) de elementos en la respuesta.

### **items**: 
Describe los elementos individuales del array.

### **$ref: '#/components/schemas/Estudiante'**: 
Hace referencia al esquema definido en components/schemas/Estudiante. Esto significa que cada elemento del array en la respuesta será un objeto con las propiedades definidas en el esquema Estudiante.

### **'500'**: 
Define una respuesta para un error interno del servidor.

### **description**: 
Descripción de la respuesta de error (Error interno del servidor). Indica que si ocurre un problema interno en el servidor al procesar la solicitud, se devolverá esta respuesta.

![image](https://github.com/Splinnk/Solucion-Swagger/assets/114356147/d5a744e5-b790-413f-a97a-50866635a032)

Se repiten los mismos campos en los otros cuatro métodos con los que cuenta nuestra API y aquí podemos ver el código YAML que nos brinda la documentación:

````yaml
openapi: 3.0.0
info:
  title: Estudiantes API
  version: 1.0.0
  description: API para gestionar estudiantes
  
servers:
  - url: http://localhost:8080/quinto/api.php
  
tags:
  - name: Estudiantes
    description: Operaciones CRUD para estudiantes

paths:
  /estudiantes:
    get:
      tags:
        - Estudiantes
      summary: Obtener todos los estudiantes
      description: Devuelve una lista de todos los estudiantes
      responses:
        '200':
          description: Lista de estudiantes
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Estudiante'
        '500':
          description: Error interno del servidor


    post:
      tags:
        - Estudiantes
      summary: Crear un nuevo estudiante
      description: Crea un nuevo estudiante con los datos proporcionados
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Estudiante'
      responses:
        '201':
          description: Estudiante creado exitosamente
        '400':
          description: Solicitud incorrecta
        '500':
          description: Error interno del servidor
  /estudiantes/{cedula}:
  
    delete:
      tags:
        - Estudiantes
      summary: Eliminar un estudiante
      description: Elimina un estudiante por su cédula
      parameters:
        - name: cedula
          in: path
          required: true
          description: Cédula del estudiante a eliminar
          schema:
            type: string
      responses:
        '200':
          description: Estudiante eliminado exitosamente
        '400':
          description: Solicitud incorrecta
        '404':
          description: Estudiante no encontrado
        '500':
          description: Error interno del servidor

    put:
      tags:
        - Estudiantes
      summary: Actualizar un estudiante
      description: Actualiza los datos de un estudiante existente
      parameters:
        - name: cedula
          in: path
          required: true
          description: Cédula del estudiante a actualizar
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Estudiante'
      responses:
        '200':
          description: Estudiante actualizado exitosamente
        '400':
          description: Solicitud incorrecta
        '404':
          description: Estudiante no encontrado
        '500':
          description: Error interno del servidor

components:
  schemas:
    Estudiante:
      type: object
      required:
        - cedula
        - nombre
        - apellido
        - direccion
        - telefono
      properties:
        cedula:
          type: string
          description: Cédula del estudiante
        nombre:
          type: string
          description: Nombre del estudiante
        apellido:
          type: string
          description: Apellido del estudiante
        direccion:
          type: string
          description: Dirección del estudiante
        telefono:
          type: string
          description: Teléfono del estudiante
````

Si desean ver nuestro código publicado pueden acceder a: 👉 [**API Estudiante**](https://app.swaggerhub.com/apis/INTELIGENCIAARTIFICI/estudiantes-api/1.0.0) 👈



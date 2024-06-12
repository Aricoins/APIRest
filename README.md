# 🌐 **WeCode API Documentation** 🌐

## 📂 CRUD de Usuarios

### ➕ Crea un nuevo usuario
**POST: /api/v1/users** (automáticamente vía **Clerk**)

**Objeto Usuario**:
```json
{
    "id": "type int not null (serializado)",
    "username": "type string unique",
    "email": "type string unique not null",
    "first_name": "type string max 100",
    "last_name": "type string max 100",
    "imageUrl": "type string not null",
    "skills": "type string max 500",
    "description": "type string max 500",
    "created_at": "type timestamp default current",
    "updated_at": "type timestamp default current",
    "onboarding_state": "type boolean default false"
}
```
**Response**: Objeto **Usuario** creado. ✅

### 🔄 Devuelve todos los usuarios
**GET: /api/v1/users**

### 🔍 Devuelve un usuario por su ID
**GET: /api/v1/users/:id**

### ✏️ Actualiza un usuario por su ID
**PUT: /api/v1/users/update/:id**

**Campos actualizables**:
```json
{
    "username",
    "first_name",
    "last_name",
    "skills",
    "description",
    "onboarding_state",
    "imageUrl"
}
```
**Response**: Objeto **Usuario** actualizado. ✅

### 🗑️ Elimina un usuario por su ID
**DELETE: /api/v1/users/delete/:id**

## 📝 CRUD de Posts

### ➕ Publica un nuevo contenido
**POST: /api/v1/posts**

**Objeto Post**:
```json
{
    "id": "type int not null (serializado)",
    "title": "type string max 100 not null",
    "content": "type string not null",
    "userId": "type string not null (referenciado)",
    "imageUrl": "type string max 255",
    "tags": "type string max 255 (tags separados por ',')",
    "created_at": "type timestamp default current",
    "updated_at": "type timestamp default current"
}
```
**Response**: Objeto **Post** creado. ✅

### 🔄 Devuelve todos los posts
**GET: /api/v1/posts?limit=10&offset=0**

**Response**: Array de objetos **Posts** opcionalmente paginados del más reciente al más antiguo. 📄

### 🔍 Devuelve los posts por id del usuario
**GET: /api/v1/posts/user/:id?limit=10&offset=0**

**Response**: Array con objetos **Posts** de un usuario, opcionalmente paginados del más reciente al más antiguo. 📄

### 🔍 Devuelve los posts por un tag en específico
**GET: /api/v1/posts/tag/:tag?limit=10&offset=0**

**Response**: Array de objetos **Posts** con un tag, opcionalmente paginados del más reciente al más antiguo. 📄

### 🔍 Devuelve un post por su id
**GET: /api/v1/posts/:id**

### 🔍 Devuelve los posts mediante búsqueda incremental
**GET: /api/v1/posts/search/:searchParam**

### ✏️ Actualiza un post por su id
**PUT: /api/v1/posts/update/:id**

**Campos actualizables**:
```json
{
    "title",
    "content",
    "imageUrl",
    "tags"
}
```
**Response**: Objeto **Post** actualizado. ✅

### 🗑️ Elimina un post por su id
**DELETE: /api/v1/posts/delete/:id**

### 📊 Devuelve los tags ordenados por la cantidad de post creados con ese tag (opcionalmente con un límite de cantidad)
**GET: /api/v1/tags?limit=10**

**Response**: Array de objetos **Tags** ordenados por la cantidad de posts creados con cada tag, opcionalmente limitados en cantidad. 🔖

## 💬 CRUD de Comentarios

### ➕ Publica un nuevo comentario en un post específico
**POST: /api/v1/comments/:postId**

**Objeto Comentario**:
```json
{
    "id": "type int not null (serializado)",
    "content": "type string not null",
    "userId": "type string not null (referenciado)",
    "postId": "type int not null (referenciado)",
    "created_at": "type timestamp default current",
    "updated_at": "type timestamp default current"
}
```
**Response**: Objeto **Comentario** creado. ✅

### 🔄 Obtiene todos los comentarios de un post específico
**GET: /api/v1/comments/:postId**

### ✏️ Actualiza un comentario por su id
**UPDATE: /api/v1/comments/update/:id**

**Campos actualizables**:
```json
{
    "content"
}
```
**Response**: Objeto **Comentario** actualizado. ✅

### 🗑️ Elimina un comentario por su id
**DELETE: /api/v1/comments/delete/:id**

## 👥 CRUD de Seguidores

#### Seguir a un usuario
* **Método:** POST
* **Endpoint:** `/api/v1/followers/follow`
* **Cuerpo de la solicitud:**
```json
{
    "follower_id": "ID del usuario que quiere seguir",
    "followed_id": "ID del usuario a seguir"
}
```
* **Respuesta:** Objeto que contiene la información de seguimiento en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.

#### Dejar de seguir a un usuario
* **Método:** POST
* **Endpoint:** `/api/v1/followers/unfollow`
* **Cuerpo de la solicitud:**
```json
{
    "follower_id": "ID del usuario que quiere dejar de seguir",
    "followed_id": "ID del usuario que se deja de seguir"
}
```
* **Respuesta:** Objeto que contiene la información de dejar de seguir en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.

#### Obtener los seguidores de un usuario
* **Método:** GET
* **Endpoint:** `/api/v1/followers/:id/followers`
* **Parámetro de ruta:**
```json
{
    "id": "ID del usuario"
}
```
* **Respuesta:** Matriz que contiene la información de los seguidores del usuario en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.

#### Obtener a los usuarios que sigue un usuario
* **Método:** GET
* **Endpoint:** `/api/v1/followers/:id/following`
* **Parámetro de ruta:**
```json
{
    "id": "ID del usuario"
}
```
* **Respuesta:** Matriz que contiene los usuarios seguidos por el usuario en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.

#### Obtener las publicaciones de los usuarios seguidos
* **Método:** GET
* **Endpoint:** `/api/v1/followers/:id/followed_posts`
* **Parámetro de ruta:**
```json
{
    "id": "ID del usuario"
}
```
* **Respuesta:** Matriz que contiene las publicaciones de los usuarios seguidos por el usuario en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.

#### Obtener los usuarios más seguidos
* **Método:** GET
* **Endpoint:** `/api/v1/followers/top_followed`
* **Respuesta:** Matriz que contiene información sobre los cinco usuarios más seguidos en caso de éxito. En caso de error, devuelve un código de estado 500 y un mensaje de error.


## 🏷️ CRUD de Tags

### 🔍 Devuelve los tags ordenados por la cantidad de post creados con ese tag (opcionalmente con un limite de cantidad)
**GET: /api/v1/tags?limit=10**

**Response**: Array de objetos **Tags** ordenados por la cantidad de posts creados con cada tag, opcionalmente limitados en cantidad. 🔖

## 🎣 Ruta Clerk Webhooks: /api/v1/webhooks

### 🎉 Webhooks para integración con Clerk

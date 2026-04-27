# biblioteca-api — bautista-post1-u5

Aplicación Spring Boot que implementa el patrón Repository con JPA/Hibernate para gestionar una biblioteca de libros. Incluye un CRUD completo con base de datos H2 embebida, estructurado en las capas Entity, Repository, Service y Controller.

## Tecnologías

- Java 17
- Spring Boot 3.2.5
- Spring Data JPA / Hibernate
- H2 Database (embebida)
- Lombok
- Maven

## Estructura del Proyecto

```
src/main/java/com/universidad/patrones/
├── BibliotecaApiApplication.java
├── model/
│   └── Libro.java
├── repository/
│   └── LibroRepository.java
├── service/
│   └── LibroService.java
└── controller/
    └── LibroController.java
```

## Cómo ejecutar

1. Clona el repositorio:
```bash
git clone https://github.com/bautista/bautista-post1-u5.git
cd bautista-post1-u5
```

2. Configura la variable de entorno JAVA_HOME apuntando a Java 17.

3. Ejecuta la aplicación:
```bash
.\mvnw.cmd spring-boot:run -DskipTests
```

4. La aplicación estará disponible en `http://localhost:8080`

5. La consola H2 estará disponible en `http://localhost:8080/h2-console`
   - JDBC URL: `jdbc:h2:mem:biblioteca_db`
   - Username: `sa`
   - Password: *(vacío)*

## Endpoints REST

| Método | URL | Descripción | Respuesta |
|--------|-----|-------------|-----------|
| GET | `/api/libros` | Listar todos los libros | 200 OK |
| GET | `/api/libros/{id}` | Obtener un libro por ID | 200 OK / 404 Not Found |
| POST | `/api/libros` | Crear un nuevo libro | 201 Created |
| PUT | `/api/libros/{id}` | Actualizar un libro | 200 OK |
| DELETE | `/api/libros/{id}` | Eliminar un libro | 204 No Content / 404 Not Found |
| GET | `/api/libros/buscar?q={palabra}` | Buscar libros por palabra | 200 OK |

## Ejemplo de uso

### Crear un libro (POST)

**Request:**
```json
{
    "titulo": "Clean Code",
    "autor": "Robert C. Martin",
    "isbn": "978-0132350884",
    "anioPublicacion": 2008,
    "categoria": "Ingenieria de Software"
}
```

**Response (201 Created):**
```json
{
    "id": 1,
    "titulo": "Clean Code",
    "autor": "Robert C. Martin",
    "isbn": "978-0132350884",
    "anioPublicacion": 2008,
    "categoria": "Ingenieria de Software"
}
```

### Listar todos los libros (GET)

**Request:** `GET http://localhost:8080/api/libros`

**Response (200 OK):**
```json
[
    {
        "id": 1,
        "titulo": "Clean Code",
        "autor": "Robert C. Martin",
        "isbn": "978-0132350884",
        "anioPublicacion": 2008,
        "categoria": "Ingenieria de Software"
    }
]
```

### Eliminar un libro (DELETE)

**Request:** `DELETE http://localhost:8080/api/libros/1`

**Response:** `204 No Content`

### Buscar por palabra (GET)

**Request:** `GET http://localhost:8080/api/libros/buscar?q=Clean`

**Response (200 OK):**
```json
[
    {
        "id": 1,
        "titulo": "Clean Code",
        "autor": "Robert C. Martin",
        "isbn": "978-0132350884",
        "anioPublicacion": 2008,
        "categoria": "Ingenieria de Software"
    }
]
```

## Dependencias principales

```xml
<dependencies>
    <dependency>spring-boot-starter-web</dependency>
    <dependency>spring-boot-starter-data-jpa</dependency>
    <dependency>spring-boot-starter-validation</dependency>
    <dependency>h2 (runtime)</dependency>
    <dependency>lombok</dependency>
</dependencies>
```

## Autor



Bautista Daniel — Ingeniería de Sistemas, 2026
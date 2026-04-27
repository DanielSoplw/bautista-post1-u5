# biblioteca-api — bautista-post2-u5

Aplicación Spring Boot que implementa una API REST aplicando DTOs para separar el modelo de dominio del contrato público de la API, manejo global de errores con `@ControllerAdvice`, y documentación interactiva con SpringDoc/Swagger UI.

## Tecnologías

- Java 17
- Spring Boot 3.2.5
- Spring Data JPA / Hibernate
- H2 Database (embebida)
- Lombok
- SpringDoc OpenAPI 2.3.0 (Swagger UI)
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
├── dto/
│   ├── LibroRequestDTO.java
│   └── LibroResponseDTO.java
├── mapper/
│   └── LibroMapper.java
├── exception/
│   └── GlobalExceptionHandler.java
└── controller/
    ├── LibroController.java
    └── LibroControllerV2.java
```

## Cómo ejecutar

1. Clona el repositorio:
```bash
git clone https://github.com/DanielSoplw/bautista-post2-u5.git
cd bautista-post2-u5
```

2. Configura Java 17:
```powershell
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-17.0.18.8-hotspot"
$env:PATH = "$env:JAVA_HOME\bin;$env:PATH"
```

3. Ejecuta la aplicación:
```bash
.\mvnw.cmd spring-boot:run -DskipTests
```

4. La aplicación estará disponible en `http://localhost:8080`

5. La consola H2 estará disponible en `http://localhost:8080/h2-console`
   - JDBC URL: `jdbc:h2:mem:biblioteca_db`
   - Username: `sa`
   - Password: *(vacío)*

6. La documentación Swagger UI estará disponible en `http://localhost:8080/swagger-ui.html`

## Endpoints REST v2

| Método | URL | Descripción | Respuesta |
|--------|-----|-------------|-----------|
| GET | `/api/v2/libros` | Listar todos los libros | 200 OK |
| GET | `/api/v2/libros/{id}` | Obtener un libro por ID | 200 OK / 404 Not Found |
| POST | `/api/v2/libros` | Crear un nuevo libro | 201 Created |
| DELETE | `/api/v2/libros/{id}` | Eliminar un libro | 204 No Content |

## Manejo de Errores

| Código | Descripción |
|--------|-------------|
| 400 | ISBN duplicado o datos de entrada inválidos |
| 404 | Libro no encontrado |

## Ejemplos de uso

### Crear un libro (POST) — 201 Created

**Request:**
```json
{
    "titulo": "Refactoring",
    "autor": "Martin Fowler",
    "isbn": "978-0201485677",
    "anioPublicacion": 1999,
    "categoria": "Ingenieria de Software"
}
```

**Response (201 Created):**
```json
{
    "id": 1,
    "titulo": "Refactoring",
    "autor": "Martin Fowler",
    "isbn": "978-0201485677",
    "anioPublicacion": 1999,
    "categoria": "Ingenieria de Software"
}
```

### Obtener libro inexistente (GET) — 404 Not Found

**Request:** `GET http://localhost:8080/api/v2/libros/999`

**Response (404 Not Found):**
```json
{
    "error": "Libro no encontrado: 999"
}
```

### ISBN duplicado (POST) — 400 Bad Request

**Response (400 Bad Request):**
```json
{
    "error": "Ya existe un libro con ISBN: 978-0201485677"
}
```

### Título vacío (POST) — 400 Bad Request

**Response (400 Bad Request):**
```json
{
    "errores": [
        "titulo: El título es obligatorio"
    ]
}
```

## Dependencias principales

```xml
<dependencies>
    <dependency>spring-boot-starter-web</dependency>
    <dependency>spring-boot-starter-data-jpa</dependency>
    <dependency>spring-boot-starter-validation</dependency>
    <dependency>h2 (runtime)</dependency>
    <dependency>lombok</dependency>
    <dependency>springdoc-openapi-starter-webmvc-ui 2.3.0</dependency>
</dependencies>
```

## Autor

Bautista Daniel — Ingeniería de Sistemas, 2026
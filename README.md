# Categories App - Spring Boot + Docker

Este proyecto es una API REST de ejemplo para la gestión de **categorías**, construida con **Spring Boot** y empaquetada en una imagen de Docker.

## Tecnologías usadas

- Java 17
- Spring Boot 3
- Maven
- Docker
- MySQL (conexión externa)
- Docker Hub

---

## Estructura básica del modelo

```java
@Entity
@Table(name = "categories")
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;         // Requerido, único, 3-50 caracteres
    private String description;  // Opcional, hasta 255 caracteres
    private LocalDateTime creationDate; // Asignado automáticamente al crear
}
```

---

## Cómo construir y ejecutar el contenedor

### 1. Clonar este repositorio

```bash
git clone https://github.com/tu_usuario/categories-app.git
cd categories-app
```

### 2. Construir la imagen

```bash
docker build -t img-app-categories:v1 .
```

### 3. Crear una red de Docker (si no existe)

```bash
docker network create test-network
```

### 4. Ejecutar el contenedor

```bash
docker run -dit \
  -p 8082:8004 \
  --name c-app-categories \
  --network test-network \
  -e DB_HOST=test-db \
  -e DB_PORT=3306 \
  -e DB_DATABASE=test \
  -e DB_USER=root \
  -e DB_PASSWORD=admin \
  -e PORT=8004 \
  img-app-categories:v1
```

---

## Endpoints REST disponibles

- `POST /api/categorias` – Crear categoría
- `GET /api/categorias` – Listar todas las categorías
- `GET /api/categorias/{id}` – Obtener categoría por ID
- `PUT /api/categorias/{id}` – Actualizar categoría
- `DELETE /api/categorias/{id}` – Eliminar categoría

---

## Descargar y ejecutar desde otra máquina

1. Asegúrate de tener Docker instalado y correr MySQL con la misma red.
2. Descarga la imagen desde Docker Hub:

```bash
docker pull tu_usuario_dockerhub/img-app-categories:v1
```

3. Corre el contenedor igual que en la sección anterior.

---

## Autor

Luis Sagnay
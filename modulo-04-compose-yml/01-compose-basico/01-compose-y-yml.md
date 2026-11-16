# 🐳 Docker Compose y YAML

## 📌 ¿Qué es Docker Compose?

Herramienta que permite definir y administrar aplicaciones compuestas por varios servicios mediante un archivo `compose.yaml`.

Cada servicio puede utilizar su propia imagen y configuración.

## 📂 Fundamentos YAML

| Elemento | Función |
|---|---|
| Mapas | Organizan pares clave-valor. |
| Listas | Agrupan elementos mediante `-`. |
| Indentación | Define la jerarquía de los elementos. |
| Valores | Pueden ser texto, números, booleanos o `null`. |

## ⚙️ Estructura de `compose.yaml`

```yaml
name: mi-proyecto

services:
  api:
    build: ./api
    ports:
      - "9000:8000"
    environment:
      DEBUG: ${DEBUG}

  postgres:
    image: postgres:17
```

- `name`: establece el nombre del proyecto.
- `services`: agrupa los servicios de la aplicación.
- `api`, `postgres`: nombres asignados a los servicios.

## 🔧 Configuración de servicios

| Propiedad | Función |
|---|---|
| `image` | Utiliza una imagen existente. |
| `build` | Construye una imagen desde un Dockerfile. |
| `ports` | Publica puertos del contenedor en el host. |
| `expose` | Declara puertos internos del servicio. |
| `environment` | Define variables de entorno. |

### Puertos

```yaml
ports:
  - "9000:8000"
```

- `9000`: puerto del computador (host).
- `8000`: puerto del contenedor.

### Variables de entorno

Archivo `.env`:

```env
DEBUG=true
PORT=9000
```

Uso en `compose.yaml`:

```yaml
environment:
  DEBUG: ${DEBUG}

ports:
  - "${PORT}:8000"
```

Compose sustituye `${VARIABLE}` por el valor correspondiente del archivo `.env`.

## 🧩 Varios servicios

Cada servicio puede tener su propia imagen y configuración.

```yaml
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"

  backend:
    build: ./backend
    ports:
      - "8000:8000"

  postgres:
    image: postgres:17
```

Compose crea y administra los contenedores y una red interna para facilitar la comunicación entre servicios.

## 💻 Comandos principales

| Comando | Función |
|---|---|
| `docker compose config` | Valida y muestra la configuración. |
| `docker compose up -d` | Crea e inicia los servicios en segundo plano. |
| `docker compose ps` | Muestra los contenedores del proyecto. |
| `docker compose stop` | Detiene los contenedores. |
| `docker compose start` | Inicia contenedores existentes. |
| `docker compose down` | Detiene y elimina contenedores y redes del proyecto. |
| `docker compose logs` | Consulta los registros de los servicios. |

> **Importante:** `docker compose down` no elimina por defecto las imágenes ni los volúmenes nombrados.

## 🔄 Flujo general

1. Definir los servicios en `compose.yaml`.
2. Configurar imágenes, puertos y variables.
3. Validar con `docker compose config`.
4. Crear e iniciar con `docker compose up -d`.
5. Administrar los servicios con Docker Compose.

---

**Idea clave:** Docker construye y ejecuta los contenedores; Docker Compose organiza y administra los servicios de una aplicación.
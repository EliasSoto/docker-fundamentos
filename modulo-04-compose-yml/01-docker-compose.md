# 🐳 Docker Compose
### Configuración y administración de servicios

> Organización, comunicación y administración de aplicaciones mediante múltiples contenedores.

---

## 📦 1. Volúmenes, redes y dependencias

### 💾 Volúmenes — `volumes`

Permiten conservar datos aunque se elimine un contenedor.

```yaml
services:
  postgres:
    image: postgres:17
    volumes:
      - datos_postgres:/var/lib/postgresql/data

volumes:
  datos_postgres:
```

| Tipo | Función |
|---|---|
| Named volume | Docker administra el almacenamiento. |
| Bind mount | Conecta una carpeta local con el contenedor. |

### 🌐 Redes — `networks`

Permiten la comunicación entre contenedores.

```yaml
services:
  api:
    image: mi_api
    networks:
      - red_app

  postgres:
    image: postgres:17
    networks:
      - red_app

networks:
  red_app:
```

Los servicios se comunican utilizando su nombre como hostname:

```text
API ──────► postgres:5432
              │
              └── DNS interno de Docker
```

### 🔗 Dependencias — `depends_on`

Establece el orden de inicio entre servicios.

```yaml
services:
  api:
    image: mi_api
    depends_on:
      - postgres

  postgres:
    image: postgres:17
```

**Importante:** iniciar un contenedor no significa que su servicio esté listo.

### ❤️ Healthcheck

Comprueba si un servicio está preparado para trabajar.

```yaml
healthcheck:
  test: ["CMD-SHELL", "pg_isready -U postgres"]
  interval: 5s
  timeout: 3s
  retries: 5
  start_period: 10s
```

Se puede combinar con `depends_on`:

```yaml
depends_on:
  postgres:
    condition: service_healthy
```

Así, la API espera a que PostgreSQL esté saludable antes de iniciarse.

---

## ⚙️ 2. Comandos y ciclo de vida

| Comando | Función |
|---|---|
| `docker compose up -d` | Crear e iniciar servicios. |
| `docker compose down` | Detener y eliminar contenedores y redes. |
| `docker compose stop` | Detener sin eliminar. |
| `docker compose start` | Iniciar contenedores existentes. |
| `docker compose restart` | Reiniciar servicios. |
| `docker compose build` | Construir imágenes. |
| `docker compose pull` | Descargar imágenes. |
| `docker compose ps` | Listar contenedores del proyecto. |
| `docker compose logs` | Consultar registros. |
| `docker compose exec` | Ejecutar comandos dentro de un contenedor. |
| `docker compose config` | Validar y mostrar la configuración resuelta. |

<details>
  <summary>💡 Diferencia entre stop y down</summary>

  - `stop`: detiene los contenedores, pero los conserva.
  - `down`: elimina los contenedores y las redes del proyecto.
  - `down -v`: también elimina los volúmenes asociados al proyecto (excepto los externos).
</details>

---

## 🧩 3. Perfiles — `profiles`

Permiten activar servicios opcionales según la necesidad.

Ejemplo: ejecutar Adminer solamente cuando necesitemos administrar PostgreSQL.

```yaml
services:
  api:
    image: mi_api

  postgres:
    image: postgres:17

  adminer:
    image: adminer
    profiles:
      - herramientas
    ports:
      - "8080:8080"
```

Activar el perfil:

```bash
docker compose --profile herramientas up -d
```

<text color="success" weight="medium" size="sm">✓</text> API y PostgreSQL se inician normalmente.

<text color="success" weight="medium" size="sm">✓</text> Adminer se inicia al activar `herramientas`.

---

## 🗂️ 4. Múltiples archivos Compose

Permiten separar la configuración común de los ajustes específicos de cada entorno.

**Estructura del proyecto:**

```text
mi-proyecto/
│
├── compose.yaml
├── compose.dev.yaml
├── compose.prod.yaml
└── Dockerfile
```

### Archivo principal — `compose.yaml`

Contiene los servicios y configuraciones comunes.

```yaml
services:
  api:
    build: .
    image: mi_api

  postgres:
    image: postgres:17
```

### Desarrollo — `compose.dev.yaml`

Agrega configuraciones para trabajar localmente.

```yaml
services:
  api:
    ports:
      - "8000:8000"
    volumes:
      - .:/app
```

### Combinar archivos

```bash
# Desarrollo
docker compose -f compose.yaml -f compose.dev.yaml up -d

# Producción
docker compose -f compose.yaml -f compose.prod.yaml up -d
```

<text color="secondary" size="xs">Los archivos se combinan siguiendo las reglas de combinación de Docker Compose.</text>

---

## 🔧 5. Configuración por entorno

Permite utilizar distintos valores según el entorno de ejecución.

### Variables de entorno — `.env`

```env
APP_PORT=8000
DEBUG=true
```

En `compose.yaml`:

```yaml
services:
  api:
    image: mi_api
    ports:
      - "${APP_PORT}:8000"
    environment:
      DEBUG: ${DEBUG}
```

Compose sustituye las variables utilizando los valores disponibles.

### 🌱 Archivos por entorno

**`.env.dev`**

```env
APP_PORT=8000
DEBUG=true
```

**`.env.prod`**

```env
APP_PORT=80
DEBUG=false
```

Ejecutar según el entorno:

```bash
# Desarrollo
docker compose --env-file .env.dev up -d

# Producción
docker compose --env-file .env.prod up -d
```

### Diferencias importantes

| Configuración | Función |
|---|---|
| `.env` | Valores para sustituir variables en Compose. |
| `--env-file` | Selecciona un archivo de variables para Compose. |
| `env_file` | Carga variables dentro del contenedor. |
| `environment` | Define variables dentro del contenedor. |

> ⚠️ Las variables de `.env` no llegan automáticamente al contenedor. Deben declararse mediante `environment` o `env_file`.

---

## 📚 Resumen general

| Concepto | Utilidad |
|---|---|
| 💾 `volumes` | Persistencia de datos. |
| 🌐 `networks` | Comunicación entre contenedores. |
| 🔗 `depends_on` | Dependencias y orden de inicio. |
| ❤️ `healthcheck` | Comprobar disponibilidad. |
| ⚙️ Comandos Compose | Administrar el ciclo de vida. |
| 🧩 `profiles` | Activar servicios opcionales. |
| 🗂️ `-f` | Combinar archivos Compose. |
| 🔧 `.env` | Configurar distintos entornos. |

---

### 🚀 Idea clave

Docker Compose permite organizar una aplicación completa: sus servicios, almacenamiento, redes, dependencias y configuraciones para desarrollo y producción.
# 🐳 Instalación y puesta en marcha de Docker Desktop

## 🎯 Objetivo

Comprobar que Docker está correctamente instalado y que Docker Engine puede descargar imágenes y ejecutar contenedores.

## 1. Verificar la instalación

Primero comprobamos que Docker CLI y Docker Compose estuvieran instalados.

```powershell
docker --version
docker compose version
```

Ambos comandos mostraron sus respectivas versiones.

## 2. Comprobar Docker Engine

Ejecutamos:

```powershell
docker info
```

Este comando muestra información del entorno Docker.

Entre los datos importantes que revisamos:

- **Client:** información de Docker CLI.
- **Server:** información del Docker Engine.
- **Operating System:** Docker Desktop (containerized).
- **Kernel Version:** versión del kernel Linux utilizado mediante WSL 2.
- **Architecture:** arquitectura del entorno de ejecución.

> Si Docker Engine no está iniciado, Docker CLI no podrá comunicarse con el servidor.

## 3. Ejecutar un contenedor de prueba

Para comprobar que Docker podía descargar imágenes y ejecutar contenedores, utilizamos:

```powershell
docker run hello-world
```

Docker realizó las siguientes operaciones:

1. Buscó la imagen `hello-world:latest` localmente.
2. Como no estaba disponible, la descargó desde Docker Hub.
3. Creó un contenedor a partir de esa imagen.
4. Ejecutó el programa `/hello`.
5. Mostró el mensaje `Hello from Docker!`.

### Flujo de ejecución
```mermaid
flowchart TB
    CMD(["docker run hello-world"])
    CLIENT["Docker CLI / Client"]
    DAEMON["Docker Daemon"]
    CHECK{"¿Existe la imagen<br/>localmente?"}
    REG[("Registry<br/>Docker Hub")]
    PULL["Descargar imagen"]
    CREATE["Crear contenedor"]
    EXEC["Ejecutar programa<br/>/hello"]
    OUT(["Hello from Docker!"])

    CMD --> CLIENT
    CLIENT --> DAEMON
    DAEMON --> CHECK
    CHECK -->|"No"| REG
    REG --> PULL
    PULL --> CREATE
    CHECK -->|"Sí"| CREATE
    CREATE --> EXEC
    EXEC --> OUT

    style REG fill:#fef3c7,stroke:#d97706
    style PULL fill:#f3e8ff,stroke:#9333ea
    style CREATE fill:#f0fdf4,stroke:#16a34a,stroke-width:2px
    style EXEC fill:#f0fdf4,stroke:#16a34a
    style DAEMON fill:#bae6fd,stroke:#0284c7,stroke-width:2px
    style OUT fill:#dcfce7,stroke:#16a34a,stroke-width:2px
```
## 4. Revisar los contenedores

Utilizamos:

```powershell
docker ps -a
```

Este comando muestra todos los contenedores, incluyendo los que ya finalizaron.

Resultado obtenido:

| Campo | Resultado |
|---|---|
| IMAGE | `hello-world` |
| COMMAND | `/hello` |
| STATUS | `Exited (0)` |
| NAMES | `zealous_shtern` |

**¿Qué significa `Exited (0)`?**

- `Exited`: el contenedor terminó su ejecución.
- `0`: el programa finalizó correctamente, sin errores.

El contenedor terminó porque `hello-world` solamente ejecuta un mensaje y luego finaliza.

## 5. Revisar las imágenes locales

Ejecutamos:

```powershell
docker images
```

Este comando muestra las imágenes almacenadas localmente.

Imágenes encontradas:

| Imagen | Tamaño en disco |
|---|---:|
| `hello-world:latest` | 25.9 kB |
| `sd_grpc:semana11` | 262 MB |

La imagen `hello-world` quedó almacenada localmente después de descargarla desde Docker Hub.

Por eso, al ejecutar nuevamente:

```powershell
docker run hello-world
```

Docker puede reutilizar la imagen local sin descargarla otra vez.

> **Importante:** ejecutar nuevamente `docker run` crea un nuevo contenedor, aunque se utilice la misma imagen.

## 6. Comandos utilizados

| Comando | Función |
|---|---|
| `docker --version` | Consulta la versión de Docker CLI. |
| `docker compose version` | Consulta la versión de Docker Compose. |
| `docker info` | Muestra información del entorno Docker. |
| `docker run hello-world` | Descarga la imagen si es necesario y ejecuta un contenedor. |
| `docker ps -a` | Lista todos los contenedores. |
| `docker images` | Lista las imágenes locales. |

## ✅ Resultado

Se comprobó que Docker Desktop está correctamente instalado y operativo en Windows, utilizando WSL 2 como backend para ejecutar el entorno Linux.

Se verificó la comunicación entre Docker Client y Docker Daemon, la descarga de imágenes desde Docker Hub y la creación y ejecución de contenedores.


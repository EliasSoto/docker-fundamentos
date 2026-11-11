# 🐳 2.1 — Docker CLI y comandos esenciales

## 🎯 Objetivo

Conocer Docker CLI, comprender cómo se estructura un comando y reconocer las principales instrucciones para administrar contenedores e imágenes.

## 1. ¿Qué es Docker CLI?

Docker CLI (*Command Line Interface*) es la herramienta que permite comunicarnos con Docker Engine mediante comandos desde una terminal.

```text
Usuario / PowerShell
        |
     Docker CLI
        |
     Docker API
        |
   Docker Daemon
        |
  Imágenes y contenedores
```

## 2. Estructura de un comando

```powershell
docker [opciones] COMANDO [argumentos]
```

Ejemplo:

```powershell
docker run -d --name servidor nginx
```

| Elemento | Función |
|---|---|
| `docker` | Ejecuta la CLI. |
| `run` | Operación que se realizará. |
| `-d` | Ejecuta en segundo plano. |
| `--name servidor` | Asigna un nombre. |
| `nginx` | Imagen utilizada. |

## 3. Ayuda integrada

| Comando | Función |
|---|---|
| `docker --help` | Muestra los comandos disponibles. |
| `docker run --help` | Muestra la ayuda de `run`. |
| `docker version` | Consulta versiones de Docker. |
| `docker info` | Muestra información del entorno Docker. |

## 4. Comandos esenciales

| Comando | Función |
|---|---|
| `docker run` | Crea e inicia un contenedor. |
| `docker create` | Crea un contenedor sin iniciarlo. |
| `docker ps` | Lista contenedores activos. |
| `docker ps -a` | Lista todos los contenedores. |
| `docker logs` | Consulta registros. |
| `docker inspect` | Muestra información detallada. |
| `docker stats` | Consulta consumo de recursos. |
| `docker top` | Muestra procesos del contenedor. |
| `docker pull` | Descarga una imagen. |
| `docker images` | Lista imágenes locales. |
| `docker tag` | Asigna una etiqueta a una imagen. |
| `docker rm` | Elimina un contenedor. |
| `docker rmi` | Elimina una imagen. |

## 5. Opciones frecuentes

| Opción | Función |
|---|---|
| `-d` | Modo segundo plano (*detached*). |
| `-it` | Modo interactivo con terminal. |
| `--name` | Asigna un nombre. |
| `-p` | Publica un puerto. |
| `-e` | Define variables de entorno. |
| `-v` | Monta un volumen. |
| `--rm` | Elimina el contenedor al finalizar. |

### Modos de ejecución

```powershell
# Segundo plano
docker run -d nginx

# Interactivo
docker run -it ubuntu bash
```

## 6. Docker CLI vs. Docker Compose

| Herramienta | Propósito |
|---|---|
| Docker CLI | Administrar recursos y ejecutar comandos Docker. |
| Docker Compose | Definir y administrar aplicaciones con múltiples servicios. |

Ejemplo:

```powershell
docker compose up -d
```

---

## 💡 Aprendizajes

- Comprender la comunicación entre Docker CLI y Docker Engine.
- Identificar la estructura de los comandos.
- Utilizar la ayuda integrada.
- Reconocer comandos para administrar contenedores e imágenes.
- Diferenciar las opciones de ejecución interactiva y segundo plano.

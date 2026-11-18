# 🐳 Comandos Docker y Docker Compose

## 1. Docker: Contenedores

| Comando | Significado |
|---|---|
| `docker ps` | Muestra los contenedores en ejecución. |
| `docker ps -a` | Muestra todos los contenedores. |
| `docker run -d --name {nombre} {imagen}` | Crea y ejecuta un contenedor en segundo plano. |
| `docker start {contenedor}` | Inicia un contenedor detenido. |
| `docker stop {contenedor}` | Detiene un contenedor. |
| `docker rm {contenedor}` | Elimina un contenedor detenido. |
| `docker exec -it {contenedor} bash` | Abre una terminal dentro del contenedor. |
| `docker logs -f {contenedor}` | Sigue los registros en tiempo real. |
| `docker inspect {contenedor}` | Muestra información detallada. |
| `docker stats` | Muestra el consumo de recursos. |

## 2. Docker: Imágenes

| Comando | Significado |
|---|---|
| `docker images` | Lista las imágenes locales. |
| `docker pull {imagen}` | Descarga una imagen. |
| `docker build -t {nombre}:{tag} .` | Construye una imagen desde un Dockerfile. |
| `docker push {nombre}:{tag}` | Publica una imagen en un registro. |

## 3. Docker: Redes y volúmenes

| Comando | Significado |
|---|---|
| `docker network ls` | Lista las redes. |
| `docker network create {nombre}` | Crea una red. |
| `docker volume ls` | Lista los volúmenes. |
| `docker volume create {nombre}` | Crea un volumen. |

## 4. Docker Compose: Servicios y proyectos

| Comando | Significado |
|---|---|
| `docker compose up -d` | Crea e inicia los servicios en segundo plano. |
| `docker compose up -d --build` | Construye las imágenes e inicia los servicios. |
| `docker compose down` | Detiene y elimina los contenedores y redes del proyecto. |
| `docker compose ps` | Muestra el estado de los servicios. |
| `docker compose logs -f` | Sigue los registros de los servicios. |
| `docker compose exec {servicio} bash` | Abre una terminal dentro de un servicio activo. |
| `docker compose stop` | Detiene los servicios sin eliminarlos. |
| `docker compose pull` | Descarga las imágenes de los servicios. |

## 5. Información y ayuda

| Comando | Significado |
|---|---|
| `docker version` | Muestra las versiones de Docker. |
| `docker info` | Muestra información general del entorno Docker. |




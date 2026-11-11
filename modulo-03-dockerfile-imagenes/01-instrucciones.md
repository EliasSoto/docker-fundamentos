# 🐳 Dockerfile y configuración de puertos

## 📌 ¿Qué es un Dockerfile?

Es un archivo de texto que contiene instrucciones para construir una imagen personalizada de Docker. Cada instrucción cumple una función dentro del proceso de construcción o ejecución del contenedor.

## ⚙️ Instrucciones del Dockerfile

| Instrucción | Descripción |
|---|---|
| `FROM` | Selecciona la imagen base sobre la que construiremos nuestra imagen. |
| `ARG` | Define variables que podemos utilizar durante la construcción. |
| `RUN` | Ejecuta comandos durante la construcción, cuyos resultados quedan en la imagen. |
| `WORKDIR` | Establece el directorio de trabajo dentro de la imagen. Si no existe, Docker lo crea. |
| `COPY` | Copia archivos o carpetas desde el proyecto local hacia la imagen. |
| `ENV` | Define variables de entorno que estarán disponibles al ejecutar el contenedor. |
| `EXPOSE` | Documenta el puerto interno que utiliza la aplicación. No publica el puerto en nuestro computador. |
| `ENTRYPOINT` | Define el comando principal que ejecutará el contenedor al iniciarse. |
| `CMD` | Define el comando o los argumentos predeterminados que se utilizarán al iniciar el contenedor. |

### Diferencia entre RUN, CMD y ENTRYPOINT

- `RUN`: se ejecuta durante la construcción de la imagen.
- `CMD`: define el comportamiento predeterminado al iniciar el contenedor.
- `ENTRYPOINT`: establece el ejecutable principal del contenedor.

## 🔌 Configuración de puertos

Docker permite conectar un puerto de nuestro computador con uno del contenedor.

```bash
docker run -p 9000:8000 mi_api
```

- `9000`: puerto de nuestro computador (externo).
- `8000`: puerto donde escucha la aplicación dentro del contenedor (interno).

**Diferencia importante:**

- `EXPOSE 8000`: documenta el puerto interno de la aplicación.
- `-p 9000:8000`: publica el puerto y permite acceder a la aplicación desde nuestro computador.

## 🚫 .dockerignore

Archivo que permite excluir archivos y carpetas del contexto de construcción, evitando enviar información innecesaria a Docker.

Ejemplo:

```text
venv/
__pycache__/
.git/
.env
*.pyc
```

## 🏗️ Construcción de imágenes

```bash
docker build -t mi_primera_imagen .
```

Construye una imagen utilizando el Dockerfile del directorio actual.

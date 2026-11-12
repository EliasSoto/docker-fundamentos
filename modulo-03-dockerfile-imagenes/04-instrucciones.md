# 🐳 Dockerfile – Instrucciones básicas

Las instrucciones de un `Dockerfile` permiten definir cómo se construye una imagen y cómo se comportará el contenedor al ejecutarse.

## 📋 1. Instrucciones utilizadas

### `FROM`
Define la imagen base sobre la que se construirá nuestra imagen.

```dockerfile
FROM ubuntu
```
En este caso, utilizamos Ubuntu como punto de partida para construir nuestra imagen.

### `ARG`
Define una variable disponible durante la construcción de la imagen.

```dockerfile
ARG VERSION=1.0
```
Permite recibir valores al ejecutar `docker build`, por ejemplo:

```bash
docker build --build-arg VERSION=2.0 -t mi_imagen .
```

### `RUN`
Ejecuta comandos durante la construcción de la imagen. Cada instrucción `RUN` genera una capa en la imagen.

```dockerfile
RUN apt-get update
RUN echo "Construyendo versión: $VERSION"
RUN pwd
```

- `apt-get update`: actualiza los índices de paquetes.
- `echo`: muestra un mensaje durante la construcción.
- `pwd`: muestra el directorio de trabajo actual.

**Importante:** Estos comandos se ejecutan al construir la imagen, no cada vez que iniciamos el contenedor.

### `WORKDIR`
Establece el directorio de trabajo dentro de la imagen. Si no existe, Docker lo crea.

```dockerfile
WORKDIR /app
```
Los siguientes comandos utilizarán `/app` como directorio de trabajo, salvo que se indique otra ruta.

### `EXPOSE`
Documenta el puerto interno que utilizará la aplicación dentro del contenedor.

```dockerfile
EXPOSE 8000
```
No publica el puerto automáticamente. Para permitir el acceso desde nuestra máquina utilizamos `-p` al ejecutar el contenedor.

### `ENV`
Define variables de entorno que estarán disponibles durante la ejecución del contenedor.

```dockerfile
ENV MENSAJE="Hola desde Docker"
```
La aplicación podrá consultar esta variable mientras se ejecuta.

### `COPY`
Copia archivos o directorios desde nuestro proyecto hacia la imagen.

```dockerfile
COPY requirements.txt .
```
Copia `requirements.txt` al directorio de trabajo actual. Como anteriormente establecimos `/app`, el archivo quedará en `/app/requirements.txt`.

### `ENTRYPOINT`
Define el ejecutable principal que se ejecutará al iniciar el contenedor.

```dockerfile
ENTRYPOINT ["cat"]
```
En este caso, el contenedor ejecutará el comando `cat`, que permite mostrar el contenido de archivos.

### `CMD`
Define el comando predeterminado o los argumentos que recibirá el `ENTRYPOINT`.

```dockerfile
CMD ["/app/requirements.txt"]
```
Como tenemos un `ENTRYPOINT` definido, Docker combina ambas instrucciones y ejecuta:

```bash
cat /app/requirements.txt
```

---

## ⚖️ 2. Diferencias importantes

| Instrucciones | Diferencia |
|---|---|
| `ARG` / `ENV` | `ARG` se utiliza durante la construcción; `ENV` permanece disponible durante la ejecución. |
| `RUN` / `CMD` | `RUN` ejecuta comandos al construir la imagen; `CMD` define qué ejecutar al iniciar el contenedor. |
| `ENTRYPOINT` / `CMD` | `ENTRYPOINT` establece el ejecutable principal; `CMD` proporciona sus argumentos predeterminados. |
| `WORKDIR` / `COPY` | `WORKDIR` establece dónde trabajar; `COPY` lleva archivos a ese destino. |
| `EXPOSE` / `-p` | `EXPOSE` documenta el puerto; `-p` publica el puerto para acceder desde el host. |
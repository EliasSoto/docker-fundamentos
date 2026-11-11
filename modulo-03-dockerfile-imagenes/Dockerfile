# Imagen base del contenedor
FROM ubuntu

# Variable disponible durante la construcción
ARG VERSION=1.0

# Actualiza los índices de paquetes de Ubuntu
RUN apt-get update

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Documenta el puerto interno utilizado por la aplicación
EXPOSE 8000

# Variable de entorno disponible durante la ejecución
ENV MENSAJE="Hola desde Docker"

# Muestra la versión durante la construcción
RUN echo "Construyendo versión: $VERSION"

# Muestra el directorio de trabajo actual
RUN pwd

# Copia requirements.txt desde el proyecto a /app
COPY requirements.txt .

# Define el comando principal del contenedor
ENTRYPOINT ["cat"]

# Define los argumentos predeterminados del comando
CMD ["/app/requirements.txt"]
# 🌐 Redes personalizadas, DNS y comunicación entre servicios

Docker permite crear redes personalizadas para conectar contenedores y facilitar la comunicación entre los diferentes servicios de una aplicación.

## 1. 🔗 Redes personalizadas

Son redes creadas por el usuario para conectar contenedores dentro de un mismo host.

Por ejemplo, podemos tener una aplicación compuesta por tres servicios:

```text
       RED PERSONALIZADA
    ┌─────────────────────────┐
    │                         │
    │   ┌──────────┐          │
    │   │ Frontend │          │
    │   └──────────┘          │
    │                         │
    │   ┌──────────┐          │
    │   │ Backend  │          │
    │   └──────────┘          │
    │                         │
    │   ┌──────────┐          │
    │   │PostgreSQL│          │
    │   └──────────┘          │
    │                         │
    └─────────────────────────┘
```

**Ventajas:**
- Permiten organizar los contenedores según la aplicación.
- Facilitan la comunicación entre servicios.
- Proporcionan resolución DNS automática mediante nombres.

## 2. 🔎 Resolución DNS en Docker

Docker incorpora un sistema DNS interno en las redes personalizadas.

Esto permite que los contenedores encuentren otros servicios utilizando sus nombres, sin necesidad de conocer sus direcciones IP.

**Ejemplo:**

El backend necesita conectarse a PostgreSQL. En lugar de utilizar su dirección IP, puede utilizar:

`postgres:5432`

Docker identifica el nombre `postgres` y lo resuelve a la dirección IP interna correspondiente.

**¿Por qué es útil?**

Las direcciones IP de los contenedores pueden cambiar cuando se recrean. Utilizar nombres permite mantener la comunicación sin tener que actualizar manualmente las direcciones IP.

## 3. 🔄 Comunicación entre servicios

Los contenedores conectados a una misma red pueden comunicarse directamente entre sí.

Por ejemplo, en una aplicación web:

```text
       FRONTEND
           │
           │ HTTP
           ▼
        BACKEND
           │
           │ Consulta a la BDD
           ▼
       POSTGRESQL
```

El frontend envía solicitudes al backend y este puede consultar la base de datos.

Para comunicarse, los servicios utilizan el nombre del contenedor o servicio y el puerto interno correspondiente.

**Importante:** no es necesario publicar los puertos de todos los contenedores al host. Los servicios pueden comunicarse internamente mediante su red Docker.


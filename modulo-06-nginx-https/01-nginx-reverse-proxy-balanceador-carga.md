# 🌐 Nginx: Reverse Proxy y Balanceador de Carga

## 1. ¿Qué es Nginx?

Nginx es un servidor web que también puede funcionar como **Reverse Proxy** y **Balanceador de carga**.

Actúa como intermediario entre los clientes y los servicios de una aplicación, recibiendo solicitudes y dirigiéndolas hacia el destino correspondiente.

Puede comunicarse con:
- Clientes externos a Docker.
- Contenedores dentro de Docker.
- Diferentes servicios dentro de una misma red Docker.

## 2. Funciones principales

| Función | Descripción |
|---|---|
| **Reverse Proxy** | Recibe solicitudes y las reenvía a otros servicios. |
| **Balanceador de carga** | Distribuye solicitudes entre varias instancias de un servicio. |
| **Servidor web** | Entrega archivos estáticos, como HTML, CSS y JavaScript. |
| **Terminación HTTPS** | Gestiona conexiones seguras mediante certificados TLS. |

### Enrutamiento vs. balanceo

- **Enrutamiento:** dirige solicitudes a diferentes servicios según la ruta solicitada.
- **Balanceo:** distribuye solicitudes entre varias instancias del mismo servicio.

## 3. Protocolos y puertos

Los servicios utilizan protocolos y puertos para comunicarse.

| Comunicación | Protocolo | Puerto destino |
|---|---|---:|
| Computador → Nginx | HTTP | `80` |
| Computador → Nginx | HTTPS | `443` |
| Nginx → Frontend | HTTP | `80` |
| Nginx → API 1 | HTTP | `8000` |
| Nginx → API 2 | HTTP | `8000` |
| API 1 → PostgreSQL | PostgreSQL sobre TCP | `5432` |
| API 2 → PostgreSQL | PostgreSQL sobre TCP | `5432` |

> Los puertos son ejemplos y pueden cambiar según la configuración de cada servicio.

## 4. Comprender los puertos

Un servicio **escucha en un puerto** para recibir conexiones entrantes.

Por ejemplo, PostgreSQL utiliza el puerto `5432` por defecto.

Cuando API 1 quiere conectarse a PostgreSQL:

```text
┌─────────┐       TCP :5432       ┌────────────┐
│  API 1  │ ────────────────────► │ PostgreSQL │
└─────────┘                       └────────────┘
```

- API 1 inicia la conexión.
- PostgreSQL escucha en el puerto `5432`.
- API 1 se conecta a ese puerto.
- PostgreSQL procesa la consulta y devuelve una respuesta.

### Puerto de origen y destino

- **Puerto de origen:** identifica el extremo desde donde se inicia la conexión. Normalmente lo asigna automáticamente el sistema operativo.
- **Puerto de destino:** corresponde al puerto donde escucha el servicio al que queremos conectarnos.

## 5. Publicación de puertos en Docker

En Docker Compose utilizamos `ports` para publicar un puerto del contenedor hacia el host.

```yaml
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"

  postgres:
    image: postgres:17
```

En este ejemplo:

| Puerto | Función |
|---|---|
| `8080` | Puerto del computador (host). |
| `80` | Puerto donde escucha Nginx dentro del contenedor. |
| `5432` | Puerto interno predeterminado de PostgreSQL. |

Los contenedores que comparten una red Docker pueden comunicarse directamente mediante el nombre del servicio y su puerto interno, sin necesidad de publicar sus puertos al host.

Ejemplo de conexión:

```text
postgres:5432
```

## 6. Consideraciones importantes

- Nginx trabaja principalmente con tráfico HTTP/HTTPS.
- Puede comunicarse con servicios dentro y fuera de Docker.
- No es necesario utilizar Nginx para todas las comunicaciones.
- Las APIs pueden conectarse directamente a PostgreSQL mediante un driver.
- PostgreSQL utiliza su propio protocolo sobre TCP, no HTTP.
- Los contenedores deben compartir una red Docker para comunicarse directamente mediante sus nombres de servicio.

---

### 💡 Idea clave

Nginx funciona como punto de entrada e intermediario para dirigir el tráfico de una aplicación. Sin embargo, cada servicio utiliza el protocolo y el puerto que corresponden a su función.

# 🌐 Modelos OSI y TCP/IP

> Comprendiendo cómo se comunican los dispositivos y aplicaciones dentro de una red.

---

## 🧱 1. Modelo OSI

El modelo OSI (*Open Systems Interconnection*) es un modelo conceptual que divide la comunicación de red en **7 capas**, cada una con una función específica.

| Capa | Nombre | Función |
|:---:|---|---|
| 7 | Aplicación | Interacción con aplicaciones y servicios de red. |
| 6 | Presentación | Formato, codificación y cifrado de datos. |
| 5 | Sesión | Establece y administra sesiones de comunicación. |
| 4 | Transporte | Gestiona la entrega de datos mediante TCP o UDP. |
| 3 | Red | Direccionamiento IP y enrutamiento. |
| 2 | Enlace de datos | Comunicación dentro de la red local mediante tramas y direcciones MAC. |
| 1 | Física | Transmisión de bits mediante señales eléctricas, ópticas o inalámbricas. |

---

## 🌍 2. Modelo TCP/IP

Es una arquitectura utilizada en las redes para permitir la comunicación entre dispositivos. Agrupa las funciones en **4 capas**.

| Capa | Función | Ejemplos |
|---|---|---|
| Aplicación | Permite intercambiar información entre aplicaciones. | HTTP, HTTPS, DNS, gRPC |
| Transporte | Gestiona el transporte de datos. | TCP, UDP |
| Internet | Direccionamiento y enrutamiento. | IP |
| Acceso a la red | Comunicación con la red física o local. | Ethernet, Wi-Fi |

### 🔄 Comparación OSI vs TCP/IP

| Modelo OSI | Modelo TCP/IP |
|---|---|
| Aplicación | Aplicación |
| Presentación | Aplicación |
| Sesión | Aplicación |
| Transporte | Transporte |
| Red | Internet |
| Enlace de datos | Acceso a la red |
| Física | Acceso a la red |

**Importante:** OSI es un modelo de referencia para comprender las comunicaciones, mientras que TCP/IP representa la arquitectura utilizada en Internet y otras redes.

---

## 💻 3. Cliente y servidor

Son los roles que cumplen las aplicaciones cuando se comunican.

- **Cliente:** aplicación o dispositivo que inicia una solicitud para obtener información o utilizar un servicio.
- **Servidor:** aplicación que espera solicitudes, las procesa y entrega respuestas.

### Ejemplo de comunicación

Un frontend que consulta una API:

| Paso | Acción |
|---|---|
| 1 | El cliente realiza una solicitud HTTP. |
| 2 | El servidor recibe la solicitud. |
| 3 | El servidor procesa la información. |
| 4 | El servidor devuelve una respuesta. |
| 5 | El cliente recibe y utiliza los datos. |

**Ejemplos:**

- Navegador → servidor web.
- Frontend → API FastAPI.
- API → base de datos PostgreSQL.

Un mismo programa puede actuar como cliente y servidor dependiendo de la comunicación.

---

## 🔌 4. Socket

Un **socket** es un extremo de comunicación que permite a dos aplicaciones intercambiar información mediante una red.

Para comprenderlo:

- **IP:** identifica el dispositivo.
- **Puerto:** identifica el punto de comunicación del servicio.
- **Socket:** representa el extremo de comunicación utilizado por la aplicación.

### Ejemplo de conexión TCP

| Elemento | Dirección |
|---|---|
| IP de origen | `192.168.1.10` |
| Puerto de origen | `52000` |
| IP de destino | `192.168.1.20` |
| Puerto de destino | `8000` |

Una conexión TCP se identifica mediante esta combinación de cuatro valores, conocida como *4-tupla*.

### Ejemplo práctico con FastAPI

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

| Parámetro | Función |
|---|---|
| `main:app` | Aplicación que queremos ejecutar. |
| `--host 0.0.0.0` | Escucha en todas las interfaces IPv4 disponibles. |
| `--port 8000` | Utiliza el puerto 8000. |

La aplicación queda preparada para recibir conexiones en ese puerto.

---

## 🐳 5. Aplicación en Docker

Imaginemos una arquitectura con tres contenedores:

| Contenedor | Función | Puerto |
|---|---|---|
| Frontend | Cliente | 3000 |
| API FastAPI | Servidor | 8000 |
| PostgreSQL | Servidor de base de datos | 5432 |

### Flujo de comunicación

1. El frontend actúa como cliente y solicita información a la API.
2. La API recibe y procesa la solicitud.
3. La API actúa como cliente al consultar PostgreSQL.
4. PostgreSQL responde a la API.
5. La API devuelve la información al frontend.

**Conceptos involucrados:**

- IP: permite localizar cada contenedor.
- Puerto: identifica el servicio al que queremos conectarnos.
- TCP: permite transportar los datos.
- Socket: representa el extremo de comunicación.
- Cliente/servidor: define los roles de las aplicaciones.

---

## 🎯 Conceptos clave

| Concepto | Resumen |
|---|---|
| OSI | Modelo conceptual de 7 capas. |
| TCP/IP | Arquitectura de comunicación de 4 capas. |
| Cliente | Inicia solicitudes. |
| Servidor | Recibe solicitudes y proporciona servicios. |
| Socket | Extremo de comunicación de una aplicación. |
| Puerto | Punto de comunicación asociado a un servicio. |


# 🌐 Redes y protocolos

En este módulo aprendemos cómo se comunican los dispositivos, aplicaciones y servicios a través de una red, y qué protocolos permiten realizar estas comunicaciones.

---

## 📡 1. Protocolos de transporte: TCP y UDP

Son protocolos que permiten transportar información entre dispositivos a través de una red.

| Protocolo | Características | Uso |
|---|---|---|
| **TCP** | Orientado a conexión, confiable y verifica la entrega de datos. | HTTP, HTTPS, transferencia de archivos. |
| **UDP** | No establece conexión ni garantiza la entrega de todos los paquetes. | Streaming, videojuegos y llamadas en tiempo real. |

### 🔹 TCP
- Establece una conexión antes de transmitir información.
- Comprueba que los datos lleguen correctamente.
- Permite retransmitir segmentos perdidos.
- Mantiene el orden de los datos.

### 🔹 UDP
- Envía datos sin establecer una conexión previa.
- No garantiza la entrega ni el orden de los paquetes.
- Tiene menos sobrecarga que TCP.
- Es útil cuando importa más la velocidad que recuperar cada paquete perdido.

---

## 🌍 2. HTTP y HTTPS

Son protocolos de comunicación utilizados para intercambiar información entre clientes y servidores.

| Protocolo | Características |
|---|---|
| **HTTP** | Permite solicitar y transferir información entre cliente y servidor. |
| **HTTPS** | Utiliza HTTP junto con TLS para cifrar y proteger la comunicación. |

### 🔹 HTTP
Permite realizar solicitudes mediante métodos como:

- `GET`: obtener información.
- `POST`: enviar o crear información.
- `PUT`: actualizar información.
- `DELETE`: eliminar información.

### 🔹 HTTPS
- Cifra la información transmitida.
- Protege los datos frente a la interceptación.
- Permite verificar la identidad del servidor mediante certificados digitales.

---

## 🔎 3. DNS (Domain Name System)

Es el sistema encargado de traducir nombres de dominio a direcciones IP.

**Ejemplo:**

Cuando escribimos `google.com`, el DNS permite encontrar la dirección IP asociada a ese dominio.

```text
Usuario
   |
   v
google.com
   |
   v
Servidor DNS
   |
   v
Dirección IP
   |
   v
Servidor de destino
```

Esto evita tener que recordar las direcciones IP de los servidores que queremos visitar.

---

## ⚡ 4. gRPC (Remote Procedure Call)

Es un framework de comunicación que permite que diferentes programas invoquen métodos de otros programas a través de una red.

A diferencia de REST, que normalmente trabaja mediante rutas y solicitudes HTTP, gRPC permite llamar directamente a métodos definidos en un servicio remoto.

### 🔹 Tecnologías utilizadas

| Tecnología | Función |
|---|---|
| **gRPC** | Gestiona las llamadas a métodos remotos. |
| **HTTP/2** | Transporta la comunicación. |
| **Protocol Buffers** | Define y serializa los mensajes intercambiados. |

### 🔹 ¿Cómo funciona?

1. Se define un contrato `.proto` con los servicios, métodos y mensajes.
2. Se implementa un servidor gRPC que ejecuta los métodos.
3. Se genera un cliente gRPC que permite invocar esos métodos.
4. El cliente envía una solicitud y recibe la respuesta del servidor.

### 🔹 Ejemplo de arquitectura

```text
       FRONTEND
           |
           | HTTP / REST
           v
        BACKEND
        FastAPI
           |
           | gRPC / HTTP2
           v
      SERVIDOR gRPC
      (Geolocalización)
           |
           | SQL
           v
       POSTGRESQL
```

### 🔹 ¿Quiénes pueden utilizar gRPC?

Cualquier programa que implemente un cliente compatible:

- Otros backends.
- Aplicaciones móviles.
- Sistemas de seguimiento GPS.
- Otros servicios o microservicios.

También es posible utilizar gRPC desde aplicaciones web mediante gRPC-Web.

### 🔹 ¿Cuándo utilizarlo?

- Comunicación entre microservicios.
- Sistemas distribuidos.
- Comunicación frecuente entre diferentes servicios.
- Aplicaciones que necesitan intercambio eficiente de información.

**Importante:** gRPC no reemplaza necesariamente a REST. Ambos pueden coexistir en una misma arquitectura.

---

## 🧠 5. Resumen general

| Tecnología | Función principal |
|---|---|
| **TCP** | Transporte confiable de datos. |
| **UDP** | Transporte rápido sin garantía de entrega. |
| **HTTP** | Comunicación entre clientes y servidores web. |
| **HTTPS** | Comunicación HTTP cifrada mediante TLS. |
| **DNS** | Traducción de dominios a direcciones IP. |
| **gRPC** | Invocación de métodos entre programas mediante una red. |


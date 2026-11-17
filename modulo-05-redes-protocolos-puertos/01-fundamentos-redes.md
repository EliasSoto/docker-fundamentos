# 🌐 Redes, protocolos y puertos

> Fundamentos de redes y comunicación entre servicios, aplicados al entorno de Docker.

## 📚 Fundamentos de redes

Una **red** es un conjunto de dispositivos que pueden comunicarse entre sí para intercambiar información.

Por ejemplo: computadores, servidores, teléfonos y bases de datos conectados mediante una red.

### 🔹 Conceptos fundamentales

| Concepto | Descripción | Ejemplo |
|---|---|---|
| **IP** | Identificador numérico de un dispositivo dentro de una red. | `192.168.1.10` |
| **Subred** | División lógica de una red que agrupa dispositivos dentro de un rango de direcciones IP. | `192.168.1.0/24` |
| **Gateway** | Puerta de enlace que permite comunicarse con otras redes. Normalmente es el router. | `192.168.1.1` |
| **DNS** | Traduce nombres de dominio a direcciones IP. | `google.com` → IP |
| **NAT** | Traduce direcciones IP entre redes, permitiendo que varios dispositivos compartan una misma IP pública. | Red local → Internet |

### 🖥️ Ejemplo de una red local

Imaginemos una red doméstica con distintos dispositivos conectados al mismo router:

| Dispositivo | Dirección IP |
|---|---|
| Router | `192.168.1.1` |
| Computador | `192.168.1.10` |
| Notebook | `192.168.1.11` |
| Teléfono | `192.168.1.12` |

Todos pertenecen a la misma subred:

`192.168.1.0/24`

Esto significa que pueden comunicarse directamente dentro de la red local, siempre que las reglas de comunicación lo permitan.

### 🔄 ¿Cómo se relacionan estos conceptos?

1. Cada dispositivo tiene una dirección IP para identificarse.
2. La subred determina qué direcciones pertenecen al mismo segmento de red.
3. El gateway permite comunicarse con otras redes.
4. DNS permite encontrar servicios mediante nombres en lugar de recordar direcciones IP.
5. NAT permite traducir direcciones para facilitar la comunicación entre redes diferentes.

---

### 🎯 Objetivo del módulo

Comprender cómo se comunican los dispositivos y servicios dentro de una red, para posteriormente aplicar estos conceptos a Docker:

- Comunicación entre contenedores.
- Redes personalizadas.
- Resolución DNS entre servicios.
- Publicación de puertos.
- Diagnóstico de conectividad y conflictos de puertos.
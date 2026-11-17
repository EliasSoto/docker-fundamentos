# 🌐 Redes en Docker

Docker permite configurar redes para controlar cómo se comunican los contenedores entre sí, con el computador anfitrión (host) y con redes externas.

Existen diferentes tipos de redes, cada una con un propósito específico.

## 1. 🔵 Bridge

Es la red más utilizada en Docker. Permite que varios contenedores se comuniquen entre sí dentro de un mismo computador (host).

**Ejemplo:**

```text
       COMPUTADOR (HOST)
    ┌─────────────────────────┐
    │                         │
    │   ┌─────────┐           │
    │   │ Frontend│           │
    │   └────┬────┘           │
    │        │                │
    │   ┌────▼────┐           │
    │   │ Backend │           │
    │   └────┬────┘           │
    │        │                │
    │   ┌────▼────┐           │
    │   │PostgreSQL│          │
    │   └─────────┘           │
    │                         │
    │      RED BRIDGE         │
    └─────────────────────────┘
```

**Características:**
- Conecta contenedores dentro de un mismo host.
- Permite la comunicación entre contenedores.
- Las redes bridge personalizadas permiten comunicarse utilizando nombres de contenedores o servicios.
- Es habitual en aplicaciones desarrolladas localmente.

## 2. 🟠 Host

Permite que un contenedor comparta directamente la red del computador anfitrión.

En lugar de tener una red aislada propia, utiliza la red del host.

**Ejemplo:**

```text
       COMPUTADOR (HOST)
    ┌─────────────────────────┐
    │                         │
    │     RED DEL HOST        │
    │                         │
    │    ┌──────────────┐     │
    │    │  Contenedor  │     │
    │    │              │     │
    │    │  Aplicación  │     │
    │    └──────────────┘     │
    │                         │
    └─────────────────────────┘
```

**Características:**
- Comparte la red del host.
- No necesita publicar puertos mediante `ports`.
- Puede generar conflictos si otro programa utiliza el mismo puerto.
- Tiene particularidades en Docker Desktop para Windows y macOS.

## 3. 🔴 None

Permite ejecutar un contenedor sin conectividad de red externa.

El contenedor queda aislado de otros contenedores y de Internet mediante interfaces de red externas. Conserva la interfaz local `localhost` (loopback).

**Ejemplo:**

```text
       COMPUTADOR (HOST)
    ┌─────────────────────────┐
    │                         │
    │    ┌──────────────┐     │
    │    │  Contenedor  │     │
    │    │              │     │
    │    │  Aplicación  │     │
    │    │              │     │
    │    │  SIN RED     │     │
    │    └──────────────┘     │
    │                         │
    └─────────────────────────┘
```

**Características:**
- No tiene conectividad de red externa.
- No puede comunicarse con otros contenedores mediante una red Docker.
- No puede acceder a Internet.
- Es útil cuando necesitamos aislamiento de red.

## 4. 🟢 Overlay

Es una red virtual que permite conectar contenedores que se ejecutan en **diferentes computadores o servidores (hosts)**.

A diferencia de Bridge, que conecta contenedores dentro de un mismo host, Overlay permite extender la comunicación entre varios hosts Docker.

### Ejemplo práctico

Imaginemos que estamos desarrollando una aplicación con un amigo. Cada uno tiene Docker instalado en su propio computador.

```text
       MI COMPUTADOR                 COMPUTADOR DE MI AMIGO
    ┌──────────────────┐           ┌──────────────────────┐
    │                  │           │                      │
    │    Frontend      │           │    Servicio gRPC     │
    │                  │           │                      │
    │    Backend       │           │    PostgreSQL        │
    │                  │           │                      │
    └────────┬─────────┘           └──────────┬───────────┘
             │                                │
             └──────────────┬─────────────────┘
                            │
                   ┌────────▼────────┐
                   │  RED OVERLAY    │
                   │                 │
                   │ Comunicación    │
                   │ entre hosts      │
                   └─────────────────┘
```

Gracias a Overlay, el backend de mi computador podría comunicarse con el servicio gRPC que se ejecuta en el computador de mi amigo.

### ¿Qué necesitamos?

Para utilizar Overlay en Docker Engine normalmente necesitamos **Docker Swarm**, que permite administrar varios computadores como un clúster.

Pasos generales:

1. Inicializar Docker Swarm.
2. Incorporar los demás computadores al clúster.
3. Crear una red Overlay compartida.
4. Permitir la comunicación entre los hosts mediante los puertos necesarios.

**Comandos básicos:**

Inicializar Swarm:

```bash
docker swarm init
```

Crear una red Overlay:

```bash
docker network create -d overlay red_distribuida
```

Estos comandos son ilustrativos. Para conectar varios computadores también debemos configurar los nodos del clúster y su conectividad de red.

**Características:**
- Conecta contenedores de diferentes hosts.
- Permite distribuir una aplicación entre varios servidores.
- Se utiliza habitualmente con Docker Swarm.
- Es útil para arquitecturas distribuidas y microservicios.

---

## 📊 Comparación de los tipos de redes

| Red | Característica principal | Alcance |
|---|---|---|
| 🔵 Bridge | Conecta contenedores entre sí. | Un host |
| 🟠 Host | Comparte la red del computador anfitrión. | Un host |
| 🔴 None | Aísla al contenedor de la red externa. | Sin conectividad externa |
| 🟢 Overlay | Conecta contenedores entre diferentes hosts. | Varios hosts |

## 💡 Conceptos importantes

- **Host:** computador o servidor donde se ejecuta Docker.
- **Contenedor:** entorno aislado donde se ejecuta una aplicación.
- **Red Docker:** permite establecer la comunicación entre contenedores.
- **Docker Swarm:** herramienta que permite administrar varios hosts Docker como un clúster.

### 🎯 Idea principal

Cada red tiene un propósito diferente:

- `Bridge`: comunicación entre contenedores en un mismo computador.
- `Host`: el contenedor comparte la red del computador.
- `None`: aislamiento de red externa.
- `Overlay`: comunicación entre contenedores distribuidos en diferentes computadores.

**Especialmente importante:** Overlay permite distribuir los servicios de una aplicación entre varios servidores sin perder la posibilidad de comunicación entre sus contenedores.
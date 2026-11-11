# 1.3 Arquitectura de Docker

## ⚙️ ¿Cómo funciona Docker?

Docker utiliza diferentes componentes que trabajan juntos para recibir instrucciones, administrar contenedores y obtener imágenes.

## 🧩 Componentes principales

| Componente | Función |
|---|---|
| **Docker Client** | Envía instrucciones mediante comandos. |
| **Docker Daemon** | Recibe las solicitudes y administra las operaciones. |
| **Docker API** | Permite la comunicación entre el Client y el Daemon. |
| **Docker Engine** | Conjunto de componentes que permite construir y ejecutar contenedores. |
| **Docker Registry** | Almacena y distribuye imágenes. |

## 🔄 ¿Cómo trabajan juntos?

Cuando ejecutamos:

```bash
docker run nginx
```

Ocurre lo siguiente:

1. **Client:** envía la instrucción.
2. **Daemon:** recibe la solicitud y administra la operación.
3. **Registry:** proporciona la imagen de Nginx si no está disponible localmente.
4. **Daemon:** crea e inicia el contenedor.

## 📊 Diagrama de funcionamiento

```text
          USUARIO
              │
              ▼
      ┌───────────────┐
      │ Docker Client │
      └───────┬───────┘
              │
          Docker API
              │
              ▼
      ┌───────────────┐
      │ Docker Daemon │
      └───────┬───────┘
              │
        ┌─────┴─────┐
        ▼           ▼
    REGISTRY     IMAGEN
        │           │
        └─────┬─────┘
              ▼
        CONTENEDOR
```

## 💡 Conceptos importantes

- **Imagen:** base que contiene lo necesario para crear un contenedor.
- **Contenedor:** instancia creada a partir de una imagen donde se ejecuta una aplicación.
- **Docker Engine:** motor que permite construir y ejecutar contenedores.

> **En resumen:** el Client envía las instrucciones, el Daemon administra las operaciones y el Registry proporciona las imágenes. Docker Engine reúne los componentes principales que hacen posible este funcionamiento.
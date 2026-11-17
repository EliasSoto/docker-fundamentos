# 🔌 Puertos en Docker

Los puertos permiten identificar los servicios que reciben comunicaciones de red. En Docker debemos distinguir entre los puertos del **host** y los del **contenedor**.

## 🖥️ 1. Puerto del host y del contenedor

- **Host:** nuestro computador donde se ejecuta Docker.
- **Contenedor:** entorno donde se ejecuta la aplicación.
- **Puerto:** identifica el servicio al que se dirige una comunicación.

Un contenedor puede utilizar el puerto `8000` sin que necesariamente esté disponible desde nuestro computador.

## 🌐 2. Publicación de puertos (`ports`)

Permite acceder desde el host a un servicio que se ejecuta dentro de un contenedor.

```yaml
ports:
  - "9000:8000"
```

**Formato:** `PUERTO_HOST:PUERTO_CONTENEDOR`

- `9000`: puerto de nuestro computador.
- `8000`: puerto donde escucha la aplicación dentro del contenedor.

Ejemplo: `http://localhost:9000`

## 📦 3. Exposición de puertos (`expose`)

Declara los puertos internos que utiliza un servicio dentro de Docker, sin publicarlos en el host.

```yaml
expose:
  - "5432"
```

Se utiliza principalmente como documentación de los puertos internos del servicio. No es obligatorio para que otros contenedores de la misma red puedan comunicarse con él.

## 📋 4. Diferencias

| Característica | `ports` | `expose` |
|---|---|---|
| Publica al host | Sí | No |
| Declara puertos internos | Sí | Sí |
| Comunicación entre contenedores | Sí | No es necesario |

# 🐳 Construcción y etiquetado de imágenes

## 🏗️ Construir imágenes

Utilizamos `docker build` para crear imágenes a partir de un Dockerfile.

```bash
docker build -t mi_api:1.0 .
```

- `-t`: asigna un nombre y una etiqueta (*tag*).
- `mi_api`: nombre de la imagen.
- `1.0`: versión de la imagen.
- `.`: contexto de construcción actual.

## 🏷️ Etiquetar imágenes

Utilizamos `docker tag` para crear una nueva referencia a una imagen existente, sin duplicarla.

```bash
docker tag mi_api:1.0 mi_api:2.0
```

Ambas etiquetas apuntan a la misma imagen y comparten sus capas.

## ☁️ Registry y Docker Hub

Un **Registry** es un servicio que permite almacenar y compartir imágenes Docker.

Docker Hub es uno de los más conocidos.

| Comando | Función |
|---|---|
| `docker push` | Sube una imagen al Registry. |
| `docker pull` | Descarga una imagen desde el Registry. |

Es similar a GitHub, pero orientado al almacenamiento y distribución de imágenes Docker.

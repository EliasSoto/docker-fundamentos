# 🐳 2.5 Administración de imágenes Docker

Las imágenes son plantillas utilizadas para crear contenedores. Docker permite descargarlas, listarlas, etiquetarlas y eliminarlas.

## 📌 Comandos principales

| Comando | Función |
|---|---|
| `docker pull ubuntu` | Descarga una imagen desde Docker Hub. |
| `docker images` | Lista las imágenes locales. |
| `docker tag ubuntu ubuntu:mi-version` | Asigna otra etiqueta a una imagen. |
| `docker rmi ubuntu` | Elimina una imagen local. |

## 🔍 Información de las imágenes

Al ejecutar `docker images` aparecen columnas como:

- **REPOSITORY:** nombre de la imagen.
- **TAG:** etiqueta o versión.
- **IMAGE ID:** identificador de la imagen.
- **SIZE:** tamaño.

## ⚙️ Ejemplo práctico

```powershell
# Descargar Ubuntu
docker pull ubuntu

# Etiquetar la imagen
docker tag ubuntu ubuntu:mi-version

# Listar imágenes
docker images

# Eliminar una etiqueta
docker rmi ubuntu:mi-version
```

## 💡 Importante

- `docker pull` descarga una imagen, pero no crea un contenedor.
- `docker tag` crea otra referencia a la misma imagen, no una copia independiente.
- `docker rmi` elimina una imagen o etiqueta local.
- No se puede eliminar una imagen mientras esté siendo utilizada por un contenedor.
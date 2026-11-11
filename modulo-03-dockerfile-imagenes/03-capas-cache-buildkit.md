# 🐳 Capas, caché y Multi-stage builds

## 📚 Capas (Layers)

Son los cambios que componen una imagen Docker. Se generan a partir de las instrucciones que modifican el sistema de archivos.

## ⚡ Caché de construcción

Docker guarda resultados de construcciones anteriores para reutilizarlos y evitar ejecutar nuevamente instrucciones que no han cambiado.

```powershell
# Consultar espacio utilizado por la caché
docker builder du

# Limpiar caché de construcción no utilizada
docker builder prune
```

## ⚙️ BuildKit

Es el motor moderno de construcción de Docker. Optimiza el proceso mediante:
- Reutilización de caché.
- Ejecución de tareas independientes en paralelo.
- Mejoras en el rendimiento y visualización del progreso.

## 🏗️ Multi-stage builds

Permite utilizar varias etapas dentro de un mismo Dockerfile.

- **Builder:** prepara y construye la aplicación.
- **Imagen final:** contiene solamente lo necesario para ejecutarla.

```dockerfile
# Etapa de construcción
FROM python:3.12 AS builder

# Etapa de ejecución
FROM python:3.12-slim
```

Se utiliza `COPY --from=builder` para copiar archivos desde una etapa anterior.

**Objetivo:** reducir el tamaño de las imágenes y evitar incluir herramientas innecesarias.

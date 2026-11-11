# 🐳 Laboratorio: Ciclo de vida de contenedores

## 🎯 Objetivo

Practicar la administración del ciclo de vida de un contenedor Docker mediante la imagen de **Nginx**, aprendiendo a crearlo, iniciarlo, detenerlo, pausarlo, consultar sus registros y eliminarlo.

## 🧪 Desarrollo del laboratorio

Se utilizó la imagen local de Nginx para realizar las siguientes operaciones:

1. **Crear y ejecutar:** se creó el contenedor `mi_servidor` en segundo plano.
2. **Pausar y reanudar:** se congelaron temporalmente sus procesos y luego se reanudaron.
3. **Detener e iniciar:** se detuvo el contenedor y se inició nuevamente sin crear otro.
4. **Reiniciar:** se reinició el mismo contenedor.
5. **Consultar logs:** se revisaron los registros de inicio de Nginx.
6. **Eliminar:** se detuvo y eliminó el contenedor. Finalmente, se comprobó que la imagen seguía almacenada localmente y se eliminó.

## 📋 Tabla de comandos

| Comando | Descripción |
|---|---|
| `docker run` | Crea e inicia un contenedor. |
| `docker create` | Crea un contenedor sin iniciarlo. |
| `docker start` | Inicia un contenedor detenido. |
| `docker stop` | Detiene un contenedor. |
| `docker restart` | Reinicia un contenedor. |
| `docker pause` | Congela temporalmente sus procesos. |
| `docker unpause` | Reanuda los procesos. |
| `docker ps` | Lista los contenedores activos. |
| `docker ps -a` | Lista todos los contenedores. |
| `docker logs` | Muestra los registros del contenedor. |
| `docker rm` | Elimina un contenedor. |
| `docker images` | Lista las imágenes locales. |
| `docker rmi` | Elimina una imagen local. |

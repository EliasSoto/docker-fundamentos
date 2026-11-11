# 🐳 2.4 Ejecutar comandos dentro de un contenedor

Docker permite ejecutar comandos dentro de un contenedor en funcionamiento mediante `docker exec`.

## 📌 Comandos principales

| Comando | Función |
|---|---|
| `docker exec nginx_lab ls` | Ejecuta un comando puntual. |
| `docker exec -it nginx_lab bash` | Abre una terminal interactiva. |
| `whoami` | Muestra el usuario actual. |
| `pwd` | Muestra el directorio actual. |
| `cd /etc` | Cambia de directorio. |
| `exit` | Cierra la sesión interactiva. |

## 🔍 Diferencia entre opciones

- `-i`: mantiene la entrada interactiva.
- `-t`: asigna una terminal.
- `bash`: inicia una terminal Bash.

## ⚙️ Ejecución interactiva

```bash
docker exec -it nginx_lab bash

whoami
pwd
cd /etc
exit
```

## 💡 Importante

- `docker exec` ejecuta comandos en un contenedor existente y en funcionamiento.
- `exit` cierra la sesión interactiva, pero no detiene el contenedor.
- `docker run` crea e inicia un contenedor nuevo, mientras que `docker exec` trabaja sobre uno existente.
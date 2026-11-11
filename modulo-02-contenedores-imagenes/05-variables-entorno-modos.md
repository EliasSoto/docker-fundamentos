# 🐳 2.6 Variables de entorno y modos de ejecución

## 📌 Variables de entorno (`-e`)

Permiten entregar valores a un contenedor al momento de crearlo.

```powershell
docker run -d --name prueba -e MI_VARIABLE=Hola ubuntu sleep 3600

# Consultar la variable
docker exec prueba printenv MI_VARIABLE
```

## ⚙️ Modos de ejecución

| Opción | Función |
|---|---|
| `-it` | Permite interactuar con el contenedor mediante una terminal. |
| `-d` | Ejecuta el contenedor en segundo plano (*detached*). |

**Ejemplos:**

```powershell
# Ejecución interactiva
docker run -it ubuntu bash

# Ejecución en segundo plano
docker run -d --name servidor nginx
```

## 🔍 Acceder a un contenedor activo

Aunque un contenedor se haya iniciado en segundo plano, podemos abrir una terminal dentro de él:

```powershell
docker exec -it servidor bash
```

Para salir de la terminal:

```bash
exit
```

## 💡 Importante

- `-e` define variables de entorno.
- `-it` permite interactuar mediante una terminal.
- `-d` ejecuta el contenedor en segundo plano.
- `docker exec -it` permite entrar a un contenedor que ya está funcionando.
- Cuando termina el proceso principal, el contenedor se detiene.
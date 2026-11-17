# 🧪 Laboratorio: Diagnóstico de redes Docker

## 🎯 Objetivo
Practicar la conectividad entre contenedores, el diagnóstico de redes, los conflictos de puertos y el aislamiento de red.

## 1. 🌐 Crear redes personalizadas

```bash
docker network create red_app
docker network create red_privada
```

Crear dos contenedores conectados a `red_app`:

```bash
docker run -dit --name servidor --network red_app alpine
docker run -dit --name cliente --network red_app alpine
```

Comprobar la conectividad:

```bash
docker exec cliente ping -c 4 servidor
```

Conectar `servidor` a una segunda red:

```bash
docker network connect red_privada servidor
```

Crear un tercer contenedor conectado únicamente a `red_privada`:

```bash
docker run -dit --name privado --network red_privada alpine
```

Comprobar que `cliente` no puede comunicarse directamente con `privado`:

```bash
docker exec cliente ping -c 4 privado
```

Inspeccionar las redes:

```bash
docker network inspect red_app
docker network inspect red_privada
```

## 2. 🔌 Diagnosticar conflictos de puertos

Crear el primer servidor web:

```bash
docker run -d --name web1 -p 8080:80 nginx
```

Intentar publicar el segundo contenedor en el mismo puerto:

```bash
docker run -d --name web2 -p 8080:80 nginx
```

El resultado esperado es el error `port is already allocated`, porque el puerto del host ya está ocupado.

Solucionar el conflicto utilizando otro puerto:

```bash
docker run -d --name web2 -p 8081:80 nginx
```

Comprobar ambos servidores desde el navegador:

```text
http://localhost:8080
http://localhost:8081
```

## 3. 🔒 Aislamiento de red con `none`

Crear un contenedor sin conectividad de red externa:

```bash
docker run -dit --name aislado --network none alpine
```

Comprobar que no tiene acceso a Internet:

```bash
docker exec aislado ping -c 4 8.8.8.8
```

Inspeccionar su configuración de red:

```bash
docker inspect aislado
```

Se pueden observar valores vacíos en campos como `Gateway`, `IPAddress` y `MacAddress`.

## 4. 🧹 Limpieza del laboratorio

Eliminar los contenedores creados:

```bash
docker rm -f servidor cliente privado web1 web2 aislado
```

Eliminar las redes personalizadas:

```bash
docker network rm red_app red_privada
```

## 💡 Conclusión

Este laboratorio permitió comprobar cómo Docker administra la comunicación entre contenedores, cómo resolver conflictos de puertos y cómo aislar servicios mediante diferentes configuraciones de red.
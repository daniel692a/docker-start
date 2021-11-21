# Primeros pasos con Docker
### ¿Qué es Docker?
La idea detrás de Docker es crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues. Docker.

Para que podamos acceder como usuarios normales a una aplicación, dicha aplicación software necesita estar **ejecutándose en una máquina**. Pero además, dependiendo del tipo de aplicación, dicho ordenador también necesita tener **instaladas una serie de cosas para que la aplicación se ejecute correctamente**: cierta versión de Java instalado, un servidor de aplicaciones, etc. Docker me permite meter en un contenedor (“una caja”) todas aquellas cosas que mi aplicación necesita para ser ejecutada (java, Maven, tomcat…) y la propia aplicación.
## Conceptos clave

* Image: es una especie de **plantilla**, una captura del **estado** de un contenedor. Las imágenes se utilizan para crear contenedores, y nunca cambian.
* Dockerfile: Es un **archivo de configuración** que se utiliza para crear *imágenes*. En dicho archivo indicamos qué es lo que queremos que tenga la imagen, y los distintos comandos para instalar las herramientas. Normalmente creamos imágenes **modificando otras imágenes padre**. Ejecutando el comando docker build sobre ese DockerFile, se nos creará la imagen correspondiente, lista para crear un contenedor.
* Containers: Son **instancias en ejecución** de una imagen. Son los que ejecutan cosas, los que ejecutarán nuestra aplicación. Si creas un contenedor a partir de una imagen, y mientras que se está ejecutando el contenedor cambias algo o instalas alguna herramienta, al parar dicho contenedor y después volver a ejecutar otra vez la misma imagen, esos cambios no se verán reflejados.
* Volumes: No es una buena práctica guardar los datos persistentes dentro de un contenedor de Docker. Para eso están los volúmenes, fuera de los contenedores. Así podremos crear y borrar contenedores sin preocuparnos por que se borren los datos. Además los volúmenes se utilizan para compartir datos entre contenedores.
* Links: Sirven para **enlazar contenedores** entre sí, que están **dentro de una misma máquina**, sin exponer a los contenedores cuáles son los datos de la máquina que los contiene.

## Correr/Ejecutar una imagen

```bash
docker run image
```

## Acceder al contenedor
```bash
docker run -it image bash
```

## Crear nuestra propia imagen
1. Crear un archivo Dockerfile
2. `docker build -t myimage:v1.0 .`
   > Construye nuestra imagen, -t nos permite asignar un tag con nombre_de_la_imagen:version
3. `docker image ls`
   > Nos muestra las imágenes que están en nuestra computadora
4. `docker run --name mycontainer -p 8000:80 myimage:v1.0`
    > Si requiere de un puerto para ver como servidor, se pone el parámetro -p y el puerto

**Borrar imágenes**: `docker system prune -af`

# Práctica 6.1 - Dockerización del despliegue de una aplicación Node.js

## Despliegue con Docker

Antes de comenzar con la práctica, vamos a conectarnos a nuestra máquina virtual a través de SSH.

![Screenshot_1](../assets/images/Practica%206.1/Screenshot_1.png) 

Una vez realizada la conexión, para poder realizar la práctica, tenemos que clonar un repositorio de github en nuestra Debian, por lo que vamos a hacerlo para tenerlo todo preparado.

![Screenshot_2](../assets/images/Practica%206.1/Screenshot_2.png) 

Y por último, vamos a instalar docker, para ello, primero hacemos update del apt, ya que si no, puede que tengamos errores al descargar docker. Tras esto, lo descargamos desde la propia consola de comandos.

![Screenshot_3](../assets/images/Practica%206.1/Screenshot_3.png) 

![Screenshot_4](../assets/images/Practica%206.1/Screenshot_4.png) 

Una vez ya instalado docker, vamos a ir al repositorio clonado, lugar donde encontraremos el dockerfile, el cual vamos a analizar.

![Screenshot_5](../assets/images/Practica%206.1/Screenshot_5.png) 

- Con **FROM** indicamos que vamos a utilizar la imagen de Docker Hub oficial de Node, en su versión 18.16.0 junto con Alpine, una diminuta distribución Linux.

- **RUN** ejecuta un comando en una nueva capa de la imagen (podemos tener varios comandos **RUN**).

- **WORKDIR** define el directorio sobre el que se ejecutarán las subsiguientes instrucciones del Dockerfile.

- **COPY** como su nombre indica, copia los archivos que le indiquemos dentro del contenedor, en este caso package.json
Recordemos que package.json cumplía ciertas funciones importantes:

    Centraliza la forma de interactuar con la aplicación por medio de definición de scripts (indica comandos que podemos correr dentro de nuestro proyecto, asociándolos a una palabra clave para que npm (o yarn) los reconozca cuando queramos ejecutarlos.)

    Gestiona de una forma clara y sencilla las dependencias necesarias para que la aplicación pueda funcionar correctamente.

- Con otro **RUN** ejecutamos el ya conocido comando que nos instala las dependencias que se indican en el archivo que hemos copiado en el paso anterior, el package.json.

- Con **COPY** copiamos todos los archivos de nuestro directorio /src al contenedor.

- **EXPOSE** nos permite documentar que puertos están expuestos o a la escucha en el contenedor (sólo será accesible desde otros contenedores).

- Y finalmente **CMD** nos permite ejecutar un comando dentro del contenedor. En este caso iniciamos la aplicación.

Una vez analizado el contenido de este archivo, vamos a hacer una build de la imagen de docker. Vamos a llamarla `librodirecciones` y le indicaremos tanto el nombre, como que haga la build con el contexto de nuestro directorio actual de trabajo, y el Dockerfile que se encuentra en él.

![Screenshot_6](../assets/images/Practica%206.1/Screenshot_6.png) 

![Screenshot_7](../assets/images/Practica%206.1/Screenshot_7.png) 

Tras esto, y ver que todo ha ido bien, vamos a iniciar el contenedor con nuestra aplicación. Gracias a la opción `-p`, vamos a poder indicar que se escuchen conexiones entrantes de cualquier maquina en nuestro puerto 3000 (La de la máquina anfitrión), que haremos que coincida con el puerto 3000 del contenedor (Por eso `-p 3000:3000`). Y con la opción de -d lo que haremos es que corra en modo demonio, en background.

![Screenshot_8](../assets/images/Practica%206.1/Screenshot_8.png) 

Ya lo hemos realizado, por lo que intentamos acceder con nuestra IP, y veremos que hay un error de conexión.

![Screenshot_9](../assets/images/Practica%206.1/Screenshot_9.png) 

Con esto comprobamos que los contenedores tienen su propia red, la aplicación por defecto va a intentar buscar la base de datos en nuestro localhost, pero realmente está en otro host, el de su contenedor.

Cada contenedor es un host diferente, por mucho que se corra en la misma máquina, y esto lleva a la aplicación a fallar cuando intenta conectar.

Podríamos solucionarlo utilizando comandos network del propio Docker, pero vamos a hacerlo con Docker Compose, una herramienta que nos permite administrar contenedores.

## Docker Compose

Como he mencionado antes, Docker Compose nos permite gestionar aplicaciones multicontenedor.

Vamos a instalar Docker Compose en nuestra máquina, a través de la consola de comandos.

![Screenshot_10](../assets/images/Practica%206.1/Screenshot_10.png) 

Comprobamos la versión y que está instalada correctamente de la siguiente manera.

![Screenshot_11](../assets/images/Practica%206.1/Screenshot_11.png) 

Ahora que tenemos nuestro Docker Compose instalado, vamos a ver un archivo YAML que utiliza Docker Compose para describir la aplicación, el cual es el siguiente.

![Screenshot_12](../assets/images/Practica%206.1/Screenshot_12.png) 

Viendo que efectivamente tenemos el archivo, para levantar la infraestructura basada en los contenedores es tan fácil como utilizar un comando.

![Screenshot_13](../assets/images/Practica%206.1/Screenshot_13.png) 

Gracias a esto, se crean las tablas necesarias en la base de datos, y ahora lo que haremos es construir nuestros contenedores a partir de las imágenes, con el siguiente comando.

![Screenshot_14](../assets/images/Practica%206.1/Screenshot_14.png) 

Una vez ya hemos construido las imágenes, podemos finalmente levantar los contenedores, realizando un test para comprobar que todo funciona correctamente.

![Screenshot_15](../assets/images/Practica%206.1/Screenshot_15.png) 

### Tarea

Probad que la aplicación junto con la BBDD funciona correctamente. El funcionamiento de la API es:

    GET /persons/all muestra todas las personas en el libro de direcciones
    GET /persons/1 muestra la persona con el id 1
    PUT /persons/ añade una persona al libro de direcciones
    DELETE /persons/1 elimina a la persona con el id 1

![Screenshot_16](../assets/images/Practica%206.1/Screenshot_16.png) 

Primero, añadimos a una persona al libro de direcciones.

```curl -X PUT http://localhost:3000/persons -H 'Content-Type: application/json' -d '{"id": 1, "firstName": "Raúl", "lastName": "Profesor"}'```

Ahora, vamos a listar a todas las personas en el libro de direcciones.

```curl -X GET http://localhost:3000/persons/all -H 'Content-Type: application/json'```

Buscaremos a la persona que hemos añadido con su ID en concreto (1)

```curl -X GET http://localhost:3000/persons/1 -H 'Content-Type: application/json'```

Finalmente, borraremos a la persona con un ID en concreto (1). Como se ve en la imagen, con el comando de listar a todas las personas comprobamos que efectivamente, se ha borrado.

```curl -X DELETE http://localhost:3000/persons/1 -H 'Content-Type: application/json'```
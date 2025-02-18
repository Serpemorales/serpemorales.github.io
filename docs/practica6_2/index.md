# Práctica 6.2 - Despliegue de una aplicación PHP con Nginx y MySQL usando Docker y docker-compose

Como ya es costumbre, antes de comenzar a realizar la práctica, vamos a conectarnos por SSH a nuestra máquina virtual.

![Screenshot_1](../assets/images/Practica%206.2/Screenshot_1.png) 

## Proceso de dockerización de Nginx+PHP+MySQL

### 1. Estructura de directorios

Antes de comenzar, vamos a definir la estructura de directorios que vamos a tener al finalizar la práctica. Lo suyo es que la dejemos ya creada por completo, así en cada paso iremos con más fluidez. Con los correspondientes comandos, creamos todo, asegurándonos de que quede de la siguiente manera.

![Screenshot_3](../assets/images/Practica%206.2/Screenshot_3.png) 

Eso lo hemos creado con los siguientes comandos.

![Screenshot_2](../assets/images/Practica%206.2/Screenshot_2.png) 

### 2. Creación de un contenedor Nginx

El primer paso es crear y correr un contenedor Nginx, para que así podamos alojar nuestra aplicación en PHP. Dentro de nuestra carpeta **practica6-2**, vamos a modificar el archivo `docker-compose.yml`, añadiendo lo siguiente.

![Screenshot_4](../assets/images/Practica%206.2/Screenshot_4.png) 

Una vez modificado y guardado, vamos a crear un contenedor con la última versión de la imagen de Nginx, este archivo será el encargado de descargarla, crear el contenedor y publicar o escuchar en el puerto 80 del contenedor, que es también el 80 de nuestra máquina. Iniciamos el proceso.

![Screenshot_5](../assets/images/Practica%206.2/Screenshot_5.png) 

Utilizando la opción `-d` indicamos que el contenedor se ejecute en segundo plano. Para comprobar que esta corriendo, podemos hacerlo con el siguiente comando.

![Screenshot_6](../assets/images/Practica%206.2/Screenshot_6.png) 

Como comprobación extra, desde la máquina anfitriona vamos a acceder a la IP de nuestra máquina virtual y podremos ver la página de bienvenida de Nginx.

![Screenshot_7](../assets/images/Practica%206.2/Screenshot_7.png) 

### 3. Creación de un contenedor PHP

Ahora vamos a ir a la carpeta `www/html` y modificaremos el archivo `index.php`

Quedará de la siguiente manera.

![Screenshot_8](../assets/images/Practica%206.2/Screenshot_8.png) 

Ahora vamos a guardar el archivo y dirigirnos a la carpeta nginx, para modificar el archivo de configuración `default.conf` con la siguiente configuración.

![Screenshot_9](../assets/images/Practica%206.2/Screenshot_9.png) 

En el mismo directorio de nginx, vamos a modificar el archivo Dockerfile de la siguiente manera.

![Screenshot_10](../assets/images/Practica%206.2/Screenshot_10.png) 

Y tras terminar esto, vamos a modificar el archivo `docker-compose.yml`.

![Screenshot_11](../assets/images/Practica%206.2/Screenshot_11.png)

Ahora que ya tenemos modificado el archivo `docker-compose.yml`, se creará un nuevo contenedor PHP-FPM en el puerto 9000, enlazará el contenedor nginx con el de php, y se creará un volumen que se va a montar en el directorio `/var/www/html`.

Vamos a ejecutar el contenedor, tenemos que asegurarnos siempre de que ejecutamos el comando donde esté nuestro archivo `docker-compose.yml`

![Screenshot_12](../assets/images/Practica%206.2/Screenshot_12.png)

Como antes, vamos a comprobar que los contenedores están ejecutados como es debido.

![Screenshot_13](../assets/images/Practica%206.2/Screenshot_13.png)

Y para una última comprobación, nos dirigimos a nuestra máquina anfitriona y comprobamos de nuevo la IP de nuestra máquina virtual, debiendo ver algo así.

![Screenshot_14](../assets/images/Practica%206.2/Screenshot_14.png)

### 4. Creación de un contenedor para datos

Antes hemos montado el directorio `www/html` en ambos contenedores, pero esto no es una manera adecuada de hacerlo. Por eso, vamos a hacer un contenedor independiente que se encargará de contener los datos, y lo enlazaremos con el resto de los contenedores.

Primer tenemos que editar de nuevo el archivo de `docker-compose.yml`.

![Screenshot_15](../assets/images/Practica%206.2/Screenshot_15.png)

Volvemos a realizar el comando para recrear y lanzar todos nuestros contenedores.

![Screenshot_16](../assets/images/Practica%206.2/Screenshot_16.png)

Y realizamos la correspondiente comprobación de que todo están corriendo adecuadamente.

![Screenshot_17](../assets/images/Practica%206.2/Screenshot_17.png)

### 5. Creación de un contenedor MySQL

Ahora vamos a crear un contenedor con una base de datos MySQL. Para ello, vamos a empezar modificando la imagen PHP e instalando la extensión de PHP para MySQL, para poder conectarnos desde nuestra aplicación PHP a la base de datos. Vamos a modificar el archivo Dockerfile del directorio php.

![Screenshot_18](../assets/images/Practica%206.2/Screenshot_18.png)

Volvemos a editar el archivo `docker-compose.yml`, para que se cree el contenedor para MySQL y el contenedor de los datos de MySQL en el que tendremos la base de datos y las tablas.

![Screenshot_19](../assets/images/Practica%206.2/Screenshot_19.png)

Cuando lo terminemos de modificar, vamos a editar también nuestro archivo `index.php`, para comprobar la conexión a la base de datos.

![Screenshot_20](../assets/images/Practica%206.2/Screenshot_20.png)

Una vez guardado, vamos a lanzar los contenedores, y verificar que se están ejecutando correctamente.

![Screenshot_21](../assets/images/Practica%206.2/Screenshot_21.png)

![Screenshot_22](../assets/images/Practica%206.2/Screenshot_22.png)

### 6. Verificación de conexión a la base de datos

Si accedemos a la IP de nuestra máquina virtual desde el navegador de la máquina anfitriona, veremos lo siguiente.

![Screenshot_23](../assets/images/Practica%206.2/Screenshot_23.png)

Esto se debe a que, a pesar de que si existen algunas tablas, no son visibles para un usuario normal. Para poder verlas, vamos a modificar el archivo `index.php` y vamos a cambiar lo siguiente, `$user por root` y `$password a secret`.

![Screenshot_24](../assets/images/Practica%206.2/Screenshot_24.png)

Tras guardarlo, vamos a refrescar la página en el navegador, y ya veremos que nos dan todas las tablas de la base de datos.

![Screenshot_25](../assets/images/Practica%206.2/Screenshot_25.png)

### 7. Esquema de la infraestructura completa de contenedores

En la siguiente imagen, podemos ver como se dividen los servicios en contenedores de Docker, para trabajar de forma independiente, pero a su vez todos conectados.

![Screenshot_26](../assets/images/Practica%206.2/Screenshot_26.jpg)
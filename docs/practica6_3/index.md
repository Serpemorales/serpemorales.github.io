# Práctica 6.3 - Despliegue de servidores web con usuarios autenticados mediante LDAP usando Docker y docker-compose

Como siempre, antes de comenzar a realizar la práctica, vamos a conectarnos por SSH a nuestra máquina virtual.

![Screenshot_1](../assets/images/Practica%206.3/Screenshot_1.png) 

## Despliegue con Docker de NGINX + demonio de autenticación LDAP + OpenLDAP

Para comenzar la práctica, tenemos que crear un directorio uqe contenga nuestro index.html, el cual tendrá un texto muy simple. Podemos crear todo de la siguiente manera.

![Screenshot_2](../assets/images/Practica%206.3/Screenshot_2.png) 

Ahora, vamos a comprobar que se ha creado correctamente, abriendo el archivo html

![Screenshot_3](../assets/images/Practica%206.3/Screenshot_3.png)

Una vez creado este directorio, vamos a crear otro, que va a contener el contenido de la configuración pertinente de Nginx

![Screenshot_4](../assets/images/Practica%206.3/Screenshot_4.png)

Volvemos a comprobar el archivo para ver que se ha creado correctamente

![Screenshot_5](../assets/images/Practica%206.3/Screenshot_5.png)

Para saber un poco de esta configuración, vamos a explicar lo que sucede en ella:

- Estamos pidiéndole que escuche peticiones HTTP en el puerto 8081, ya que el 8080 está ocupado por la práctica anterior.

- Le pedimos que cuando se acceda al sitio web, se solicite autorización den el directorio del sitio web que se llama */auth-proxy*.

- Se crea una nueva localización para ese directorio */auth-proxy*, que es donde se realizará la configuración de cómo conectarnos a nuestro openldap.

- Se indica también la URL de nuestro openldap.

- El DN base sobre el que se va a realizar las búsquedas en openldap

- El usuario y contraseña con el que nos vamos a poder conectar para realizar las consultas.

Una vez comprendido el contenido de este archivo, vamos a crear el `docker-compose.yml`.

![Screenshot_6](../assets/images/Practica%206.3/Screenshot_6.png)

Una vez creado, ejecutamos el compose y comprobar que podemos acceder a la IP de nuestra máquina virtual, utilizando el puerto 8081 y loguearnos en el servidor LDAP que hemos desplegado.

![Screenshot_7](../assets/images/Practica%206.3/Screenshot_7.png)

![Screenshot_8](../assets/images/Practica%206.3/Screenshot_8.png)

![Screenshot_9](../assets/images/Practica%206.3/Screenshot_9.png)

## Despliegue con Docker de PHP + Apache con autenticación LDAP

Ahora vamos a continuar trabajando en nuestro directorio `Practica6.3`, que es el directorio donde creamos los otros dos del punto anterior.

Lo primero es crear un `index.php`

![Screenshot_10](../assets/images/Practica%206.3/Screenshot_10.png)

Y ahora vamos a crear el directorio Docker, y dentro de el un archivo llamado Dockerfile, vamos a completarlo con las directivas adecuadas.

![Screenshot_11](../assets/images/Practica%206.3/Screenshot_11.png)

![Screenshot_12](../assets/images/Practica%206.3/Screenshot_12.png)

Una vez ya tenemos creado nuestro Dockerfile, vamos a crear un archivo llamado `ldap-demo.conf`, el cual es prácticamente la configuración LDAP. Aquí estableceremos los criterios de conexión con el contenedor de Openldap, password y URL.

Como veremos en la imagen, las directivas `PassEnv` nos permiten omitir las credenciales y pasarlas luego como variables de entorno cuando corramos la imagen del contenedor.

![Screenshot_13](../assets/images/Practica%206.3/Screenshot_13.png)

Ahora vamos a crear el archivo .htaccess.

![Screenshot_14](../assets/images/Practica%206.3/Screenshot_14.png)

Ahora vamos a construir la imagen, para poder correr el contenedor.

![Screenshot_15](../assets/images/Practica%206.3/Screenshot_15.png)

Una vez ya creado, vamos a correr el contenedor indicando las credenciales de nuestra cuenta LDAP mediante la flag `-e`. Vamos a probarlo con un servidor LDAP externo, como si integrásemos nuestro despliegue con un servidor ya existente de la empresa.

Vamos a utilizar un servidor público en Internet.

![Screenshot_16](../assets/images/Practica%206.3/Screenshot_16.png)

Ahora que está todo operativo, vamos a acceder desde nuestra máquina, utilizando la IP de la máquina virtual y el puerto 3000.

Vemos que al loguearnos, todo está correcto.

![Screenshot_17](../assets/images/Practica%206.3/Screenshot_17.png)

![Screenshot_18](../assets/images/Practica%206.3/Screenshot_18.png)

Con esto, damos por finalizada la práctica.



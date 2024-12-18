## PRACTICA DE AMPLIACIÓN

En esta práctica, vamos a configurar un servidor Nginx con unos hosts virtuales en los que podamos alojar distintos sitios webs pero utilizando solo un servidor. También, tenemos que lograr que cada host virtual apunte al directorio `public_html` de distintos usuarios en nuestro sistema operativo. Así, cada uno podrá gestionar su web desde su carpeta personal.

Antes de comenzar, vamos a conectarnos a nuestra máquina virtual mediante **SSH**.

![Screenshot_1](../assets/images/Practica%202.6/Screenshot_1.png)

### 1. Instalación de Nginx

El primer paso sería instalar Nginx. En mi caso personal, ya tengo todo instalado de prácticas anteriores, y se puede ver en la **práctica 2.1** el paso a paso. Aún así, en resumidas cuentas, sería tan sencillo instalarlo con el gestor de paquetes utilizando los siguientes comandos:

``sudo apt-get update``

``sudo apt-get install nginx``

Para comenzar todo, voy a comprobar que mi Nginx funciona correctamente, para ello miramos su *status* y vemos si lo podemos ver en el navegador web.

![Screenshot_2](../assets/images/Practica%202.6/Screenshot_2.png)

![Screenshot_3](../assets/images/Practica%202.6/Screenshot_3.png)

### 2. Creación de usuarios

Para poder realizar la práctica, vamos a tener que crear al menos 2 usuarios distintos. Para ello, utilizando el comando *useradd* como veremos en la imagen, creamos dos usuarios, y les asignamos una contraseña con el comando *passwd*

En las imágenes podemos observar el proceso, el cual es sencillo.

![Screenshot_4](../assets/images/Practica%202.6/Screenshot_4.png)

En mi caso, he creado los usuarios **momo** y **alicia**, a parte del mio personal que ya estaba creado.

### 3. Estructura de carpetas

Ahora que tenemos nuestros usuarios creados, tenemos que crearle a cada uno una carpeta *public_html*, asegurándonos de darle los permisos necesarios para que Nginx pueda acceder a estas, pero sin hacer que el usuario pierda sus permisos. Para ello, vamos a loguearnos con los nuevos usuarios, con el comando *su usuario*

Para el usuario **momo**, sería de la siguiente manera

![Screenshot_5](../assets/images/Practica%202.6/Screenshot_5.png)

Como vemos, se ha creado el directorio, y con los correspondientes comandos que se ven en la imagen, se pueden poner los permisos.

Vamos a realizar lo mismo, pero con el usuario **alicia**

![Screenshot_6](../assets/images/Practica%202.6/Screenshot_6.png)

Una vez creadas las carpetas y asignados los correspondientes permisos, vamos con cada usuario a crear dentro de esta un archivo **index.html** donde realizaremos una web sencilla. En el caso de **momo**, ha sido esta sencilla web

![Screenshot_7](../assets/images/Practica%202.6/Screenshot_7.png)

![Screenshot_8](../assets/images/Practica%202.6/Screenshot_8.png)

Y para el caso del usuario **alicia**, hemos repetido el mismo proceso, de manera que nos queda la web de la siguiente manera

![Screenshot_9](../assets/images/Practica%202.6/Screenshot_9.png)

![Screenshot_10](../assets/images/Practica%202.6/Screenshot_10.png)

Aprovechando que estamos aún con los usuarios, vamos a crear para cada uno de ellos el certificado de seguridad para la web. Para ello, tenemos que irnos a nuestro usuario principal, **sergio** en mi caso, y generarlos con el siguiente comando.

``sudo openssl req -x509 -newkey rsa:4096 -keyout /etc/ssl/private/usuario.pem -out /etc/ssl/certs/usuario.pem -sha256 -days 365 -nodes``

El de **momo** lo generamos primero, cuando nos pregunte common name, ponemos el de nuestra web.

![Screenshot_11](../assets/images/Practica%202.6/Screenshot_11.png)

Después, creamos el de **alicia**, así cada usuario tendrá su propio certificado de seguridad.

![Screenshot_14](../assets/images/Practica%202.6/Screenshot_14.png)

Una vez realizado esto, seguimos con la configuración de los host

### 4. Configuración de los Host

Para empezar a configurar, tenemos que trasladarnos a la carpeta ``sites-available`` de nginx.

![Screenshot_13](../assets/images/Practica%202.6/Screenshot_13.png)

Una vez dentro, vamos a crear dos archivos, uno será para **momo.es** de la usuaria **momo**, el otro será para **alicia.es** de la usuaria **alicia**. Tras realizarlos, quedarían de esta manera.

![Screenshot_15](../assets/images/Practica%202.6/Screenshot_15.png)

En mi caso, como ya he generado los certificados, he realizado también la re-dirección a ``HTTPS``. Si nos fijamos en la imagen, el root es el *public_html* que realizamos anteriormente, mientras que el certificado ssl son los que he generado en el paso anterior. Una vez configurado el primero, hacemos lo mismo con el segundo

![Screenshot_16](../assets/images/Practica%202.6/Screenshot_15.png)

Para que los hosts se activen y funcionen, tenemos que realizar el enlace entre ``sites-available`` y ``sites-enabled``, para ello, simplemente utilizamos el comando *ln* de la siguiente manera.

![Screenshot_17](../assets/images/Practica%202.6/Screenshot_17.png)

Una vez realizada, vamos a reiniciar Nginx para ver que todo funciona correctamente y se guarden los cambios.

![Screenshot_18](../assets/images/Practica%202.6/Screenshot_18.png)

### 5. Comprobaciones

Ahora ya tenemos nuestras webs listas, pero si queremos visualizarlas correctamente, tendremos que añadirlas a nuestro archivo ``host`` del sistema operativo, utilizando la ip de nuestra máquina virtual y añadiendo las webs de nuestros usuarios.

![Screenshot_19](../assets/images/Practica%202.6/Screenshot_19.png)

Ahora ya podemos visitar las webs, ambas nos advertirán de que hay riesgo potencial de seguridad. Al ser una práctica, no tenemos que preocuparnos de esto, por lo que avanzaremos hacia la web, viendo que se ve lo que hicimos en el ``public_html``. Además, para una comprobación mas exacta, podemos ir a ver los certificados, viendo que cada web tiene el suyo tal y como los generamos anteriormente.

#### Web de Alicia

![Screenshot_20](../assets/images/Practica%202.6/Screenshot_20.png)

![Screenshot_21](../assets/images/Practica%202.6/Screenshot_21.png)

![Screenshot_22](../assets/images/Practica%202.6/Screenshot_22.png)

#### Web de Momo

![Screenshot_23](../assets/images/Practica%202.6/Screenshot_23.png)

![Screenshot_24](../assets/images/Practica%202.6/Screenshot_24.png)

![Screenshot_25](../assets/images/Practica%202.6/Screenshot_25.png)

Como podemos comprobar, ambas se ven correctamente y tienen su certificado, por lo que todo ha salido bien, y con ello, concluye la práctica.
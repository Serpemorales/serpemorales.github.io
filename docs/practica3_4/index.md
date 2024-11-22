# Práctica 3.4: Despliegue de una aplicación Flask (Python)

## Procedimiento completo para el despliegue

Vamos a comenzar a realizar el procedimiento para poder desplegar la aplicación Flask. Vamos a comenzar instalando el gestor de paquetes de Python pip.

![Screenshot_1](../assets/images/Practica%203.4/Screenshot_1.png) 

Cuando hemos instalado este gestor de paquetes, ya podemos instalar el paquete pipenv, el cual nos va a servir para gestionar nuestros entornos virtuales, necesarios para esta práctica.

![Screenshot_2](../assets/images/Practica%203.4/Screenshot_2.png) 

Comprobamos que se ha instalado correctamente, mostrando su versión en consola, y acto seguido tras comprobarlo, creamos un directorio para almacenar nuestro proyecto.

![Screenshot_3](../assets/images/Practica%203.4/Screenshot_3.png) 

![Screenshot_4](../assets/images/Practica%203.4/Screenshot_4.png) 

Como hemos creado el directorio con sudo, los permisos de este directorio van a pertenecer a root. Vamos a cambiarlo, pues es importante para que Nginx no de errores al acceder a la aplicación.

![Screenshot_5](../assets/images/Practica%203.4/Screenshot_5.png) 

![Screenshot_6](../assets/images/Practica%203.4/Screenshot_6.png) 

Una vez ya asignados los permisos, vamos a crear un archivo oculto .env, dentro vamos a poner todas las variables de entorno necesarias. Por eso, tras crearlo, vamos a editar el archivo y añadirlas, indicando el archivo py y el entorno.

![Screenshot_7](../assets/images/Practica%203.4/Screenshot_7.png) 

![Screenshot_8](../assets/images/Practica%203.4/Screenshot_8.png) 

Ya con este archivo creado, vamos a iniciar nuestro entorno virtual, y podremos comprobar si se ha iniciado correctamente mirando el nombre antes de nuestro usuario.

![Screenshot_9](../assets/images/Practica%203.4/Screenshot_9.png) 

Ya en nuestro entorno virtual, vamos a instalar las dependencias necesarias para el proyecto, de una manera muy sencilla.

![Screenshot_10](../assets/images/Practica%203.4/Screenshot_10.png) 

Ahora vamos a crear la aplicación Flask, vamos a crear un archivo que contendrá la aplicación como tal, que será application.py, y crearemos también wsgi.py, que se encargará de iniciar esta aplicación.

![Screenshot_11](../assets/images/Practica%203.4/Screenshot_11.png) 

![Screenshot_12](../assets/images/Practica%203.4/Screenshot_12.png) 

Una vez creados estos archivos y editados, vamos a correr la aplicación, utilizando en nuestra aplicación http://IPmaquinavirtual:5000 para poder acceder. Comprobamos que todo este correcto, mostrándose en pantalla.

![Screenshot_13](../assets/images/Practica%203.4/Screenshot_13.png) 

![Screenshot_14](../assets/images/Practica%203.4/Screenshot_14.png) 

Bien, ya hemos comprobado que funciona, ahora comprobaremos que Gunicorn funciona, utilizando un comando para probar esta aplicación, accediendo al navegador de la misma manera, y comprobando si vemos el mensaje por pantalla.

![Screenshot_15](../assets/images/Practica%203.4/Screenshot_15.png) 

![Screenshot_16](../assets/images/Practica%203.4/Screenshot_16.png) 

Gunicorn funciona, por lo que aún estando en el entorno virutal, vamos a tomar nota de la ruta desde la que ejecutamos gunicorn, porque mas adelante será necesaria.

![Screenshot_17](../assets/images/Practica%203.4/Screenshot_17.png) 

Ahora tendríamos que instalar Nginx, en nuestro caso lo teníamos de prácticas anteriores, pero nos aseguramos de que este en correcto funcionamiento, pues vamos a necesitarlo para el resto de la práctica.

![Screenshot_18](../assets/images/Practica%203.4/Screenshot_18.png) 

Saldremos del entorno virutal, y vamos a crear un archivo para que systemd corra nuestro Gunicorn como si fuese otro servicio del sistema. Es importante rellenar bien todos los datos necesarios con los nuestros.

![Screenshot_19](../assets/images/Practica%203.4/Screenshot_19.png) 

Tras crearlo, procedemos a la activación del servicio, y lo iniciamos para que esté activo.

![Screenshot_20](../assets/images/Practica%203.4/Screenshot_20.png) 

Ahora vamos a configurar nuestro Nginx, al igual que en prácticas anteriores, vamos a dirigirnos a sites-available, lugar donde crearemos nuestro archivo y lo editaremos de la siguiente manera. Es importante que tras crearlo, realicemos el link simbólico.

![Screenshot_21](../assets/images/Practica%203.4/Screenshot_21.png) 

![Screenshot_22](../assets/images/Practica%203.4/Screenshot_22.png) 

Si queremos asegurarnos de que el link se ha creado correctamente, podemos hacerlo de la siguiente manera.

![Screenshot_23](../assets/images/Practica%203.4/Screenshot_23.png) 

También vamos a asegurarnos de que Nginx no contiene errores, y tras eso, si todo está correcto, vamos a reiniciarlo y comprobar que sigue activo.

![Screenshot_24](../assets/images/Practica%203.4/Screenshot_24.png) 

Ahora ya no podemos utilizar la IP como antes para acceder, ahora necesitamos acceder por el server_name. Para poder hacerlo, vamos a tener que ir al archivo hosts de nuestra máquina anfitriona, y editarlo para que quede de la siguiente manera.

![Screenshot_25](../assets/images/Practica%203.4/Screenshot_25.png) 

Ya con estos cambios, podemos acceder desde el navegador y comprobar que se despliega correctamente.

![Screenshot_26](../assets/images/Practica%203.4/Screenshot_26.png) 

## Procedimiento completo para el despliegue con repositorio

Ahora vamos a repetir todo el proceso, pero con una aplicación que copiaremos desde un repositorio de github. Lo vamos a clonar en nuestro directorio /var/www

![Screenshot_27](../assets/images/Practica%203.4/Screenshot_27.png) 

Al igual que antes, vamos a dar los permisos adecuados para la carpeta, para que Nginx no tenga errores.

![Screenshot_28](../assets/images/Practica%203.4/Screenshot_28.png) 

Ahora vamos a crear y activar nuestro entorno virtual de la misma manera que antes. Además, una vez activado, vamos a instalar las dependecias del proyecto de la aplicación.

![Screenshot_29](../assets/images/Practica%203.4/Screenshot_29.png) 

![Screenshot_30](../assets/images/Practica%203.4/Screenshot_30.png) 

Ya tras esto, vamos a instalar las dependecias restantes necesarias.

![Screenshot_31](../assets/images/Practica%203.4/Screenshot_31.png) 

Ahora no necesitamos crear una aplicación flask, por lo que simplemente creamos el wsgi.py igual que antes, pero en lugar de poner "from application import app" simplemente poner "from app import app". Al igual que antes, inicializamos para comprobar que todo va bien, tanto desde el servidor web integrado de Flask como de Gunicorn. Recordar también apuntar la ruta de Gunicorn.

![Screenshot_32](../assets/images/Practica%203.4/Screenshot_32.png) 

Ya realizado esto, vamos a seguir con los pasos para utilizar Nginx. Al igual que antes, vamos a crear un servicio para que Gunicorn sea un servicio del sistema más, esta vez con la nueva ruta de Gunicorn

![Screenshot_33](../assets/images/Practica%203.4/Screenshot_33.png) 

![Screenshot_36](../assets/images/Practica%203.4/Screenshot_36.png) 

Una vez creado, habilitado e iniciado el servicio, vamos a ir a a sites-available de nuestro Nginx, creando un archivo propio. Desvinculamos el anterior para asegurarnos de que no hay fallos.

![Screenshot_34](../assets/images/Practica%203.4/Screenshot_34.png) 

Recordad crear el enlace simbólico de nuevo y reiniciar nginx. Cuando vamos que todo está correcto, tenemos que volver a editar el archivo hosts de nuestra máquina anfitriona, si no no podremos acceder.

![Screenshot_35](../assets/images/Practica%203.4/Screenshot_35.png) 

Ya con nuestro enlace, accedemos a el desde el navegador, para ver que efectivamente, funciona correctamente.

![Screenshot_37](../assets/images/Practica%203.4/Screenshot_37.png)

## Cuestiones


> Cuestion 1
> Busca, lee, entiende y explica qué es y para que sirve un servidor WSGI

Un servidor WSGI es básicamente una especificación que define como debe comunicarse un servidor web con una aplicación Python, de manera que se facilite la interacción entre ambas. Actúa como puente y mejora la compatibilidad entre ellas, y además es un componente clave para el despliegue de aplicaciones web Python en producción. Su principal beneficio al final es la capacidad que tiene para permitir que las aplicaciones Python se puedan ejecutar en diferentes servidores web sin necesidad de que estos entiendan directamente el código Python, asegurando que las aplicaciones sean mas portables.








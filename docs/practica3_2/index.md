# Práctica 3.2: Despliegue de aplicaciones con Node Express

## Instalación de Node.js, Express y test de la primera aplicación

Antes de comenzar, vamos a desactivar Tomcat para evitar problemas.

![Screenshot_1](../assets/images/Practica%203.2/Screenshot_1.png) 

Tras esto, procedemos con la práctica, y vamos a tener que instalar tanto Node.js como Express. Después crearemos un archivo js y comprobaremos que nuestro primer despliegue funciona correctamente. Lo primero es instalar Node.JS, y empezamos con un update y upgrade de apt

![Screenshot_2](../assets/images/Practica%203.2/Screenshot_2.png) 

![Screenshot_3](../assets/images/Practica%203.2/Screenshot_3.png) 

Una vez realizado esto, vamos ha añadir un el repositorio de NodeJS con el siguiente comando.

![Screenshot_4](../assets/images/Practica%203.2/Screenshot_4.png) 

Ahora, podemos instalar NodeJS y comprobar que la instalación es satisfactoria

![Screenshot_5](../assets/images/Practica%203.2/Screenshot_5.png) 

![Screenshot_6](../assets/images/Practica%203.2/Screenshot_6.png) 

Una vez hecho esto, vamos con ExpressJS. Primero lo instalamos

![Screenshot_7](../assets/images/Practica%203.2/Screenshot_7.png) 

Y después vamos a crear una carpeta para el proyecto, donde vamos a inicializarlo e instalarle express.

![Screenshot_8](../assets/images/Practica%203.2/Screenshot_8.png) 

![Screenshot_9](../assets/images/Practica%203.2/Screenshot_9.png) 

Una vez seguidos estos sencillos pasos, vamos a crear un archivo de prueba llamado app.js, añadiendo lo siguiente

![Screenshot_10](../assets/images/Practica%203.2/Screenshot_10.png)

Vamos a comprobar que todo ha ido bien, yendo al navegador y indicando nuestra ip seguida de :3000

![Screenshot_11](../assets/images/Practica%203.2/Screenshot_11.png)

## Despliegue de una nueva aplicación

Ahora vamos a realizar un despliegue de una aplicación de terceros, vamos a empezar clonando el repositorio de github correspondiente

![Screenshot_12](../assets/images/Practica%203.2/Screenshot_12.png)

Nos movemos al nuevo directorio creado, instalamos las librerías necesarias y iniciamos la aplicación

![Screenshot_13](../assets/images/Practica%203.2/Screenshot_13.png)

![Screenshot_14](../assets/images/Practica%203.2/Screenshot_14.png)

![Screenshot_15](../assets/images/Practica%203.2/Screenshot_15.png)

Como vemos, nos sale un error en el que nodemon no se encuentra, para solucionar el problema es tan sencillo como instalarlo, de la siguiente manera

![Screenshot_16](../assets/images/Practica%203.2/Screenshot_16.png)

Una vez instalado, podemos ir a nuestra IP:3000 y ver como efectivamente, se ha desplegado

![Screenshot_17](../assets/images/Practica%203.2/Screenshot_17.png)

## Cuestiones

Cuando ejecutamos el comando npm run start, lo que estamos haciendo es ejecutar un script:

**¿Donde podemos ver que script se está ejecutando?**

Podemos verlo dentro del archivo package.json, concretamente dentro del objeto scripts.

**¿Que comando está ejecutando?**

Se ejecuta el comando node server.js


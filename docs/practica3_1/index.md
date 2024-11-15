# Práctica 3.1: Instalación de Tomcat

## Instalación de Tomcat

Lo primero va a ser instalar nuestro Tomcat, la manera más recomendable es con el administrador de paquetes, siguiendo algún tutorial online. No debería darnos demasiados problemas, hasta comprobar que se ha instalado correctamente

![Screenshot_1](../assets/images/Practica%203.1/Screenshot_1.png) 

Una vez instalado, vamos a nuestra URL para ver que se visualiza de forma correcta, entrando con el usuario y contraseña que hemos elegido.

![Screenshot_2](../assets/images/Practica%203.1/Screenshot_2.png) 

## Despliegue manual mediante la GUI de administración

Ahora vamos a probar a realizar un despliegue manual de una aplicación empaquetada en formato WAR, para ello, en la página que hemos visto antes, buscamos la sección que permite desplegar el WAR, seleccionando nuestro archivo

![Screenshot_3](../assets/images/Practica%203.1/Screenshot_3.png) 

Tras esto, le damos a desplegar, y ya nos saldrá como un directorio más al que tendremos acceso

![Screenshot_4](../assets/images/Practica%203.1/Screenshot_4.png) 

## Despliegue con Maven

**Instalación de Maven**

Ahora vamos a realizar un despliegue con Maven, pero primero, vamos a instalarlo. Yo lo haré mediante el gestor de paquetes APT, y para ello, empezaremos con una actualización de los repositorios 

![Screenshot_5](../assets/images/Practica%203.1/Screenshot_5.png) 

Después, si ha ido todo correcto, vamos a instalar Maven

![Screenshot_6](../assets/images/Practica%203.1/Screenshot_6.png) 

y para finalizar, vamos a comprobar que se instaló de manera adecuada con el siguiente comando

![Screenshot_7](../assets/images/Practica%203.1/Screenshot_7.png) 

**Configuración de Maven**

Para que podamos realizar los despliegues, vamos a tener que hacer una correcta configuración.

Vamos a comenzar añadiendo roles a nuestro usuario en Tomcat, es importante y bastante recomendable que los roles manager-script/manager-jmx no los tenga el mismo usuario que tenga el rol de manager-gui, por eso en mi caso, voy a separarlos.

En el archivo tomcat-users.xml, vamos a modificar de manera que quede así

![Screenshot_8](../assets/images/Practica%203.1/Screenshot_8.png) 

Tras esto, nos toca editar el archivo de maven, dentro de la carpeta, estará settings.xml, aquí tenemos que poner un identificador para el servidor sobre el que vamos a desplegar y las credenciales, importante que todo sea dentro del bloque servers del XML

![Screenshot_9](../assets/images/Practica%203.1/Screenshot_9.png) 

Por último, vamos a modificar el POM del proyecto para hacer referencia a que el despliegue se realice con el plugin de Maven para Tomcat, en mi caso, he utilizado el de rock paper scissors que nos ha proporcionado la propia práctica. Clonando el repositorio y modificando su correspondiente archivo POM, añadiendo un bloque nuevo al final.

![Screenshot_10](../assets/images/Practica%203.1/Screenshot_10.png) 

![Screenshot_11](../assets/images/Practica%203.1/Screenshot_11.png) 

**Despliegue**

Una vez hecho esto, reiniciamos tomcat para que pille bien las configuraciones, y así nos preparamos para desplegar nuestra aplicación

![Screenshot_12](../assets/images/Practica%203.1/Screenshot_12.png) 

Vamos a utilizar el comando `mvn tomcat7:deploy`

![Screenshot_13](../assets/images/Practica%203.1/Screenshot_13.png) 

Si vemos que hace deploying en nuestra url y que pone BUILD SUCCESS, es porque se ha desplegado con éxito. Podemos ir a la pagina de Tomcat para ver que efectivamente, esta ahí

![Screenshot_14](../assets/images/Practica%203.1/Screenshot_14.png) 

Y si pulsamos, está de manera totalmente funcional

![Screenshot_15](../assets/images/Practica%203.1/Screenshot_15.png) 

## Cuestiones

**Cuestión 1**

> Habéis visto que los archivos de configuración que hemos tocado
> contienen contraseñas en texto plano, por lo que cualquiera con acceso
> a ellos obtendría las credenciales de nuestras herramientas.
> 
> En principio esto representa un gran riesgo de seguridad, ¿sabrías
> razonar o averiguar por qué esto está diseñado de esta forma?

  
El diseño de herramientas como Tomcat asume que la seguridad de los archivos de configuración recae en las prácticas de administración del sistema y los permisos del entorno. Por ejemplo, en Tomcat se espera que los archivos de configuración, como `tomcat-users.xml`, sean accesibles únicamente por el usuario que ejecuta el servidor y por root

Mantener contraseñas en texto plano simplifica la configuración y asegura la compatibilidad con estándares, pero también se basa en que el administrador del sistema configure permisos estrictos y garantice que el entorno sea seguro.

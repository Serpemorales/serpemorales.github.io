# Práctica 2.3 - Proxy Inverso con Nginx

## Clonación de Máquina Virtual

Primero vamos a tener que clonar la Máquina Virtual para así tener dos servidores, el que ya teníamos de antes, y el del proxy. Es muy importante que generemos nuevas direcciones MAC en esta clonación.

![Screenshot_1](../assets/images/Practica%202.2/Screenshot_1.png) 

Una vez tengamos las dos máquinas, ya podemos empezar.

![Screenshot_2](../assets/images/Practica%202.2/Screenshot_2.png) 

## Configuración Máquina Principal

**AVISO: Recordar a la hora de probar todo en el navegador desactivar la caché o utilizar ventana privada.**

Para preparar la máquina principal, vamos a cambiar el nombre de nuestra web ya creada por `webserver`, y para ello tenemos que cambiar su nombre en todos los archivos que sean necesarios. Además, haremos que el servidor en lugar de escuchar el puerto 80 escuche el 8080.

![Screenshot_3](../assets/images/Practica%202.2/Screenshot_3.png) 

Tras este cambio, es necesario que deshagamos el link simbólico antiguo, y creemos uno nuevo, reiniciando tras esto Nginx.

![Screenshot_4](../assets/images/Practica%202.2/Screenshot_4.png) 


## Configuración Máquina Proxy


Ahora tenemos que configurar esta máquina para poder acceder al proxy por nuestra web. Para ello, vamos a crear en *sites-avalaible* un nuevo archivo, configurándolo de la siguiente forma.

![Screenshot_5](../assets/images/Practica%202.2/Screenshot_5.png) 

Como se ve, en mi caso le he añadido ya el header, pero no es necesario por ahora.

Tras esto, vamos a realizar el link simbólico y a reiniciar nginx en esta máquina, para dejar todo a punto .

![Screenshot_6](../assets/images/Practica%202.2/Screenshot_6.png) 

Es importante que modifiquemos también el archivo hosts, añadiendo la IP de la máquina que hace de proxy.

![Screenshot_7](../assets/images/Practica%202.2/Screenshot_7.png) 

## Comprobaciones

Dentro del navegador, si accedemos a las herramientas de desarrollador (En el caso de Firefox con *F12*) podremos comprobar que el estado sea 200 OK, indicando que todo está correcto.

![Screenshot_8](../assets/images/Practica%202.2/Screenshot_8.png) 

## Añadir cabecera

Como indiqué antes, ahora vamos a añadir una cabecera, de esta manera podemos demostrar de forma más clara que la petición pasa por el proxy inverso y después llega al servidor web por el mismo camino.

![Screenshot_9](../assets/images/Practica%202.2/Screenshot_9.png) 

Tras hacerlo en el proxy, lo haremos también en el del servidor web, de manera que quedaría así.

![Screenshot_10](../assets/images/Practica%202.2/Screenshot_10.png) 

Es importante que sean nombres distintos, para que sepamos identificar bien cual es cada uno. En mi caso el del proxy se ha llamado `Proxy_inverso_sergio` y el del servidor web se ha llamado `servidor_web_sergio`.

Ahora abrimos de nuevo la web, y volvemos a usar las herramientas de desarrollador de Firefox. Si todo va bien, podremos ver en la cabecera ambos host, de esta manera.

![Screenshot_11](../assets/images/Practica%202.2/Screenshot_11.png) 

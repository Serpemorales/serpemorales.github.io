# Práctica 2.4 - Balanceo de carga con proxy inverso en Nginx

## Preparación

Primero vamos a conectarnos con el SSH a nuestra máquina.

![Screenshot_1](../assets/images/Practica%202.4/Screenshot_1.png) 

Y una vez conectados, vamos a desvincular los sitios web de las prácticas anteriores, para así evitar problemas.

![Screenshot_2](../assets/images/Practica%202.4/Screenshot_2.png) 

Este proceso lo realizaremos con el resto de máquinas también.

## Nginx Servidor Web 1

**AVISO: Recordar a la hora de probar todo en el navegador desactivar la caché o utilizar ventana privada.**

Primero, vamos a crear en el primer servidor un nuevo directorio llamado webserver1, con su correspondiente carpeta HTML.

![Screenshot_3](../assets/images/Practica%202.4/Screenshot_3.png) 

Tras esto, vamos a crear el archivo HTML, que se verá de la siguiente manera. En el servidor 2 será igual, pero cambiando el web 1 por 2.

![Screenshot_4](../assets/images/Practica%202.4/Screenshot_4.png) 

Una vez realizada esa configuración, vamos a crear el webserver1, en mi caso, he copiado el webserver anterior para hacerlo mas fácil, cambiando el archivo con las configuraciones nuevas.

![Screenshot_5](../assets/images/Practica%202.4/Screenshot_5.png) 

![Screenshot_6](../assets/images/Practica%202.4/Screenshot_6.png) 

Una vez hecho esto, volvemos a hacer el link, y ya podremos pasar al segundo servidor.

![Screenshot_7](../assets/images/Practica%202.4/Screenshot_7.png) 

## Nginx Servidor Web 2

Vamos a clonar el servidor 1, asegurándonos de que tiene una IP distinta al primero.

![Screenshot_8](../assets/images/Practica%202.4/Screenshot_8.png) 

Como tenemos que modificar todo lo del servidor 1, cambiamos el nombre de webserver1 a webserver2

![Screenshot_9](../assets/images/Practica%202.4/Screenshot_9.png) 

Cambiamos también el archivo HTML, de manera que se muestre que es el servidor 2
.
![Screenshot_10](../assets/images/Practica%202.4/Screenshot_10.png) 

Y cambiamos el archivo de webserver2, dejando todo igual que el primero, pero cambiando el 1 por el 2. Al igual que antes, volvemos a hacer el proceso de vinculación y reiniciamos en nginx.

![Screenshot_11](../assets/images/Practica%202.4/Screenshot_11.png)

![Screenshot_12](../assets/images/Practica%202.4/Screenshot_12.png) 

## Nginx Proxy Inverso

En el caso del proxy, tenemos que configurarlo para que realice el reparto de peticiones entre ambos servidores. En sites-available, vamos a crear un archivo de configuración llamado balanceo, y dentro de se archivo, vamos a poner los siguientess datos.

![Screenshot_13](../assets/images/Practica%202.4/Screenshot_13.png) 

En el bloque de upstream, hemos puesto que vaya a uno de esos dos servidores de manera aleatoria, y esas ip pertenecen cada una a uno de los dos servidores que hemos configurado. Hacemos el link correspondiente, y reiniciamos de nuevo, tras esta configuración, solo nos queda cambiar el archivo hosts de nuestra máquina principal y podremos pasar a realizar las comprobaciones.

![Screenshot_14](../assets/images/Practica%202.4/Screenshot_14.png) 

![Screenshot_15](../assets/images/Practica%202.4/Screenshot_15.png) 

## Comprobaciones

Vamos a realizar las comprobaciones, tras poner el nombre de nuestra web, nos va redirigiendo a uno u otro de manera aleatoria, además, comprobamos con las herramientas de desarrollador que se muestra el header que pusimos.

### Servidor web 1

![Screenshot_18](../assets/images/Practica%202.4/Screenshot_18.png) 

![Screenshot_20](../assets/images/Practica%202.4/Screenshot_20.png) 

### Servidor web 2

![Screenshot_19](../assets/images/Practica%202.4/Screenshot_19.png) 

![Screenshot_21](../assets/images/Practica%202.4/Screenshot_21.png) 

## Comprobación con caida de servidor

Tras cerrar el Servidor número 1, sigo refrescando la página, y ahora solo aparece el servidor número 2, por lo que todo está correcto.

![Screenshot_22](../assets/images/Practica%202.4/Screenshot_22.png) 

![Screenshot_19](../assets/images/Practica%202.4/Screenshot_19.png) 

# Cuestiones

## Cuestión 1

> Busca información de qué otros métodos de balanceo se pueden aplicar
> con Nginx y describe al menos 3 de ellos.

**IP-hash**: este método utiliza un algoritmo que toma la dirección IP de origen y destino del cliente y el servidor para generar una clave hash única. IT permite la persistencia de la sesión.

**Round-robin**: es el método predeterminado para el equilibrio de carga. Indica al equilibrador de carga que vuelva a la parte superior de la lista y se repita de nuevo.

**"El Menos conectado"**: este método utiliza un algoritmo de equilibrio de carga dinámico. Redistribuye las conexiones al miembro del grupo que administran la menor cantidad de conexiones abiertas en el momento en que se recibe la nueva solicitud de conexión.

## Cuestión 2

> Si quiero añadir 2 servidores web más al balanceo de carga, describe
> detalladamente qué configuración habría que añadir y dónde.

Una vez ya tengamos configurados esos 2 servidores nuevos, sería tan sencillo como añadir sus IP y puertos a la sección de y colocarlas en el bloque de upstream, siguiendo las otras IP de la misma manera que configuramos las anteriores.

## Cuestión 3

> Describir los pasos a seguir para configurar un balanceo de carga con
> una de las webs de prácticas anteriores.

Lo primero sería modificar el archivo del proxy inverso, para poder añadir el bloque de upstream, con las correspondientes IP de los servidores, también, si queremos que sea random, añadirle el random para que decida uno de estos.

Después, tendríamos que definir el bloque location en el proxy_pass, para asegurarnos de que las peticiones recibidas se muevan a uno de los servidores que tendremos activos.

Realmente, respecto a la práctica anterior, no serían demasiados cambios, mas allá de modificar el proxy, y asegurarnos de que cada servidor tiene su IP y sus identificaciones correctas.


# Práctica 4.1 - Configuración de un servidor DNS

### ATENCIÓN

Antes de comenzar la práctica, vamos a eliminar todos los datos que hemos ido introduciendo en el archivo hosts de nuestro sistema durante las otras prácticas, para así asegurarnos de que no interfiere de ninguna manera.

![Screenshot_1](../assets/images/Practica%204.1/Screenshot_1.png) 

## Instalación del servidor DNS

Para empezar, tenemos que instalar el servidor DNS que vamos a utilizar. En mi caso, he seguido utilizando la máquina virtual de Debian, y vamos a instalar **Bind**. La más recomendada es Bind9, por lo que la instalaremos de una manera muy sencilla utilizando los repositorios oficiales. Antes de instalarlos, nos conectamos a nuestra máquina virtual por SSH.

![Screenshot_2](../assets/images/Practica%204.1/Screenshot_2.png) 

Y una vez ya conectados, introducimos el comando necesario para instalar el servidor DNS, de la siguiente manera.

```sudo apt-get install bind9 bind9utils bind9-doc```

![Screenshot_3](../assets/images/Practica%204.1/Screenshot_3.png) 

## Configuración del servidor

En nuestro caso, sólo vamos a utilizar IPv4, por lo que vamos a modificar el archivo de configuración de bind para indicar esto.

Este archivo estará por defecto en el directorio */etc/default*, y para indicar que solo se use el IPv4 simplemente debemos modificar la línea siguiente con el texto que se indica.

```OPTIONS = "-u bind -4"```

De manera que quedaría de la siguiente forma

![Screenshot_4](../assets/images/Practica%204.1/Screenshot_4.png) 

También, antes de seguir, vamos a ver el archivo named.conf que se encuentra en */etc/bind*, que es el siguiente

![Screenshot_5](../assets/images/Practica%204.1/Screenshot_5.png) 

En ese archivo podemos comprobar que están los archivos de configuración que usaremos, los 3 que vienen indicados en el **include**.

## Configuración de *named.conf.options*

Antes de modificar los archivos, recomiendo hacer una copia de seguridad, por si en algún momento queremos regresar al archivo de configuración original. Para copiarlo, podemos hacerlo de la siguiente manera.

![Screenshot_6](../assets/images/Practica%204.1/Screenshot_6.png) 


Una vez creada nuestra copia, vamos a ir a modificar el archivo **named.conf.options**, en el cual tenemos que asegurarnos de incluir ciertos contenidos.

- Vamos a añadir una lista de acceso para que solo accedan los hosts que deseemos, los cuales serán de la red 192.168.X.0/24. Recordad que la X depende de la red a la que estemos conectados. Se debe añadir al comienzo del archivo, quedaría de la siguiente manera.

![Screenshot_7](../assets/images/Practica%204.1/Screenshot_7.png) 


Tras esto, vamos a añadir mas líneas, esta vez más cantidad, y es para asegurarnos de.

- Que solo se podrán permitir las consultas recursivas a los hosts que hemos dado acceso

- Que no se permitan transferencias de zonas a nadie.

- Configuraremos el servidor para que escuche las consultas DNS en el puerto 53 y en la IP de la red privada (De la máquina virtual Debian).

- Permitir consultas recursivas.

- Y vamos a comentar la última línea de **listen-on-v6 { any; }; , ya que como hemos visto antes, las consultas serán IPv4 y no IPv6.

Si lo hemos hecho correctamente, debe quedar algo así

![Screenshot_8](../assets/images/Practica%204.1/Screenshot_8.png) 


Para comprobar si todo está correcto, vamos a utilizar un comando, que si no devuelve ningún error y devuelve la línea de comandos, es que todo estará correcto

![Screenshot_9](../assets/images/Practica%204.1/Screenshot_9.png) 


Si todo está correcto, reiniciamos el servidor y comprobamos que esté en funcionamiento

![Screenshot_10](../assets/images/Practica%204.1/Screenshot_10.png) 


## Configuración de *named.conf.local*

Ahora vamos con el siguiente archivo de configuración, donde vamos a declarar una zona llamada *deaw.es*.

![Screenshot_11](../assets/images/Practica%204.1/Screenshot_11.png) 


## Creación del archivo de zona

Ahora tenemos que crear nuestro archivo de zona de resolución directa en el directorio que hemos indicado antes en el archivo de configuración, y también nombrarlo con el mismo nombre.

Tras crearlo, debería quedarnos así.

![Screenshot_12](../assets/images/Practica%204.1/Screenshot_12.png) 


En la parte final, debemos poner nuestras IPs privadas correspondientes.

## Creación del archivo de zona para la resolución inversa

Ahora tenemos que volver al archivo de **named.conf.local**, ya que tenemos que añadir un nuevo archivo de zona, y tenemos que añadir las líneas a la configuración.

![Screenshot_13](../assets/images/Practica%204.1/Screenshot_13.png) 


El primer número **254** indica el tercer byte de la red, cada uno tendrá la suya. Una vez añadido, podemos hacer el archivo de configuración inversa.

![Screenshot_14](../assets/images/Practica%204.1/Screenshot_14.png) 


## Comprobación de configuraciones

Ahora tenemos que comprobar que todo funciona correctamente, y para ello vamos a comenzar con la de la zona de resolución directa.

![Screenshot_15](../assets/images/Practica%204.1/Screenshot_15.png) 


Nos indica que todo OK, por lo que vamos a comprobar la de resolución inversa, la cual también nos devuelve un OK.

![Screenshot_16](../assets/images/Practica%204.1/Screenshot_16.png) 


Tras esta comprobación, volvemos a reiniciar el servicio, y comprobamos que funcione correctamente.

![Screenshot_17](../assets/images/Practica%204.1/Screenshot_17.png) 


## Comprobación de las resoluciones y de las consultas

Antes de realizar estas comprobaciones, vamos a asegurarnos de que el cliente está configurado para usar como servidor DNS el que hemos instalado y configurado, por lo que tenemos que cambiar la configuración de red para que la máquina lo utilice como servidor principal. Realizamos la siguiente modificación.

![Screenshot_18](../assets/images/Practica%204.1/Screenshot_18.png) 

Con esto realizado, ya podemos comprobar las resoluciones, lo haremos de dos maneras, la primera es utilizando **nslookup**

![Screenshot_19](../assets/images/Practica%204.1/Screenshot_19.png) 


Y la segunda utilizando **dig**

![Screenshot_20](../assets/images/Practica%204.1/Screenshot_20.png) 


![Screenshot_21](../assets/images/Practica%204.1/Screenshot_21.png) 


## Cuestiones

> Cuestión 1
> ¿Qué pasará si un cliente de una red diferente a la tuya intenta hacer uso de tu DNS de alguna manera, le funcionará?¿Por qué, en qué parte de la configuración puede verse?

No funcionará porque en la configuración limitamos el acceso solo a nuestra red con el acl confiables, en **named.conf.options**

> Cuestión 2
> ¿Por qué tenemos que permitir las consultas recursivas en la configuración?

Porque sin consultas recursivas, el servidor no podrá buscar respuestas en otros servidores DNS cuando no sea autoritativo para un dominio.

> Cuestión 3
> El servidor DNS que acabáis de montar, ¿es autoritativo?¿Por qué?

Si lo es, ya que en el archivo **named.conf.local** hemos declarado dos zonas específicas.

> Cuestión 4
> ¿Dónde podemos encontrar la directiva $ORIGIN y para qué sirve?

La encontramos en los archivos de zona,  y sirve para definir el dominio al que pertenecen los registros.

> Cuestión 5
> ¿Una zona es idéntico a un dominio? 

No, una zona es parte de un dominio, pero un dominio puede tener una o varias zonas.

> Cuestión 6
> ¿Pueden editarse los archivos de zona de un servidor esclavo/secundario?

No, porque se copian de manera automática del primario, por lo que no los editamos directamente.

> Cuestión 7
> ¿Por qué podría querer tener más de un servidor esclavo para una misma zona?

Para mejorar la redundancia y disponibilidad, así si uno nos falla, los otros pueden seguir funcionando.

> Cuestión 8
> ¿Cuántos servidores raíz existen?

Existen 13 servidores raíz, aunque cada uno tiene varias réplicas distribuidas, no son 13 servidores físicos y ya.

> Cuestión 9
> ¿Qué es una consulta iterativa de referencia?

Es cuando un servidor DNS devuelve otra dirección para que el cliente continúe buscando por su cuenta.

> Cuestión 10
> En una resolución inversa, ¿a qué nombre se mapearía la dirección IP 172.16.34.56?

Se mapearía como **56.34.16.172.in-addr.arpa.**

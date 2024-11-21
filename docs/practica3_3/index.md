# Práctica 3.3: Despliegue de una aplicación React en Netlify (PaaS)

## Creación de nuestra aplicación

Tras loguearnos por SSH en nuestro Debian, vamos a crear un directorio para albergar la aplicación y crear 3 archivos, dos html y un js, que conformarán la sencilla aplicación de ejemplo. Deben quedar de la siguiente manera

![Screenshot_1](../assets/images/Practica%203.3/Screenshot_1.png) 

![Screenshot_2](../assets/images/Practica%203.3/Screenshot_2.png)

![Screenshot_3](../assets/images/Practica%203.3/Screenshot_3.png)

![Screenshot_4](../assets/images/Practica%203.3/Screenshot_4.png)

Una vez creado el directorio y los archivos, vamos a utilizar el comando npm init y comprobar que nuestra aplicación funciona correctamente de manera local

![Screenshot_5](../assets/images/Practica%203.3/Screenshot_5.png)

![Screenshot_6](../assets/images/Practica%203.3/Screenshot_6.png)

![Screenshot_7](../assets/images/Practica%203.3/Screenshot_7.png)

Vemos que efectivamente, funciona, con esto ya podríamos desplegarla en múltiples plataformas en la nube, como Heroku, AWS, GCP etc.

## Despliegue en Netlify

Para este despliegue, vamos a tomar una aplicación de ejemplo, para ello, vamos a colnar el repositorio correspondiente

![Screenshot_8](../assets/images/Practica%203.3/Screenshot_8.png)

Una vez creado, vamos a crear una cuenta en Netlify, pues la necesitaremos para realizar todo este proceso. Es muy importante que nos registremos solo con el e-mail, y aún no la vinculemos con github.

![Screenshot_9](../assets/images/Practica%203.3/Screenshot_9.png)

Ahora si podemos empezar con el despliegue mediante CLI, para ello, vamos a tener que instalarlo con el siguiente comando

![Screenshot_10](../assets/images/Practica%203.3/Screenshot_10.png)

Una vez instalado, nos identificaremos en nuestra cuenta de netlify para poder utilizarla sin problema desde la consola de comandos

![Screenshot_11](../assets/images/Practica%203.3/Screenshot_11.png)

Para poder desplegar todo sin complicación, vamos a tener que instalar todas las dependencias del archivo package.json, por lo que usaremos npm install, y después haremos un run build para contener la aplicación que debemos desplegar.

![Screenshot_12](../assets/images/Practica%203.3/Screenshot_12.png)

![Screenshot_13](../assets/images/Practica%203.3/Screenshot_13.png)

Con todo esto ya creado, podemos proceder a desplegar la aplicación en en Netlify. Nos hará algunas preguntas, debemos indicar que queremos crear y configurar un nuevo sitio, dejaremos el Team por defecto, e indicaremos que queremos ponerle de nombre "nombre"-practica3-4 y utilizaremos el directorio ./build.

![Screenshot_14](../assets/images/Practica%203.3/Screenshot_14.png)

![Screenshot_15](../assets/images/Practica%203.3/Screenshot_15.png)

Una vez terminado, si todo ha ido bien, nos saldrá un mensaje y un borrador. Si el borrador esta bien, podemos pasar a desplegar la aplicación. Nos darán un link para comprobar que esta todo bien.

![Screenshot_16](../assets/images/Practica%203.3/Screenshot_16.png)

![Screenshot_17](../assets/images/Practica%203.3/Screenshot_17.png)

## Despliegue mediante conexión con Github

Ahora vamos a desplegar mediante una conexión con Github, para ello, vamos a empezar borrando el despliegue en Netlify, para evitar problemas. También aprovecharemos para borrar el directorio donde hicimos el clonado del repositorio de Github.

![Screenshot_18](../assets/images/Practica%203.3/Screenshot_18.png)

![Screenshot_19](../assets/images/Practica%203.3/Screenshot_19.png)

Como la idea es simular que lo vamos a subir a Github por primera vez, en vez de hacer un clonado, vamos a obtener el zip sin que tenga ninguna referencia a Github

![Screenshot_20](../assets/images/Practica%203.3/Screenshot_20.png)

Una vez lo tengamos, vamos a crear una carpeta nueva y a descomprimir aquí el correspondiente ZIP que hemos descargado.

![Screenshot_21](../assets/images/Practica%203.3/Screenshot_21.png)

Ahora vamos a Github para crear un repositorio completamente vacío, que será donde subiremos lo que hemos descargado.

![Screenshot_22](../assets/images/Practica%203.3/Screenshot_22.png)

Una vez hecho esto, vamos a proceder a desplegar la aplicación en el repositorio de Github, realizando todo el proceso para hacer el push y subir todo el contenido.

![Screenshot_23](../assets/images/Practica%203.3/Screenshot_23.png)

![Screenshot_24](../assets/images/Practica%203.3/Screenshot_24.png)

![Screenshot_25](../assets/images/Practica%203.3/Screenshot_25.png)

Con esto ya tenemos todo el código en GitHub, y vamos a tener que vincular nuestra cuenta de Github con la de Netlify, vamos a importar un proyecto en Netlify, dándole a importar desde Github.

![Screenshot_26](../assets/images/Practica%203.3/Screenshot_26.png)

Vamos a especificar que solo sea el repositorio que hemos creado anteriormente.

![Screenshot_27](../assets/images/Practica%203.3/Screenshot_27.png)

Y ya quedará listo, desplegándose la aplicación, ya que Netlifyse encarga de hacer el build de forma automática.

![Screenshot_28](../assets/images/Practica%203.3/Screenshot_28.png)

Ahora, cuando hagamos un cambio en el proyecto y hagamos un commit push en Github, automáticamente se generará un nuevo despliegue en Netlify. Para ello, haremos unas comprobaciones, vamos a ver que el archivo robots.txt, está de la siguiente manera.

![Screenshot_29](../assets/images/Practica%203.3/Screenshot_29.png)

Una vez comprobado, vamos a modificar el archivo, que está en la carpeta public, y vamos a añadir en Disallow nuestro nombre y apellido de la siguiente manera.

![Screenshot_30](../assets/images/Practica%203.3/Screenshot_30.png)

Una vez hecho el cambio, volvemos a hacer un despliegue en Github, podemos comprobar con date que se ha producido el deploy.

![Screenshot_31](../assets/images/Practica%203.3/Screenshot_31.png)

![Screenshot_32](../assets/images/Practica%203.3/Screenshot_32.png)

En el dashboard de Netlify podemos comprobar que se ha producido un deploy, y vemos como esta haciendo el Building.

![Screenshot_33](../assets/images/Practica%203.3/Screenshot_33.png)

Y cuando termina, volvemos a ir al archivo robots.txt, y efectivamente, veremos el cambio reflejado.

![Screenshot_34](../assets/images/Practica%203.3/Screenshot_34.png)
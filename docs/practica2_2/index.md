# Práctica 2.2 - Autenticación en Nginx

## Comprobación de Paquetes

Primero, comprobamos que los paquetes necesarios están instalados. En mi caso lo están.

![Screenshot_1](../assets/images/Practica%202.2/Screenshot_1.png)

## Creación de usuarios y contraseñas para el acceso web

Vamos a crear un archivo oculto que se llama ***.htpasswd***. Lo vamos a crear en el directorio de configuración */etc/nginx* donde se pueda guardar el usuario y la contraseña. Como se puede repetir con tantos usuarios como haga falta, lo he realizado con mi nombre y mi apellido.

![Screenshot_2](../assets/images/Practica%202.2/Screenshot_2.png)
![Screenshot_3](../assets/images/Practica%202.2/Screenshot_3.png)
![Screenshot_4](../assets/images/Practica%202.2/Screenshot_4.png)

Compruebo que todo esté correcto.

![Screenshot_5](../assets/images/Practica%202.2/Screenshot_5.png)

## Configurando el servidor Nginx para usar autenticación básica

Lo primero va a ser configurar nuestra web para añadir la directiva *auth_basic* y así proteger la web.

![Screenshot_6](../assets/images/Practica%202.2/Screenshot_6.png)

Una vez guardada la configuración, reiniciamos el servidor

![Screenshot_7](../assets/images/Practica%202.2/Screenshot_7.png)

## Probando la nueva configuración

Tras esto, he comprobado que desde mi máquina física he podido acceder al sitio y me ha pedido autentificación

![Screenshot_8](../assets/images/Practica%202.2/Screenshot_8.png)

Y si cancelo la autentificación sale el **error 401**

![Screenshot_9](../assets/images/Practica%202.2/Screenshot_9.png)

Ahora, para la *Tarea 1*, he intentado entrar con un usuario erróneo, y luego con uno correcto.

Accedo a los log de acceso y error para que se vean ambos intentos.

En el de acceso vemos como nos muestra que no hay ningún problema

![Screenshot_10](../assets/images/Practica%202.2/Screenshot_10.png)

Mientras que en el de error vemos que nos dice que no se ha encontrado ese usuario en el archivo que creamos, dando lugar a que no pueda autentificarse.

![Screenshot_11](../assets/images/Practica%202.2/Screenshot_11.png)

Después hemos tenido que configurar para que el servidor solo bloquee cierta parte de la web. En nuestro caso, no podemos bloquear solo contact, por lo que hice el ejemplo con el propio index.

![Screenshot_12](../assets/images/Practica%202.2/Screenshot_12.png)

## Combinación de la autenticación básica con restricción por IP

También tenemos la opción de permitir o denegar la entrada a la web a partir de las IP. con las directivas allow y deny. Además, podemos también hacer que sea necesario tanto autentificarse con el usuario como tener la IP correcta.

En la Tarea 1 de esta sección, teníamos que prohibir el acceso con la IP de la máquina anfitriona, y comprobar que el acceso fuese denegado.

![Screenshot_13](../assets/images/Practica%202.2/Screenshot_13.png)

Y efectivamente, nos sale un **error 403** cuando intentamos entrar

![Screenshot_14](../assets/images/Practica%202.2/Screenshot_14.png)

También podemos ver el propio mensaje de error en el ***error.log***

![Screenshot_15](../assets/images/Practica%202.2/Screenshot_15.png)

Para finalizar, configuramos para que necesitemos acceder desde la máquina anfitriona tanto con una IP válida como con el usuario, ambas cosas a la vez. Tras poner las directivas, lo compruebo y funciona perfectamente.

![Screenshot_16](../assets/images/Practica%202.2/Screenshot_16.png)

![Screenshot_17](../assets/images/Practica%202.2/Screenshot_17.png)

## Cuestiones finales

**Cuestion 1**

Supongamos que yo soy el cliente con la IP 172.1.10.15 e intento acceder al directorio `web_muy_guay` de mi sitio web, equivocándome al poner el usuario y contraseña. ¿Podré acceder? ¿Por qué?

```
    location /web_muy_guay {
    #...
    satisfy all;    
    deny  172.1.10.6;
    allow 172.1.10.15;
    allow 172.1.3.14;
    deny  all;
    auth_basic "Cuestión final 1";
    auth_basic_user_file conf/htpasswd;
}
```
No se podrá, porque nos está pidiendo que tenemos que utilizar tanto una IP correcta como un usuario.

**Cuestion 2**

Supongamos que yo soy el cliente con la IP 172.1.10.15 e intento acceder al directorio `web_muy_guay` de mi sitio web, introduciendo correctamente usuario y contraseña. ¿Podré acceder?¿Por qué?

```
    location /web_muy_guay {
    #...
    satisfy all;    
    deny  all;
    deny  172.1.10.6;
    allow 172.1.10.15;
    allow 172.1.3.14;

    auth_basic "Cuestión final 2: The revenge";
    auth_basic_user_file conf/htpasswd;
    } 
```
Si podremos acceder, ya que pese al deny all, se permite el acceso a nuestra IP, y además, hemos introducido el usuario y contraseña de manera correcta.

**Cuestion 3**

Supongamos que yo soy el cliente con la IP 172.1.10.15 e intento acceder al directorio `web_muy_guay` de mi sitio web, introduciendo correctamente usuario y contraseña. ¿Podré acceder?¿Por qué?

```
    location /web_muy_guay {
    #...
    satisfy any;    
    deny  172.1.10.6;
    deny 172.1.10.15;
    allow 172.1.3.14;

    auth_basic "Cuestión final 3: The final combat";
    auth_basic_user_file conf/htpasswd;
}
```
No podremos acceder, puesto que aunque la directiva sea satisfy any, nuestra IP está denegada, y esa restricción tiene prioridad y bloquea el acceso.

**Cuestion 4**

Supongamos que quiero restringir el acceso al directorio de proyectos porque es muy secreto, eso quiere decir añadir autenticación básica a la sección de proyectos.

Completa la configuración para conseguirlo:

```
    server {
        listen 80;
        listen [::]:80;
        root /var/www/freewebsitetemplates.com/preview/space-science;
        index index.html index.htm index.nginx-debian.html;
        server_name freewebsitetemplates.com www.freewebsitetemplates.com;
        location              {

            try_files $uri $uri/ =404;
        }
		location /Proyectos {
			auth_basic "Área restringida";
			auth_basic_user_file /etc/nginx/.htpasswd;
			try_files $uri $uri/ =404ç
		}
    }
```
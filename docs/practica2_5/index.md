# Práctica 2.5 - # Proxy inverso y balanceo de carga con SSL en NGINX

## Creación de certificado autofirmado

Para comenzar el proceso, tenemos que crear un certificado autofirmado en nuestra máquina que contenga el proxy inverso, y para comenzar, tenemos que crear un directorio de la siguiente manera.

![Screenshot_2](../assets/images/Practica%202.5/Screenshot_2.png) 

Una vez creado, podemos proceder a la creación del certificado, introduciendo los parámetros que nos van pidiendo.

Los datos que se ven en el comando son los siguientes:

-   **openssl**: es la herramienta de línea de comandos que usamos para gestionar certificados, claves y otros archivos relacionados con OpenSSL.
    
-   **req**: este subcomando se usa para generar solicitudes de certificado, o también solicitudes de firma de certificados (CSR).
    
-   **-x509**: al añadir esta opción, le indicamos a OpenSSL que queremos un certificado autofirmado en lugar de una solicitud de firma de certificado.
    
-   **-nodes**: le dice a OpenSSL que no proteja el certificado con una contraseña. Esto es importante para que Nginx pueda leer el archivo sin pedir una contraseña cada vez que se reinicia el servidor.
    
-   **-days 365**: define la duración de validez del certificado; en este caso, lo configuramos para un año.
    
-   **-newkey rsa:2048**: especifica que generaremos un nuevo certificado y una clave al mismo tiempo. Elegimos una clave RSA de 2048 bits para asegurarla.
    
-   **-keyout**: le indica a OpenSSL dónde guardar el archivo con la clave privada.
    
-   **-out**: le dice a OpenSSL dónde guardar el archivo del certificado que estamos creando.

![Screenshot_3](../assets/images/Practica%202.5/Screenshot_3.png) 

## Configuración SSL en el Proxy Inverso

**AVISO: Recordar a la hora de probar todo en el navegador desactivar la caché o utilizar ventana privada.**

Ahora vamos a modificar el archivo que ya teníamos creado llamado balanceo, cambiando el bloque server y cambiando el puerto de escucha 80, añadiendo las configuraciones que veremos en la imagen a continuación.

![Screenshot_4](../assets/images/Practica%202.5/Screenshot_4.png) 

Tras este cambio, vamos a reiniciar nginx para que los cambios aparezcan.

![Screenshot_5](../assets/images/Practica%202.5/Screenshot_5.png) 


## Comprobaciones


Ahora, cuando entremos en nuestra web, nos saltará un aviso, puesto que nuestro certificado es autofirmado. Aceptamos, ya que no hay problema, puesto que nuestro certificado es seguro, ya que lo hemos generado nosotros. Una vez en la web, vamos a comprobar que el certificado es correcto. Pulsando en el candado, le damos a más información.

![Screenshot_6](../assets/images/Practica%202.5/Screenshot_6.png) 

Después, en el apartado de seguridad le daremos a ver certificado.

![Screenshot_7](../assets/images/Practica%202.5/Screenshot_7.png) 

Ahí ya podremos ver todos los datos de nuestro certificado, como en la siguiente imagen.

![Screenshot_8](../assets/images/Practica%202.5/Screenshot_8.png) 

Si intentásemos acceder al http, nos sale la web básica de nginx, porque por ahora no nos está redirigiendo al https.

![Screenshot_9](../assets/images/Practica%202.5/Screenshot_9.png) 

## Redirección forzosa a HTTPS

Para que no importe desde donde accedemos a la web, vamos a añadir un nuevo bloque server, para que nos redirija automáticamente al HTTPS.

Así quedaría el nuevo bloque junto al anterior.

![Screenshot_10](../assets/images/Practica%202.5/Screenshot_10.png) 

Como de costumbre, reiniciamos NGINX para reflejar los cambios.

![Screenshot_11](../assets/images/Practica%202.5/Screenshot_11.png) 

Tras esto, compruebo que efectivamente, al ir por HTTP, me redirige automáticamente al HTTPS.

![Screenshot_12](../assets/images/Practica%202.5/Screenshot_12.png) 

Para comprobarlo mejor, vamos a ver los logs de acceso, tanto del HTTP como del HTTPS

![Screenshot_13](../assets/images/Practica%202.5/Screenshot_13.png) 

![Screenshot_14](../assets/images/Practica%202.5/Screenshot_14.png) 

## Cuestiones finales

### Cuestion 1

Hemos configurado nuestro proxy inverso con todo lo que nos hace falta pero no nos funciona y da un error del tipo `This site can't provide a secure connection, ERR_SSL_PROTOCOL_ERROR.`

Dentro de nuestro server block tenemos esto:

```
server {
    listen 443;
    ssl_certificate /etc/nginx/ssl/enrico-berlinguer/server.crt;
    ssl_certificate_key /etc/nginx/ssl/enrico-berlinguer/server.key;
    ssl_protocols TLSv1.3;
    ssl_ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5:!DSS;
    server_name enrico-berlinguer;
    access_log /var/log/nginx/https_access.log;

    location / {
        proxy_pass http://red-party;
        }
    }
```
El error que vemos es un error de SSL, y es porque en el comienzo del server, nos falta un ssl al lado del listen 443, de manera que quede como

```listen 443 ssl;```


### Cuestion 2

¿Cómo solucionamos el siguiente error?

![Screenshot_15](../assets/images/Practica%202.5/Screenshot_15.png) 

Este error, `NET::ERR_CERT_REVOKED`, significa que el certificado SSL del sitio ha sido revocado por la autoridad de certificación (CA) que lo emitió. Esto puede ocurrir por varias razones, como problemas de seguridad, la expiración del certificado, o incluso un error administrativo.

Para intentar solucionarlo, primero verificamos si el certificado realmente ha sido revocado. Si es así, solicitamos un nuevo certificado y lo reemplazamos en la configuración de Nginx, asegurándonos de reiniciar el servidor para aplicar los cambios. También podemos intentar limpiar la caché del navegador o probarlo en otro navegador, ya que a veces el problema puede estar relacionado con la caché del certificado en el navegador.
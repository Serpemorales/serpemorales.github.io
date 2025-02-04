# Práctica 5.2 - Ejercicios Git y Github (II)

## Ejercicios de creación y actualización de repositorios

### Ejercicio 1

Vamos a configurar Git con nuestro nombre de usuario, el correo electrónico y activaremos el coloreado de la salida. Además, mostraremos la configuración inicial.

![Screenshot_1](../assets/images/Practica%205.2/Screenshot_1.png) 

![Screenshot_2](../assets/images/Practica%205.2/Screenshot_2.png) 

### Ejercicio 2

Vamos a crear un repositorio nuevo con el nombre libro, y vamos a ver su contenido (Ahora mismo no habrá nada)

![Screenshot_3](../assets/images/Practica%205.2/Screenshot_3.png) 

### Ejercicio 3

Vamos a comprobar el estado del repositorio, después añadiremos un fichero llamado indice.txt.

![Screenshot_4](../assets/images/Practica%205.2/Screenshot_4.png) 

![Screenshot_5](../assets/images/Practica%205.2/Screenshot_5.png) 

Añadimos el fichero a la zona de intercambio temporal, y volvemos a comprobar el estado del repositorio.

![Screenshot_6](../assets/images/Practica%205.2/Screenshot_6.png) 

### Ejercicio 4

Vamos a hacer un commit con estos últimos cambios, añadiendo el mensaje de "Añadido índice del libro." También comprobaremos el estado.

![Screenshot_7](../assets/images/Practica%205.2/Screenshot_7.png) 

### Ejercicio 5

Vamos a modificar el archivo indice.txt de antes.

![Screenshot_8](../assets/images/Practica%205.2/Screenshot_8.png)

Tras esto, mostramos los cambios con respecto a la última versión guardada en nuestro repositorio y hacemos un commit con el mensaje "Añadido capítulo 3 sobre gestión de ramas".

![Screenshot_9](../assets/images/Practica%205.2/Screenshot_9.png)

### Ejercicio 6

Mostramos los cambios de la última versión del repositorio con respecto a la versión anterior.

![Screenshot_10](../assets/images/Practica%205.2/Screenshot_10.png)

Vamos a cambiar el mensaje del último commit por “Añadido capítulo 3 sobre gestión de ramas al índice.” y volvemos a mostrar los últimos cambios del repositorio.

![Screenshot_11](../assets/images/Practica%205.2/Screenshot_11.png)

## Ejercicios de manejo del historial de cambios

### Ejercicio 1

Mostramos el historial de cambios del repositorio y creamos una nueva carpeta llamada "Capítulos"

![Screenshot_12](../assets/images/Practica%205.2/Screenshot_12.png)

Dentro de la nueva carpeta, creamos el archivo capitulo1.txt con el siguiente texto:

![Screenshot_13](../assets/images/Practica%205.2/Screenshot_13.png)

Después, añadimos los cambios a la zona de intercambio temporal y hacemos un commit con el mensaje “Añadido capítulo 1.”, volviendo a mostrar el historial de cambios.

![Screenshot_14](../assets/images/Practica%205.2/Screenshot_14.png)

### Ejercicio 2

En la carpeta capítulos, creamos ahora un archivo llamado capitulo2.txt.

![Screenshot_15](../assets/images/Practica%205.2/Screenshot_15.png)

Tras esto, vamos a añadir los cambios a la zona de intercambio temporal, haciendo un commit con el mensaje “Añadido capítulo 2." y mostrando las diferencias entre la última versión y las dos anteriores

![Screenshot_16](../assets/images/Practica%205.2/Screenshot_16.png)

### Ejercicio 3

Vamos a la carpeta capítulos de nuevo, creando el archivo llamado capítulo3.txt.

![Screenshot_17](../assets/images/Practica%205.2/Screenshot_17.png)

Ahora, añadimos los cambios a la zona de intercambio temporal, haciendo un commit con el mensaje “Añadido capítulo 3." y mostrando las diferencias entre la primera y la última versión del repositorio.

![Screenshot_18](../assets/images/Practica%205.2/Screenshot_18.png)

### Ejercicio 4

Vamos a modificar la última línea del fichero indice.txt.

![Screenshot_19](../assets/images/Practica%205.2/Screenshot_19.png)

Después, añadimos los cambios a la zona de intercambio temporal, realizando un commit con el mensaje “Añadido capítulo 5 al índice.” y mostrando quien ha hecho los cambios sobre este fichero.

![Screenshot_20](../assets/images/Practica%205.2/Screenshot_20.png)

## Ejercicios de deshacer cambios

### Ejercicio 1

Eliminamos la última linea del fichero indice.txt y guardamos.

![Screenshot_21](../assets/images/Practica%205.2/Screenshot_21.png)

Comprobamos el estado del repositorio, después desharemos los cambios realizados en el archivo indice.txt y volveremos a comprobar el estado del repositorio.

![Screenshot_22](../assets/images/Practica%205.2/Screenshot_22.png)

### Ejercicio 2

Eliminamos la última linea del fichero indice.txt y guardamos.

![Screenshot_21](../assets/images/Practica%205.2/Screenshot_21.png)

Añadimos estos cambios a la zona de intercambio temporal, comprobando el estado del repositorio. Después quitamos los cambios de la zona de intercambio temporal, pero las mantenemos en nuestro directorio de trabajo, comprobando el estado del repositorio.

Finalmente, deshacemos los cambios del fichero indice.txt y comprobamos el estado del repositorio una última vez.

![Screenshot_23](../assets/images/Practica%205.2/Screenshot_23.png)

### Ejercicio 3

Eliminamos la última linea del fichero indice.txt y guardamos.

![Screenshot_21](../assets/images/Practica%205.2/Screenshot_21.png)

Eliminamos el fichero capitulo3.txt, añadimos un nuevo fichero vacío llamado capitulo4.txt y añadimos todos estos cambios a la zona de intercambio temporal, comprobando el estado del repositorio.

Después, quitaremos los cambios de la zona de intercambio temporal, pero dejándolos en el directorio de trabajo, comprobando de nuevo el estado del repositorio.

Por último, vamos a deshacer los cambios realizados para volver a la versión del repositorio, comprobando su estado.

![Screenshot_24](../assets/images/Practica%205.2/Screenshot_24.png)

### Ejercicio 4

Eliminamos la última linea del fichero indice.txt y guardamos.

![Screenshot_21](../assets/images/Practica%205.2/Screenshot_21.png)

Eliminamos el fichero capitulo3.txt, realizando un commit en el que pongamos "Borrado accidental", comprobando el historial del repositorio.

Después desharemos el último commit pero manteniendo los cambios anteriores en el directorio de trabajo y la zona de intercambio temporal. Comprobamos el historial y el estado del repositorio.

Volvemos a hacer el commit igual que antes, y lo desharemos junto a los cambios anteriores del directorio de trabajo, para volver a la versión anterior.

Comprobamos de nuevo el historial y el estado del repositorio.

![Screenshot_25](../assets/images/Practica%205.2/Screenshot_25.png)

![Screenshot_26](../assets/images/Practica%205.2/Screenshot_26.png)

## Ejercicios de gestión de ramas

### Ejercicio 1

Creamos una rama llamada bibliografía y mostramos todas las ramas.

![Screenshot_27](../assets/images/Practica%205.2/Screenshot_27.png)

### Ejercicio 2

Vamos a crear el fichero capitulo4.txt dentro de la carpeta capítulos.

![Screenshot_28](../assets/images/Practica%205.2/Screenshot_28.png)

Añadiremos estos cambios a la zona de intercambio temporal y haremos un commit con el mensaje “Añadido capítulo 4.”. Además, mostraremos la historia del repositorio incluyendo las ramas.

![Screenshot_29](../assets/images/Practica%205.2/Screenshot_29.png)

### Ejercicio 3

Cambiamos a la rama bibliografía, y vamos a crear el archivo bibliografia.txt

![Screenshot_30](../assets/images/Practica%205.2/Screenshot_30.png)

Añadiremos estos cambios a la zona de intercambio temporal y haremos un commit con el mensaje “Añadida primera referencia bibliográfica.”. Además, mostraremos la historia del repositorio incluyendo las ramas.

![Screenshot_31](../assets/images/Practica%205.2/Screenshot_31.png)

### Ejercicio 4

Vamos a fusionar la rama bibliografía con la rama master, mostrando a su vez la historia del repositorio incluyendo las ramas. Una vez fusionadas, borraremos la rama de bibliografía y mostraremos de nuevo la historia.

![Screenshot_32](../assets/images/Practica%205.2/Screenshot_32.png)

### Ejercicio 5

Creamos la rama bibliografía, cambiamos a ella y modificamos el archivo bibliografia.txt, añadiendo este cambio a la zona de intercambio temporal y haciendo un commit con el mensaje “Añadida nueva referencia bibliográfica.”.

![Screenshot_33](../assets/images/Practica%205.2/Screenshot_33.png)

![Screenshot_33_1](../assets/images/Practica%205.2/Screenshot_33_1.png)

Tras esto, volvemos a la rama master, donde modificaremos el archivo bibliografia.txt

![Screenshot_34](../assets/images/Practica%205.2/Screenshot_34.png)

Añadiremos estos cambios a la zona de intercambio temporal y haremos un commit con el mensaje “Añadida nueva referencia bibliográfica.”, y fusionaremos la rama bibliografía con la rama master. Tendremos un conflicto, por lo que debemos modificar el archivo bibliografia.txt para resolverlo.

Tras terminar añadiremos los cambios a la zona de intercambio temporal y hacemos un commit con el mensaje “Resuelto conflicto de bibliografía.”, mostrando la historia del repositorio con sus ramas.

![Screenshot_35](../assets/images/Practica%205.2/Screenshot_35.png)

![Screenshot_36](../assets/images/Practica%205.2/Screenshot_36.png)

## Ejercicios de repositorios remotos

### Ejercicio 1

Creamos un repositorio público llamado libro-git, lo añadimos de manera local a nuestro repositorio de libro y mostramos todos los repositorios remotos configurados.

![Screenshot_37](../assets/images/Practica%205.2/Screenshot_37.png)

![Screenshot_38](../assets/images/Practica%205.2/Screenshot_38.png)

### Ejercicio 2

Vamos a añadir los cambios del repositorio local al repositorio remoto en Github, y accederemos para comprobar que se han subido correctamente.

![Screenshot_39](../assets/images/Practica%205.2/Screenshot_39.png)

![Screenshot_40](../assets/images/Practica%205.2/Screenshot_40.png)

### Ejercicio 3

Vamos a colaborar en el repositorio remoto de otro usuario.

![Screenshot_41](../assets/images/Practica%205.2/Screenshot_41.png)

Tras tener acceso, vamos a clonarlo, y añadir el fichero autores.txt con nuestro nombre y correo

![Screenshot_42](../assets/images/Practica%205.2/Screenshot_42.png)

![Screenshot_43](../assets/images/Practica%205.2/Screenshot_43.png)

Ahora añadimos estos cambios a la zona de intercambio temporal, hacemos un commit en el que ponga "Añadido autor" y subimos los cambios al repositorio remoto.

![Screenshot_44](../assets/images/Practica%205.2/Screenshot_44.png)

![Screenshot_45](../assets/images/Practica%205.2/Screenshot_45.png)

### Ejercicio 4

Hacemos una bifurcación del repositorio remoto `asalber/libro-git` en GitHub.

![Screenshot_46](../assets/images/Practica%205.2/Screenshot_46.png)

Lo clonaremos, creando una nueva rama llamada autoría y activando esta.

![Screenshot_ç](../assets/images/Practica%205.2/ç.png)

Tras esto, añadimos el archivo autores.txt con nuestro nombre y correo

![Screenshot_47](../assets/images/Practica%205.2/Screenshot_47.png)

Ahora añadimos estos cambios a la zona de intercambio temporal, hacemos un commit en el que ponga "Añadido nuevo autor" y subimos los cambios de la rama autoria al repositorio remoto en GitHub.

![Screenshot_48](../assets/images/Practica%205.2/Screenshot_48.png)

![Screenshot_49](../assets/images/Practica%205.2/Screenshot_49.png)

Haremos un pull request de los cambios de la rama autoría, comprobando que sale todo correctamente.

![Screenshot_50](../assets/images/Practica%205.2/Screenshot_50.png)

![Screenshot_51](../assets/images/Practica%205.2/Screenshot_51.png)
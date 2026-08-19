Para transferir recursos entre sistemas operativos, esto es util para una fase de explotación  como para la fase de pos-explotación y cualquier procedimiento dentro de esta. 

Para transferir recursos entre sistemas operativos existen varios métodos, el mas simple es usar python y crear un servidor web en el directorio donde están los recursos que queremos compartir, dicho de otra forma lo que se hace es ubicarnos en el directorio donde están localizados los recursos que queremos compartir y desde esa ubicación llamar al interprete de python, ya sea python 2 o python 3 porque son las versiones que vienen de forma predeterminada en la mayoria de distros orientadas a ciberseguridad.

# Uso con Python 2
Si se utiliza python 2 hay que hacer uso del parámetro:
```
python2 -m SimpleHTTPServer
```
Es importante saber que debe ser escrito tal cual, debido a que es importante por las letras en mayúsculas es decir no es "case sensitive".

Lo que hace es llamar al modulo Simple HTTP Server de la biblioteca estandar para iniciar un servidor web, hay que tener en cuenta que si no se le indica ningún puerto de forma predeterminada el puerto que se le va asignar es el puerto 8000, podemos hacer uso del puerto 33 para ser discretos.

# Uso con Python 3
Si se usa python 3 hay que hacer uso del parámetro siguiente:
```
python3 -m http.server
```
Y es lo mismo que el otro, no es case sensitive y si no se le indica el puerto usará el 8000.

---
Y en este punto los recursos de ese directorio donde se ejecuta la anterior orden se convierte en la raíz del servidor web, por ejemplo si desde la maquina victima que tenga alguna herramienta para descargar recursos como "WGET", podríamos descargarnos digamos un recurso que tengamos en este directorio que estemos sirviendo como LinPEAS que es un script de codigo abierto escrito en bash que ayuda a encontrar formas de escalar privilegios, podriamos usar LinPEAS para enumerar mas el sistema que ya esta comprometido y buscar potenciales formas de escalar privilegios y si queremos pasar el fichero desde la maquina atacante hasta la maquina victima, lo que se haría seria simplemente desde la maquina victima usariamos una herramienta que nos permitiese descargar recursos como "WGET" indicando que descargaremos un recurso via HTTP porque el servidor que establecimos es HTTP o sea usa este protocolo que en este caso el host desde donde lo sacaremos es la IP de nuestra maquina atacante con la que la maquina victima tiene conexión y que tiene el puerto asignado sea el 8000 o el 33, adicionalmente indicarle el nombre del recurso a descargar que en ese caso seria linpeas.sh:
![[Servidores HTTP con Python{{date}}.png]]
Y al hacer esto veremos que del lado de la maquina atacante, o sea que desde nuestro servidor hay una descarga por parte de la IP correspondiente de la maquina victima y dentro de la maquina victima podremos ver ya el recurso descargado:
![[Servidores HTTP con Python{{date}}-1.png]]
y después de eso ejecutar LinPEAS:
![[Servidores HTTP con Python{{date}}-2.png]]

```
./linpeas.sh
```

Algo extra seria montar un "Apache" y configurarlo para que haga todo este proceso pero usando Python seria la forma mas rápida y simple de conseguir esto.
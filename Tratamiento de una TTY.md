TTY son las siglas de TeleTYpewriter, esto se refiere a las sesiones de la terminal que permiten la "comunicación" entre el usuario y el sistema operativo a través de una interfaz de línea de comandos, cuando se habla del tratamiento de la TTY lo que se busca es convertir un shell básico en una TTY interactiva para mejorar la experiencia y el uso que hagamos en ella, porque cuando se compromete un sistema por ejemplo a través de una shell reversa, esa shell que se devuelve generalmente no es interactiva y perfectamente se puede operar con ella, pero no es la mejor opción porque en este tipo de shells no se puede tener atajos del teclado e incluso en ciertas circunstancias no nos dejará ejecutar algunas herramientas, por lo que lo mejor sería hacer un pequeño tratamiento de la TTY y con eso se consigue pasar esa shell normal a una mejorada, hay varias maneras de hacerlo.

# Metodología para hacer el tratamiento
1) Desde la shell reversa que hayamos obtenido, obtendremos una pseudoterminal para añadir mas interactividad 
2) Hay que hacer uso de la Bash Built-in, estos son comandos integrados de la shell bash, que al ejecutarlos de cierta forma y en cierto orden se le pueden añadir mas funcionalidad a la pseudoterminal.
3) Hay que Setear las variables de entorno correspondientes en la maquina victima para que sean congruentes con la configuracion previa que hicimos usando las Bash Built-ins
4) Si aplicase podemos redimensionar las dimensiones de la pseudoterminal para que se adapte al tamaño de nuestro emulador de terminal.
Hacer este tratamiento no es obligatorio pero es muy bueno hacerlo por comodidad para que las labores de pos-explotacion sean mas comodas.

# Practica 
Minuto 2:57:10
Hay softwares para hacer esto pero en este caso vamos hacerlo con Python
1) Identificar si en la maquina victima tiene Python en el sistema, se puede saber esto escribiendo:
```
   which python
```
para que nos de la ruta de donde está instalado python:
![[Tratamiento de una TTY{{date}}-1.png]]

2) Haciendo uso de python se hace la metodología anteriormente vista, lo primero es obtener una pseudoterminal, para esto podemos utilizar en Python 2 una ejecucion simple de comando con el parametro "-c", importando el modulo pty
```
   python -c 'import pty; pty.spawn("/bin/bash)'
```
para con esto crear una nueva sesión de bash en una pseudoterminal y la crearemos llamando el binario bash, con esto consiguiendo mejorar la interactividad de la shell bash.
3) El paso dos es usar las Bash Built-ins para añadirle las funcionalidades a la pseudoterminal, llo primero es ejecutar "Ctrl+Z" que para lo que sirve es para poner a dormir un proceso y además de detenerlo es mandarlo a segundo plano, o sea que a nivel de la maquina atacante suspenderemos la sesión remota, devolviendole el control a la terminal de la maquina atacante o sea la nuestra y a nivel de la maquina victima el shell remoto se detiene temporalmente pero sigue activo:
![[Tratamiento de una TTY{{date}}-2.png]]
despues del "Ctrl+Z" que ya que estamos en nuestra terminal ejecutaremos:
![[Tratamiento de una TTY{{date}}-3.png]]
```
stty raw -echo; fg
```
que como tal esto configura la terminal que funcione en modo "raw" es decir sin procesar y que desactive el "echo" de caracteres, donde en este caso nuestra maquina va a cambiar el modo de operación de la terminal para que en este caso envíe y reciba datos sin procesamiento adicional, y como va a desactivar la impresión de los caracteres que se reciban porque desactivamos a "echo" y "echo" es imprimir y en la maquina victima no pasa nada aun, y este comando se concatena con " ; " para que se ejecute otro comando que es "fg" que es "foreground" que significa primer plano es decir "fg" va a traer al primer plano el ultimo proceso suspendido que en este caso es la shell remota, lo que pasa después de esto es que vamos a poder tener la shell remota en un estado interactivo  y en la maquina victima se va a reactivar la shell remota permitiendo que siga ejecutándose porque en ningún momento la quitamos como que se suspendió, pero no la podemos verla aun porque debemos ejecutar un comando adicional que es como tal para establecer la configuración de una shell remota, por lo que se hace un reset de las configuraciones antes de quererle setear una nueva configuración, esto se hace para evitar conflictos en las configuraciones
![[Tratamiento de una TTY{{date}}-4.png]]
y una vez reseteadas las configuraciones podemos indicarle el tipo de terminal que queremos usar para usar "xterm" porque "xterm" es usado por su compatibilidad a nivel global (xterm es un emulador de terminal para el sistema xwindows que es un entorno grafico comun en sistemas UNIX y UNIXLike que nos permite emular una TTY a traves de una ventana grafica basicamente emulando de cierta forma los comportamientos de una terminal fisica)
![[Tratamiento de una TTY{{date}}-5.png]]

 y despues de eso, de decir que queremos usar "xterm" por lo que ahora si podemos usar atajos y tenemos una terminal interactiva como "Ctrl + C" sin matar el proceso de la shell reversa 
 ![[Tratamiento de una TTY{{date}}-6.png]]
4) Ahora lo que debemos setear son dos variables en este caso la shell que usamos que es "bash" y el tipo de terminal que debe ser el mismo que seleccionamos previamente, por consecuencia para cambiar el valor de una variable de entorno usaremos "export" luego la variable, el signo de "=" y el valor por lo que la variable "SHELL" va a valer "bash" tanto absoluta como relativa 
```
export SHELL=/bin/bash/ TERM=xterm
```
![[Tratamiento de una TTY{{date}}-7.png]]
y la variable "TERM" va a valer "xterm" y se puede comprobar que los nuevos valores sirvieron si ahora si se limpia la pantalla no como el anterior ejemplo:
![[Tratamiento de una TTY{{date}}-8.png]]

5) El ultimo paso es adaptar las dimensiones de la terminal para que se adapten a nuestras dimensiones de nuestra terminal de la maquina atacante, ejecutamos:
```
nano /etc/passwd
```
![[Tratamiento de una TTY{{date}}-9.png]]
![[dimensiones.png]]

y como se puede llegar a ver el tamaño de la shell remota se ve mas pequeña que nuestra ventana, para cambiarlo debemos escribir:
```
stty rows x columns x
```
donde "x" es el valor que le vamos a poner, y si queremos que nuestra shell remota sea comoda para nosotros podemos abrir una propia terminal y checar el valor actual de esta con el comando ![[dimensiones2.png]]

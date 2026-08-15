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
![[Tratamiento de una TTY{{date}}.png]]

2) Haciendo uso de python se hace la metodología anteriormente vista, lo primero es obtener una pseudoterminal, para esto podemos utilizar en Python 2 una ejecucion simple de comando con el parametro "-c", importando el modulo pty
```
   python -c 'import pty; pty.spawn("/bin/bash)'
```
para con esto crear una nueva sesión de bash en una pseudoterminal y la crearemos llamando el binario bash, con esto consiguiendo mejorar la interactividad de la shell bash.
3) El paso dos es usar las Bash Built-ins para añadirle las funcionalidades a la pseudoterminal
DirBuster es una herramienta principalmente diseñada para hacer enumeración de directorios y recursos ocultos y esta herramienta está disponible en la maquina que dan en el examen del eJPT. 
DirBuster tiene interfaz grafica pero tiene su versión de línea de comandos que es Dirb.
![[Interfaz DirBuster{{date}}.png|700]]
Esta es la interfaz de DirBuster, tenemos el target donde se especificará la URL del objetivo a escanear, word method donde podemos indicar el método HTTP que van usar las solicitudes por ejemplo usar únicamente GET o estar alternando entre HEAD y GET, también podemos configurar el número de hilos que esto lo que hará es que vaya mucho mas rápido pero es mucho mas propenso a falsos positivos, podemos seleccionar el tipo de escaneo es decir, podemos basarnos en una wordlist o podemos hacer fuerza bruta para que genere todas las posibles combinaciones, también podemos cargar una wordlist para hacer dicho escaneo que sería lo mas optimo, también se puede configurar el conjunto de caracteres y la longitud minima y maxima en el caso para la fuerza bruta si es que la seleccionamos, también se puede seleccionar el punto de inicio estandar o personalizar la URL inicial para temas de fuzzing, también se puede habilitar la fuerza bruta para directorios y ficheros (ataques de fuerza bruta y ataques de diccionario no son lo mismo), también podemos activar la búsqueda recursiva en subdirectorios es decir que si por ejemplo conseguimos un directorio llamado "/importante" y dentro de "/importante" está "/contraseñas" pues con la búsqueda recursiva va a buscar recursos dentro de "/importante" y dentro de "/contraseñas" adicionalmente que también permite usar extensiones en blanco o meramente a especificar las extensiones de ficheros a buscar y con todo configurado podemos lanzar el escaneo dándole a "Start".

Un ejemplo de configuración típico de DirBuster sería escanear un sitio web, una maquina para probar seria una que se encuentra en TryHackMe llamada "ColddBox: Easy" para este tipo de practicas. Pero en el caso que quiera conseguir una wordlist en sistemas operativos como Parrot, Kali Linux u otro que este enfocado en ciberseguridad generalmente estos sistemas ya vienen con wordlist de forma predeterminada y las mas comunes están en carpetas como:
```
`ls /usr/share/wordlists`
```
![[Dir_Wordlists{{date}}.png]]
y los mas recomendables son la que está en Dirb llamada "big.txt":
```
ls -l /usr/share/wordlists/dirb/big.txt
```
o la que está en DirBuster llamada "directory-list-2.3-medium.txt":
```
ls -l /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
y no es necesario usar estas wordlists de ahuevo pero generalmente sirven en la mayoría de casos aunque por propia cuenta incluso podemos crear una wordlist.

Lo anterior fue con la interfaz grafica pero también está su versión de línea de comandos, para invocar esta herramienta es mediante el siguiente comando:
```
dirb http://10.10.221.238/ /usr/share/wordlists/dirb/big.txt -t 11 -o we-dirb.txt
```
1) Como primer parámetro escribimos el nombre de la herramienta "dirb"
2) Como segundo parámetro Especificamos la URL a tratar.
3) Como tercer parámetro indicamos la ruta absoluta como relativa donde se encuentra la wordlist que vamos a usar, sino indicamos una dirb va a utilizar la predeterminada que es "common.txt"
4) Como cuarto parámetro "-t" para indicar el número de hilos
5) Como quinto parámetro "-o" para indicar como exportar el resultado de la enumeración a un fichero 
**12/08/2026** -----------------------------------------------------------------------------------------------

Existen herramientas distintas para el mismo objetivo, lo que las podría diferenciar es como interactúan estas herramientas con el objetivo, como en el caso anterior con una aplicación web ya que unas pueden ser mas o menos ruidosas o pueden añadir mas funcionalidades que otras, prácticamente la esencia de estas herramientas es hacer un tipo ataque de diccionario, se dice que es un como tipo de ataque de diccionario porque como tal no buscamos acceder a ningún lugar, simplemente descubrir recursos que están ocultos, Dirb y DirBuster no son las únicas herramientas, existen otras como Gobuster, WFUS, UFUS y muchos mas, solo que en el curso que estoy viendo menciona que como esas herramientas si las piden o podrían poner para resolver el examen de eJPT 


**Gobuster** es mucho más completo que **Dirb** y **Dirbuster**, ya que abarca más contextos de enumeración además de directorios ocultos. Aunque en el eJPT es poco probable que se use al haber mejores alternativas para el examen, herramientas como Dirb y DirBuster prácticamente no se usan por ser lentas e inferiores. GoBuster esta hecho en Go que es un lenguaje de programación hecho por Google y tiene todas las ventajas de este lenguaje, por eso se llama GoBuster, Go es un lenguaje de programación que para conexiones y sockets es lo mejor, por lo que la sintaxis de GoBuster es muy simple, como lo siguiente:
1) Escribir primero "gobuster".
2) Escribir parámetros.
3) Escribir argumentos.
El comando para ver comandos disponibles y las banderas es:
```
gobuster -h
```
![[Enumeración de Directorios con GoBuster{{date}}.png]]
GoBuster tiene varios modos de enumeración que no solo se limitan a directorios sino a otros paradigmas y tenemos que indicarle primero eso; cual va a ser el contexto que va a ser la enumeración, tendremos "dir" para hacer enumeración de directorios o ficheros, "dns" para hacer enumeración de subdominios DNS, "fuzz" para hacer fuzzing, "s3" para enumerar buckets a nivel de la nube de amazon, "vhost" para hacer enumeraciones de virtual hosting.

Para el caso de "dir" el comando y parámetros es el siguiente:
```
gobuster dir -u http://10.10.179.41/ -w /usr/share/wordlists/dirb/big.txt -t 11 -x txt,php,bk,zip
```
1) Invocar la herramienta escribiendo: "gobuster"
2) Escoger el modo de operación en este caso: "dir"
3) Escribir "-u" para hacer referencia a la URL a continuación
4) Escribir la URL a enumerar
5) Escribir "-w" para indicar la ruta absoluta o relativa a la wordlist que se va a usar 
6) Escribir "-t" del numero de hilos de conexiones a usar
7) Y por ultimo "-x" para indicar la extensión de los ficheros que queremos que descubra a nivel de extensión por ejemplo: .txt, .php, .bk, .zip
No pude terminar de sacar las capturas ejecutando Gobuster porque la página que estaba usando de prueba (`[http://testphp.vulnweb.com](http://testphp.vulnweb.com)`) estaba caída. Me salía puro error de `timeout` (código 28) y rechazo de conexión (código 7), así que me pasé un buen rato intentando arreglar la red de la máquina virtual. Estuve moviendo los modos de red en VirtualBox de NAT a Puente, reiniciando el `NetworkManager` y checando los DNS pensando que el problema era mi Kali Linux. Al final probé hacerle peticiones a `[http://example.com](http://example.com)` con `curl` y sí respondió sin broncas con un `200 OK`, por lo que confirmé que la red estaba bien y que simplemente el servidor de vulnweb andaba tirado. La sintaxis y los parámetros de Gobuster ya quedaron anotados para aplicarlos si se necesitan. Con la página de ejemplo si pude usar GoBuster:
![[Enumeración de Directorios con GoBuster{{date}}-1.png]]

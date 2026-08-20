La enumeration de Directorios no es igual a "[[Glosario#Fuzzing|fuzzing]]", es un modo parecido pero el modo de ejecución es diferente.

La enumeración es una técnica para poder encontrar recursos ocultos por ejemplo en una aplicación web u ocultos a simple vista como en un hiperenlace, o sea si detectamos un wordpress
![[Enumeración de Directorios{{date}}.png]]
al cual le cambiaron la URL de login y dicha URL no está diferenciada en ninguna parte de la pagina pero uno que tiene una herramienta de enumeración de directorios a traves de una wordlist logramos identificar que por ejemplo el directorio acceso33 existe 
![[Enumeración de Directorios{{date}}-1.png]]
y así podemos conseguir recursos que a simple vista están ocultos, no porque estén ocultos en sí sino que a menos que no sepas la URL completa no puedes llegar a ellos y estas herramientas son las que nos permiten a cierta forma ocultos. Algunos ejemplos de herramientas para este tipo de trabajo son:
1) DirBuster
2) Dirb
3) Gobuster
DirBuster y Dirb son parte de la [[Glosario#eJPT |eJPT]] en el sistema que nos pueden dar para que empiece uno el examen, digamos que es el estandar que usa eJPT pero estos dos (DirBuster y Dirb) son malos y Gobuster es mejor.

La enumeración de directorios no se limita únicamente a aplicaciones web esto se puede proyectar a muchos otros paradigmas como por ejemplo a subdominios, host virtuales o incluso involucrando otros protocolos ajenos a HTTP o HTTPS.

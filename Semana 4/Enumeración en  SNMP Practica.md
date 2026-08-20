Para empezar con la enumeración hay que hacer lo de siempre:

Primero vemos si los puertos SNMP están abiertos, para ver si están abiertos es con Nmap: sudo nmap -Pn -sU -p161 10.0.2.4

![[Pasted image 20260806153116.png]]

cuando ejecutamos ese comando de nmap dos dará información, si esta abierto el puerto 161 o no, como se ve si esta abierto en la maquina Metasploitable3 para el paso 2 se puede usar Nmap, para verificar y ver que versión de SNMP esta usando usamos el siguiente comando:
```
sudo nmap -Pn -sU -sV -p161 10.0.33.4
```

![[Pasted image 20260806153504.png]]

aquí se muestra la versión de SNMP que esta usando que es la versión SNMPv1 y que además nos ayudó también a ver la cadena de comunidad que en este caso es publica. 

En este caso la cadena de comunidad fue fácil de encontrar pero que pasa cuando esto no es así y fue configurada de otra manera, para encontrarlo podemos hacer un ataque de diccionario y existen muchas herramientas para esto como "onesixtyone" a la que le podemos enviar una wordlist para que la herramienta pruebe cada una de estas palabras de esta  wordlist y determine si alguna de estas es el nombre de cadena de comunidad configurada y para enviarle esta wordlist usamos el parámetro "-c" si necesitamos una wordlist para esto podemos crear una propia con base al contexto de la empresa que estemos auditando o descargar alguna que este por la re, en este caso la herramienta contiene una wordlist predeterminada y con esa es suficiente saber que la cadena de comunidad es "public":
![[Pasted image 20260806170155.png]]
 lo siguiente que será como el paso 4 seria ver la enumeración de las potenciales MIBS y para eso se pueden usar varias herramientas como recomendación es "snmpwalk" que es una herramienta que permite recorrer y enumerar un servicio que utilice el protocolo SNMP mostrando en este caso los objetos de SNMP de una forma legible y esa enumeración que nos de hay que filtrarla porque suele ser mucha información porque lo que nos va arrojar esta herramienta es todos los objetos hallados en todas las MIBs que podremos ver tanto el OID como su valor entre otros elementos. Como se usa "snmpwalk" es simple hay que llamar a la herramienta y después le vamos a indicar la versión de SNMP a la que nos enfrentamos que en este caso es "SNMPv1" seguido del parámetro "-c" que es community le indicamos la cadena de comunidad que conseguimos antes que en este caso sabemos que es "public" por lo que tendremos permisos de lectura y acto seguido enviaremos todo esto a un fichero que bien puede llamarse:
```
 snmp_scan.txt": snmpwalk -v 1 -c public 10.0.2.4 > snmp_scan.txt
```
 y para leer el fichero es: 
```
cat snmp_scan.txt
```
 ![[Pasted image 20260806171223.png]]
nos da este chingo de información pero hay que filtrarla, para que sea mas fácil identificar la información los OIDs que pertenecen a la misma MIB tendrán una estructura común en sus primeros componentes por ejemplo:

iso.3.6.1.2.1.1.1.0 tenemos este MIB completo que hay que recordar que el MIB es una colección de definiciones que especifican las propiedad de objetos gestionados en una red y dentro del MIB tenemos componentes

iso.3.6.1.2.1.1.1.0
![[Pasted image 20260806172106.png|380]]

es una estructura jerárquica que va a cambiar dependiendo en tipo de MIB que se use, en este caso es MIB 2 porque es un estandar que podría ser la mayoría de casos.

El primer carácter se le conoce como "root" en este caso es **iso** y puede tener tres valores 1, 2 o 3
![[Pasted image 20260806172339.png|520]]
el 1 correspondieria a la ISO es deci a la Organizacion Internacional del Estandar 
el 2 es para ISO Member Body es decir representa a los cuerpos miembros de la ISO 
el 3 Identified Organization es decir representa organizaciones especificas bajo la raiz de la ISO 

El segundo caracter corresponde a organizaciones 
![[Pasted image 20260806172532.png]]

el tercer caracter corresponde a areas especificas dentro de la organizacion  
![[Pasted image 20260806173019.png]]

el cuarto caracter son las subcategorias dentro de dicha areas con estos estados
![[Pasted image 20260806173107.png]]

el quinto nivel que corresponde a objetos especificos dentro de una subcategoria de la que fue antes mencionada 
![[Pasted image 20260806173205.png]]

el sexto nivel es que especifica lo que nos interesa a nosotros que es la instancia especifica del objeto por consecuencia el valor del OID va a estar cambiando a medida que se asignen nuevos caracteres  
![[Pasted image 20260806173254.png]]

Dicho de otra forma: 1.3.6.1.2 no tendra un valor como tal en el sentido tradicional de datos porque es un nodo intermedio en la jerarquia ya que los OIDs que tienen valores especificos son aquellos que identifican objetos gestionables de forma final  pero en este caso este OID es un OID valido que en este caso indicaria la categoria de gestion dentro de la jerarquuia de internet administrada en este caso por DOT que esta es una organizacion reconocidas por la ISO
![[Pasted image 20260806173545.png]]
 pero en este caso iso.3.6.1.2.1.1.1.0 vale en este caso la cadena de string que como tal es el valor de "sysDescr" es decir la descripcion textual del sistema donde podemos ver el procesador que usa, el SO y demas. Por consecuencia un OID puede variar ya que por ejemplo iso.3.6.1.2 es un OID valido que puede identificar un objeto en cuestion pero si se le añaden mas caracteres a la jerarquia estariamos identificando otro objeto que se corresponde con este nuevo OID 1.3.6.1.2.1: MIN-II (Management Information Base) por lo que de cierta forma los OIDs son dinamicos o "modulares" y de recordatorio un MIB es un conjunto de varios OIDs digamos que los OIDs entre mas caracteres tengan mas especificos son y con menos caracteres mas generalistas son con respecto al objeto que estan identificando.

Para filtrar OID para obtener la informacion que necesites se pueden filtrar desde el fichero donde se habra guardado toda la informacion que la herramienta pudo recopilar. O si se quiere consultar el valor de un OID completo a nivel de un OID que identifique a un objeto en especifico igual se puede hacer con snmpwalk pero tambien se le tiene que enviar el OID en especifico y el resultado es que nos va a responder con su valor asi: 
![[Pasted image 20260810144524.png]]
por lo que todo esto es la metodologia para enumerar SNMP (si queremos filtrar el fichero que generamos con snmpwalk se recomentaria hacer con los comandos de Linux que seria "grab" o con "awk" pero estos comandos son algo de nivel por lo que se deberia de tomar un cursito de linux para hacking etico)

# Enumeración de SNMP con Nmap
Se puede hacer todo lo anterior pero con Nmap y sus scripts pero se explica lo anterior para no depender de una sola herramienta. 

Cuando a Nmap le metemos el parametro "-sC" lanzara scripts de la categoria default que para SNMP son los siguientes: "sysdescr", "snmp-processes" que este consultara los siguientes OIDs![[Pasted image 20260810150016.png]]
que nos va arrojar informacion sobre los procesos en ejecución del sistema operativo del sistema victima y de manera adicional va a lanzar "snmp-netstat" que va arrojar los siguientes OIDs con informacion ssobre las conexiones de red activas en la maquina victima y como ultimo va a lanzar "snmp-win32-services" que va a consultar los siguientes OIDs y nos va a arrojar informacion sobre sobre los servicios de windows que esten en ejecucion:
![[Pasted image 20260810150504.png]]
por lo que el comando a ejecutar seria este:

```
sudo nmap -Pn -sU -p161 --script snmp-sysdescr,snmp-processes,snmp-netstat,snmp-win32-services
```
 por lo que la enumeracion en su mayoria de casos de SNMP sera:
 1) Primero detectar si esta activo si lo está mirar su version
 2) Luego de la version descubrir cual es la cadena de comunidad que esta usando(predeterminada o sino hacer un pequeño ataque de diccionario)
 3) Luego enumerar las MIBs y por consecuencia los OIDs que estén disponibles y con base a ello ya obtenemos la información que queremos y podemos empezar a filtrarla o hacer consultas individuales a los OIDs que nos interesen
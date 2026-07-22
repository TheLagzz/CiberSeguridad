Es prácticamente un constructor de Dorks y es la pagina web "DorkSearch.com" entonces puede ser considerado una automatización de Google Dorking.

Otra forma de automatización es con una herramienta publica en GitHub llamada "Fast Google Dorks Scan" que es un programa de terminal.
Hay que tener en cuenta que como todo hay herramientas publicas que cumplen con su función pero podrían tener algún virus.
# Nmap
Es una herramienta para hacer reconocimiento activo, el reconocimiento activo es lo que implica interactuar directamente con la red o el sistema objetivo como escaneo de puertos o ping para obtener información precisa y técnica. Proporciona datos más exactos pero conlleva un alto riesgo de ser detectado por los sistemas de defensa.

## Parámetros Principales
Los parámetros principales que mas llegaremos a usar es:
- "-sS" que sirve para hacer escaneos TCP SYN Scan también conocido como escaneo semiabierto o escaneo sigiloso.
- "-sT" que es para hacer escaneos TCP es decir para completar el "Three-Way Handshake" cosa que no pasa en el escaneo "-sS" donde el Three-Way Handshake no se completa por lo que es mas sigiloso.
- "-sU" que es para descubrir puertos abiertos que estén corriendo algún servicio que use el protocolo UDP.
- "-p" para indicar los puertos a escanear ya sea uno solo, varios o un rango de puertos si le enviamos a este parámetro un "-" en seguida ("-p-") es lo mismo que hacer -655335 es decir esto va escanear todos los puertos
- "-o" que sirve para identificar la versión del sistema operativo pero este es muy ruidoso y solo se recomienda que se haga en maquinas de bWAPP o en CTFs o meramente en examenes de certificaciones
- "--min-rate" y "--max-rate" para indicar un numero mínimo y un numero máximo de paquetes que va enviar Nmap a los objetivos por segundo, que este numero va a depender mucho de la arquitectura de red que esté montada el que numero de paquetes mínimos y máximos debes elegir
- "-Pn" este parámetro sirve para indicar que nos haga la fase de descubrir si un host está activo o no a través del protocolo ICMP
- "--script" para ejecutar un script dentro del escaneo hay que tener en cuenta que estos scripts están escritos en LUA que se pueden ver en "ls /usr/share/nmap/scripts/" 
- "-sC" para enviar los scripts pero únicamente los de categoria default que básicamente es lo mismo que hacer un "--script default"
- "-sV" permite tener mas información de las versiones de los servicios ya que aquí obligamos a Nmap a consumir dichos servicios y extraer información de ellos por ejemplo a través de los banners
- "-oN" para exportar la salida de los escaneos en diferentes formatos sea .nmap .xml y .gnmap
- "--open" para durante el escaneo únicamente nos muestre los puertos abiertos.
- "-v" que también puede expandirse mas para obtener mas información hasta "-vvv", la información de los escaneos es en tiempo real.
Se puede escanear con Nmap de una manera mas profunda lanzando los scripts predeterminados y consumiendo los servicios para obtener sus versiones pero esto genera mucho trafico en la red, se podría hacer en puertos existentes pero no es muy optimo porque puede tardar mucho el escaneo y generará mucho trafico en la red innecesario y si hay un elemento de seguridad sensible, lo siguiente seria lo ideal:
- Escaneo sigiloso a todos los puertos (lo mas ligero y silencioso posible para así detectar todos los puertos abiertos)
- Con base a todos lo puertos abiertos darles con la silla jajaja (los que se permitan)

### Ejemplo
Lo que podríamos hacer es un "sudo nmap -sS -Pn -n --min-rate 3333 --max-rate 4756 --open 10.0.33.4  -oX raw.xml" lo que si se debería hacer es guardar el output después de cada escaneo.
Y una vez que descubrimos los puertos abiertos hay que hacerles algo y podemos enviarle los scripts predeterminados mediante "-sCV -p21, 22, 80, 135, 445, 3306 10.0.33.4 -oN final.nmap" (los números son los puertos abiertos que se podrían haber encontrado) y nuevamente también se guarda y exporta. 

Existen herramientas que puedes hacer uso de estos scripts como RustScan o AutoRecon.
# ¿Qué es internet?
Internet es un **sistema distribuido de conmutación de paquetes** basado en el protocolo TCP/IP. No es una nube, es una **topología de nodos interconectados** (routers, servidores, cables y satélites) donde la información viaja fragmentada y por rutas dinámicas. Para la seguridad, esto implica que **no hay un centro que defender**, sino miles de millones de puntos de entrada, y que el control de ruta (el enrutamiento) es tan vulnerable como el contenido que transporta.
# ¿Qué es una red o networking?
Red o también llamado _networking_, es el sistema de dispositivos (computadoras, servidores, teléfonos) enlazados entre sí mediante cables o conexiones inalámbricas. Permite que los equipos colaboren y compartan datos, bases de información, impresoras o acceso a Internet. Incluye el hardware (como _routers_ y _switches_) y el software que administra cómo viaja la información entre los equipos.
## Tipos
- Redes Privadas:
- Redes Públicas:
# Marcadores o huellas
Los dispositivos tienen huellas o mejor dicho tienen medios de identificación pero siendo uno que no cambia.
- Dirección IP
- Dirección de Control de Acceso a Medios (MAC) es como un numero de serie(no cambia).

# Direcciones IP
Una dirección IP se puede utilizar para identificar un host en una red durante un periodo de tiempo donde la dirección IP luego se puede asociar con otro dispositivo sin que cambie la dirección IP. Una dirección IP se divide en segmentos, para conocer una IP se divide de la siguiente forma:

| Octeto 1 | Octeto 2 | Octeto 3 | Octeto 4 |
| -------- | -------- | -------- | -------- |
| 192.     | 168.     | 1.       | 1        |
| 0-255    | 0-255    | 0-255    | 0-255    |
Una IP o dirección IP es un conjunto de números que se dividen en cuatro octetos. El valor de cada octeto se resumirá como la dirección IP del dispositivo en la red. Este número se calcula mediante una técnica conocida como direccionamiento IP y subredes. Las direcciones IP pueden cambiar de un dispositivo a otro, pero no pueden estar activas simultáneamente más de una vez dentro de la misma red.

Las direcciones IP siguen un conjunto de estándares conocidos como protocolos. Estos protocolos son la columna vertebral de las redes y obligan a muchos dispositivos a comunicarse del mismo modo. Los dispositivos pueden estar tanto en una red pública como privada. Dependiendo de dónde se encuentren determinará qué tipo de dirección IP tienen: una dirección IP pública o privada.

Se utiliza una dirección pública para identificar el dispositivo en Internet, mientras que una dirección privada se utiliza para identificar un dispositivo, entre otros dispositivos

**Ejemplo:**

| Nombre del Dispositivo | Dirección IP | Tipo de Dirección IP |
| ---------------------- | ------------ | -------------------- |
| DESKPTOP-KJE57FD       | 192.168.1.77 | Privado              |
| DESKPTOP-KJE57FD       | 86.157.52.21 | Público              |
| CMNatic-PC             | 192.168.1.74 | Privado              |
| CMNatic-PC             | 86.157.52.21 | Público              |
![[Pasted image 20260708183322.png]]
Estos dos dispositivos podrán utilizar sus IP privadas para comunicarse entre sí sin embargo cualquier dato enviado desde internet desde cualquiera de los dispositivos será identificado por la misma dirección IP pública, las direcciones IP públicas son proporcionadas por el Internet Service Provider (**ISP**) o en español dicho como el Proveedor de Servicios de Internet.

# ¿Qué es IPv4?
Es un protocolo de internet, mejor dicho como Protocolo De Internet Versión 4, es el sistema de direccionamiento fundamental que permite a los dispositivos conectarse e identificarse en internet. Utiliza direcciones numéricas de 32 bits ( $2^{32}$ ) que al final dan como resultado 4,29 mil millones de direcciones IP, que están compuestas del 0 a 255 separados por puntos como el que se vio en el ejemplo anterior (192.168.1.77)

# ¿Qué es IPv6?
Como el problema que surge de IPv4 es la escases de direcciones IP, con IPv6 proporciona hasta $2^{128}$ direcciones IP que son mas de **340 billones de direcciones IP** y también proporciona mas eficiencias gracias a nuevas tecnologías. Las direcciones con IPv4 y IPv6 son distintas:

![[Pasted image 20260708185411.png]]

# Direcciones MAC
Todos los dispositivos de una red tendrán una interfaz de red física, que es una placa de microchip que se encuentra en la placa base del dispositivo. A esta interfaz de red se le asigna una dirección única en la fábrica en la que se construyó, llamada a **MAC** (Media Access Control). La dirección MAC utiliza 12 caracteres en hexadecimal, dividido de dos en dos y separado por dos puntos, a los dos puntos se les llama "separadores". Por ejemplo: _a4:c3:f0:85:ac:2d_. 
Los primeros seis caracteres representan la empresa que creó la interfaz de red y los últimos seis son un numero único.
![[Pasted image 20260708190802.png]]
Algo interesante con las direcciones MAC es que pueden ser falsificadas o "suplantadas" en un proceso conocido como _spoofing_. Esta suplantación ocurre cuando un dispositivo de red finge identificarse como otro utilizando su dirección MAC. Cuando esto sucede, a menudo puede romper diseños de seguridad mal implementados que asumen que los dispositivos que se comunican en una red son confiables.

Considera el siguiente escenario: un firewall está configurado para permitir cualquier comunicación hacia y desde la dirección MAC del administrador. Si un dispositivo simulara o hiciera "_spoofing_" de esta dirección MAC, el firewall pensaría que está recibiendo comunicación del administrador cuando no es así.

Lugares como cafeterías, cafés y hoteles por igual suelen utilizar el control de direcciones MAC cuando se hace uso de sus redes de "Invitados" o "Públicas".

# ¿Qué es ICMP?
El Protocolo de mensajes de control de Internet (ICMP) es un protocolo que se utiliza dentro de una red para comunicar problemas con la transmisión de datos. En esta definición de ICMP, una de las principales maneras en que se utiliza un ICMP es determinar si los datos llegan a su destino y en el momento correcto. Esto hace que el ICMP sea un aspecto importante del proceso de generación de informes de errores y de las pruebas para ver qué tan bien una red está transmitiendo datos. Sin embargo, también se puede utilizar para ejecutar ataques de denegación de servicio distribuida (DDoS).
## Usos de ICMP
El protocolo **ICMP** (Internet Control Message Protocol) se utiliza principalmente para tres propósitos:

- **Informe de errores:** Si los datos no llegan correctamente a su destino, el dispositivo receptor o un enrutador intermedio envía un mensaje ICMP al emisor informando del problema (por ejemplo, si un paquete es demasiado grande y el enrutador tiene que descartarlo).
    
- **Herramientas de diagnóstico (Rendimiento de red):**
    
    - **Ping:** Mide de forma simple cuánto tiempo tardan los datos en viajar entre dos puntos mediante _solicitudes de eco_ (Echo Request) y _respuestas de eco_ (Echo Reply).
        
    - **Traceroute:** Muestra la ruta exacta (los enrutadores o "saltos") que recorre un paquete hasta su destino y el tiempo que tarda entre cada dispositivo, lo que permite identificar en qué punto de la red hay retrasos.
        
- **Ataques de denegación de servicio (Uso malicioso):** Se puede utilizar para saturar un dispositivo y degradar el rendimiento de la red mediante técnicas como la **inundación de ICMP (ICMP Flood)**, el **ataque Smurf** y el **Ping de la muerte (Ping of Death)**.
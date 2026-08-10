 SNMP es un protocolo que significa Simple Network Management Protocol este es de la Capa de Aplicacion que se basa en el protocolo IP para poder intercambiar informacion por ejemplo entre una solucion administrativa de red y cualquier dispositivo que soporte SNMP porque generalmente estos protocolos se encuentran entre dispositivos de red a nivel de hardware como routers o switches pero igualmente se pueden implementar en servidores. Este protocolo se usa para la administracion de redes para monitoreas y gestionar dispositivos que esten conectados a una red, como impresoras, firewalls o dispositivos de IoT osea con la mayoria de dispositivos.

Algo importante es conocer sobre la base de datos de gestion o MIB (Management Information Base) es una coleccion estructurada de objetos que pueden ser gestionados en una red, en este contexto un objeto es una variable a nivel de la gestion que representa una caracteristica muy especifica de un dispositivo de red como por ejemplo:

sysName que es una variable dentro de la base de datos del MIB que es fundamental para el protocolo SNMP, en este caso este objeto es una variable que por consecuencia va almacenar un valor que en este caso va a ser el nombre del sistema operativo

sysDescr esta variable va almacenar una descripcion textual del sistema operativo
 Van a ver muchisimos objetos en el MIB pero estos son unos ejemplos.

Hay que tener en cuenta que cada objeto dentro del MIB para que pueda ser diferente cada uno va a tener un identificador unico llamado Identificador de Objeto o por sus siglas en ingles OID (Object IDentifier) por ejemplo el objeto sysDescr este cuenta como un OID que generalmente va a ser el siguiente: 1.3.6.2.1.1.1.0 (en MIB-II (RFC 1213)) por lo que es un estandar asi que asi siempre lo vas a encontrar, lo que si puede cambiar en la version del MIB que se este usando en el protocolo SNMP por lo que dependiendo del MIB cambiaran los OID y generalmente algun dispositivo va a tener varias versiones de MIB por lo que podremos consultar multiples OID y por consecuencia puede tener objetos redundantes o info similar ya ahi solo deberiamos filtrar la informacion.

Los las categorias para MIB son como las siguientes:

1) Estandar
2) Propietarias de Aplicaciones
3) Sistemas Operativos
4) Seguridad
5) Hardware
6) Redes Inalambricas
7) Almacenamiento
MIB-II (RFC 1213) es de las MIB mas comunmente utilizadas donde se definen objetos de gestion muy basica para dispositivos de la red que podrian ser los que uno podria encontrar en la mayoria de casos y podrian tener muchos MIB pero depende de muchisimas cosas pero basicamente todo en por la configuracion que se haya querido hacer previamente en la infraestructura  de red.

Pero en resumen hay que quedarse como que el MIB es una base de datos estructurada concretamente de objetos que  son definidos y estos objetos nos dan informacion muy variada que nos puede servir para obtener mas informacion del activo que vayamos a auditar y que cada objeto es identificado por un ID unico que llamaremos OID y es como tal consultando cada uno de estos OID en donde esta la informacion que nos puede ayudar.

El protocolo SNMP ademas que tiene MIB y dentro de los MIB hay OIDs hay mas elementos que nos pueden ser de utilidad como el NMS (Network Management System) que como tal es un software o conjunto de software que administraran y monitorearan los dispositivos en la red mediante el SNMP

Adicionalmente existe el Agente SNMP que va a ser el software que va a residir en los dispositivos de red y que se va a comunicar en este caso con el NMS estos agentes van a recopilar informacion de la MIF y se la van a enviar el NMS.

Existe el PDU (Protocol Data Unit) como tal van a ser las unidades de datos utilizadas en la comunicacion  atraves de este protocolo.

Por otro lado tenemos el TRAP o notificaciones que son como tal estos mensajes enviados por los agentes al NMS para informar de eventos o cambios de estados que sean relevantes.

Otra cosa a tener en cuenta es las versiones de este protocolo (SNMP) actualmente tiene 3. La version 1 y 2 no cuentan con cifrado cosa que en la version 3 si se cuenta, pero generalmente donde se puede enumerar mas facil y rapido es en la version 1 y 2, que la version 2 (SNMPv2) se divide a su vez en tres versiones o subversiones SNMPv2p(Party-Based), SNMPv2c(Community-Based) y SNMPv2u(User-Based). La unica version que digamos mas funcionó fue la Community Based porque en este caso utiliza cadenas de comunidad para controlar el acceso en este caso a la informacion que maneja este protocolo.

# Cadena de Comunidad (Community String o Cadena SNMP)
 Este es como tal un mecanismo de autentificacion simple que se puede implementar tanto en la version 1 de SNMP como en la version C de SNMP para controlar de esta forma el acceso de los agentes a la informacion del SNMP, es como una clave de acceso que pueden usar los agentes y como tal existen dos tipos de la Community String que es la READ ONLY (ro) que unicamente permite acceso de lectura en este caso el NMS podra ser unicamente operaciones de lectura sobre los objetos SNMP en la MIF de este caso el dispositivo que este usando este protocolo y el otro tipo es Read-Write (rw) en este caso el NMS puede tanto leer como modificar los valores dentro de los objetos de la MIB( creo es eso)  y como tal para la cadena de comunidad para el tipo Read Only es la cadena Read-Only(RO)-> public mientras que para la cadena Read Write era RW la cadena de comunidad es private ya que en muchas ocaciones esta cadena se puede alterar por ejemplo las personas que administren el servidor que estemos auditando por lo que podriamos hacer un ataque de diccionario para descubrir cual es esta cadena de comunidad que se esta usando y una vez obtenida empezar a hacer las consultas a este protocolo y es que se suele dejar de forma predeterminada la cadena de la comunidad por lo que es muy simple ya que conociendo que podriamos tener una cadena o bien llamda public o bien llamada private es simplemente cuestion de probar cual de estas dos cadenas nos funciona a la hora de hacer las consultas a este protocolo y si se da el caso de que la cadena se sigue usando con su nombre de forma predeterminada y no se haya alterado de forma indirecta tendriamos la clave para poder acceder a informacion sensible que dependiendo el caso podriamos unicamente leer o leer y modificar y esto principamente se va a ver en SNMP de version 1 y en SNMP de version 2 C.

No existe una metodologia a seguir como tal para SNMP para enumerar este protocolo pero si hay algunas formas de intentarlo de la mejor manera porque no es un protocolo no tan conocido ni tan comun y puede llegar a ser confuso por tantos terminos si no se han visto antes pero la forma o metodologia que puede ayudar es simple y es la siguiente:
1) Detectar si hay un puerto abierto corriendo con este protocolo que usualmente este protocolo suele estar corriendo en el 161 por  UDP y es importante que es UDP porque el escaneo con Nmap tiene que ser bajo puertos UDP no TCP 
2) Determinar la version de SNMP igualmente con Nmap porque apartir de la version sabremos de que forma podemos empezar a enumerar 
3) Si la version es 1 o es la version 2 C  hay que hacer el descubrimiento de la cadena de comunidad por lo que ya sabemos que puede ser tanto "public" como "private" de forma predeterminada pero si en este caso la cambiaron podriamos hacer un ataque de diccionario para intentar descubrir dicha cadena si resulta ser private o public pues el ataque de diccionario podemos saltarlo.
4) Hay que hacer la enumeracion del MIB o de los MIBs que se esten usando y cuando enumeremos los MIB de forma indirecta tambien vamos a enumerar todos los objetos que esta o estas puedan contener, evidentemente objetos identificados cada uno con un OID
5) Consultar la informacion en especifico de cada OID para por ejemplo obtener el nombre del sistema operativo o el sistema operativo que se esta usando o ver las interfaces de red del sistema operativo y en general la informacion que queramos de los objetos contenidos dentro de las MIBs 

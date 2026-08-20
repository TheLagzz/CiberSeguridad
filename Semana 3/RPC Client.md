rcpclient es un herramienta pero no es una herramienta que la ejecutamos y ya sino que accederemos a una linea de comandos dentro de ella donde se agregaran nuevos comandos que unicamente aplican en este contexto, para esto el comando para activar esta herramienta es: rcpclient -U "(usuario)%(contraseña) (direccionIPdelobjetivo)", para mi maquina queda como rpcclient -U "vagrant%vagrant" 10.0.2.4. Con esto entramos a la linea de comandos que nos ofrece RPC Client  estamos logueados como el usuario que ingresamos con las credenciales validas.

Algunos comandos que se pueden usar son:

**enumdomusers** para enumerar todos los usuarios del dominio **en el servidor**

![[Screenshot 2026-07-28 170821.png]]
tambien podemos buscar usuario con su "rid" despues de usar enumdomusers como el siguiente:
**queryuser 0x1f4** que usa el del administrador como se ve en la captura anterior![[Screenshot 2026-07-28 171106.png]]
lo que significa "rid" son las siglas de **Relative IDentifier** es un identificador que se asigna de forma unica pero a cada cuenta de usuario y grupo en un dominio formando parte del **SID** (Security IDentifier) haciendonos poder distinguir en cierta forma las diferentes cuentas que existen dentro del mismo dominio.

tambien tenemos el siguiente comando:

enumdomgroups
![[Screenshot 2026-07-28 171423.png]]
que es interesante porque ayuda a identificar en este caso la estructura del dominio y posibles privilegios informacion que nos puede ser util en futuras fases adicionalmente que podemos hacer consultas por el "rid"
para poder ver que otras enumeraciones puede tener rpcclient podemos escribir "enum" y nos dira cuales enumeraciones podemos tener cuando le debos dos veces a Tab:
![[Pasted image 20260728173612.png]]
tambien si queremos usar query o consultas mediante el "rid" de cada grupo
![[Pasted image 20260728173644.png]]

Lo mejorcito para la enumeracion y que se suele recomandar segun lo aprendido es que primero enumere a fondo con Nmap y ya luego con cada herramienta ya que dependiendo el contexto y la infraestructura que se pueda encontrar se van a tener que suar distintas herramientas.

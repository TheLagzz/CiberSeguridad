Después de haber obtenido credenciales de la manera que sea por recursos compartidos o cualquier otra forma posible, ahora que tenemos credenciales lo que hay que ver es como podemos emplearlas para seguir enumerando en este caso el protocolo SMB y hacer uso de las credenciales con herramientas vistas antes como "SMB client" "Enum for linux" "crackmapexec" y "nmap" y otra herramienta que se puede ver como "rcp client" y esta herramienta se puede usar sin credenciales pero con credenciales es mucho mejor y hata RCP Client puede darnos incluso muchisima mas información que las herramientas antes mencionadas.

Me la pasé un buen rato fijando y explorando como configurar la maquina virtual Metasploitable3 y haciendo que la maquina virtual Metasploitable3 y Kalilinux puedan visualizarce mutuamente, todo esto para que desde la terminal de kalilinux pueda ejecutar un ping para ver si se pueden comunicar y como si pude al menos pude hacer uso de nmap para saber que puertos tiene activos o abiertos. 
![[Pasted image 20260727203206.png]]
28/07/2026
bueno ahora si ya jalo la maquina virtual de metasploitable3 windows, para hacer uso de la herramienta "smbclient -L (dirección ip) -U (nombredeusuario)%(contraseña)" que en este caso seria smbclient -L 10.0.2.4 -U vagrant%vagrant.
![[smbclient_metasploitable3.png]]ahora tambien se puede hacer uso de otra herramienta para obtener informacion con credenciales, **enum4linux** que como dije sirve aun si no tienes credenciales pero cuando tienes credenciales te da un chingo de información muy buena, por lo que podemos hacer uso de esta herramienta con el siguiente comando "enum4linux -S -u (nombredeusuario) -p (contraseña)" y lo tendriamos que poner de esta manera para metasploitable3 enum4linux -S -u vagrant -p vagrant. "-S" significa Share "-U" significa users
![[Screenshot 2026-07-28 141000.png]]
![[Screenshot 2026-07-28 141046.png]]
nos da toda esta fokin informacion muy interesante porque estamos usando credenciales. Podemos usar "-U" para mostrarnos los usuarios del sistema
![[Screenshot 2026-07-28 141329.png]]![[Screenshot 2026-07-28 141431.png]]
y debemos siempre estar almacenando esta información que podríamos utilizarlo para alguna otra cosa. Tambien podemos hacer uso de "-a" que significa **all** para poder llegarle hasta el alma al protocolo SMB
![[Screenshot 2026-07-28 141737.png]]
# Uso de crackmapexec para el protocolo SMB con credenciales
Podemos usar tambien la herramienta "crackmapexec" haciendo uso del siguiente comando "crackmapexec smb (direccionipdelamaquina) -u (usuario) --(lo que queremos enumerar)" como el siguiente comando crackmapexec smb 10.0.2.4 -u vagrant -p vagrant --shares para ver los recursos compartidos
![[Screenshot 2026-07-28 143915.png]]
para ver usuarios es crackmapexec smb 10.0.2.4 -u vagrant -p vagrant --users![[Screenshot 2026-07-28 144057.png]]
tambien podriamos hacer uso de esta misma herramienta para ejecutar comandos si lo tenemos permitido, como este comando: crackmapexec smb 10.0.2.4 -u vagrant -p vagrant -x 'ipconfig'
![[Screenshot 2026-07-28 144901.png]]
y asi conseguimos ejecutar un comando en su maquina para tener informacion por medio de ipconfig![[Screenshot 2026-07-28 145145.png]]
y tambien otro ejemplo de ejecucion puede ser con "whoami" para saber y mostrar el nombre del usuario actual, el dominio y los permisos de la cuenta que ha iniciado sesion en la consola.

# Enumeracion con Nmap
Podemos hacer uso de la herramienta Nmap para hacer lo mismo pero es un chorrote que siento yo que no podria ser necesario tanto comando para algo que se hace mas rapido con las otras herramientas, el comando que se puede usar es:
nmap --script smb-enum-* --scripts-args 'smbuser=vagrant, smbpass=vagrant' -p 445 10.0.2.4
![[Screenshot 2026-07-28 165926.png]]
y hay mas info pero realmente un buen, tal vez no toda sirva pero ahi está solo no pongo mas porque se me satura mas la hoja.

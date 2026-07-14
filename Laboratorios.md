Lo vamos a meter las maquinas en Kali Linux. Desde nuestro Kali Linux nos vamos a conectar a maquinas en la nube que nos ayudaran a aprender a hacerlas vulnerables. Para pentesting web o de sistemas de redes. Los enfoques están enfocados en eJPTv2 para el curso de YouTube Hixec.

# Conectarse a Laboratorios mediante OpenVPN
Lo básico que se debe saber sobre los laboratorios en plataformas como TryHackMe o HackTheBox es que no se descarga como tal una maquina virtual sino un archivo de configuración (.ovpn) este archivo se ejecuta con el cliente OpenVPN en el que ya viene preinstalado por defecto en sistemas orientados a ciberseguridad como fue antes dicho en el apunte anterior.

# ¿Cómo conectarse y ejecutar?
Para poder conectarse el archivo se debe ejecutar obligatoriamente con permisos elevados (**sudo**). Una vez la conexión es exitosa se crea una nueva interfaz de red en el sistema (comúnmente llamada tun0) a la cual se le asigna una IP correspondiente a la red interna de los laboratorios, en una ejecución normal la terminal donde fue ejecutada y se lanzo el comando queda inutilizable porque el proceso en primer plano. Pero para no tener una venta de terminal bloqueada se puede mandar la ejecución a segundo plano añadiendo un **&** al final del comando todo esto enviando toda la salida de texto  a **/dev/null**.
### Automatización con Alias
Para no tener que escribir todo el comando largo cada vez para estudiar se puede editar el archivo de configuración del shell **(.bashrc o .zshrc)**. De esta manera al escribir ese alias la conexión VPN se levanta automáticamente como usuario root y en segundo plano. (Es un pedotote pero supongo que si ahorra tiempo jajaja)

### Matar el proceso de OpenVPN
Si necesitamos matar el proceso de manera limpia podemos usar **sudo killall openvpn**.


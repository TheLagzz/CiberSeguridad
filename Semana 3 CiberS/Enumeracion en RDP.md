Primero hay que saber como siempre que significan las siglas, RDP significa Remote Desktop Protocol que es un protocolo desarrollado por Microsoft que permite a los usuarios conectarse de forma remota a una interfaz grafica de un dispositivo que use este protocolo principalmente para hacer labores de administracion remota y en entornos empresariales este protocolo se usa mucho y los servicios que usan este protocolo generalmente corren en el puerto 3389.

# ¿Qué podriamos hacer nosotros para enumerar?
Nmap en muchos aspectos es suficiente para enumerar RDP.

Los pasos para enumerar RDP serian los siguientes:

1) ¿Existe vida ahí? Para saber si el puerto esta abierto mediante un: nmap -Pn -p3389 (direccionIP)
2) Despues enviar algunos de estos scripts para enumerar como: nmap -sCV --script rdp-enum-encryption, rdp-vuln-ms12-020, rdp-ntlm-info -p3389 (direccion IP) y estos scripts no estan incluidos en la categoria default de Nmap o no todos
rdp-enum-encryption lo que hace es enumerar los metodos de cifrado que estan soportados por el servidor RDP

rdp-vulv-ms12-020 este script comprueba si el servidor RDP es vulnerable a alguna vulnerabilidad critica que se reportó en el boletin de seguridad de microsoft conocido como ms12-020 vulnerabilidad que permite la ejecucion remota de codigo debido a una falla que hubo en esa version

rdp-ntlm-info que esta se encarga de recopilar la información de la autentificacion ntlm del servidor RDP y nos brindara informacion como el nombre del dominio el nombre del servidor y la version del sistema operativo esto sin necesidad de que estemos logueados que es bueno para recopilar mas datos de como esta configurado el sistema victima

![[Pasted image 20260730191943.png]]
estaba intentando ese comando y quise que se solucionara dandole permisos o ejecutandolo con sudo pero sigue marcando lo mismo

nambre no pude hacer que funcionara bien el comando, ni Gemini pudo ayudarme que es lo que pasaba, todo el rato que estuve fue de investigacion con Gemini y aprueba y error de mi parte.

31/07/2026

Despues de un ratotote ya pude ver que problema habia del porque no jalaba el comando completo, pues el script de encryption tiene ya un estandar para cifrados modernos y la maquina virtual Windows Metasploitable3 es de hace ya una decada y usa un cifrado viejo y el script no esta preparado para esos cifrados y pues lo mandaba a la chingada por la version que tenia. Pero mira nada mas el problema es por tener versiones recientes de Nmap y KaliLinux que no podemos enumerar bien y rapidamente las versiones de la maquina objetivo, de que s epuede se puede pero con muchos cambios  tal vez bajando una version menos actualizada de Nmap porque la version del instructor del video su Nmap es la version 7.94 y la mia es 7.98SVN, lo que le salio al instructor seria algo asi:![[Pasted image 20260731175315.png]]

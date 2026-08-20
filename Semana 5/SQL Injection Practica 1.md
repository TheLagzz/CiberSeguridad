Para estas practicas se hará uso de la plataforma PortSwigger, la Web Security Academy (WSA) en los laboratorios correspondientes a las inyecciones SQL, los laboratorios a resolver son:

![[SQL Injection Practica 1{{date}}.png]]
Ya dentro del laboratorio nos manda a una pagina web en el mismo navegador como esta, que seria el primer laboratorio:
![[SQL Injection Practica 1{{date}}-1.png]]
En este caso el laboratorio nos enseña una tienda donde podemos seleccionar varios productos, adicionalmente que se pueden ver sus categorías, el problema aquí es como identificar potenciales puntos para inyectar código SQL y provocar potencialmente una inyección SQL si es que la hay; lo que hay que observar es que se puede hacer en cualquier input que se vea, ya sea en la URL porque se envia por GET en la propia página que se esté auditando, todos los inputs son potenciales vías de entrada, por lo que en este laboratorio se observa en la URL de la página de la tienda que hay un parámetro llamado "category" que está llamando en este caso la categoría "Gifts":
![[SQL Injection Practica 1{{date}}-2.png]]
![[SQL Injection Practica 1{{date}}-3.png]]

Por lo que podríamos deducir que en este caso "Gifts" es un dato dentro de la base de datos que está por detras de este sitio web y concretamente de esta página y que "category" puede ser una columna que almacene varios datos, entre ellos "Gifts" y las demás categorías en la tienda y que a su vez como esta es una columna tiene que estar dentro de una tabla, y en este contexto la tabla pues es evidente, si las categorias filtran productos pues la tabla posiblmente sea de productos, productos que tengan más datos almacenados en columnas como su nombre, su precio, su categoría y más cosas, por lo que en este caso puede ser una potencial vía de inyección de código SQL y podríamos hacerlo desde la misma URL. (Deberíamos abrir BurpSuit para entenderlo mucho mejor y se pasará todo el tráfico del navegador por el proxy de BurpSuit haciendo uso de la extensión FoxyProxy)

(Debo checar como se usa BurpSuit e instalarlo junto con FoxyProxy)
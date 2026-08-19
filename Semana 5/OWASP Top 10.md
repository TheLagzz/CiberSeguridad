# ¿Qué es OWASP Top 10?
El OWASP Top 10 es una lista que cataloga las 10 principales vulnerabilidades a nivel de aplicaciones web, es una organización internacional sin fines de lucro y esta lista se renueva cada 3 años basada en nuevas investigaciones principalmente en el contexto de la ciberseguridad en este momento (el momento en que salga la lista) y de las aportaciones que haga la comunidad a nivel global. El propósito de esta lista es funcionar como un punto de referencia al nivel de cuales son las vulnerabilidades mas criticas y mas comunes en aplicaciones web, dicho de otra forma las vulnerabilidades que aparecen aqui son posiblemente las que consiga en el mundo real porque son las mas comunes y de hecho para muchas certificaciones a nivel de pentesting web muchas se basan en esta lista para clasificar como va a ser su examen o su contenido a la hora de formar al estudiante. 

# Vulnerabilidades para Pentesting Web

## SQL Injection
Una inyección SQL es una vulnerabilidad que le permitiria a un atacante romper una consulta SQL que esté previamente definida y luego de romperla inyectar instrucciones SQL para alterar así el funcionamiento de la base de datos y por consecuencia poder obtener información confidencial hallada en esta. Esta vulnerabilidad principalmente se produce porque no se hace una correcta sanitización de los datos que ingresan al servidor a través de una consulta SQL donde el usuario puede ingresar datos, por ejemplo:

Digamos una aplicación web que tiene un formulario de inicio de sesión donde le pide al usuario su nombre de usuario y la contraseña, la aplicación luego compara la entrada del usuario con la información almacenada en su base de datos para verificar así la identidad del usuario, es decir la consulta que podría ejecutarse en el servidor podría ser un:
```
SELECT * FROM usuarios WHERE nombre_usuario = 'entrada' AND contrasena = 'entrada'
```

suponiendo que hay un usuario legitimo que quiere ingresar, digamos que se llama "Naruto" que tiene la contraseña "Sasuke" pues una consulta legitima sería:
SELECT * FROM usuarios WHERE nombre_usuario = 'naruto' AND contrasena = 'sasuke' que de ser correcta puede acceder a la intranet.

Pero que pasaría ahora si por ejemplo Sasuke no tiene un usuario pero igualmente quiere acceder pues simplemente Sasuke pondría de nombre de usuario "Naruto" pero como no sabe sus contraseña podría romper la consulta y lo podría ser de multiples formas, una forma simple sería comentando por ejemplo con dos guiones (todo lo que esté despues de los dos guiones será comentado por lo que se va ignorar lo que le siga):
```
SELECT * FROM usuarios WHERE nombre_usuario = 'naruto' --' AND contrasena = '33'
```
provocando que parte de la consulta se comente y no se ejecute dando así lugar a que la lógica de la consulta cambie, donde en este caso seleccionaríamos todo desde la tabla de usuarios donde el nombre el nombre de usuarios sea igual a Naruto y a secas por lo que en este caso la condición que "aseguraría" la seguridad de estos datos no estaría y si digamos la aplicación web no valida o escapa adecuadamente esta entrada de datos "Sasuke" podrá acceder a la intranet como el usuario de "Naruto", en auditorias reales no lo vas a tener tan fácil como esto, en algunos casos las inyecciones SQL que se consigan parezcan absurdas y si lleguen a ser mu fáciles de explotar, pero mayoritariamente los payloads a usar no van a ser tan simples como simplemente comentar la consulta, ahora si que el chiste o el enfoque de una inyección SQL es solo alterar la consulta intuyendo en este caso como sería la consulta, ya que por lo general o a menos que sea una auditoria Whitebox no se obtendrá la consulta como tal para poder analizarla.

## Tipos de Inyecciones SQL
Las inyecciones SQL se pueden clasificar en tres tipos y esto se hace con la base a las diferencias en los métodos de ataque y extracción de datos, así como las condiciones bajo las cuales cada técnica es mas efectiva, estos tipos son "In-Band", "Out-of-Band" y "Blind" o "Inferenciales".

Dentro de cada una de estas tres, a su vez se tienen varias subcategorías de inyecciones SQL que básicamente entran en cada categoría correspondiente pero se diferencian en la forma de ser explotadas.

### In-Band
Las inyecciones SQL "In-Band" o "En Banda" son las mas comunes que se pueden conseguir y se caracterizan porque podemos explotarlas usando el mismo canal de comunicación
![[OWASP Top 10{{date}}-1.png]]
el mismo que se usaría para recoger los datos habitualmente y a su vez este tipo se divide principalmente en dos subcategorías, las "Error-Based" y las "UNION-Based".

Las "Error-Based" implica deliberadamente consultas SQL que intencionalmente estén mal formadas para provocar así mensajes de error dentro del sistema gestor de bases de datos y que estos mensajes a su vez nos los muestren en el frontend de la aplicación web para que de esta forma pueda revelarnos información critica sobre la infraestructura de la base de datos, es decir, buscamos un error para que nos muestre mas información a raíz de este error.
![[OWASP Top 10{{date}}.png]]

### UNION-Based
Estas se basan en que usamos la cláusula UNION para combinar los resultados de dos o mas SELECT en una unica consulta, lo que nos permitiría así extraer datos de las otras tablas

### Out-of-Band
Esta se produce cuando no podemos usar el mismo canal para lanzar los ataques y recoger la información y estas no son tan comunes, se pueden conseguir y es posible pero no son tan comunes como las otras.

### Blind - Inferenciales
Estas inyecciones a ciegas se les llaman así porque nosotros como auditores enviamos datos al servidor y debemos observar el comportamiento de la aplicación para de esa forma inferir si la consulta SQL inyectada se ejecutó correctamente o no ya que como tal aquí no mostrará ningún tipo de aviso o de error, que nos puede indicar si realmente el payload que enviamos se ejecutó con éxito o no, por eso es a ciegas y las inyecciones SQL a ciegas se dividen a su vez en dos subcategorías las "Boolean-Based" y las "Time-Based". Las "Boolean-Based" se trata de realizar consultas SQL que devuelvan un resultado booleano (verdadero o falso) y observar así los cambios en el comportamiento de la aplicación web mientras que las "Time-Based" se trata de introducir retrasos en la respuesta del servidor, inyectando así consultas que hacen que el servidor de la base de datos espera antes de responder, es decir, enviar el payload pero dentro del payload por ejemplo a través de una función o instrucción del lenguaje SQL, pedirle al servidor que después de ejecutar la consulta, espere por ejemplo unos 11 segundos para darnos la respuesta, hay que usar la lógica, si nos devuelve una respuesta en menos o mas de 11 segundos pues el código no se ejecutó correctamente y si lo hace exactamente en 11 segundos entonces si lo hizo correctamente,.
Google u otros buscadores tienen ciertos operadores que permiten filtrar mas la información, cada uno de estos operadores se pueden usar de forma separada pero cuando se combinan varios se conoce lo que se le denomina un "dork". Estos operadores pueden ser palabras como "site" u operadores lógicos como AND u OR hasta símbolos de "+" o "-" o simplemente las comillas dobles.

# Operadores
Cuando hacemos una búsqueda web en Google lo mas común es escribir de manera organizada y con muchos nexos pero no es necesario, podemos escribir algo como "gramática ingles y francés" y el buscador puede empezar a buscar de manera separada "gramática francés", "gramática ingles", "ingles y francés" y otras combinaciones por lo que se pueden utilizar ciertos operadores o símbolos que hacen una búsqueda mas forzada.

### Comillas ("")
Se utilizan para buscar una frase o palabra **exactamente en el mismo orden** en el que fue escrita. Al encerrar el texto entre comillas, Google omitirá las páginas que contengan los términos separados o en diferente orden, mostrando únicamente los sitios web que tengan la cadena exacta indexada.
- **Ejemplo:** Si buscas `"banderillas de queso con cátsup"`, el motor descartará recetas que lleven solo queso o solo cátsup por separado, y se enfocará estrictamente en la coincidencia exacta de toda la frase.
### Suma (+)
Si ingresamos a la barra de búsqueda **Tools +De Hixec** se obliga a Google a incluir la preposición "De" porque muchas veces Google se traga las preposiciones. Podría ser contradictorio con el uso normal que se le da porque se supone que hace todas las combinaciones pero de esta manera haciendo uso de la suma es al inicio de una palabra obligamos a que busque con esa preposición.

### Resta (-)
Si ingresamos a la barra de búsqueda **Hixec -Tools** lo que hará Google es buscar todos los resultados que contengan "Hixec" pero que bajo ninguna circunstancia incluya la palabra "Tools".

### Multiplicación ("asterisco")
Si ingresamos a la barra de búsqueda "* Tools" (pero tiene que ir el asterisco pegada a la palabra) va a mostrarnos las paginas que contengan la palabra Tools y que culminen en dicha palabra. En este contexto este operador mas que multiplicar algo hace referencia a lo que se ve en informática que es mas un grupo de caracteres o la ausencia de estos por lo que al haber hecho de esa manera la búsqueda le estamos pidiendo a Google que nos devuelva las paginas indexadas donde esta palabra esté y también las frases que culminen en **Tools** o que la completen es como decirle "muéstrame Tools y todo lo que esté antes de él" 

# Operadores Descriptivos
Se les dice así porque son palabras que describen la información que van a filtrar los cuales son los siguientes:

### "site:"
"site:" recibe como input cualquier dominio o subdominio donde queremos hacer las búsquedas, por ejemplo si queremos buscar "Tools" dentro del dominio "hixec.com" deberemos escribir "Tools site:hixec.com" y solamente nos regresará resultados con la palabra "Tools" y que a su vez están dentro del dominio "hixec.com"

### "inurl:"
A diferencia de "site:" aquí si podemos podemos poner una URL con su protocolo además que nos sirve para filtrar información de una sola pagina de un sitio web ya que con "site:" buscábamos dentro de todo el dominio y aquí podemos filtrar únicamente por una pagina en concreto (recordar que una pagina web no es igual a un sitio web)

### "intext:"
Este operador nos va a devolver todas las paginas cuya palabra clave que le indiquemos o "frase" esté dentro de las etiquetas **body** del código HTML ósea dentro del contenido de la pagina. Si ingresamos "Hixec intext: tools" va a devolver todas las paginas indexadas que contengan la palabra Hixec donde sea y las paginas que contengan entre las etiquetas **body** la palabra "tools".

### "intitle:"
Este operador nos va a devolver todas las paginas cuya palabra clave esté dentro de las etiquetas "title" del HTML es decir en el titulo individual de cada pagina.

### "allintitle" y "allintext"
Estos operadores permiten poner frases o varias palabras claves en lugar de una sola por ejemplo con allintitle podemos hacer una búsqueda de "Tools De Hixec" pero no saldrá ningún resultado porque no existe ninguna pagina con esa frase en su titulo. Pero allintext su funcionamiento redunda un poco porque podrías hacer de uso de intitle e intext al mismo tiempo.

### "filetype:"
Este operador busca por tipo de fichero concretamente la extensión de este y además de buscar por la extensión se asegura que el fichero si tenga el formato correcto es decir que si buscamos un PDF con ayuda de este operador solamente veremos documentos que si sean PDFS y no veremos un TXT que solamente le cambiaron la extensión a PDF sin realmente cambiar el formato. Si queremos buscar todos los documentos PDF subidos a Microsoft y que están indexados en Google tendríamos que escribir en la barra de búsqueda "site:microsoft.com filetype:pdf"

### "ext:"
Este es casi igual que **filtetype** pero está algo obsoleto porque no comprueba si el formato de los ficheros es el correcto y esto puede provocar que tengas ficheros indexados que realmente no son lo que buscas ya que solamente filtra por la extensión y no hace la comprobación que haría filetype

### "cache:"
Sirve para devolvernos a las versiones de las paginas que ha indexado Google porque Google suele almacenar las paginas que indexa y lo hace en su propia cache por lo que con este operador si le indicas la URL te llevará a la pagina web almacenada en los servidores de Google dedicados a la cache

# Operadores Lógicos

### AND & OR
Estos son case sensitive por lo que no es igual "AND" que "and" u "OR" que "or", por lo que estos operadores siempre en mayúsculas. 
Podemos decir que "AND" = "Y" ósea que se se deben cumplir todas las condiciones y "OR" = "O" ósea se cumple una condición o las otras
**Ejemplo:** Si quisiéramos buscar en todo el dominio de Microsoft.com todas las paginas que en su contenido tengan la palabra "tools" y además que en su URL contengan la palabra "free" deberíamos escribir en la barra de búsqueda: "site:microsoft.com intext:tools AND inurl:free" y por otro lado si quisieramos buscar lo mismo pero quisieramos que fuera la palabra "free" o la palabra "gratis" en la URL se usaría "site:microsoft.com intext:tools inurl:free OR inurl:gratis" y en este caso cuando estamos combinando varios operadores de búsqueda estamos formando un **dork**.
La gracia de hacer esto es combinarlos todo lo que se pueda para filtrar tanto la información con la intensión de solamente en una búsqueda podamos filtrar tanto la información que solamente lleguemos a conseguir lo que se requiere en ese momento.

# Dorks Creados por la Comunidad
Si se quiere consultar Dorks creados y enfocados mas a temas de operaciones de seguridad ofensiva, existe una pagina web que tiene muchos ya creados que se llama Google Hacking Database que recopila miles de Dorks que han sido revisados y aprobados y se pueden usar en un trabajo.
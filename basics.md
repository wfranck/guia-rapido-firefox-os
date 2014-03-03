# Conceptos

Antes de empezar con nuestra primer app, vamos a aprender algunos conceptos básicos de desarrollo para Firefox OS. Como sabemos, las app están basadas en HTML5 como en una página web, aún no sabemos lo que los diferencia. Si pensamos en las demás plataformas móviles que conocemos, podemos ver algunos requisitos mínimos para un aplicativo móvil.:

* Tener un ícono.
* Tener un nombre.
* Funcionar offline si es posible.

En Firefox OS, una aplicación es, a groso modo, una página web que posee un ícono, un nombre y puede funcionar offline -- dependiendo de cómo el desarrollador hace su trabajo. Todas esas informaciones respecto de una aplicación, tales como nombre e ícono, son definidas en un archivo manifest, como veremos en la próxima sesión.

## El manifest

El [manifest](https://developer.mozilla.org/pt-BR/docs/Apps/Manifest) es un archivo del tipo [JSON](http://json.org) que describe una aplicación. En general ese archivo se llama **manifest.webapp** y se pone al lado de su archivo principal HTML que normalmente se llama **index.html**. 

<<[Ejemplo de Manifest](code/sample_manifest.webapp)

Arriba podemos ver un ejemplo de manifest de la aplicación llamada memos[^memos]. Entre otras cosas, él describe qué hace la aplicación, cuál es el ícono y nombre del mismo, qué archivo es utilizado para cargar la aplicación (en este caso index.html) y qué permisos de accso al hardware necesita. Ese archivo es utilizado por Firefox OS para agregar la aplicacieon al dispositivo y por Firefox Marketplace para crear una lista del mismo en la tienda como podemos ver en la imagen debajo:

[^memos]: Es una app de ejemplo para Firefox OS que [podemos ver en Firefox Marketplace](https://marketplace.firefox.com/app/memos) y cuyo [código fuente está disponible en github](https://github.com/soapdog/memos-for-firefoxos)

![Lista de memos en Firefox Marketplace](images/originals/memos-marketplace.png)

La misma información del manifest es utilizada para poner la aplicación en el dispositivo, como podemos ver en la captura de pantalla del simulador:

![Memos en el simulador](images/originals/memos-simulator.png)

Con sus archivos HTML, CSS, JavaScript y de un manifest, ya tienes una app lista para correr en Firefox OS. Continuando con el tema, vamos a aprender los tipos de aplicaciones existentes.

## Tipos de aplicaciones

En Firefox OS existen dos tipos de aplicaciones: aplicaciones hosteadas y aplicaciones empaquetadas.

* **Aplicaciones Hosteadas:** están almacenadas en un servidor web, como un site. cuando son utilizadas por el usuario, se hace accede al servidor remoto en caso de que sus archivos no estén en caché.
* **Aplicaciones Empaquetadas:** son distribuídas como un archivo zip  y son copiadas al dispositivo durante la instalación.

Existen pros y contras para cada solución. Aplicaciones hosteadas son más fáciles de actualizar, basta cambiar los archivos en el servidor. Así, son más difíciles de hacer funcionar offline, porque necesitan de utilización de [**appcache**](https://developer.mozilla.org/pt-BR/docs/HTML/Using_the_application_cache) para eso. Otro punto es que incluso utilizando el appcache, la aplicación demora un poco más para llamar, pues el caché necesita ser verificado.
Las Aplicaciones empaquetadas, por otro lado, están en el teléfono desde la instalación y no necesitan verificar el cache antes de ejecutar. En tanto, la acualización es más compleja e incluye el envío de la nueva versión de la app para que Firefox Marketplace y/o la creación de rutinas de actualización dentro del mismo, en caso que la distribuyas fuera del marketplace.

No existe una regla sobre qué tipo de aplicación usar. Personalmente, prefiero hacer aplicaciones empaquetadas que tener que lidiar con appcache y no tener que hostear la app en algún servidor. Las aplicaciones empaquetadas distibuídas en Firefox Marketplace quedan hospedadas en el servidor de Mozilla y, en mí opinión, eso es más fácil. Vale la pena decir que el mundo de las herramientas de desarrollo con JavaScript ya produjo generadores de archivos de papcache que facilitan mucho la vida de quien está creamndo app hosteadas. La elección es de cada uno, por eso, a lo largo de este libro utilizaré aplicaciones empaquetados, porque es más fácil de mantener en nuestro foco aplicaciones que no forman parte de servicios de hosting. PAra quien quiera saber más de aplicaciones hosteadas, basta mirar [el link de de aplicaciones hosteadas en el centro del desarrollador](https://marketplace.firefox.com/developers/docs/hosted).

## Niveles de acceso al hardware

Existen tres niveles de acceso al hardware en Firefox OS. Cada nivel posee APIs a las que pueden o no acceder.

* **Normal:** Los aplicativos normales poseen acceso a WebAPIs más frecuentemente utilizadas, tales como geolocalización, y obtener fotos de la cámara. Aplicaciones hosteadas y aplicaciones empaquetadas que no declaren un tipo de manifest son, por definición, normal.
* **Privilegiado:** Una aplicación tiene acceso a todas als APIs disponibles para una app normal y alguna más. Una exigencia es que todas las aplicaciones privilegiadas sean empaquetadas, o sea, no puedes tener una aplicación hosteada que tenga acceso Privilegiado. Esas aplicaciones tienen acceso a APIs más "profundas" de Firefox OS, como una API de contactos sin interacción con el usuario.
* **Certificado:** Aplicaciones certificadas tienen acceso total al hardware y sólo pueden ser construidas por Mozilla y sus socios de hardware. Ellos tienen acceso, por ejemplo, al sistema de telefonía. Un ejemplo de aplicación certificado es el discador de Firefox OS.

En general la mayoría de las aplicaciones no necesitan de nada ademas de que el acceso normal ofrece. Por eso, algunas veces es necesario un acceso privilegiado para poder utilizar ciertas APIs. Cuando creamos una aplicación privilegiada y lo enviamos a Firefox Marketplace el proceso de aprobación es más riguroso (y eso es bueno).

En la [página sobre WebAPIs en el wiki de Mozilla](https://wiki.mozilla.org/WebAPI) podemos ver cuáles de las APIs están implementadas en cuáles plataformas y cuál es el nivel de acceso necesario apra utilizarlos.

![Nivel de acesso para cada API](images/originals/webapi-access.png)

Como podemos ver en la imajen de arriba, el acceso a *Geolocation API* está disponible para todas las aplicaciones, encuanto la API *WIFI Information API* está disponible solamente para aplicaciones privilegiadas.

## Las WebAPIs

En Firefox OS no necesitamos nada además que las tecnologías web para construir app que son capaces de hacer lo mismo en otras plataformas en nativo. Toda la parte de acceso al hardware es hecha através de WebAPIs. Para conocer la lista de APIs disponibles para la versión actual de Firefox OS basta [visitar la página sobre WebAPIs en el wiki de Mozilla](https://wiki.mozilla.org/WebAPI). 

Para ilustrar qué fáciles son esas API voy a mostrar algunos ejemplos de uso. 

### Ejemplo #1: Realizar llamadas

Imaginemos que tienes un programa que necesita abrir el discador del teléfono con un número preescrito. Basta utilizar el código debajo:

<<[Enviando um número para el teléfono](code/webapi_samples/dial.js)

Ese código apenas abre el teclado para discar y un número preescrito, así que el usuario de teléfono necesita presionar el botón de discado para hacer la llamada. Ese tipo de API, que necesita de una acción del usuario antes de ejecutar su función, es común y da seguridad, al final, utilizando esa API no tienes que hacer un programa que llama para algeun lugar sin la aprobación del usuario. Otras APIs que son capaces de hacer llamadas sin la confirmación del usuario están disponibles para niveles más elevador de aplicaciones. La API del ejemplo está disponible  para todas las aplicaciones.

Esa API es una Web Activity. Para saber más sobre ese tipo de API visite [este archivo en el blog de Mozilla](https://hacks.mozilla.org/2013/01/introducing-web-activities/). 

### Ejemplo #2: Guardar un contacto

<<[Guardando un contato](code/webapi_samples/contact.js)

Esa API crea un objeto con los datos de contacto y lo guarda en el teléfono, sin inferencia del usuario, y está disponible solamente para aplicaciones privilegiadas. Ese padrón, donde se crea un objeto con un callback de éxito y de error, es muy utilizado en las WebAPIs.

Para saber más sobre API de contactos, visite [la página da *Contacts API* en el wiki de Mozilla](https://wiki.mozilla.org/WebAPI/ContactsAPI).

### Ejemplo #3: Tomando una imagen con la cámara

<<[Tomando una imagen](code/webapi_samples/pick.js)

Aquí vemos otro ejemplo de una [WebActivity](https://hacks.mozilla.org/2013/01/introducing-web-activities/) (hablaremos de web activities más adelante del libro). Las Web Activities están disponibles para todas las aplicaciones. En el caso de este ejemplo, utilizamos una actividad del tipo *pick* y pasamos los *MIME Types* deseados. Al ejecutar ese código, el sistema muestra una pantalla para el usuario pidiendole seleccionar de dónde debe venir la imagen (cámara, álbum, wallpapers) y en caso que el usuario seleccione una imagen se ejecuta un callback de éxito; en caso él cancele la acción, un callback de error es ejecutado. En caso de tener éxito, el programa recibe un blob con la imagen. En la imagen debajo podemos ver un ejemplo del flujo:

![Ejemplo del activity *pick*](images/originals/pick_image.png)

## Conclusión

En este capítulo vimos algunos conceptos básicos sobre Firefox OS que serán desarrollados en los próximos capítulos. Ahora es hora de colocar manos a la masa y hacer una app!


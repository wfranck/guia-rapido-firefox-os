# Herramientas de Desarrollo

Firefox posee diversas herramientas para ayudar a los desarrolladores web a hacer su trabajo. Mucha gente asún usa [FireBug](https://addons.mozilla.org/pt-BR/firefox/addon/firebug/) y no sabe que Firefox ya incluye herramientas propias. En esta sección vamos a ver rápidamente algunas herramientas que son muy útiles para quien está desarrollando apps.

Quien esté interesado en conocer más sobre esas herramientas y lo que más cambia, puede dar una mirada en la [página de MDN sobre herramientas de desarrollador](https://developer.mozilla.org/en-US/docs/Tools).

## Conociendo el Modo de Diseño Adaptable

Una de las cosas más cómodas de cuando estamos desarrollando para web es la forma en que podemos simplemente guardar el HTML y recargar la página en el browser para ver los cambios, sin la necesidad de un compilador o cosas del tipo. Por más que el simulador de Firefox OS también permita este tipo de workflow, a veces queremos simplemente ir testeando las cosas en Firefox en el mismo escritorio. Este tipos de test en escritorio es muy común cuando estamos lidiando con aplicaciones hospedadas que deben adaptarse al desktop, tablets y teléfonos. En esos casos puedes utilizar el **Modo de Design Responsive** para adaptar la pantalla (y el viewport) para tamaños comunes de tablet y teléfonos, y ver como su trabajo queda en esas pantallas.

La utilización del modo de diseño responsive es especialmente importante para quien está trabajando con [**media queries**](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries), pues permite que redimensiones la pantalla justo a la manera que debe ser el test de su CSS.

El modo de diseño responsive puede ser activado en el **menu Herramientas -> Desarrollador Web -> Modo de Diseño Adaptable**[^responsive-design-view], como podemos ver en la imagen debajo.

[^responsive-design-view]: En inglés *Responsive Design View*.

![Activando el Modo de Diseño Adaptable](images/originals/responsive-design-view.png)

Al activar este modo, la pantalla de Firefox se modifica de manera que puedas modificar el tamaño de viewport utilizando las costado de la pantalla o el box de selección.

![Ejemplo de Mofo de Diseño Adaptable](images/originals/responsive-view-sample.png)

La mayoría de lso teléfonos corriendo Firefox OS y que estaban en el mercado hasta 2013 funcionan con una resolución de 480x320. Por eso, en vez que simplemente hacer las cosas pensando esa resolución, y mejor  utilizar media queries y la metodología llamada de diseño adaptable. Para quien quiere saber más sobre diseño adaptable recomiendo el libro [Responsive Web Design](http://www.abookapart.com/products/responsive-web-design) y [Mobile First](http://www.abookapart.com/products/mobile-first). En brasil [**Casa do Código**](http://casadocodigo.com.br),  [Web Design Responsivo](http://www.casadocodigo.com.br/products/livro-web-design-responsivo) y [A Web Mobile](http://www.casadocodigo.com.br/products/livro-web-mobile), ó [pacote de livros de web responsiva e mobile](http://www.casadocodigo.com.br/products/colecao-webdesign).

En síntesis, el modo de diseño responsive permite que la gente testée nuestras apps en diversos tamaños de tela, sin ser necesario quedar redimensionando la pantalla principal de Firefox. En mi opinión, es una de las herramientas más útiles de un mundo y no sé porqué los demás navegadores aún no copiaron...


## Otras Herramientas

Las herramientas de desarrollador de Firefox son similares a las de Firebug y de Google Chrome. Ellas permiten que interactúes con el DOM y con el ambiente de JavaScript de la página que está cargada y mjucho más. Con ellas puedes testear tus funciones JavaScript, enviar comandos de depuración y status vía el [objeto console](https://developer.mozilla.org/en-US/docs/Web/API/console) y manipular tanto con el DOM como el CSS de la página. Son herramientas imprescindibles para quien está trabajando con web.

![Página con la Consola de JavaScript visible](images/originals/console-open.png) 

Además de la *consola de JavaScript* existen varias otras herramientas como un [*editor de estilo*](https://developer.mozilla.org/en-US/docs/Tools/Style_Editor), [*monitor de red*](https://developer.mozilla.org/en-US/docs/Tools/Network_Monitor), [*profiler de JavaScript*](https://developer.mozilla.org/en-US/docs/Tools/Profiler), [*depurador de JavaScript*](https://developer.mozilla.org/en-US/docs/Tools/Debugger), [*inspector de páginas*](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector) entre otros.

Como vimos en la aplicación que construímos en el capítulo anterior, la consola puede ser utilizada para verificar el funcionamiento de nuestro programa. Existen muchos desarrolladores web que aún utilizan *alerts()* esparcidos por el código para debuggear cosas. Aprender a utilizar las herramientas de desarrollador es un paso muy importante en la formación de cualquier desarrollador.

Una herramienta que vale destacar es el [*depurador remoto*](https://developer.mozilla.org/en-US/docs/Tools/Remote_Debugging), que permite que conectes un teléfono corriendo Android o Firefox OS a su computadora y utiliza las herramientas de desarrollador de su computadora para depurar lo que se está ejecutando en su dispositivo móvil.

## Conclusión

Este fue un capítulo de exposición para dar al lector referencias para aprender más sobre las herramientas que vienen en Firefox. La utilización de esas herramientas facilitan mucho la vida de la gente y cuando las juntamos con el simulador de Firefox OS tenemos una combinación imbatíble para la construcción de apps. Por eso, en el próximo capítulo vamos a aprender un poco más sobre el simulador.

# Introducción {#introduction}

## Firefox OS

![Firefox OS](images/originals/firefox_os_simulator.png)

[Firefox OS](http://www.mozilla.org/pt-BR/firefox/os/) es la nueva plataforma móvil libre desarrollada por [Mozilla](http://mozilla.org) y sus socios. Dispositivos con Firefox OS ya están a la venta en diversos países y se prevee que en 2014 comiencen a distribuirse comercialmente en Argentina.

Presentado inicialmente para mercados emergentes, Firefox OS tiene como objetivo traer el próximo millón de personas a la web. Para conseguir esto, los dispositivos con Firefox OS son sontruídos para estar optinmizados como *el primer smartphone* de la persona y tiene precios muy competitivos. El objetivo es ser una alternativa para que las personas migren de aparatos de gama media-baja a smartphones corriendo Firefox OS.

[^PT-anywhere]: Referencia de datos.

Tristemente en mercados emergentes, los smartphones con una performance aceptable son muy caros. Las personas pueden comprar smartphones baratos  pero las plataformas utilizadas actualmente para este tipo de paratos están siendo construídas con foco en smartphones de alto desempeño, dejando los aparatos de poco valor con una mala performance.

Otro factor importante cuando hablamos de Firefox OS es que los sistemas móviles actuales más populares son pequeñas islas propietarias donde estás amarrado a la voluntad de los fabricantes que poseen privilegios sobre la plataforma. En esos sistemas propietarios, por lo general, sólo puedes distribuir aplicaciones en canales autorizados y el fabricante queda con un porcentaje de todas las transacciones financieras que pasan por la aplicación.

Además de tener sujeto a los desarrolladores através de tiendas de apps, esos sistemas poseen sistema de desarrollo propios e incompatibles entre sí -- por ejemplo: Apple con Objetive-C/Cocoa y Google con Java para Android. De esa forma, para construir una aplicación nativa para iOS y Android, el desarrollador necesita aprender los dos lenguajes y recrear el programa dos veces. Firefox OS trae para el mundo mobile una propuesta diferente al tener HTML5 como sistema de desarrollo de apps nativas. HTML5 es el sistema abierto y libre utilizado por los navegadores modernos de la web. Aplicativos basados en esa tecnología posee un potencial para ser multiplataforma naturalmente (siendo menos trabajo garantizar que una web app funciona en varias plataformas que contruir la msima app varias veces para cada una).

## La plataforma que HTML5 merece

La web está en todo lugar, desde la computadora al teléfono celular, el SmartTV y hasta videojuegos. El lenguaje de programación de la web, JavaScript, es uno de los lenguajes más difundidos en el mundo, básicamente presente en todos los tipos de dispositivos[^JS-anywhere]. Cuando las personas hablan sobre HTML5 ellas en general están hablando de la unión de las tres tecnologías: el HTML 5, CSS 3 y JavaScript. Ese trío es poderoso, el HTML 5 simplifica HTML y expande sus capacidades en relación con XHTML 1.0, CSS 3 viene con más capacidad para layout y animaciones, y Javascript hoy es una de los fantásticos lenguajes que pueden utilizar tanto principiantes como para desarrolladores experimentados.

[^JS-anywhere]: Para una idea mire [presentación JavaScript Anywhere do Jaysdon](http://jaydson.org/javascript-everywhere-no-fisl-14/).

Firefox OS básicamente es una extensión móvilde la web donde HTML5 está en primer lugar . Al tornar HTML5 un ciudadano de primera clase en su plataforma, Mozilla torna el nuevo sistema accesible a millones de desarrolladores web. El HTML5 funciona muy bien en navegadores modernos de escritorio y laptops. Por eso , antes de Firefox OS, no había una plataforma móvil que hiciese lo mismo. Respecto a competidores que producen navegadores que implementan HTML5, FirefoxOS vá más allá implementando no sólo HTML sinó tamvién una serie de APIs de acceso al hardware vía JavaScript.

## Acceso al hardware WebAPI

Plataformas anteriores también intentaron crear sistemas operativos cuyas aplicaciones estaban basadas en tecnologías web. Así que iPhone fue creado, la única manera de crear apps era através de webapps. WebOS también utilizaba HTML, CSS y JavaScript. La diferencia con FirefoxOS con esas plataformas es que éste ofrece acceso al hardware y componentes del sistema vía JavaScript. En iOS las webapps no tienen ese tipo de acceso y se tornan ciudadanos de segunda clase, incapaces de competir con aplicaciones nativas.

Al hablar del acceso al hardware estamos hablando cosas como acceder a los contactos del teléfono, enviar SMS, acceder a la cámara y las fotos del dispositivo. En FirefoxOS, gracias a la colección de APIs llamadas [WebAPI](https://wiki.mozilla.org/WebAPI), el desarrollador puede aprovechar todas esas funcionalidades utilizando nada más que las tecnologías de HTML5.

Otra diferencia es que, al contrario de plataformas anteriores, como WebOS, que también promovía el acceso al hardware vía JavaScript, Mozilla está trabajando en conjunto con W3C y otros grupos para que WebAPI se vuelva un patrón abierto de la web[^WA-anywhere] y pueda ser implementado por otros vendedores, como Google, Apple o RIM. Conforma las APIs son implementadas por los demás fabricantes, sus aplicativos mnecesitarán, en caso de que implementen tecnologías web, de cada vez menos cambios para funcionar en plataformas diferentes.

[^WA-anywhere]: Distribución de Referencia.

Mozilla no está implementando WebAPI solamente en Firefox OS, sus esfuerzos también tienen foco en la implementación de Firefox para Desktop y en Firefox Movile para Android. Así, aplicaciones construidas con base a esta API estarán inmediatemente aptas para correr donde sea que Firefox esté. Y, en breve, en cualquier navegador, en caso que WebAPI realmente se convierta en patrón.

## Libertad de desarrollo y distribución

Como todo Mozilla, Firefox OS está construído abierto y de forma libre. Todo el desarrollo puede ser acompañado por [GitHub de Mozilla](https://github.com/mozilla-b2g/B2G). Con Firefox OS puedes tener la libertad de acompañar y contribuir con el desarrollo del sistema y también para distribuir tus propias aplicaciones, sea en tu propia página o en [Firefox Marketplace](https://marketplace.firefox.com/).

La idea principal es que no quedes preso a Mozilla. Si quieres modificar el código fuente de del sistema y modificarlo para tus necesidades, puedes hacerlo. Si quieres construir aplicaciones para utilización interna de su empresa o distribuir tus creaciones solamente en tu propia página, puedes. En otras plataformas, estás amarrado a distribuir tus aplicativos únicamente via la tienda autorizada del fabricante y, por lo tanto, sujeto a los criterios y el proceso de aprobación del mismo. Firefox Marketplace también posee un proceso y criterio de aprobación, pero eres libre de utilizarlo o no. Asei como la web, donde eres libro para hospedar su página como cfrea mejor, en Firefox OS también.

## Conclusión

En síntesis, HTML5 qudó para quedarse y evolucionar constantemente. Firefox OS que es el nuevo sistema operativo móvil de Mozilla -- totalmente livre y construido abiertamente -- que ofrece una implamentación robusta de HTML 5 y va más allá ofreciendo APIs de acceso al hardware vía JavaScript. Esas APIs están patrocinadas junto con los órganos competentes y promovidas para adopción de otras organizaciones.

En el próximo capítulo vamos a ver qué es necesario para crear aplicaciones para FirefoxOS. En breve tendremos una app funcionando.

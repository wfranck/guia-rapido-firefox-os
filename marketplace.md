# Firefox Marketplace

![Firefox Marketplace](images/originals/marketplace.png)

[Firefox Marketplace](http://marketplace.firefox.com) es el store de Firefox donde puedes tomar e instalar aplicaciones para Firefox OS, Firefox Desktop y Firefox para Android. Es el principal canal para distribución de aplicaciones para Firefox OS, sin embargo no necesitas usarlo si no quieres.

Para distribuir aplicaciones en el marketplace necesitas estar identificado via [Mozilla Persona](https://login.persona.org/about). Basta cliquear **Sign Up** y seguir las instrucciones. Una vez identificado, estás listo para enviar aplicaciones para Firefox Marketplace.

## Checklist antes de pensar e enviar su app

Toda aplicación que es enviada para el marketplace pasa por un proceso de aprobación. Aplicaciones normales pasan por un proceso menos riguroso que aplicaciones pribilediadas, pues utilizan APIs menos sensibles. Antes de enviar la aplicación, familiaricese con [Los criterios de validación de marketplace](https://developer.mozilla.org/en-US/docs/Web/Apps/Publishing/Marketplace_review_criteria). Los puntos más importantes son:

* Forefox OS no tiene un boteon volver como el navegador o Android. Si dentro de su app el usuario navega a algún punto y no tiene cómo volver (y queda aprisionado en una pantalla), su app será rechazada.
* Su app debe contener íconos 60x60, utilizados por Firefox OS, y una descripción detallada sobre qué hace en su manifest.
* Si su app pide permisos para alguna funcionalidad, debe usarla. Marcar la app como privilegiada y no utilizar nada de las APIs privilegiadas hará que su app sea rechazada con un pedido de modificación para el tipo normal.
* Su app necesita tener una política de privacidad bien explicada en el marketplace.
* El manifest de una aplicación debe venir del mismo dominio, en caso de apps hosteadas.

Existen otros criterios además de los mostrados. Vale la pena ver esos criterios antes de enviar una app. Al final, se pierde mucho tiempo con una aplicación rechazada por tonterías que puedes resolver en cinco minutos.

## Preparando su app para el envío

La preparación de su app para el envío depente del tipo de app qie es. Aplicaciones hosteadas simplemente necesitan estar disponibles en algún servidor web. Aplicaciones empaquetadas deben ser zipeadas antes del envío y merecen más atención.

Mucha gente comete el error de seleccionar la carpeta que contiene los archivos de la aplicación y lo zipea. Eso hace que el zip tenga una carpeta y esa carpeta tenga todos los archivos. Eso no es la manera correcta de zipear apps para Firefox OS. Lo correcto es que el zip contenga directamente los archivos de la aplicación. Específicamente, lo que es necesario es que el manifest esté en *raíz del archivo zip*, o sea, que el no esté dentro de ninguna carpeta dentro del archivo comprimido. En Mac OS X y en Linux podemos navegar por terminal hasta dentro de la carpeta que está nuestra aplicación y ejecutar un comando `zip -r miapp.zip *`, como podemos ver an la captura de pantalla que sigue.

![Zipeando corretamente los archivos](images/originals/marketplace-preparing-packaged-app.png)

El archivo zip final es lo que enviaremos para el marketplace.

## Envio para Firefox Marketplace

Después que su aplicación esté lista y seguros de todos los requisitos serán aprobados, debemos navegar hasta **Mis Eníos**[^mis-envios] utilizando el botón de engranaje.

![Mis Envios](images/originals/marketplace-my-submissions.png)

Dentro de la página de administración de sus aplicaciones, debes cliquear en **Enviar una nueva aplicación** en el menú superior.

![Link para enviar la nueva aplicación](images/originals/marketplace-new-app.png)

Ese link lo llevará para el formulario de entrada de nueva aplicación que puede verse en la pantalla abajo.

![Enviar nueva app](images/originals/marketplace-step-1.png)

En esa pantalla puedes seleccionar las siguientes opciones:

* Si la aplicación es hosteada o empaquetada.
* Si es gratuita o paga(o con *in-app purchases*).
* En qué dispositivos funciona (Firefox OS, Firefox Desktop, Firefox for Mobile en el Teléfono, Firefox for Mobile en Tablet).

Hechas esa elección, puedes pasar a la segunda pantalla. En este libro estamos haciendo el proceso para el envío de una app empaquetada, sin embargo los demás tipod de app tienen un workflow semejante.

Estamos asumiento, a efectos de este ejemplo, una aplicación empaquetada gratuita para Firefox OS. En este caso, pide que la gente haga u upload del archivo que preparamos en la etapa anterior.

[^mis-envios]: En castellano *My Submissions*.

Luego del envó del archivo, será procesado y se mostrarán más opciones.

![Luego del envío del archivo zip](images/originals/marketplace-step-1_5.png)

Como podemos ver en la captura, el programa que envié no contiene errores, pero contiene seis avisos. Fuera de eso, podemos marcar los **requisitos mínimos** para que la app sea instalada. En este ejemplo, el último requisito, que habla sobre resoluciónde pantalla qHD, debe ser desmarcado, visto que esta aplicación funciona en cualquier resolución.

El próximo paso, llamado **Paso #3: Detalles**, es donde usted provee la información sobre su aplicación, tales como categoiría y descripción, tales como categoría y descripción, y proporciona capturas de pantalla.

![Proveyendo detalles](images/originals/marketplace-step-3.png)

Luego de proveer los detalles, el proceso de envío está terminado y sólo basta aguardar la aprobación de revisores del marketplace. Felicitaciones, tienes una aplicación en Firefox OS!!!

En la página de [Administración de Aplicaciones](https://marketplace.firefox.com/developers/submissions) puedes verificar el status de sus envíos y modificar los detalles si es necesario.

Para saber más sobre el envío de aplicaciones para Firefox Marketplace, lea [ese archivo en la central de desarrollador de Firefox OS](https://marketplace.firefox.com/developers/docs/submission).

## Conclusión

Felicitaciones!!!! Ahora tienes una aplicación en Firefox Marketplace. Has conocido un nuevo mercado!

Esoeri que hayas gustado de esta guía rápida. Pretendo actualizar esta guía constantemente (inclusive encontrando un buen editor para mejorar mi analfabetismo). Así que, esté atengo para las novedades. Se bajó este libro de Leanpub, esté tranquilo que será avisado de las actualizaciones.

No deje de darme feedback. Quedé despierto la noche entera escribiendo este libro, o sea, realmente gusto del proyecto! Estoy constantemente mirando Twitter, mi cuenta es [@soapdog](http://twitter.com/soapdog).

Ahora que eres parte de los desarrolladores para Firefox OS, haga parte de la comunidad en Brasil [Comunidade Mozilla Brasil](http://mozillabrasil.org.br) y ayude a los proyectos libres, como Firefox OS, para que cresca aún más.

# El Simulador de Firefox OS

![Dashboard del Simulador de Firefox OS](images/originals/simulator-dashboard.png)

En el capítulo [Requisitos para Desarrollar App para FirefoxOS](#setup) instalamos el simulador de Firefox OS y en el capítulo[Nuestra Primer App](#firstapp) utilizadmos el simulador para testear Memos. Ahora, vamos a profundizar nuestro conocimiento sobre el simulador viendo las tareas más coomunes.

Para saber mas sonre el simulador visite [la página de MDN sobre el simulador](https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator).

## Agregando Aplicaciones

Puedes agregar aplicaciones empaquetadas o guardadas en el simulador. El procedimiento es similar, aunque con diferencias sútiles. Por eso, vamos a ver cada una de ellas separadamente.

### Agregando aplicaciones empaquetadas

El foco de este libro son las aplicaciones empaquetadas, simplemente porque encuentro más fácil trabajar con ellos.
Entonces, ya sabes como hacer para agregar una aplicación que está en la carpeta dentro de su computadora, al final, hicimos eso cuando testeamos [Nuestra Primer App](#firstapp). Así, vamos a repetir la explicación para que quede más claro.

Para agregar una aplicación empaqu4etadas clequeamos en el botón **Add Directory** en **Dashboard do Simulador**, como podemos ver debajo.

![Mostrando el botón para agregar aplicaciones empaquetadas al simulador](images/originals/simulator-add-directory.png)

Al cliquear el botón resaltado en la imagen, Firefox abre una ventana de selección de archivos. En esa ventana, debes navegar en su disco y localizar el **archivo de manifest** de la aplicación que quiere agregar. Si todo es correcto, la aplicación será agregada al simulador y llamaré a la app en ejecución. En caso que algo esté mal con el manifest el simulador avisará.

![Ejemplo de manifest inválido](images/originals/simulator-invalid-manifest.png)

Siempre que hagas alguna modificación de la aplicación podrás tocar el botón **Refresh** para actualizar la app en el simulador.

### Agregando aplicaciones hosteadas

Incluso que la aplicación que pretender correr como hosteada esté dentro de la misma máquina que está corriendo el simulador, debes testearla utilizando un servidor web. Se utiliza el procedimiento descrito arriba para testear una aplicación hosteada, puede que tengas algún bug en la configuración de su servidor (como servir el manifest con MIME Type equivocada) que no te darás cuenta.

Muchas de las aplicaciones hospedadas no son exclusivas para Firefox OS y sin sites/webapps adaptables para el dispositivo que está accediendo en aquel momento. Este tipo de sites normalmente posee sistemas de backend que no tienes cómo testear directamente con el procedimiento de aplicaciones empaquetadas. Por lo tanto, lo ideal es testearla a partir del servidor web. Para hacer eso, debes escribir la dirección del site o del manifest en el campo de texto al lado del botón **Add URL**.

![Agregando una app hosteada al simulador](images/originals/simulator-add-url.png)

Al cliquear el botón, el manifest es verificado y, en caso que esté correcto, la aplicacieon es agregada al simulador que es iniciada con la aplicación corriendo. Así como el procedimiento para apps empaquetadas, el dashboard mostrará si dá algún error en el manifest.

Siempre que hagas alguna modificación en la aplicación puedes presionar el botón **Refresh** para actualizar una app en el simulador.

## Debug

Con la aplicación corriendo en el simulador ya estamos listos para depurarlo. Para eso cliqueamos en el botón **Connect**, al lado de la entrada de la aplicación, en el dashboard del simulador. Eso abrirá el simulador con la aplicación elegida corriendo y conectar la **Consola de JavaScript** en la app. Debajo podemos ver qué botón apretar.

![Qué botón apretar para depurar una app](images/originals/simulator-press-connect.png)

Luego de apretar ese botón verás una pantalla similar a esta:

![Herramientas de desarrollador conectadas al simulador](images/originals/simulator-connected.png)

Con las herramientas conectadas puedes testear el JavaSctipt, depurar el DOM, cambiar el estilo de las cosas, entre otros. Como la chicos dicen los chicos de la startup *pivotar hasta que la aplicación esté bien*.

Luego que su app esté funcionando bien en el simulador, es hora de testearla en un dispositivo de verdad.

## Enviando al dispositivo

Nada sustituye la experiencia de testear en un dispositivo de verdad. En el simulador quedas cliqueando las cosas con el mouse en una pantalla de la computadora, en un aparto relal colocas los dedos en la pantalla del del teléfono. Es una experiencia muy diferente. Solo vamos a ejemplificar este tipo de cosas: algunos años atrás yo y Raphael Eckhardt (es hizo la tapa del libro) estábamos haciendo un juego tipo puzzle -- no muy diferente de un bejeweled de la vida -- que inluía arrastrar y soltar piezas del juego en el "tablero". Encuanto testeábamos en el simulador, todo estaba bien. Pero, cuando pasamos al teléfono notamos que a mano quedaba frente al tablero y que las piezas eran tan pequeñas que se perdían debajo del dedo en cuanto las arrastrábamos. Tuvimos que cambiar nuestro arte y nuestra UX, pues los mouses son muy diferentes en mano.

Puedes comprar un dispositivo de desarrollador corriendo Firefox OS en la [tienda de geeksphone](http://shop.geeksphone.com/en/). Yo recomiento el [Geeksphone Keon](http://www.geeksphone.com/), pues es más similar a los dispositivos que están siendo vendidos para los consumidores finales en términos de resolución y capacidad. También puedes instalar Firefox OS en alguinos dispositivos que corren Android, sin embargo ese tipo de cosas es destinadas solamente a entusiastas que saben muy bien lo que están haciendo y poseen más bugs que als versiones que corren en Geeksphone y ZTEs.

En caso que tengas un dispositivo que corra Firefox OS y esté con drivers al día, puedes enviar aplicaciones directo del simulador para el telésono conectado a la computadora. Cuando el simulador detecta que conectó un teléfono con Firefox OS, muestra un aviso **Device Connected**.

![Device Connected!](images/originals/simulator-device-connected.png)

Con el teléfono conectado (y detectado), el simulador agregará un botón cerca de los botones **Connect** y **Refresh**, llamado **Push**. Al presionar ese botón, un pedido de **permiso aparece en el teléfono** y, en caso que el usuario acepte, la aplicación se instala en el aparato.

![Qué botón apretar para enviar la app al aparato](images/originals/simulator-press-push.png)

Y la ventana de permisos aparece con la foto debajo.

![No es la mejor foto del mundo pero muestra la ventana de permisos (son 4:25 AM)](images/originals/simulator-remote-push.jpg)

COn la aplicación corriendo en el dispositivo, puedes utilizar *remote debuggin* para conectar una consola de javascript y depurar su app.

## Conclusión

La conclusión es que el simulador de Firefox OS es exelente!!! Chistes a parte, a esta altura del libro ya tienes una buena idea de cómo funciona el desarrollo de aplicaciones para Firefox OS. Por eso, en el próximo capítulo vamos a ver como distribuí nuestras aplicaciones.

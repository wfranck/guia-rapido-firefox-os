# Distribuyendo sus aplicaciones

Tenemos la aplicación lista, pero falta saber cómo hacemos para distribuirla. En este capítulo vamos a distribuir su aplicación **fuera de Firefox Marketplace**. Como vimos en la [Introducción](#introduction), Mozilla no busca impedir su libertad de ninguna manera. Así podemos distribuir nuestras creaciones como creamos mejor.

Esa parte de distribución fuera de Firefox Marketplace tiene más sentido (e nmi opinión) para aplicaciones con intereses segmentados, como aplicaciones para utilización interna en empresas o solamente para sus clientes. Aplicaciones en el marketplace están disponibles para cualquiera lo baje o compre. La única manera que una app esté en el marketplace y restringir la utilización es con algún sistema de usuario dentro de la aplicacieon (y mantenido por un backend), , como es el caso de apps como *Evernote*, que puede tener una cuenta de su propio sistema para utilización. Otro caso donde tiene sentido distribuir fuera del Marketplace es cuando ya tienes un canal de marketing montado y es capaz de atender un gran número de personas independientemente del mercado. Por ejemplo, si su sitio personal tiene una app para Firefox OS, tiene sentido distribuir la app en su propio sitio (además de distribuir también en el marketplace).

El proceso de distribución de aplicaciones hosteadas y empaquetadas es semejante, sin embargo con llamadas a funciones diferentes -- por eso voy a mostrarlos separadamente. Independientemente del tipo de app sea hosteado o empaquetado, debes crear un botón o página que ejecute la llamada de instalación. Eso puede ser un botón tipo **Instale nnuestra App** o una dirección especial que, cuando abra, cause la llamada a la rutina de instalación. Al ejecutar las llamadas de instalacieon, Firefox OS pregunta al usuario si desea instalar la app o no. Así, no tiene como instalar una app sin la confirmación del mismo.

## Aplicaciones hosteadas

<<[Rutina para instalación de una app hosteada](code/distribution/hosted_apps_distribution.js)

En el ejemplo de arriba, `manifestURL` debe contener la dirección del archivo manifest. Al ejecutar esa rutina en Firefox OS pide al usuario confirmar la instalación de la app y, dependiendo de la acción del mismo se llama al callback de error o de éxito.

Para mayores informaciones sobre esas rutinas vea la [página de MDN sobre instalación de aplicaciones](https://developer.mozilla.org/es/docs/Aplicaciones/JavaScript_API).

## Aplicaciones empaquetadas

La instalación de aplicaciones empaquetadas es muy similar, sin embargo, en vez de llamar `mozApps.install()`, debemos llamar `mozApps.installPackage()`, como podemos ver en el ejemplo debajo.

<<[Rutina para instalación de una aplicación empaquetada](code/distribution/packaged_apps_distribution.js)

W> Cuidado: Tengo la impresión que la instalación de apps empaquetadas fuera de marketplace aún no es posible en la versión actual de Firefox OS. Por ma que la API esté documentada, creo que ella aún no fue totalmente implementada, nunca la testié. Aviso dado, si funciona, mante un mail para actualizar el libro.

## Conclusión

Vimos rápidamente cómo es realizada la instalación de una aplicación fuera de Firefox Marketplace a través de las rutinas de instalación y gerenciamiento de **Open Web Apps**. Existen otras rutivas, por ejemplo, para detectar si la app está instalada o no (asei puedes esconder el botón de instalar si la app ya está instalada). Para saber meås sobre esas rutinas no deje de ver la [página de MDN sobre instalación de aplicaciones](https://developer.mozilla.org/es/docs/Aplicaciones/JavaScript_API) (ya hablé de eso en este capítulo, lo sé).

En el próximo capítulo vamos a ver cómo distribuir su aplicación en Firefox Marketplace.

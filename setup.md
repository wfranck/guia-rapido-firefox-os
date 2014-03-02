# Requisitos para Desarrollar App para FirefoxOS {#setup}

Para desarrollar y testear aplicaciones hechas para Firefox OS no necesitas nada más además que una versión reciente de Firefox, del complemento llamado Firefox OS Simulator y de un buen editor de texto para programar[^editores].

[^editores]: Existen varios y buenos editores con diferencia en el grado de commplejidad y funcionalidad. Uno muy popular que recomiendo para alguien que aún no posee un editor favorito es [SublimeText](http://sublimetext.com/). Personalmente yo utilizo [WebStorm](http://www.jetbrains.com/webstorm/) que es un IDE completo para creación de web apps.

## Obteniedo Firefox

Cada navegador posee diferente motor de renderización y ejecución de JavaScript. Google Chrome, Opera y Safari utilizan el motor conocido como WebKit (o Blinkque es un fork de WebKit). Firefox utiliza el motor llamado Gecko, sea desktop, android o Firefox OS. Por tanto, para desarrollar apps para Firefox OS es mejor utilizar Firefox para Desktop, pues ambos utilizan el mismo sistema de renderuzación y ejecución de JavaScript.

Además de eso, Mozilla dispone de un simulador de Firefox OS que funciona como un complemento de Firefox. Así, es necesario instalar Firefox para desktop para poder correr el simulador de Firefox OS.

La versión actual estable de Firefox puede ser [obtenida en esta página](http://getfirefox.com). Basta seguir las instrucciones para instalarlo en su sistema operativo preferido.

## Instalando el Simulador de Firefox OS

Luego de la instalación de Firefox, el próximo paso es la instalación del simulador de Firefox OS que serå utilizado para testear nuestras aplicaciones. Con Firefox instalando y funcionando, vamos al menú **Herramientas** y seleccione **Complementos**[^tools-add-ons], Como podemos ver en la imagen de abajo:

[^tools-add-ons]: En caso que su sistema esté en inglés, busque el menú **Tools** y **Add-ons**.

![Menu **Herramentas** com menu **Complementos** selecionado](images/originals/tools.png)

Utilizando la herramienta de busqueda presente en la esquina superiro derecha, busque **firefox os simulator** e instale el simulador.

![Administrador de complementos mostrando el simulador](images/originals/addons-simulator.png)

Luego de que el complemento es instalado, el estará disponible en el menú **Herramientas -> Desarrollador Web -> Firefox OS Simulator**

![Donde está el simulador luego de ser instalado](images/originals/tools-web-developer-simulator.png)

## Conclusión

Ahora que tenemos todo el ambiente preparado, vamos a aprender unos conceptos básicos para construir nuestra primer app.

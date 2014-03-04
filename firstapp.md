#  Nuestra Primer App {#firstapp}

![Memos, un block de notas minimalista](images/originals/memos-app.png)

En este capítulo vamos a contruir la aplicación **Memos** que es un block de notas que creé para que sirva de ejemplo en mis conferencias. Este programa posee tres pantallas. La primera está arriba y es la pantalla principal del programa que lista los títulos de las notas. Al cliquear en una de esas notas o cliquear en el signo mas, somos redireccionados para la pantalla de edición donde podemos modificar el título y el contenido de la nota, como podemos ver abajo:

![Memos, pantalla de edición](images/originals/memos-editing-screen.png)

En esta pantalla de edición el usuario puede borrar la nota que es mostrada al cliquear en el ícono de papelera y confirmar el deseo de borrar la nota, como muestra la captura de pantalla mostrada aquí.

![Memos, confirmar borrar una nota](images/originals/memos-delete-screen.png)

El código de Memos está disponible en [Github del autor](https://github.com/soapdog/memos-for-firefoxos) para quienes quieran bajar y ver el código luego. Existe una copia del código de la app dentro del [repositorio del libro](https://github.com/wfranck/guia-rapido-firefox-os)m que contiene el código fuente en Markdown utilizado para generar este libro.

El Memos utiliza [IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB) para la construcción de su interfaz. En una futura actualización de este libro, hablaré más sobre os building blogks, en esta primer versión simplemente construiremos la app.

El primer paso es separar una carpeta para la aplicación. Vamos a llamar a la carpeta **memos**.

## Creando el manifest

El manifest de Memos es muy simple. Cree un archivo llamado **manifest.webapp** en la carpeta **memos**. Los Manifest son archivos de tipo [JSON](http://json.org) que describen una aplicación. En ellos, colocamos el nombre, la descripción, los íconos utilizados y muchas otras cosas importantes, como qué permisos necesita la aplicación para funcionar y qué archivo es utilizado para cargar la app.

Abajo podemos ver el condenido del manifest de Memos. Preste atención al copiar, pues es más facil equivocar una coma y volver su JSON inválido. Para validar su JSON, puedes utilizar varias herramientas. Una de ellas, específica para validación de manifest, es [http://appmanifest.org/](http://appmanifest.org/). Para aprender más sobre manifest visite
[la página de MDN sobre manifest](https://developer.mozilla.org/pt-BR/docs/Apps/Manifest).

<<[Manifest de la aplicación Memos (*manifest.webapp*)](code/memos/manifest.webapp)

Vamos a explicar cada uno de los campost del manifest de arriba.

|Campo		|Descripción                                                                        |
|-----------|-----------------------------------------------------------------------------------|
|name		|Ese campo es el nombre de la aplicación                                            |
|version	|Versión de la aplicación. Cambiar la versión causa un update en la app.            |
|launch_path|Cuál es el archivo que debe ser cargado cuando su app inicia.                      |
|permissions|Qué permisos necesita la app. (más información adelante)                   		|
|developer  |Quien desarrolló la aplicación.													|
|icons		|Los íconos para cada tamaño necesario.  											|


La parte más interesante de este manifest son los registros de permisos. Con ellos obtenemos permisos para *storage*, que permite que utilicemos IndexDB sin límite de espacio[^storage-permission] (gracias a eso podemos almacenar cuántas notas queramos en nuestro programa).

[^storage-permission]: Para saber más sobre permisos que puedes pedir mire [la página de MDN sobre permisos de aplicación](https://developer.mozilla.org/en-US/docs/Web/Apps/App_permissions).

Con el manifiesto listo, podemos pasar al HTML.

## Estructura del HTML

Antes empezar y hacer el HTML para Memos, vamos a dar una mirada rápida sobre [Gaia Building Blocks](http://buildingfirefoxos.com/building-blocks), que es una iniciativa de construir un conjunto de CSS y JS reutilizable con el *look and feel* de Firefox OS, para que lo aproveches en tus propias apps.

En Firefox OS, así como en la web en general, no estás obligado a utilizar el *look and feel* del sistema operativo. Utilizar o no los Building Clocks es una decisión suya que pasa por cuestiones de *branding*, conveniencia de uso, adecuación sobre lo que necesitas, entre otras. Lo importante es entender que no tendrás ningún tipo de consecuencia por parte de Firefox Marketplace por no utilizar el perfil de Firefox OS. Yo, como no soy buen diseñador, opto siempre por utilizar un paquete listo como este (o contratar un diseñador).

La estructura de HTML de nuestra aplicación fue construída para adecuarse a los patrones adoptador por Gaia Building Blocks, donde cada pantalla es una *section* y los elementos siguen una fórmula. Lo ideal ahora es que bajes el código fuente de Memos a partir del [repositorio Github](https://github.com/soapdog/memos-for-firefoxos) para que tengas los archivos de Building Blocks.

W> Nota: La versión de Building Blocks que usé no es actual y modifiqué algunos archivos. Por eso, el código que vamos a mostrar sólo va a funcionar como una versión que está en el respoitorio de Memos.

### Agregando Building Blocks

Antes que nada, copie las carpetas **shared** y **style** para la carpeta Memos, para que podamos utilizar Building Blocks. Vamos a empezar nuuestro archivo **index.html**, con los *includes* necesarios para el programa.

~~~~~~~~
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="/style/base.css" />
    <link rel="stylesheet" type="text/css" href="/style/ui.css" />
    <link rel="stylesheet" type="text/css" href="/style/building_blocks.css" />
    <link rel="stylesheet" type="text/css" href="shared/style/headers.css" />
    <link rel="stylesheet" type="text/css" href="shared/style_unstable/lists.css" />
    <link rel="stylesheet" type="text/css" href="shared/style_unstable/toolbars.css" />
    <link rel="stylesheet" type="text/css" href="shared/style/input_areas.css" />
    <link rel="stylesheet" type="text/css" href="shared/style/confirm.css" />
    <title>Memos</title>
</head>
~~~~~~~~

En *línea 01* declaramos el tipo de archivo como HTML 5. De la *línea 05 hasta la línea 15* incluímos los CSS que son utilizados por la aplicación, tales como cabeceras, listas, áreas de entrada de datos, entre otros.

### Armando la pantalla principal

Ahora podemos seguir con la implementación de las pantallas. Como dijimos anteriormente, cada pantalla es una **<section>** dentro de un **<body>** del HTML y debe tener un atributo *role* con valor *application*, como `<body role="application">`. Eso es utilizado por los selectores de los CSS de Building Blocks. Vamos a armar la primer pantalla (y declarar el body).

~~~~~~~~
<body role="application">

<section role="region" id="memo-list">
    <header>
        <menu type="toolbar">
            <a id="new-memo" href="#"><span class="icon icon-add">add</span></a>
        </menu>
        <h1>Memos</h1>
    </header>
    <article id="memoList" data-type="list"></article>
</section>
~~~~~~~~

Nuestra pantalla tiene un **<header>** que posee un botón para agregar notas e el nbombre del programa. Posee también un **<article>** que es utilizado para contener la lista de notas en la app. Nosotros utilizamos las IDs de **<article>** y del **botão** para capturar eventos cuando estamos del lado del JavaScript.

Note que la creación de la pantalla es un HTML fácil de entender. Hacer la misma pantalla en otros lenguajes es mucho más trabajoso. Simplemente declaramos nuestros componentes y damos IDs a los elementos que vamos a referenciar posteriormente.

Ahora que tenemos la pantalla principal lista, vamos a armar la pantalla de edición que es más complicada.

### Armando la pantalla de edición

~~~~~~~~
<section role="region" id="memo-detail" class="skin-dark hidden">
    <header>
        <button id="back-to-list"><span class="icon icon-back">back</span>
        </button>
        <menu type="toolbar">
            <a id="share-memo" href="#"><span class="icon icon-share">share</span>
            </a>
        </menu>
        <form action="#">
            <input id="memo-title" placeholder="Memo Title" required="required" type="text">
            <button type="reset">Remove text</button>
        </form>
    </header>
    <p id="memo-area">
        <textarea placeholder="Memo content" id="memo-content"></textarea>
    </p>
    <div role="toolbar">
        <ul>
            <li>
                <button id="delete-memo" class="icon-delete">Delete</button>
            </li>
        </ul>
    </div>
    <form id="delete-memo-dialog" role="dialog" data-type="confirm" class="hidden">
        <section>
            <h1>Confirmation</h1>
            <p>Are you sure you want to delete this memo?</p>
        </section>
        <menu>
            <button id="cancel-delete-action">Cancel</button>
            <button id="confirm-delete-action" class="danger">Delete</button>
        </menu>
    </form>
</section>
~~~~~~~~

Esa pantalla de edición contiene la pantalla de diálogo utilizada cuando un usuario intenta borrar una nota, por eso es más complicado.

En la parte superior de la pantalla, que está marcada por **<header>**, tenemos el botón de volver para la pantalla principal, un box de entrada de texto, que es utilizado para mostrar y modificar el título de la nota, y un botón utilizado para enviar la nota por email.

Después de la toolbar de arriba,  tenemos un párrafo conteniendo un área para la entrada de texto de la nota y, entonces, otra toolbar, con un botón para borrar la nota que está abierta.

Esos tres elementos y sus hijos forman la pantalla de edición. Luego de esta pantalla tenemos un **<form>** que, en verdad, representa el diálogo utilizado por la pantalla para la confirmación de borrado de las notas. Esa caja de diálogo es muy simple, conteniendo un mensaje informativo y un botón para cancelar la acción de borrar la nota y uno para confirmar.

Al cerrar esa **<section>** terminamos todas las pantallas del programa y el restante código HTML sólo sirve para incluir los archivos de JavaScript utilizados por el programa.

~~~~~~~~
<script src="/js/model.js"></script>
<script src="/js/app.js"></script>
</body>
</html>
~~~~~~~~

## Armando el JavaScript

Ahora vamos  programar de verdad y dar vida a nuestra app. Para organizar, separé el código en dos archivos JavaScript:

* **model.js:** que contiene las rutinas para lidiar con el almacenamiento y modificación de notas. Sin embargo, no contiene la lógica del programa o algo relacionado con su interfaz o tratamiento de entrada de datos.
* **app.js:** encargada de llamar a los elementos de HTML y las rutinas correspondientes, además de la lógica de la app.

Los dos archivos deben ser puestos en una carpeta llamara **js**, al lado de las carpetas **style** y **shared**.


### model.js

En Firefox OS utilizaremos [IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB) para guardar las notas.Como pedimos permiso de *storage*, podemos grabar cuantas notas permita la memoria del dispositivo.

La parte del código del model.js, que mostraré abajo, es responsable por establecer la conexión y crear el *storage* si fuera necesario.

A> Importante: Ese código fue escrito para ser entendido fácilmente y no representa las mejores prácticas de programacieon para JavaScript. Variables globales son utilizadas (ARGH!), entre otros problemas. Fuera de eso, el tratamiento de errores es básicamente inexistente. Lo más importante de este libro es enseñar el *worlflow* de cómo programar apps para Firefox OS.

~~~~~~~
var dbName = "memos";
var dbVersion = 1;

var db;
var request = indexedDB.open(dbName, dbVersion);

request.onerror = function (event) {
    console.error("Can't open indexedDB!!!", event);
};
request.onsuccess = function (event) {
    console.log("Database opened ok");
    db = event.target.result;
};

request.onupgradeneeded = function (event) {

    console.log("Running onUpgradeNeeded");

    db = event.target.result;

    if (!db.objectStoreNames.contains("memos")) {

        console.log("Creating objectStore for memos");

        var objectStore = db.createObjectStore("memos", {
            keyPath: "id",
            autoIncrement: true
        });
        objectStore.createIndex("title", "title", {
            unique: false
        });

        console.log("Adding sample memo");
        var sampleMemo1 = new Memo();
        sampleMemo1.title = "Welcome Memo";
        sampleMemo1.content = "This is a note taking app. Use the plus sign in the topleft corner of the main screen to add a new memo. Click a memo to edit it. All your changes are automatically saved.";

        objectStore.add(sampleMemo1);
    }
}
~~~~~~~

A> Importante: Nuevamente perdonen por las variables globales, esto aquí es solamente una app educativa. Otro detalle es que removí los comentarios de los códigos agregados al libro para economizar espacio. El código fuente de github está comentado.

El código arriba crea un objeto *db* y un objeto *request*. El objeto *db* es utilizado por otras funciones en el código para manipular el registro de las notas.

En la implementación de la función `request.onupgradeneeded` aprovechamos para crear una nota de ejemplo. De esa forma, así que la aplicación llama por primera, esa función es ejecutada y la base de datos es inicializada con una nota de bien venida.

Con nuestra conexión establecida y el almacenamiento inicializado, es hora de implementar las funciones para manipular las notas.

~~~~~~~~
function Memo() {
    this.title = "Untitled Memo";
    this.content = "";
    this.created = Date.now();
    this.modified = Date.now();
}

function listAllMemoTitles(inCallback) {
    var objectStore = db.transaction("memos").objectStore("memos");
    console.log("Listing memos...");

    objectStore.openCursor().onsuccess = function (event) {
        var cursor = event.target.result;
        if (cursor) {
            console.log("Found memo #" + cursor.value.id + " - " + cursor.value.title);
            inCallback(null, cursor.value);
            cursor.continue();
        }
    };
}

function saveMemo(inMemo, inCallback) {
    var transaction = db.transaction(["memos"], "readwrite");
    console.log("Saving memo");

    transaction.oncomplete = function (event) {
        console.log("All done");
    };

    transaction.onerror = function (event) {
        console.error("Error saving memo:", event);
        inCallback({
            error: event
        }, null);

    };

    var objectStore = transaction.objectStore("memos");

    inMemo.modified = Date.now();

    var request = objectStore.put(inMemo);
    request.onsuccess = function (event) {
        console.log("Memo saved with id: " + request.result);
        inCallback(null, request.result);

    };
}

function deleteMemo(inId, inCallback) {
    console.log("Deleting memo...");
    var request = db.transaction(["memos"], "readwrite").objectStore("memos").delete(inId);

    request.onsuccess = function (event) {
        console.log("Memo deleted!");
        inCallback();
    };
}
~~~~~~~~

Arriba creamos una función contructora para agregar nuevas notas ya con algunos campos inicializados. Siguiendo, implementamos funciones para listar,guardar y borrar las notas. Esas funciones, por lo general, siempre aceptan un parámetro `inCallback` que es una función de retorno para ejecutarse después del proceso de la función. Eso es necesario dado la naturaleza asíncrona de las llamadas de IndexedDB. Todos los callbacks tienen la misma forma, que es `callback(error, value)`, donde uno de los dos valores es nulo dependiendo lo que pasó.

A> Como este es un libro de caracter introductorio, opté por no utilizar [*Promises*](https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules/Promise.jsm/Promise). Visto que muchos desarrolladores aún no están familiarizados con el concepto, fuertemente recomiendo la utilización deste tipo de soluciones que vuelve el código más legible y fácil de mantener.

Con nuestras funciones para el almacenamiento y manipulación de notas listas, ahora vamos a implementar la lógica de nuestra app en el archivo **app.js**

### app.js

Ese archivo contiene nuestra lógica de programa. Como el código es mucho para ser mostrado de una vez, voy a partirlo en partes y mastrarlo de a poco.

~~~~~~~~
var listView, detailView, currentMemo, deleteMemoDialog;

function showMemoDetail(inMemo) {
    currentMemo = inMemo;
    displayMemo();
    listView.classList.add("hidden");
    detailView.classList.remove("hidden");
}


function displayMemo() {
    document.getElementById("memo-title").value = currentMemo.title;
    document.getElementById("memo-content").value = currentMemo.content;
}

function shareMemo() {
    var shareActivity = new MozActivity({
        name: "new",
        data: {
            type: "mail",
            body: currentMemo.content,
            url: "mailto:?body=" + encodeURIComponent(currentMemo.content) + "&subject=" + encodeURIComponent(currentMemo.title)

        }
    });
    shareActivity.onerror = function (e) {
        console.log("can't share memo", e);
    };
}

function textChanged(e) {
    currentMemo.title = document.getElementById("memo-title").value;
    currentMemo.content = document.getElementById("memo-content").value;
    saveMemo(currentMemo, function (err, succ) {
        console.log("save memo callback ", err, succ);
        if (!err) {
            currentMemo.id = succ;
        }
    });
}

function newMemo() {
    var theMemo = new Memo();
    showMemoDetail(theMemo);
}
~~~~~~~~

Primero, declaramos algunas variables globales para almacenar referencias a algunos elementos que pretendemos utilizar dentro de las funciones. De las variables globales, la más interesante es `currentMemo`, que es un objeto que guarda cuál nota está viendo el usuario.

Las funciones `showMemoDetail()` y `displayMemo()` funcionan juntas. La primera carga la nota elegida en `currentMemo` y manipula el CSS de los elementos, para que la pantalla de visualización/edición sea mostrada. La segunda se encarga de pegar el contenido de `currentMemo` y agrega la pantalla. Se podía hacer las dos cosas dentro de una función sola, pero cuando estaba haciendo pruebas con esta app separé las funciones para que la inserción de contenido de la nota en la interfaz quede separada de la manipulación de las pantalles. De esta forma, pude jugar más con variaciones de las funciones.

La función `shareMemo()` utiliza una [WebActivity](https://hacks.mozilla.org/2013/01/introducing-web-activities/) para crear un nuevo mensaje en el programa de email con el contenido de la nota.

La función `textChanged()` toma los datos de los campos de entrada, los coloca nuevamente en `currentMemo` y entonces guarda la nota. Eso se hace pues la idea de un programa es que el usuario nunca necesite explícitamente guardar una nota. Toda modificación en los textos de entrada causan la execución de esa rutina y la actualización de la nota en la base de datos.

La función `newMemo()` crea una neuva nota y abre la pantalla de edición para ella.

~~~~~~~~
function requestDeleteConfirmation() {
    deleteMemoDialog.classList.remove("hidden");
}

function closeDeleteMemoDialog() {
    deleteMemoDialog.classList.add("hidden");
}

function deleteCurrentMemo() {
    closeDeleteMemoDialog();
    deleteMemo(currentMemo.id, function (err, succ) {
        console.log("callback from delete", err, succ);
        if (!err) {
            showMemoList();
        }
    });
}

function showMemoList() {
    currentMemo = null;
    refreshMemoList();
    listView.classList.remove("hidden");
    detailView.classList.add("hidden");
}
~~~~~~~~

La funcieon `requestDeleteConfirmation()` es responsable de mostrar la tela de confirmacieon de borrado de notas.

Las funciones `closeDeleteMemoDialog()` y `deleteCurrentMemo()` son accionadas por los botones cancelar y confirmar de borrado de la nota.

La función `showMemoList()` es un obstáculo antes de mostrar la lista de notas, pues limpia el valor de `currentMemo`. Al final, si estamos viendo la lista de notas, entonces no estamos viendo ninguna nota. Así, la función hace hace que la pantalla principal sea mostrada.

~~~~~~~~
function refreshMemoList() {
    if (!db) {
        // HACK:
        // this condition may happen upon first time use when the
        // indexDB storage is under creation and refreshMemoList()
        // is called. Simply waiting for a bit longer before trying again
        // will make it work.
        console.warn("Database is not ready yet");
        setTimeout(refreshMemoList, 1000);
        return;
    }
    console.log("Refreshing memo list");

    var memoListContainer = document.getElementById("memoList");


    while (memoListContainer.hasChildNodes()) {
        memoListContainer.removeChild(memoListContainer.lastChild);
    }

    var memoList = document.createElement("ul");
    memoListContainer.appendChild(memoList);

    listAllMemoTitles(function (err, value) {
        var memoItem = document.createElement("li");
        var memoP = document.createElement("p");
        var memoTitle = document.createTextNode(value.title);

        memoItem.addEventListener("click", function (e) {
            console.log("clicked memo #" + value.id);
            showMemoDetail(value);

        });

        memoP.appendChild(memoTitle);
        memoItem.appendChild(memoP);
        memoList.appendChild(memoItem);


    });
}
~~~~~~~~

La función `refreshMemoList()` modifica el DOM a construir, elemento por elemento, la lista de notas incluídas en la base de datos. Sería más fácil utilizar un template con handlebars o algo parecido, pero como esta es una app *vanilla javascript*, hicimos todo a mano. Esa función es llamada por `showMemoList()` que fue mostrada anteriormente.

Esas son todas las funciones de nuestro programa. La única parte del código que falta es la inicialización de los eventos y llamada inicial para`refreshMemoList()`.

~~~~~~~
window.onload = function () {
    // elements that we're going to reuse in the code
    listView = document.getElementById("memo-list");
    detailView = document.getElementById("memo-detail");
    deleteMemoDialog = document.getElementById("delete-memo-dialog");

    // All the listeners for the interface buttons and for the input changes
    document.getElementById("back-to-list").addEventListener("click", showMemoList);
    document.getElementById("new-memo").addEventListener("click", newMemo);
    document.getElementById("share-memo").addEventListener("click", shareMemo);
    document.getElementById("delete-memo").addEventListener("click", requestDeleteConfirmation);
    document.getElementById("confirm-delete-action").addEventListener("click", deleteCurrentMemo);
    document.getElementById("cancel-delete-action").addEventListener("click", closeDeleteMemoDialog);
    document.getElementById("memo-content").addEventListener("input", textChanged);
    document.getElementById("memo-title").addEventListener("input", textChanged);

    // the entry point for the app is the following command
    refreshMemoList();

};
~~~~~~~

Ahora todos nuestros archivos están listos, podemos testear la aplicación en el simulador. 

## Test de la app en el simulador

Antes de testear la aplicación en el simulador es mejor garantizarnos que todos los archivos están en el lugar correcto. Su carpeta debe parecerse a esta:

![Lista de archivos Memos](images/originals/memos-file-list.png)

Si desconfías que puede haber algún error con lo que escribió, basta con comparar su versión con la que está en [el GitHub del autor](https://github.com/soapdog/memos-for-firefoxos) (Existe una copia del código en el código de la carpeta **code** dentro de [repositório do livro](https://github.com/wfranck/guia-rapido-firefox-os) ).

Para abrir el *Dashboard del Simulator* vamos al menú **Herramientas -> Desarrollador Web -> Firefox OS Simulator**.

![Cómo abrir el dashboard del simulador](images/originals/tools-web-developer-simulator.png)

Con el dashboard abierto, cliquée en el botón **Add Directory**, navee hasta la carpeta del código fuente de Memos y seleccion el archivo manifest.

![Agregando una nueva aplicación](images/originals/simulator-add-directory.png)

Si todo funciona correctamente, verás una aplicación Memos en la lista de apps.

![Memos apareciendo en el dashboard](images/originals/memos-on-dashboard-display.png)

Al agregar la app, el simulador llamará automáticamente con la app abierta para que puedas testear. Listo, ya puedes testear las funcionalidades de Memos. Felicitaciones, creó y testeó su perimer app. No es una app completa o revolusionaria, pero nos ayudó a entender el *workflow* de desarrollo. Siempre recuerde que puedes modificar el código fuente de la aplicación, debes presionar el botón **Refresh** para actualizar la copia que está instalada en el simulador.

## Conclusión

Felicitaciones, ya construíste ti primer aplicación mobile para Firefox OS y la testeó en el simulador. En el próximo capítulo presentaremos las herramientas para desarrollador que facilitarán su vida a la hora de programar.


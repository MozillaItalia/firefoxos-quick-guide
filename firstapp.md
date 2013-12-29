# La Nostra Prima App {#firstapp}

![Memos, un blocco note minimal](images/originals/memos-app.png)

In questo capitolo vedremo come realizzare un semplice **Notepad**, che è un'applicazione per prendere appunti. Prima di programmare vediamo di studiare il funzionamento di questa applicazione. 

Quest'applicazione ha tre schermate. La prima è la schermata principale ed è una lista delle varie note con i titoli. Quando clicchi una nota (o ne aggiungi una) si viene portati sulla schermata con i dettagli che permettono di modificare il contenuto ed il titolo della nota scelta. Possiamo vedere queste schermate qui sotto.

![Memos, schermata di modifica](images/originals/memos-editing-screen.png)

Nella schermata superiore l'utente può scegliere di cancellare la nota selezionata cliccando sul cestino. Questa azione aprirà una finestra di conferma.

![Memos, finestra di conferma della cancellazione](images/originals/memos-delete-screen.png)

Il codice sorgente per Memos è disponibile nel [Repo su Github](https://github.com/soapdog/memos-for-firefoxos) (disponibile come file [.zip](https://github.com/soapdog/memos-for-firefoxos/archive/master.zip) ). Consiglio di scaricare i file così sarà più semplice seguire la guida. Un'altra copia del codice sorgente è disponibile nella cartella dentro il [repository github repository di questo libro](https://github.com/soapdog/firefoxos-quick-guide).

Memos usa [IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB) per salvare le note e [Gaia Building Blocks](http://buildingfirefoxos.com/building-blocks) per costruire le interfacce. In un'aggiornamento futuro il libro conterrà molte informazioni su Gaia Building Blocks, ma in questa prima versione lo userò soltanto. Puoi vedere il link qui sopra per saperne di più sull'argomento vai al link precedente.

Il primo passaggio è creare una cartella per l'applicazione, chiameremo questa cartella **memos**.

## Creare un app manifest

Il manifest di Memos è molto semplice. Crea un file chiamato **manifest.webapp** nella cartella **memos**. I manifest sono dei file [JSON](http://json.org) che descrivono un'applicazione. In questo filepossiamo trovare il nome dell'app, chi è lo sviluppatore, che icone usa, qual'è il file da lanciare per l'app, quali API privilegiate sono usate e molto altro.

Qui di seguito puoi vedere il contenuto del manifest di Memos. Attenzione con il copia ed incolla, perchè è molto facile mettere una virgola nel posto sbagliato e creare un JSON sbagliato. Ci sono molti strumenti per validare un file JSON ma c'è nè uno costruito apposta per i manifest. Puoi usare il tool online su [http://appmanifest.org/](http://appmanifest.org/). Per scoprire altro su questi file [vai alla pagina su MDN ](https://developer.mozilla.org/docs/Apps/Manifest).

<<[Memos manifest (*manifest.webapp*)](code/memos/manifest.webapp)

Vediamo i campi di questo manifest:

|Campi		|Descrizione                                                                        |  
|-----------|-----------------------------------------------------------------------------------|  
|name		|Il nome dell'applicazione  		                                                |  
|version	|La versione attuale dell'applicazione  										    |  
|launch_path|Il file usato per lanciare un'applicazione 					                    |  
|permissions|I permessi API richiesti, con molte informazioni		                     		|  
|developer  |Lo sviluppatore                    												|  
|icons		|L'icona usata in diversi formati                   								|  

La parte più interessanti di questo manifest è la richiesta dei permessi di *storage* che permettono di usare IndexedDB senza restrizioni di dimensioni[^storage-permission] (con questi permessi possiamo salvare le note che vogliamo - anche se dobbiamo fare attenzione a non usare troppo spazio sul disco dell'utente!).

[^storage-permission]: Per saperne di più su questa autorizzazione leggi [la pagina MDN sui permessi](https://developer.mozilla.org/en-US/docs/Web/Apps/App_permissions).

Ora che il manifest è pronto passiamo al codice HTML.

## Scriviamo il codice HTML

Prima di iniziare a lavorare sul codice HTML, facciamo una piccola introduzione su [Gaia Building Blocks](http://buildingfirefoxos.com/building-blocks), che è un'insieme di codice CSS e JavaScript con il *look and feel* di Firefox OS che possiamo usare nelle nostre applicazioni.

Come nelle pagine web, non è richiesto di usare il *look and feel* di Firefox OS nella propria applicazione. Usare o non usare Gaia Building Blocks è una scelta personale - e le buone applicaizone possono usare uno stile distintivo ed'una esperienza utente. La cosa importante da capire è che la tua applicazione non subirà alcun tipo di pregiudizio o penalità nel Marketplace Firefox non usando il look di Gaia. Io lo uso perchè non sono un bravo designer e dei UI toolkit pronti mi piacciono.

La struttura HTML che usiamo nelle applicazioni seguirà gli schemi adottati da Gaia Building Blocks dove ogni schermata `<section>` e gli elementi seguono un formato definito. Se non hai ancora scaricato il codice sorgente dal [repository memos]
(https://github.com/soapdog/memos-for-firefoxos) fallo perchè contiene i Building Blocks necessari. per chi non ha confidenza con git e GitHub, ecco il [file .zip](https://github.com/soapdog/memos-for-firefoxos/archive/master.zip). 

W> Attenzione: la versione usata di Gaia Building Blocks non è la più recente. Aggiornare l'applicazione alla nuova versione renderà il codice compatibile in quest'applicazione. Nei tuoi progetti usa sempre l'ultima versione di Gaia Building Blocks.

### Includere Building Blocks

Prima di fare qualsiasi altra cosa copiare le cartelle **shared** e **styles** che trovi scaricando il repository Memos nella cartella **memos** che hai creato. Questo ti permetterà di usare Gaia Building Blocks nella tua applicazione. 

Prendiamo il file **index.html** inserendo il codice necessario.

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

Nella *linea 1* dichiariamo il DOCTYPE come HTML5. Dalla *linea 5 alla 15* includiamo i file CSS dei vari componenti da usare nelle app testata, liste, campi testuali e molto altro.

### Costruiamo la schermata principale

Iniziamo a costruire le varie schermate. Come menzionato sopra ogni schermata è una `<section>` dentro `<body>` nel codice HTML. Il tag body deve avere un attributo *role* con un valore uguale ad *application* perchè è usato dai selettori CSS per creare l'interfaccia, quindi il tag sarà `<body role="application">`. Creiamo la prima schermata e dichiariamo il tag body come abbiamo detto.

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

La schermata contiene un `<header>` con un pulsante che permette di aggiungere nuove note ed il nome dell'applicazione stessa. La schermata include un `<article>` che è usato per mostrare il contenuto della nota. Useremo il pulsante e l'ID dell'articolo per catturare gli eventi nella parte JavaScript.

Sottolineo il fatto che ogni schermata è un semplice pezzo di codice HTML. Costruire queste schermate in multilingua su altri sistemi richiede molto lavoro. Tutto quello che faremo è dare ad ogni contenitore un ID specifico che richiameremo successivamente.

La prima schermata è finita adesso vediamo la schermata di modifica.

### Costruire la schermata di modifica

La schermata di modifica è un'pò complessa perchè contiene la finestra di dialogo di eliminazione delle note.

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

Nella parte superiore dello schermo, rappresentato dall'elemento `<header>`: 

 * un pulsante per tornare indietro alla schermata principale, 
 * un campo di testo per modificare il titolo della nota, 
 * un pulsante per condividere la nota via.

Sotto questa barra abbiamo una `<textarea>` che contiene il contenuto della notae sotto ha un'altra barra con il cestino per cancellare la nota che si sta visualizzando.

Questi tre elementi e il loro contenuto sono la schermata di modifica. Dopo questo abbiamo un `<form>` che è usato per una finestra di conferma che verrà mostrata all'utente quando per cancellare una nota. Questa finestra è molto semplice, contiene un testo ed una finestra di conferma con due pulsanti, uno per cancellare la nota ed uno per annullare l'azione.

A questo punto chiudiamo il tag `<section>` avendo tutte le schermate necessarie, il codice HTML rimasto include i file JavaScript e chiude il file.

~~~~~~~~
<script src="/js/model.js"></script>
<script src="/js/app.js"></script>
</body>
</html>
~~~~~~~~

## Manipoliamo il codice JavaScript

Adesso ci divertiremo a dare vita alla nostra applicazione usando JavaScript. per organizzare meglio questo codice lo ho diviso in due file:

* **model.js:** contiene le routine per la memorizzazione e restituzione delle note ma non contiene codice della logica, materiali dell'interfaccia o immissione dati. In teoria potremmo utilizzare questo file in altre applicazioni che richiedono note.
* **app.js:** collega gli eventi agli elementi HTML e contiene la logica dell'applicazione.

Entrambi i file devono essere posizionati nella cartella **js** vicino a quella **style** e **shared**.

### model.js

Utilizzeremo [IndexedDB](https://developer.mozilla.org/en-US/docs/IndexedDB/Using_IndexedDB) per salvare le note. Avendo chiesto i permessi per lo *storage* nel manifest possiamo salvare quante note vogliamo - ma non abusarne! I dispositivi Firefox OS solitamente non hanno molto spazio, è sempre meglio essere consapevoli di quali dati vengono memorizzati (gli utenti daranno un voto negativo alla tua applicazione se userà troppo spazio!). Memorizzare troppo materiale creerà problemi di performance creando problemi di performance. Aggiungi nelle note di invio delle applicazione nel marketplace FireFox OS perchè hai bisogno di spazio illimitato altrimenti i revisori te lo chiederanno - se non lo puoi giustificare l'applicazione verrà rifiutata.  

La parte di codice di *model.js* mostrato qui sotto si occupa del collegamento e creazione dello storage.

A> Importante: Questo codice è scritto per essere capito velocemente e non rappresenta le migliori pratiche di programmazione JavaScript. Nel codice sono presenti delle variabili globali (andrò all'inferno per questo lo so) tra le altre chicche. La gestione degli errori è praticamente inesistente. Lo scopo principale di questo libro è insegnare il *workflow* di sviluppo di applicazioni per Firefox OS e non insegnare pattern JS. Quindi a seconda dei commenti migliorerò il codice sempre che non abbia un brutto impatto ai principianti.  

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

A> Importante: Dimentica ancora le variabili globali, questo è solo materiale di riferimento. Inoltre ho rimosso i commenti dal codice per risparmiare spazio nel libro. Su Github il codice è completo di commenti.

Il codice appena vista crea un oggetto *db* ed un'oggetto *request*. L'oggetto *db* è usato in altre funzioni nel codice per manipolare le note memorizzare.

Nella implementazione della funzione `request.onupgradeneeded` creiamo una nota di benvenuto. Questa funzione è eseguita quando l'applicazione viene lanciata per la prima volta (o quando la versione del database cambia). In questo modo al primo avvio dell'applicazione il database contiene una nota di esempio.  

Apriamo la connessione e prepariamo le funzioni base di manipolazione delle note.

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

In questo pezzo di codice abbiamo creato una funzione che crea nuove note con alcuni campi già pronti. Dopo la creazione delle funzioni per la creazione delle liste, salvataggio e cancellazione delle note. Molte di queste funzioni hanno un parametro chiamato `inCallback` questa funzione verrà invocata alla fine della funzione. Questo è necessario per la natura asincrona di IndexedDB. Tutte le callback hanno la stessa firma con `callback(error, value)` dove uno di questi valori è nullo a seconda del risultato della funzione precedente.

A> Siccome è un libro per principianti ho scelto di non usare [*Promises*](https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules/Promise.jsm/Promise) perchè non tutti i principianti potrebbero capirlo. Consiglio di usare questi concetti per avere un codice più pulito e facile da mantenere.

Ora che abbiamo la memorizzazione delle note funzionante, lavoriamo alla logica dell'applicazione nel file **app.js**.

### app.js

Questo file contiene la logica dell'applicaizone. Il codice sorgente è troppo lungo da mostrare nel libro quindi verrà diviso in parti per studiarlo meglio.

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

All'inizio dichiariamo alcune variabili globali (yuck!!!) per avere dei riferimenti del DOM che useremo in alcune funzioni. La parte più interessante è  `currentMemo` che è un'oggetto che contiene la nota attuale che l'utente sta vedendo.

Le funzioni `showMemoDetail()` e `displayMemo()` lavorano insieme. La prima carica la nota selezionata in `currentMemo` e modifica il CSS degli elementi mostrati nella schermata di modifica. La seconda prende il contenuto della variabile `currentMemo` e mostra la nota a schermo. Potremmo mettere il codice nella stessa funzione ma averlo separato permette di divertirci di più con nuove implementazioni.

La funzione `shareMemo()` usa [WebActivity](https://hacks.mozilla.org/2013/01/introducing-web-activities/) per aprire l'applicazione dell'email con un nuovo messaggio preconfezionato con il contenuto della nota selezionato. 

la funzione `textChanged()` prende il contenuto dei campi e lo inserisce nell'oggetto `currentMemo` che salva la nota. Questo perchè avremo un'applicazione con auto salvataggio. Tutte le modifiche al contenuto o al titolo invocheranno la funzione che salverà in IndexedDB.

The `newMemo()` function creates a new note and opens the editing screen with it.

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

La funzione `requestDeleteConfirmation()` mostra la richiesta di conferma di rimozione della nota.

La funzione `closeDeleteMemoDialog()` e `deleteCurrentMemo()` sono invocate dai pulsanti nella finestra di conferma.

La funzione `showMemoList()` fà una pulizia e mostra l'elenco delle note presenti. Per esempio, svuota il contenuto di `currentMemo` se non stiamo leggendo una nota.

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

La funzione `refreshMemoList()` modifica il DOM aggiornando l'elenco delle note. Sarebbe più facile alcuni sistemi di template come [handlebars](http://handlebarsjs.com/) o [underscore](http://underscorejs.org/) ma quest'applicazione contiene solo *vanilla javascript* quindi faremo tutto a manina. Questa funzione è chiamata `showMemoList()` mostrata sopra.

Queste sono tutte le funzioni usate dall'applicazione. L'unica parte mancante è il gestore eventi e la chiamata iniziale di `refreshMemoList()`.

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

Ora che tutti i file sono pronti proviamo l'applicazione nel simulatore.

## Prova l'applicazione sul simulatore

Priam di provare la nostra applicazione verifichiamo che i file sono al posto giusto. La cartella memos dovrebbe essere così:

![Lista dei file usati da Memos](images/originals/memos-file-list.png)

Se hai scritto qualcosa di sbagliato controlla [il repository memos su github](https://github.com/soapdog/memos-for-firefoxos) (C'è anche una copia del codice sorgente nella cartella **code** nel [repo del libro](https://github.com/soapdog/guia-rapido-firefox-os) ).

Apri la *Dashboard del Simulatore* vai al menu **Tools -> Web Developer -> Firefox OS Simulator**.

![Apri la dashboard del simulatore](images/originals/tools-web-developer-simulator.png)

Con la dashboard aperta, clicca il pulsante **Crea una cartella** e trova il file manifest dell'applicazione.

![Crea una nuova applicazione](images/originals/simulator-add-directory.png)

Se tutta funziona come immaginato vedrai l'applicazione Memos nella lista delle applicazioni.

![Memos mostrata nella dashboard](images/originals/memos-on-dashboard-display.png)

Quando aggiungerai una nuova applicazione, il simulatore lanciato si aprirà con l'applicazione aperta - così potrai testarla. ora proviamo le varie funzionalità di Memos. 

Congratulazioni! hai creato e provato la tua prima applicazione. Non è un'applicazione complessa o rivoluzionara - ma spero sia utile per capire il workflow di sviluppo di FireFox OS. Come hai potuto vedere non è molto diverso dallo sviluppo web classico.  

Ricordati che ogni volta che modifichi il codice sorgente devi premere il pulsante **Aggiorna** per aggiornare il contenuto dell'applicazione presente nel simulatore.

## Riassunto

In questo capitolo abbiamo costruito la nostra prima applicazione per Firefox OS e l'abbiamo lanciata nel simulatore.Nel prossimo capitolo vedremo gli strumenti da sviluppatore presenti in Firefox, che semplificano il lavoro di sviluppo.

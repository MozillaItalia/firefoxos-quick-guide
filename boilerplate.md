## Firefox OS Boilerplate App

Il [boilerplate](https://github.com/robnyman/Firefox-OS-Boilerplate-App) di cui abbiamo letto in precedenza è un'applicazione dimostrativa con molti esempi basilari. Contiene un esempio per la maggior parte delle Web Activity, la questione multilingua, installazione dell'applicazione, API HTML5 e l'interfaccia grafica di Gaia realizzata con *Gaia Building Blocks*.  
La parte interessante è che si trova su Github, quindi c'è anche una demo sempre aggiornata che puoi trovare [qui](http://robnyman.github.io/Firefox-OS-Boilerplate-App/).  

Puoi provare il boilerplate nel tuo browser preferito ma se usi Chrome vedrai che nella console apparirà "Open Web Apps not supported" che vuol dire che non supporta questo standard proposto da Mozilla. 
Lo standard "Open Web App" consiste in un accesso hardware, installazione locale, storage offline, marketplace, API per i pagamenti e le ricevute, [Persona](https://developer.mozilla.org/it/Persona) per i login e il famoso manifest. Questo insieme di caratteristiche ed il manifesto di Mozilla formano le [Open Web Apps](https://hacks.mozilla.org/2013/02/getting-started-with-open-web-apps-why-and-how/)!  
Noi sviluppatori web speriamo che le Open Web Apps vengano supportate da altri browser e sistemi operativi in modo da semplificare il lavoro per noi e per una migliore esperienza utente.  
Dopo questo messaggio pubblicitario riprendiamo il discorso!  
I prodotti di Mozilla che utilizzano Gecko supportano le Open Web Apps e in Firefox OS vediamo l'apice delle loro potenzialità. Firefox sia per Android che desktop le supporta quindi collegandosi al [marketplace](http://marketplace.firefox.com/) si possono installare le applicazioni pensate per queste interfacce (se specificate nel marketplace).  

Il boilerplate è un esempio per le Open Web Apps ([template](https://github.com/mozilla/mortar)) più il supporto proprietario (al momento!) per Firefox OS.  
NB: Le API pensate ed integrate in Firefox OS sono proposte al W3C per una loro standardizzazione (come l'API per la batteria o la vibrazione che sono uno standard). Questo a ricordare che Mozilla lavora per la standardizzazione delle sue idee e non ha interesse a chiudersi. 

Il boilerplate è diviso in tre sezioni ma io ne aggiungo una quarta per gli altri dettagli.

###I dettagli che fanno la differenza

Incominciamo da questi dettagli: 

* AppCache
* Uso OffLine
* Installare l'applicazione
* Localizzazione
* Grafica di Gaia

Alcune di queste cose le abbiamo viste o le vedremo in questa fantastica guida. Quindi passiamo agli argomenti che non sono stati ancora visti o non hanno un capitolo dedicato.   

###Uso Offline
Con Uso OffLine mi riferisco a del codice che permette di sapere se il dispositivo è connesso sfruttando l'oggetto `window.navigator.connection` che è descritto sulla [pagina MDN](http://mdn.beonex.com/en/DOM/window.navigator.connection.html) con i dettagli tecnici e il supporto crossbrowser. 
Il codice è presente in due versioni:

* Uno dei tanti pulsanti che usa [l'API diretta](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js#L331) fornisce due informazioni: la banda disponibile in MB (0 se è offline, _infinity_ se sconosciuta o solitamente la linea fissa) e se la connessione è a consumo.
* Con AppCache per sapere se si utilizza l'applicazione in modalità offline, nel boilerplate è utilizzato per mostrare il pallino verde se si è online.  

Vediamo un attimo questi due codici:

File webapp.js#L331 - window.navigator.connection
~~~~~~~~
var connection = window.navigator.mozConnection,
online = "<strong>Connected:</strong> " + (connection.bandwidth),
metered = "<strong>Metered:</strong> " + connection.metered;
~~~~~~~~

File offline.js#L15 - appCache
~~~~~~~~
var appCache = window.applicationCache;
appCache.onerror = function() {
      displayStatus.className = "offline";
      displayStatus.title = "Offline";
};
~~~~~~~~

###Installare l'applicazione
Installazione applicazione vuol dire utilizzare le Open Web Apps. Vediamo come funziona il codice di installazione e di verifica installazione. Prima di tutto verifichiamo se il sistema le supporta (con `navigator.mozApps`) dopo di che inseriamo dei test di successo o fallimento dell'installazione.

File base.js#L4 - Installazione
~~~~~~~~
if (navigator.mozApps) {
    var checkIfInstalled = navigator.mozApps.getSelf();
    checkIfInstalled.onsuccess = function () {
        if (checkIfInstalled.result) {
            // Already installed
            var installationInstructions = document.querySelector("#installation-instructions");
            if (installationInstructions) {
                installationInstructions.style.display = "none";
            }
        }
        else {
            var install = document.querySelector("#install"),
                manifestURL = location.href.substring(0, location.href.lastIndexOf("/")) + "/manifest.webapp";
            install.className = "show-install";
            install.onclick = function () {
                var installApp = navigator.mozApps.install(manifestURL);
                installApp.onsuccess = function() {
                    install.style.display = "none";
                };
                installApp.onerror = function() {
                    alert("Install failed\\n\\n:" + installApp.error.name);
                };
            };
        }
    };
} else {
    console.log("Open Web Apps not supported");
}
~~~~~~~~

Come si può vedere il codice è molto semplice, si dà l'indirizzo del file manifest e si verifica se è stato installato. Per installare il boilerplate fate click sul simbolo più in alto a destra.
Questo codice eseguito su Firefox OS, Firefox for Android e Firefox desktop aprirà un mini pop up per chiedere se installare l'applicazione.

###WebActivity
Finalmente parliamo di una delle grandi novità per gli sviluppatori web! Finalmente potremo accedere al sistema in modo più profondo! Ho già detto finalmente?  
<<<<<<< HEAD
Scherzi a parte in questa sezione possiamo accedere ad alcune delle azioni del sistema come fare una telefonata o scattare una foto. Queste WebActivity purtroppo sono solo per Firefox OS e quindi il testing è solo con simulatore ma c'è chi sta lavorando ad una [polyfill](https://github.com/Mte90/moz-polyfills) per supportare le web activity anche da browser (dove possibile).  
=======
Scherzi a parte, in questa sezione possiamo accedere ad alcune delle azioni del sistema come fare una telefonata o scattare una foto. Queste WebActivity purtroppo sono solo per Firefox OS e quindi il testing è solo con simulatore ma c'è chi sta lavorando ad una [polyfill](https://github.com/Mte90/moz-polyfills) per supportare le web activity anche da browser (dove possibile).  
>>>>>>> f82e303b2fce314d414ec1b737a9769a4b0cc54a
Non vedremo il codice nel dettaglio delle varie WebActivity, quindi rimando al [file webapp.js](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js), ma elenchiamo le varie WebActivity: 

* Cercare file
* Scattare una foto
* Avviare una telefonata
* Mandare un SMS
* Aggiungere un contatto
* Condividere un sito
* Condividere una foto con un'applicazione
* Aprire un sito
* Scrivere un'email (con l'applicazione di sistema)
* Salvare un segnalibro
* Aprire un video

###WebAPI
<<<<<<< HEAD
Questa sezione contiene sia codice (lo stesso file di prima) solo per Firefox OS ma anche un po' di HTML5 di recente introduzione. Abbiamo le notifiche, rotazione e accensione dello schermo che sono solo per Firefox OS mentre vibrazione, verifica della connessione (ne abbiamo parlato prima), geolocalizzazione, luce ambientale, prossimità, batteria sono API standard.

###API Privilegiate
Queste API sono particolari e sono disponibili solo per le app privilegiate e sono quasi tutte standard HTML5. 
C'è il codice per verificare se l'applicazione ha il focus, quindi se la scheda è aperta, ed accedere alle immagini. Questi sono standard HTML mentre selezionare i contatti e fare richieste XHR CrossDomain sono una peculiarità di Firefox OS.

##Multilingua

Nel [Boilerplate](https://github.com/robnyman/Firefox-OS-Boilerplate-App) appena visto è utilizzata una libreria javascript di nome [webL10n](https://github.com/fabi1cazenave/webL10n/tree/master). Questa libreria è presente in Gaia ma si tratta di una versione modificata (questa è la versione presente nel boilerplate).  
Il sistema riconosce in automatico la lingua utilizzata e carica la lingua in uso dell'applicazione. Al caricamento del file JavaScript della libreria viene caricato un file .ini che contiene i riferimenti alle varie lingue disponibili dell'applicazione. Dopodiché la libreria carica il file della lingua utilizzata dal browser o del sistema. Diamo un'occhiata al codice prima di vedere come avviene la magia della localizzazione.  

`<link rel="resource" type="application/l10n" href="locales/locales.ini" />
<script type="application/javascript" src="js/l10n.js"></script>`

Con questo codice il boilerplate carica i file della lingua... ma come sa dove agire per cambiare il testo?  
La libreria lo sà tramite degli attributi `data-l10n-id` ai tag di cui vogliamo la traduzione che deve contenere il nome di riferimento della stringa da mostrare.

###File della lingua

* locales.ini: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/locales.ini) che contiene i percorsi dei vari file di lingua con il loro codice di riconoscimento.
* manifest.properties: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/manifest.properties) che contiene la traduzione del manifest.
* app.properties: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/app.properties) che contiene la traduzione completa del boilerplate.

Come si può vedere è il classico file .ini `proprietà = testo` che viene elaborato da Javascript e caricato all'interno del tag contenente nell'attributo `data-l10n-id`.

## Riassunto
Abbiamo visto molte funzionalità di Firefox OS e delle Open Web Apps tramite un semplice ma completo boilerplate.
Una citazione da fare è che le WebActivity ed alcune API hanno bisogno di essere dichiarate nel file manifest per poter essere utilizzate. 
Abbiamo visto anche la questione multilingua che è molto importante e di come sia semplice integrare questa soluzione nella propria app.

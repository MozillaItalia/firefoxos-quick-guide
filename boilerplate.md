## Firefox OS Boilerplate App

Il [boilerplate][1] di cui abbiamo letto in precedenza è un'applicazione dimostrativa con molti esempi basilari. Contiene un esempio per la maggior parte delle Web Activity, la questione multilingua, installazione dell'applicazione, API HTML5 e l'interfaccia grafica di Gaia realizzata con *Gaia Building Blocks*.  
La parte interessante è che si trova su Github, quindi c'è anche una demo sempre aggiornata che puoi trovare [qui][2].

Puoi provare il boilerplate nel tuo browser preferito ma se usi Chrome vedrai che nella console apparirà "Open Web Apps not supported" che vuol dire che non supporta questo standard proposto da Mozilla.

Lo standard "Open Web App" consiste in un accesso hardware, installazione locale, storage offline, marketplace, API per i pagamenti e le ricevute, [Persona][3] per i login e il famoso manifest. Questo insieme di caratteristiche ed il manifesto di Mozilla formano le [Open Web Apps][4]!  
Noi sviluppatori web speriamo che le Open Web Apps vengano supportate da altri browser e sistemi operativi in modo da semplificare il lavoro per noi e per una migliore esperienza utente.  
Dopo questo messaggio pubblicitario riprendiamo il discorso!  
I prodotti di Mozilla che utilizzano Gecko supportano le Open Web Apps e in Firefox OS vediamo l'apice delle loro potenzialità. Firefox sia per Android che desktop le supporta quindi collegandosi al [marketplace][5] si possono installare le applicazioni pensate per queste interfacce (se specificate nel marketplace).  

Il boilerplate è un esempio per le Open Web Apps ([template][6]) più il supporto proprietario (al momento!) per Firefox OS.

NB: Le API pensate ed integrate in Firefox OS sono proposte al W3C per una loro standardizzazione (come l'API per la batteria o la vibrazione che sono uno standard). Questo a ricordare che Mozilla lavora per la standardizzazione delle sue idee e non ha interesse a chiudersi. 

Il boilerplate è diviso in tre sezioni ma io ne aggiungo una quarta per gli altri dettagli.

###I dettagli che fanno la differenza

Incominciamo da questi dettagli: 

* AppCache
* OffLine
* Installare l'applicazione
* Multilingua
* Grafica di Gaia

Alcune di queste cose le abbiamo viste o le vedremo in questa fantastica guida. Quindi passiamo agli argomenti che non sono stati ancora visti o non hanno un capitolo dedicato.   

###Offline

Con OffLine mi riferisco a del codice che permette di sapere se il dispositivo è connesso sfruttando l'oggetto `window.navigator.connection` che è descritto sulla [pagina MDN][7] dedicata con i dettagli tecnici e il supporto crossbrowser.

Il codice è presente in due versioni:

* Uno dei tanti pulsanti che usa [l'API diretta][8] fornisce due informazioni: la banda disponibile in MB (0 se è offline, infinity se sconosciuta o solitamente la linea fissa) e se la connessione è a consumo.   
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

### WebActivity

Finalmente parliamo di una delle grandi novità per gli sviluppatori web! Finalmente potremo accedere al sistema in modo più profondo! Ho già detto finalmente?  
Scherzi a parte, in questa sezione possiamo accedere ad alcune delle azioni del sistema come fare una telefonata o scattare una foto. Queste WebActivity purtroppo sono solo per Firefox OS e quindi il testing è solo con simulatore ma c'è chi sta lavorando ad una [polyfill][9] per supportare le web activity anche da browser (dove possibile).  

Non vedremo il codice nel dettaglio delle varie WebActivity, quindi rimando al file [webapp.js][10], ma per completezza ecco quelle rese disponibili da Firefox OS:

* Cercare file
* Scattare una foto
* Registrare un video
* Avviare una telefonata
* Mandare un SMS
* Aggiungere un contatto
* Modificare un contatto
* Condividere un sito
* Condividere una foto sui social network
* Condividere una foto via mail
* Aprire un sito
* Scrivere un'email (con l'applicazione di sistema)
* Salvare un segnalibro
* Aprire un video
* Modificare le impostazioni del telefono

Praticamente vi stiamo dicendo di non pensare a come implementare tutte queste funzionalità dalla vostra app. Se volete ve le diamo noi senza che voi dobbiate lavorarci.

Naturalmente l'importanza di questa idea non è limitata alle precedenti opzioni e basta, potete *registrare* la vostra WebActivity personalizzata nella vostra app per fare più o meno quello che vi pare, dal selezionare foto di gattini a prendere i contatti da una rubrica segreta o rendere disponibile un lettore di codici a barre.

+La lista completa delle WebActivity disponibili su Firefox OS la trovi [quì][15]

### WebAPI

Questa sezione del boilerplate contiene sia esempi esclusivi per Firefox OS ma anche alcuni esempi di tecnologie HTML5 di recente standardizzazione. Tra questi abbiamo le notifiche di sistema, il blocco della rotazione o dello spengimento dello schermo che sono solo per Firefox OS mentre vibrazione, verifica della connessione (ne abbiamo parlato prima), geolocalizzazione, quantità di luce ambientale, prossimità dell'utente allo schermo, accesso alla batteria sono invece API standard e quindi disponibili a chiunque abbia un browser moderno.

### API Privilegiate

Queste API sono particolari e sono disponibili solo per le app privilegiate e sono quasi tutte standard HTML5.

Tra gli esempi disponibili abbiamo: verificare se l'applicazione è in primo piano, accedere alle immagini sul dispositivo, effettuare una richiesta ad un server e prendere i contatti dal telefono. Questi esempi sono uno standard HTML5 mentre selezionare i contatti e fare richieste XHR CrossDomain sono una peculiarità di Firefox OS.

## Multilingua

Nel [Boilerplate][2] appena visto è utilizzata una libreria JavaScript chiamata [webL10n][11]. Questa libreria è presente in Gaia ma si tratta di una versione modificata (questa è la versione presente nel boilerplate).

Grazie a webL10n il sito riconosce in automatico la lingua utilizzata dal dispositivo e carica le traduzioni appropriate.

Al caricamento del file JavaScript della libreria viene caricato il file **locales.ini** che contiene i riferimenti alle varie lingue disponibili dell'applicazione. Dopodiché se c'è la lingua utilizzata dal sistema provvede a sostituire i testi che gli abbiamo indicato alla creazione dell'app, se la lingua non è presente viene lasciata la versione base (dobbiamo indicarla noi).

Diamo un'occhiata al codice prima di vedere come avviene la magia della localizzazione.

`<link rel="resource" type="application/l10n" href="locales/locales.ini" />
<script type="application/javascript" src="js/l10n.js"></script>`

Con questo codice il boilerplate carica i file della lingua... ma come sa dove agire per cambiare il testo?
La libreria si basa sugli attributi `data-l10n-id` che mettiamo agli elementi di cui vogliamo la traduzione che deve contenere il nome di riferimento della stringa da mostrare.

Ecco un esempio per chiarire le idee.

~~~~~
<html>
<head>
  <script type="text/javascript" src="l10n.js"></script>
  <link rel="prefetch" type="application/l10n" href="locales.ini" />
</head>
<body>
  <button data-l10n-id="test" title="click me!">This is a test</button>
</body>
</html>
~~~~~

Il bottone ha una proprietà `data-l10n-id` con attributo *test*, questo vuol dire che se nel file **locales.ini** esiste una riga di testo simile a questa 

~~~~~
[it]
test = Questo è un test
test.title = Cliccami!
~~~~~

Il testo all'interno del bottone verrà sostituito dal testo `Questo è un test` nel caso io chieda la lingua italiana.

### File della lingua

* **locales.ini**: [un esempio][12] che contiene i percorsi dei vari file di lingua con il loro codice di riconoscimento.
* **manifest.properties**: [un esempio][13] che contiene la traduzione del manifest.
* **app.properties**: [un esempio][14] che contiene la traduzione completa del boilerplate.

Come si può vedere è il classico file .ini `proprietà = testo` che viene elaborato da JavaScript e caricato all'interno del tag contenente nell'attributo `data-l10n-id`.

## Riassunto

Abbiamo visto molte funzionalità di Firefox OS e delle Open Web Apps tramite un semplice ma completo boilerplate.
Ricordati che per poter utilizzare le WebActivity o alcune API hai bisogno dei permessi degli utenti e quinidi devi chiedere i permessi relativi compilando il file manifest accuratamente. 
Abbiamo visto anche la questione multilingua che è molto importante e di come sia semplice integrare questa soluzione nel proprio lavoro.

[1]: https://github.com/robnyman/Firefox-OS-Boilerplate-App "Boilerplate repository"
[2]: http://robnyman.github.io/Firefox-OS-Boilerplate-App/ "Boilerplate app"
[3]: https://developer.mozilla.org/it/Persona "Persona"
[4]: https://hacks.mozilla.org/2013/02/getting-started-with-open-web-apps-why-and-how/ "Open Web Apps su Hacks"
[5]: http://marketplace.firefox.com/ "Firefox Marketplace"
[6]: https://github.com/mozilla/mortar "Template"
[7]: http://mdn.beonex.com/en/DOM/window.navigator.connection.html "Pagina di navigator.connection"
[8]: https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js#L331 "esempio di navigator.connection"
[9]: https://github.com/Mte90/moz-polyfills "WebApi polyfill"
[10]: https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js "WebApi esempio dal Boilerplate"
[11]: https://github.com/fabi1cazenave/webL10n/tree/master "WebL10n repository"
[12]: https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/locales.ini
[13]: https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/manifest.properties
[14]: https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/app.properties
+[15]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Activities

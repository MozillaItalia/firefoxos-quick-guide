## Firefox OS Boilerplate App

Il [boilerplate](https://github.com/robnyman/Firefox-OS-Boilerplate-App) che abbiamo citato poco fà è un'applicazione di esempio completa di tutti gli esempi. È ripetitivo dire esempi ma questo boilerplate contiene un'esempio per la maggior parte delle Web Activity, la questione multilingua, installazione dell'applicazione, api html5 e l'interfaccia grafica di Gaia.  
La parte interessante è che si trova su Github quindi c'è anche una demo sempre aggiornata che puoi trovare [qui](http://robnyman.github.io/Firefox-OS-Boilerplate-App/).  

Puoi provare il boilerplate nel tuo browser preferito ma se usi Chrome vedrai che nella console apparirà "Open Web Apps not supported" che vuol dire che non supporta questo standard proposto da Mozilla. Lo standard consiste in un'accesso hardware, installazione locale, storage offline, marketplace, api per i pagamenti e le ricevute, [Persona](https://developer.mozilla.org/en-US/docs/Mozilla/Persona) per i login ed il famoso manifest. Questo insieme di caratteristiche ed il manifesto di Mozilla sono le [Open Web Apps](https://hacks.mozilla.org/2013/02/getting-started-with-open-web-apps-why-and-how/)!  
Come sviluppatori web speriamo che vengano supportati da altri browser e sistemi operativi in modo da semplificare il lavoro per noi e una migliore esperienza utente.  
Dopo questo messaggio pubblicitario riprendiamo il discorso! 
I prodotti di Mozilla che usano Gecko supportano le Open Web Apps e in Firefox OS vediamo l'apice delle loro potenzialità. Firefox sia per android che desktop le supporta quindi andando al [marketplace](http://marketplace.firefox.com/) si possono installare le applicazioni pensate per queste interfacce (se specificate nel marketplace).  

Il boilerplate è un esempio per le Open Web Apps ([template](https://github.com/mozilla/mortar)) più il supporto proprietario (al momento!) per Firefox OS.  
Le api integrate in Firefox OS vengono tutte messe sotto analisi del W3C per una loro standardizzazione (come l'api per la batteria o la vibrazione). Questo a ricordare che Mozilla lavora per la standardizzazione delle sue idee non ha interesse a chiudersi. 

Il boilerplate è diviso in tre sezioni ma io ne aggiungo una quarta per gli altri dettagli.

###I dettagli che fanno la differenza

Incominciamo da questi dettagli: 

* AppCache
* Multilingua
* OffLine
* Installazione applicazione
* Grafica di Gaia

Alcune di queste cose le abbiamo viste o le vedremo in questa fantastica guida. Quindi passiamo agli argomenti che non sono stati ancora visti o non hanno un capitolo dedicato. 
Con OffLine mi riferisco a del codice che permette di sapere se il dispositivo è connesso sfruttando l'oggetto `window.navigator.connection` che ha una [pagina MDN](http://mdn.beonex.com/en/DOM/window.navigator.connection.html) con i dettagli tecnici e il supporto crossbrowser. 
Il codice c'è in due versioni in uno dei tanti pulsanti che usa [l'API diretta](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js#L312) che fornisce due informazioni la banda disponibile in MB (0  se è offline ed infinity se la banda è sconosciuta) e se la connessione è pay for use. 
L'altra soluzione è usare AppCache per sapere se si sta usando l'applicazione in modalità offline (https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/offline.js#L13) che viene utilizzato per mostrare il pallino verde se non è online.  

Installazione applicazione che vuol dire bèh l'abbiamo già detto, le Open Web Apps si installano e vediamo come funziona il codice di installazione e di verifica installazione. Prima di tutto verifichiamo se il sistema le supporta (con `navigator.mozApps`) dopo di che via con il [codice](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/base.js#L2). 
Come si può vedere il codice è molto semplice, semplicemente si dà l'indirizzo del file manifest e si verifica se è stato installato. Per installare il boilerplate basta cliccaresul simbolo più in alto a destra. Meglio semplice no?

###WebActivity
Finalmente parliamo di una delle grandi novità per gli sviluppatori web! Finalmente potremo accedere al sistema in modo più profondo! Ho già detto finalmente? 
Scherzi a parte in questa sezione possiamo accedere ad una parte delle azioni del sistema dal fare una telefonata ad scattare una foto. Queste WebActivity purtroppo sono solo per Firefox OS e quindi il testing è solo con simulatore ma c'è chi stà lavorando ad una [polyfill](https://github.com/Mte90/moz-polyfills) per supportare le web activity anche da browser. 
Puoi provare il boilerplate con la polyfill a [questo sito](http://mte90.github.io/moz-polyfills/). Siccome è in sviluppo al momento funziona solo la WebActivity Pick mentre è in sviluppo Record.  
Non vedremo il codice nel dettaglio delle varie WebActivity quindi rimando al [file](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/js/webapp.js) ma elenchiamo le varie WebActivity: 

* Cercare file
* Scattare una foto
* Avviare una telefonata
* Mandare un SMS
* Aggiungere un contatto
* Condividere un sito
* Condividere una foto con un'applicazione
* Aprire un sito
* Scrivere un'email (con al'applicazione di sistema)
* Salvare un segnalibro
* Aprire un video

###WebAPI
Questa sezione contiene sia codice (lo stesso file di prima) solo per Firefox OS ma anche un'pò di HTML5 di fresca standardizzazione. Abbiamo le notifiche, ruotazione e accensione dello schermo che sono solo per Firefox OS mentre vibrazione, verifica connessione (ne abbiamo parlato prima), geolocazione, luce ambientale, prossimità, batteria sono APi standard.

###API Privilegiate
Queste API sono particolari e sono disponibili solo per le app privilegiate e sono quasi tutte standard HTML5. 
C'è il codice per verificare se l'applicazione è in uso quindi se la scheda è aperta ed accedere alle immagini sono standard HTML mentre selezionare i contatti e fare richieste XHR CrossDomain sono una peculiarità di Firefox OS.

##Multilingua

Nel [Boilerplate](https://github.com/robnyman/Firefox-OS-Boilerplate-App) appena visto è utilizzata una libreria javascript di nome [webL10n](https://github.com/fabi1cazenave/webL10n/tree/master). Questa libreria è utilizzata anche in Gaia solo che non contiene la parte crossbrowser ed è molto semplice da usare.  
Il sistema riconosce in automatico la lingua utilizzata e carica la lingua in uso dell'applicazione. Al caricamento del file JavaScript della libreria viene caricato un file ini che contiene i riferimenti alle varie lingue disponibili dell'applicazione. Dopodichè la libreria carica il file della lingua utilizzata dal browser o del sistema. Diamo un'occhiata al codice prima di vedere come succede la magia della localizzazione.  

`<link rel="resource" type="application/l10n" href="locales/locales.ini" />
<script type="application/javascript" src="js/l10n.js"></script>`

Con questo codice il boilerplate carica i file della lingua ma come sà dove cambiarlo? Tramite degli attributi ai tag di cui vogliamo la traduzione di questo tipo `data-l10n-id` che deve contenere il nome di riferimento della stringa da mostrare.

###File della lingua

* locales.ini: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/locales.ini) che contiene i percorsi dei vari file di lingua con il loro codice di riconoscimento.
* manifest.properties: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/manifest.properties) che contiene la traduzione del manifest.
* app.properties: [un esempio](https://github.com/robnyman/Firefox-OS-Boilerplate-App/blob/gh-pages/locales/en-US/app.properties) che contiene la traduzione completa del boilerplate.

Come si può vedere è il classico file ini `proprietà = testo` che viene elaborato da Javascript e caricato all'interno del tag contenente nell'attributo `data-l10n-id`.

## Riassunto
Queste WebActivity ed API hanno bisogno di essere dichiarate nel file manifest per poter essere usate. 
Per il resto consiglio di provare questo boilerplate ed estrapolare il necessario per la tua applicazione. 
Inoltre è interessante per provare quante cose si possono fare in Firefox OS. 
Non dimentichiamo che è in continuo sviluppo e traduzione quindi ogni tanto ci sono aggiornamenti per aggiungere nuove funzionalità.  
Il multilingua è un'aspetto importante in modo così globalizzato e non và tenuto sottogamba quindi lavoriamo in multi lingua anche per le nostre applicaizoni.

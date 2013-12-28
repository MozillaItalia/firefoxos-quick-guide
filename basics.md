# Concetti Base {#concepts}

Prima di sporcarci le mani per la creazione della nostra prima applicazione, vediamo di scoprire alcuni concetti base per lo sviluppo per Firefox OS. Abbiamo visto l'[introduzione](#introduction), su come le pagine web, applicazioni in Firefox OS sono basate su HTML5. Tuttavia, non abbiamo spiegato cosa rende le applicazioni per Firefox OS differenti dalle pagine web classiche. 

Se usiamo la nostra conoscenza riguardo le altre piattaforme mobile possiamo vedere che le applicazioni native hanno:

* Un nome ed un'icona con cui l'utente lancia l'applicazione.
* Accesso ai servizi di sistema e funzionalità hardware. 

Guardando il tutto, un'applicazione per Firefox OS è una pagina web con una icona, un name e solitamente funzionano offline (a seconda dell'implementazione dell'applicazione). Tutti i dati su un'applicazione come il nome, icona e molto altro è definito nel *file application manifest* che è l'argomento della prossima sezione.

## Application Manifest

Il [manifest](https://developer.mozilla.org/docs/Apps/Manifest) è un file [JSON](http://json.org) che descrive l'applicazione. Solitamente questo file è chiamato **manifest.webapp** e và posizionato accanto al classico file HTML **index.html**.  

<<[Manifest d'esempio](code/sample_manifest.webapp)

Sopra possiamo vedere il manifest di un'applicazione chiamata memos[^promemoria]. Tra le altre cose descrive chi ha creato l'applicazione, quali icone usare, qual'è il nome dell'applicazione, che file è usato per lanciare l'applicazione (in questo caso *index.html*), che permessi d'accesso hardware richiede l'applicazione, ecc. Questo file è usato in Firefox OS per aggiungere l'applicazione alla schermata principale e per mostrare nel Marketplace Firefox le informazioni dell'applicazione.

[^promemoria]: Questa applicazione di esempio per Firefox OS si [può trovare sul Marketplace Firefox](https://marketplace.firefox.com/app/memos) mentre il [codice sorgente è su GitHub](https://github.com/soapdog/memos-for-firefoxos).

![L'applicazione Memos vista sul Marketplace Firefox](images/originals/memos-marketplace.png)

Le informazioni del manifest sono usate dal sistema per aggiungere le applicaizoni alla schermata principale, come possiamo vedere nello screenshot.

![Memos nel simulatore](images/originals/memos-simulator.png)

Riunendo il codice HTML, CSS, JavaScript ed un file manifest si possiede già un'applicazione pronta per funzionare su Firefox OS. Cambiamo argomento passando ai concetti base su quali tipi di applicazioni possono esserci.

## Tipi di Applicazioni

Firefox OS attualmente ci sono due tipi di applicazioni: hosted e packaged - forse in futuro saranno disponibili altri tipi di applicazioni (e.g., tastiere personalizzate e la possibilità di creare altri servizi di sistema).

* **Applicazioni Hosted:** Sono ospitate su un web server come i classici siti web. Questo significa che quando l'utente lancia un'applicazione hosted, il suo contenuto è caricato dal server remoto (o dalla cache, se disponibile).
* **Applicazioni Packaged:** Sono distribuiti come file zip e copiati sul dispositivo quando installato. Quando l'utente lanci un'applicazione packaged, i suoi contenuti sono caricati dallo zip invece di un server remoto.  

Ci sono pro e contro in entrambi i tipi. Da un lato le applicazioni hosted sono più facili da aggiornare, basta aggiornare i file sul server web. Comunque la parte più difficile è farlo funzionare offline, perchè richiede l'utilizzo del tanto discusso [**appcache**](https://developer.mozilla.org/pt-BR/docs/HTML/Using_the_application_cache). Le Hosted app sono limitate in quanto le WebAPI che possono usare sono minori rispetto alle packaged.   

Dall'altro lato le applicazioni packaged hanno tutto il loro contenuto memorizzato sul dispositivo - significa che sono sempre disponibili quando l'utente è offline (quindi non è necessario usare AppCache). Hanno anche la possibilità di accedere a WebAPI dedicate alla sicurezza che non sono disponibili per le applicazioni hosted. Il loro aggiornamento può può essere doloroso, perchè hai bisogno di caricare qualsiasi nuova versione nel Marketplace Firefox - significa far passare l'applicazione al processo di revisione, che può richiedere un certo tempo.   

Quando scegli quale tipo di applicazione realizzare valuta: se hai bisogno di WebAPI avanzate, dovrai utilizzare un app packaged. Se la tua applicazione funziona senza accedere a servizi di sistema avanzati o funzionalità del dispositivo oltre a quelle già disponibili in un browser web, quindi scegli un'app hosted. Se non hai un posto dove ospitare l'applicazione c'è l'opzione packaged.

Sopra ho detto che AppCache può essere problematico (necessario per le applicazioni hosted). Non preoccuparti ci sono dei tool che semplificano la generazione di file AppCache ed una distribuzione semplificata [^js-tools].

In questo libro vedremo come realizzare applicazioni packaged, così potremo esplorare tutto quello che potremo fare con le WebAPI. Inoltre la maggior parte di ciò che vedremo sui file manifest si applica anche alle app hosted. Se vuoi saperne di più sulla distribuzione delle app hosted, guarda [le applicazioni hosted nel centro di sviluppo](https://marketplace.firefox.com/developers/docs/hosted).

[^js-tools]: Ci sono omolti sutrmenti utili, guarda [Grunt](gruntjs.com), [Volo](http://volojs.org/), [Yeoman](http://yeoman.io/), [Bower](http://bower.io/). Questi strumenti si sovrappongono facilmente, è una questione di preferenza. (Mi piace Volo rispetto a Grunt perchè i Volofiles sono più semplici da leggere).

Ora che abbiamo trattato i due tipi di applicazioni supportate da Firefox OS, diamo un'occhiata ai diversi livello di accesso al sistema che può avere.

## Livelli di accesso per la sicurezza

Ci sono tre livelli di sicurezza su Firefox OS - ad ogni livello si ha più accesso alle API rispetto a quello precedente.

* **Plain (a.k.a. web):** Questo è il livello di partenza per tutte le applicazioni. Questo livello si applica alle hosted app e alle app packaged che non dichiarano una proprietà `type` nel loro file manifest. Queste applicazioni hanno un'accesso comune alle API presenti nel browser - ma non hanno un'accesso a qualsiasi delle WebAPI Mozilla.
* **Privilegiate:** Questo tipo di applicazioni ha accesso a tutte le API disponibili nel browser Firefox, oltre a quelli aggiuntivi, come i contatti, e gli allarmi di sistema. Solo **le app packaged possono essere privilegiate** ed il pacchetto deve essere firmato dal marketplace Firefox OS.
* **Certificato:** Per motivi di sicurezza, questo livello è disponibile solo a Mozilla ed i suoi partner (e.g., prodotturi telefonici, telecomunicazioni, ecc.). Un esempio di applicazioni certificate hanno un'accesso a tutte le API, come la telefonia e altro ancora. Un esempio di applicazione certificata in Firefox OS è il dealer. 

Durante lo sviluppo è possibile accedere alle API privilegiate senza richiedere premessi speciali da Mozilla. Quando distribuirai le app privilegiate dovrai andare al Marketplace Firefox. Il codice viene controllato in un rigoroso processo di approvazione e se è tutto OK sarà firmata digitalmente - questo infermerà gli utenti di Firefox OS che a questa applicazione è consentito accedere alle API sensibili.

Sulla [pagina delle WebAPIs sul Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/WebAPI) possiamo vedere le API, su cosa sono supportate e quale livello è richiesto.

![Livello di accesso alle API](images/originals/webapi-access.png)

Come si può vedere dall'immagine qui sopra, qualsiasi applicazioni può accedere alle API *IndexedDB API e FileHandle API* solamente le app privilegiate possono accedere ai *Contacts API e Device Storage API*.

## WebAPI di Mozilla

Firefox OS fornisce le APIs che permettono di costruire applicazioni che hanno le funzionalità delle applicazioni native delle altre piattaforme. L'accesso  hardware e dei servizi avviene attraverso le WebAPI. Per saperne di più sulle API disponibili nelle varie versioni di Firefox OS controlla [la pagina WebAPI nel   Wiki Mozilla](https://wiki.mozilla.org/WebAPI).

Consente di studiare alcuni esempi di codice per vedere come sono semplici le API. non prendere questi esempi come una documentazione completa sulle WebAPI, sono un piccolo esempio di come si possa accedere al dispositivo usando JavaScript.

### Eesempio #1: Fare chiamate

Immaginate di avere un'applicazione che ha bisogno di usare il dialer con un numero di telefoni già pronto. Puoi usare semplicemente il seguente codice:

<<[Invia un numero di telefono al dialer](code/webapi_samples/dial.js)

Questo codice effettua una richiesta all'applicazione dealer per chiamare un numero definito. In eraltà non partirà la chiamata, l'utente avrà bisogno di tappare il tasto della chiamate per farla. Richiede un'azione esplicita dell'utente prima di eseguire quest'azione: si tratta di un buon modello di sicurezza perchè richiede una interazione utente con il suo consenso prima di permettere che accada qualcosa.
Altre APIs possono effetuare chiamate senza una interazione utente ma richiedono un livello d'accesso elevato. Applicazioni certificate possono effettuare chiamate chiamate senza interazione con l'utente. Le API usate nel codice sopra, chiamate "Web Activities", sono disponibili per tutte le applicazioni.

Dai un'occhiata al blog [per maggiori informazioni sulle Web Activites](https://hacks.mozilla.org/2013/01/introducing-web-activities/). 

### Esempio #2: Salvare un contatto

Immagina di avere una rete intranet aziendale ce vuoi che sia possibile transferire un contatto dalla rete intranet ad una rubrica telefonica. Puoi fare questa cosa con le Conacts API.

<<[Salavare un contatto](code/webapi_samples/contact.js)

Queste API creano un oggetto con i dati del contatto e lo salvano nella rubrica telefonica senza richiedere una interazione utente. Poichè l'accesso ai contatti comporta implicazioni riguardo la privacy, queste API sno disponibili per le *app privileged*. Questo modello permette di creare un oggetto con successo ed una callback per gli errori usata in molte WebAPI.

Per usare queste API, leggi [la pagina dedicata alle *Contacts API* sul wiki di Mozilla](https://wiki.mozilla.org/WebAPI/ContactsAPI).

### Esempio #3: Prendere una immagine dalla fotocamera

Immagine di creare un'applicazione che applica dei filtri carini alle foto. Per fare questo hai biosgno di piazzare un pulsante nella tua applicazione e permettere all'utente di scattare una foto o di sceglierla dalla galleria.

<<[Scegliere una foto](code/webapi_samples/pick.js)

Qui puoi trovare degli esempi di [WebActivity](https://hacks.mozilla.org/2013/01/introducing-web-activities/). Queste activities sono disponibili per tutte le applicazioni. In questo esempio specifico stiamo usando la *pick* activity passando il *MIME Types* dei file richiesti. Quando questo codice è eseguito, il sistema mostra una schermata all'utente chiedendo se vuole fornire l'immagine da (camera, galleria, sfondi). Se l'utente seleziona una immagine, la callback di successo viene invocata. Se l'utente annulla l'operazione, la callback di errore è eseguita. Nell'immagine sottostante, possiamo vedere la finestra di richiesta sul dispositivo:

![Esempio di *pick activity*](images/originals/pick_image.png)

## Riassunto

In questo capitolo abbiamo visto che rispetto alle pagine web classiche, entrambe i tipi di applicazione per Firefox OS (hosted e packaged) si basano su un file manifest. Abbiamo visto anche che dal punto di vista della sicurezza le applicazioni packaged possono essere "privilegiate" o "certificate". Solo le app privilegiate e certificate possono accedere alle WebAPI di Mozilla. Le WebAPI non sono disponibili per le applicazioni hosted o alle pagine web classiche.

Adesso è giunta l'ora di sporcarsi le mani e creare un'applicazione.

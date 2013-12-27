# Introduzione {#introduction}

## Firefox OS

![Firefox OS](images/originals/firefox_os_simulator.png)

[Firefox OS](http://www.mozilla.org/firefox/os/) è una nuova piattaforma mobile sviluppata da [Mozilla](http://mozilla.org) e i suoi partner. Dispositivi con Firefox OS sono già disponibili in molti paesi e arriveranno anche in molti altri posti entro la fine di quest'anno.

Mirato per lo sviluppo di nuovi mercati, Firefox OS ha la missione di portare il prossimo bilione di persone online. Per raggiungere questo obiettivo, i dispositivi con Firefox OS sono costruiti per fornire un *ottimo primo smartphone* con prezzi competitivi. I dispositivi con Firefox OS non devono essere confrontati con smartphone di fascia alta come Apple iPhone 5S e Samsung Galaxy S4; sono realizzati per essere un'alternativa ai telefoni avanzati così le persone che usano questi dispositivi possono fare il passaggio a Firefox OS ad un costo accessibile e ricevere una *esperienza smartphone completa*.

Nei mercati in sviluppo come il Brasile o la Colombia, smartphone con prestazioni decenti sono solitamente troppo costosi per il consumatore medio.
Le persone possono comprare telefoni a basso costo, le piattaforme di questi telefoni sono pensate per dispositivi di fascia alta - quindi hardware del telefono tende ad avere problemi di performance, che comporta una terribile esperienza utente. Firefox OS è progettato specificamente per funzionare su hardware limitato fornendo una'esperienza utente decente. 

Un'altro fattore per la sua unicità è l'apertura di Firefox OS. Considera che i sistemi operativi mobile attuali sono dei silos proprietari, dove ogni produttore ha il privilegio di obbligare gli sviluppatori ed utenti ai loro desideri a prescindere della loro volontà (ricordi quando la Apple ha vietato dei linguaggi diversi da Objective-C nel suo app Store). In questi ecosistemi proprietari puoi distribuire le applicazioni solo su canali autorizzati - e il venditore ottiene una commessa sugli acquisti effettuati dal dispositivo.

Oltre a bloccare gli sviluppatori su canali di sviluppo proprietari, questi sistemi bloccano gli sviluppatori sui loro software development kit (SDK). Se vuoi realizzare una app nativa sia per iOS e Android usando i sistemi ufficiali sarà necessario programmare un'app in Objective-C ed un'altra in Java rispettivamente. Questo significa che uno sviluppatore saggio riutilizzerà poco tra i vari progetti (magari riutilizzare anche del materiale multimediale). Questo significa che uno sviluppatore conosca due linguaggi e realizzi lo stesso software due volte. 

Firefox OS si differenzia usando "HTML5" come piattaforma di sviluppo. HTML5 è un termine di marketing usato per indicare la la continua evoluzione degli standard web noto come HTML, CSS e JavaScript. Questi standard royalty free sono supportate dai principali browser web, questo permette di rendere le web app possibili. Sfruttando le tecnologie che includono HTML5, milioni di sviluppatori possono programmare per FireFox OS. Le applicazioni create per FireFox OS sono facili da portare  ad'altre piattaforme usando dei wrapper come [Phonegap](http://phonegap.com).

## La piattaforma che HTML5 merita

Il web è ovunque. Il suo computer, telefoni cellulari, smart TV, anche nelle tue console per i videogiochi. Il linguaggio di programmazione del web, JavaScript, è uno dei linguaggi più diffusi al mondo. Come già accennato, quando le persone parlano di HTML5 di solito si riferiscono alla combinazione di tre technologie come HTML, CSS e JavaScript. I recenti progressi in HTML hanno introdotto moltissime nuove caratteristiche - nuovi campi per i form , Web socket, markup più semantico - rispetto XHTML 1.0 e HTML 4.01. I progressi in CSS hanno introdotto moltissime nuove caratteristiche, come Flexbox e animazioni CSS, che rendono più semplice creare layout responsive. I recenti progressi in JavaScript hanno portato miglioramenti significativi alle performance e nuove funzionalità, rimenanendo facile da usare sia per i principianti che per gli sviluppatori esperti.

Firefox OS in parole povere, una estensione del web mobile. Mozilla ha aperto la sua piattaforma a milioni di sviluppatori web rendendo HTML5 l'elemento principale. Anche se ci sono altri produttori di browser che supportano HTML5 nei loro telefoni, Firefox OS va oltre, offrendo una famiglia di API per accedere all'hardware ed al sistema usando JavaScript. Queste API sono conosciute come WebAPI.

## Accesso Hardware Usando le WebAPI

Alcune piattaforme precedenti hanno provato a creare sistemi operativi che utilizzavano tecnologie web per la creazione di applicazioni. Per esempio, quando venne introdotto l'iPhone al mondo, l'unico modo per creare applicazioni era usare tecnologie web. Queste applicazioni web erano limitate dal fatto che non avevano accesso all'hardware o al dispositivo - quindi potrebbero esserci solo poche applicazioni. Quando Apple ha permesso di sviluppare in Objective-C, anche di accedere alle funzionalità del dispositivo, creando una ventata di innovazione. Purtroppo, le web app non hanno ottenuto un accesso alle caratteristiche del dispositivo, e sono state abbandonate a "cittadini di seconda classe" - questo le ha rese meno interessanti sia agli svluppatori che agli utenti, rendendole non competitive con le app mnative di quei sistemi.

Quando diciamo funzionalità del dispositivo ci riferiamo all'accesso hardware, di funzionalità del sistema e di servizi: Parliamo di cose come aggiorna la rubrica, inviare SMS, accede alla fotocamera ed alla galleria. Su Firefox OS, le [WebAPI](https://wiki.mozilla.org/WebAPI)permettono di accedere a molte di queste funzionalità. 

Un'altra piattaformi precedente, WebOS, offriva accesso all'hardware via JavaScript ma non ha mai standardizzato le sue API. Mozilla lavora con il W3C e le altre parti interessate per rendere le WebAPI uno standard aperto in modo che altri browser le adottino. Poichè queste API sono integrate in altri browser le applicazioni richiederanno sempre meno modifiche per le varie piattaforme.

È importante ricordare che le  WebAPI non sono esclusive per i dispositivi con Firefox OS. Mozilla le sta implementando in altre piattaforme in cui Firefox gira, sia su desktop che Android. In queste modo, potrai usare le *open web app* in Firefox OS, Firefox per il desktop e Firefox prr Android.

## Freedom to Develop and Distribute

Come qualunque cosa fà Mozilla, Firefox OS è costruito per l'apertura e la libertà. Tutti gli sviluppatori possono seguire il repo di [Mozilla B2G](https://github.com/mozilla-b2g/B2G) su GitHub. Con Firefox OS hai la libertà di seguire e contribuire allo sviluppo del sistema ed hai anche la libertà di distribuire le tue applicazioni nei canali del [Marketplace Firefox](https://marketplace.firefox.com/).  La cosa più spettacolare è che tutte le applicazioni di sistema sono scritte in HTML5, in modo che chiunque possa vederle e studiare come funzionano. 

L'idea principale è che Mozilla non ti blocca per niente. Se vuoi prendere il codice sorgente del sistema e cambiarlo per le tue necessità bèh puoi farlo. Se devi realizzare un'applicazione per uso interno allla tua azienda, se vuoi distruibire le tue creazioni esclusivamente sul tuo sito, sei libero di farlo. Solitamente nelle altre piattaforme sei bloccato allo store ufficiale che è l'unico canale di distribuzione delle applicazioni. Firefox OS ha un market ufficiale chiamato  Firefox Marketplace che ha un processo di approvazione, ma sei libero di distribuire le tue app fuori dal negozio. Come nel web è possibile ospitare il sito web ovunque tu voglia, anche in Firefox OS puoi fare lo stesso con le tue applicazioni. 

Purtroppo si presenta come un piccolo avvertimento: alcune WebAPI sono troppo particolari per la sicurezza per permettere a chiuqnue di usarli. Per distribuire le applicazioni che utilizzano alcune delle API "privilegiate", è necessaria una certificazione e revisione dell'applicazione con firma da Mozilla.

## Riassunto

HTML5 è pensato per rimanere e migliorare nel tempo. Firefox OS è il nuovo sistema operativo mobile aperto di Mozilla completamente basato su tecnologie web. Questo sistema è costruito per l'apertura ed offre una implementazione robusta di HTML5 che và oltre le altre piattaforme offrendo delle WebAPI che sono una raccolta di API per accedere *al sistema operativo ed all'hardware usando JavaScript*. Queste nuove API sono state standardizzate con il World Wide Web Consortium (W3C) e speriamo adottati da altri browser in futuro.

Nel prossimo capitolo vedremo come preparare un'ambiente di sviluppo per Firefox OS. 

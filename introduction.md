# Introduzione {#introduction}

## Firefox OS

![Firefox OS](images/originals/firefox_os_simulator.png)

[Firefox OS](http://www.mozilla.org/firefox/os/) è una nuova piattaforma *mobile* sviluppata da [Mozilla](http://mozilla.org) e dai suoi partner. Dispositivi con Firefox OS sono già disponibili in molti paesi e molti altri ne sono previsti entro la fine dell'anno.

Finalizzata per i mercati emergenti, la missione di Firefox OS è quella di portare il prossimo miliardo di persone online. Per raggiungere questo obiettivo, i dispositivi con Firefox OS sono costruiti per fornire un *ottimo primo smartphone* a prezzi competitivi. I dispositivi con Firefox OS non devono essere confrontati con smartphone di fascia alta come Apple iPhone 5S e Samsung Galaxy S4; sono realizzati per essere un'alternativa ai telefoni avanzati in modo che gli utenti di questi dispositivi possano compiere il passaggio a Firefox OS con un costo accessibile e ricevere una *esperienza smartphone completa*.

Nei mercati in via di sviluppo come il Brasile o la Colombia, smartphone con prestazioni decenti sono solitamente troppo costosi per il consumatore medio. Le persone sono in grado di acquistare telefoni a basso costo, le piattaforme di questi telefoni però sono progettate per dispositivi di fascia alta - questo porta l'hardware del telefono ad avere problemi nelle prestazioni, tutto ciò ha come risultato una pessima esperienza mobile per l'utente finale. Firefox OS è progettato specificatamente per funzionare su hardware limitato fornendo una discreta esperienza utente. 

Un altro fattore distintivo di Firefox OS è l'essere un ecosistema aperto. Si tenga presente che i sistemi operativi *mobile* attuali sono paragonabili a dei silos proprietari, dove ogni produttore ha il privilegio di obbligare gli sviluppatori e utenti a seguire i propri desideri a prescindere dalla loro volontà (si ricordi a proposito quando la Apple ha vietato l'uso dei linguaggi diversi da Objective-C nel suo app Store). In questi ecosistemi proprietari è possibile distribuire le applicazioni solo su canali autorizzati - e il venditore ottiene una commessa sugli acquisti effettuati dal dispositivo.

Oltre a costringere gli sviluppatori su canali di distribuzione proprietari, questi sistemi li obbligano a utilizzare i loro *Software Development Kit* (SDK). Per realizzare un'app nativa sia per iOS che Android utilizzando i sistemi ufficiali, sarà necessario programmare rispettivamente un'app in Objective-C ed un'altra in Java rispettivamente. Questo significa, dal punto di vista di uno sviluppatore, riutilizzare poco codice tra i vari progetti (magari pure le risorse multimediali non saranno riutilizzabili). In altre parole uno sviluppatore dovrebbe imparare due linguaggi e realizzare lo stesso software due volte. 

Firefox OS si differenzia grazie all'utilizzo di "HTML5" come piattaforma di sviluppo. HTML5 è un termine di marketing utilizzato per indicare le tecnologie web, in continua evoluzione, ovvero: HTML, JavaScript e CSS. Questi standard privi di brevetti sono supportati dai principali browser web, rendendo in questo modo possibili le app web. Sfruttando le tecnologie che includono HTML5, milioni di sviluppatori possono programmare per Firefox OS. Le applicazioni create per Firefox OS sono facili da migrare su altre piattaforme utilizzando dei wrapper come [Phonegap](http://phonegap.com).

## La piattaforma che HTML5 merita

Il Web è ovunque. Nel computer, nei telefoni cellulari, nelle smart TV e persino nelle *console* per videogiochi. Il linguaggio di programmazione del Web, JavaScript, è uno dei linguaggi più diffusi al mondo. Come già accennato, quando le persone parlano di HTML5 di solito si riferiscono alla combinazione di tre tecnologie, ovvero: HTML, CSS e JavaScript. I recenti progressi in HTML hanno introdotto moltissime nuove caratteristiche rispetto a XHTML 1.0 e HTML 4.01 - nuovi campi per i form , Web socket, markup più semantico. I progressi in CSS hanno introdotto moltissime nuove caratteristiche, come Flexbox e animazioni CSS, che rendono più semplice creare layout *responsive*. I recenti progressi in JavaScript hanno portato miglioramenti significativi alle prestazioni e nuove funzionalità, rimanendo facili da utilizzare sia per i principianti che per gli sviluppatori esperti.

Firefox OS è, in parole povere, un'estensione del Web mobile. Mozilla ha aperto la sua piattaforma a milioni di sviluppatori web rendendo HTML5 l'elemento principale. Anche se ci sono altri produttori di browser che supportano HTML5 nei loro telefoni, Firefox OS va oltre, offrendo una famiglia di API per accedere all'hardware e al sistema utilizzando JavaScript. Queste API sono conosciute come WebAPI.

## Accesso Hardware tramite le WebAPI

Alcune piattaforme precedenti hanno provato a creare sistemi operativi che utilizzavano tecnologie web per la creazione di applicazioni. Per esempio, quando venne presentato l'iPhone, l'unico modo per creare applicazioni era usare tecnologie web. Queste applicazioni web erano limitate dal fatto che non avevano accesso all'hardware o al dispositivo - quindi potevano esserci solo poche applicazioni. Quando Apple ha permesso di sviluppare in Objective-C, conseguentemente di accedere alle funzionalità del dispositivo, ha portato una ventata di innovazione. Purtroppo, le web app non hanno ottenuto accesso alle caratteristiche del dispositivo e sono state abbandonate come "cittadini di seconda classe" - questo le ha rese meno interessanti sia per gli sviluppatori che per gli utenti, in quanto non competitive in confronto alle app native di quei sistemi.

Quando scriviamo "funzionalità del dispositivo" ci riferiamo all'accesso hardware, di funzionalità del sistema e di servizi: parliamo di caratteristiche come aggiornamento della rubrica, invio di SMS, accesso alla fotocamera ed alla galleria. Su Firefox OS, le [WebAPI](https://wiki.mozilla.org/WebAPI) permettono di accedere a molte di queste funzionalità. 

Un'altra piattaforma precedente, WebOS, offriva accesso all'hardware via JavaScript ma non ha mai standardizzato le sue API. Mozilla lavora con il W3C e le altre parti interessate per rendere le WebAPI uno standard aperto in modo che altri browser le adottino. Poiché queste API sono integrate in altri browser, le applicazioni richiederanno sempre meno modifiche per le varie piattaforme.

È importante ricordare che le WebAPI non sono un'esclusiva dei dispositivi Firefox OS. Mozilla le sta implementando in altre piattaforme con cui Firefox è compatibile, sia desktop che Android. In questo modo, sarà possibile usare le *open web app* in Firefox OS, Firefox desktop e Firefox per Android.

## Libertà di sviluppare e di distribuire

Come qualunque cosa *made in Mozilla*, Firefox OS è costruito per l'apertura e la libertà. Tutti gli sviluppatori possono seguire il repo di [Mozilla 
B2G](https://github.com/mozilla-b2g/B2G) su GitHub. Con Firefox OS si è liberi di seguire e contribuire allo sviluppo del sistema e anche di pubblicare le proprie applicazioni nei canali di [Firefox Marketplace](https://marketplace.firefox.com/). La cosa più spettacolare è che tutte le applicazioni di sistema sono scritte in HTML5, permettendo a chiunque di vederle e studiare come funzionano. 

L'idea alla base di tutto è che Mozilla non mette alcun limite. Se si vuole prendere il codice sorgente del sistema e cambiarlo per le proprie necessità, beh, si può fare. Se si deve realizzare un'applicazione per uso interno alla propria azienda, se si vogliono distribuire le proprie creazioni esclusivamente sul proprio sito, ciò è possibile. Solitamente nelle altre piattaforme si è bloccati dallo store ufficiale, che è l'unico canale di distribuzione per le applicazioni. Firefox OS ha un market ufficiale chiamato Firefox Marketplace che ha un processo di approvazione, ma si è liberi di distribuire le proprie app fuori dal negozio. Analogamente a quanto accade sul Web dove è possibile scegliere qualunque host per il proprio sito, con Firefox OS è possibile distribuire la propria app utilizzando qualunque host.

Purtroppo esiste una piccola controindicazione: per ragioni di sicurezza, l'utilizzo di alcune WebAPI sensibili non può essere consentito a chiunque. Per distribuire le app che utilizzano alcune delle API "con privilegi" si rende necessario sottoporre l'app stessa alla revisione dello staff Mozilla, che dovrà firmare digitalmente l'app prima di poterla pubblicare.

## Riassunto

HTML5 è progettato per rimanere e migliorare nel tempo. Firefox OS è il nuovo sistema operativo *mobile* aperto di Mozilla completamente basato su tecnologie web. Questo sistema è costruito per l'apertura e offre una implementazione robusta di HTML5 che va oltre le altre piattaforme, offrendo delle WebAPI che sono una raccolta di API per accedere *al sistema operativo e all'hardware utilizzando JavaScript*. Queste nuove API sono state standardizzate con il World Wide Web Consortium (W3C) e speriamo adottate da altri browser in futuro.

Nel prossimo capitolo vedremo come preparare un ambiente di sviluppo per Firefox OS. 

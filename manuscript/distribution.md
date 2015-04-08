# Distribuire le app {#distribution}

Ora che la nostra applicazione è pronta, abbiamo bisogno di trovare un modo per renderla disponibile ai nostri utenti. Nel [capitolo introduttivo](#introduction) avevo accennato che, diversamente da Apple, Mozilla non obbliga a utilizzare il proprio canale di distribuzione - lasciando ognuno libero di esprimere la propria creatività. In questo capitolo impareremo come distribuire la nostra app **al di fuori del canale ufficiale del [Firefox Marketplace][1]**.

A mio modesto avviso, non utilizzare il canale ufficiale Mozilla per distribuire un'app è conveniente in questi due casi:

 1. Si sta sviluppando un'app per uso interno aziendale o per una ristretta cerchia di utenti. Pubblicandola su Firefox Marketplace, l'app sarà disponibile a chiunque e si renderà necessario implementare un sistema di autenticazione per consentire l'utilizzo solo agli utenti autorizzati. Ad esempio, nelle prime versioni dell'app *Evernote* era richiesta l'identificazione sui loro server prima di poterla utilizzare.
 2. Si dispone già di un grosso bacino d'utenza che è possibile sfruttare per distribuire l'app. Un esempio potrebbe essere un giornale, come il *Financial Times*, che può limitarsi a rendere disponibile l'app sul proprio sito per raggiungere la quasi totalità dei propri utenti. È bene ricordare che è possibile distribuire l'app sia su Firefox Marketplace, sia su un canale esterno, in questo modo sarà possibile sfruttare il canale di marketing preesistente e utilizzare Firefox Marketplace per raggiungere nuovi utenti.

Il processo di distribuzione delle app **packaged** e delle app **hosted** è simile, anche se utilizzano delle funzioni differenti. Ecco perché tratterò i due casi separatamente. Indipendentemente dal fatto che l'app sia pacchettizzata o ospitata, il procedimento è più o meno lo stesso: sarà necessario rendere disponibile un pulsante o un link nella pagina, denominato **Fai clic per installare l'app**, o utilizzare un particolare URL che quando aperto attiva l'esecuzione della routine di installazione. In entrambi i casi, all'utente finale verrà presentata una finestra di dialogo nativa in cui gli verrà chiesto di confermare l'installazione.

## App hosted

Nel caso la vostra app sia disponibile sul web sotto forma di un sito come facciamo a chiedere all'utente di installare la nostra app?

Ecco che quì arriva in soccorso Firefox ed una WebApi. Grazie a questo strumento possiamo chiedere all'utente di installare il nostro lavoro quando viene visitata la nostra pagina.

<<[Codice per l'installazione di app hosted](code/distribution/hosted_apps_distribution.js)

Nell'esempio riportato qui sopra `manifestURL` riporta l'indirizzo del file **manifest**. All'esecuzione di questo codice, il sistema chiederà all'utente se desidera installare l'app e, a seconda della risposta, richiamerà la callback appropriata: `success` in caso di risposta affermativa e `error` in caso contrario.

Per ulteriori informazioni su questa API consultare [la pagina su MDN sull'installazione delle app][2].

## App pacchettizzate

L'installazione di app pacchettizzate funziona in modo analogo, però in questo caso anziché utilizzare la funzione `mozApps.install()` utilizzeremo `mozApps.installPackage()`, come mostrato nel codice d'esempio riportato qui di seguito.

<<[Codice per l'installazione di app packaged](code/distribution/packaged_apps_distribution.js)

## Riassunto

In questo capitolo sono stati trattati i metodi di distribuzione delle app alternativi al sito Firefox Marketplace grazie all'utilizzo della API di *Installazione e gestione* delle *Open Web Apps*.  
Questa parte l'avevamo accennata nel capitolo [sul boilerplate](boilerplate.md) ma in questo capitolo abbiamo visto le differenze ed alcuni esempi d'uso alternativi.
Esistono molte altre routine disponibili, ad esempio per controllare se l'applicazione è installata (in questo modo sarà possibile nascondere il pulsante **Fai clic qui per installare**). Per ulteriori informazioni su queste API consultare [la pagina di MDN dedicata all'installazione delle app][2] (sì, avete ragione, questo link non è nuovo, però ci sono informazioni importanti che dovete assolutamente conoscere).

Nel prossimo capitolo impareremo come distribuire la nostra app attraverso il  **Marketplace Firefox**.

[1]: http://marketplace.firefox.com "Firefox Marketplace"
[2]: https://developer.mozilla.org/docs/Apps/JavaScript_API

# Distribuire le app {#distribution}

Ora che la nostra applicazione è pronta, abbiamo bisogno di trovare un modo per renderla disponibile ai nostri utenti. Nel [capitolo introduttivo](#introduction) avevo accennato che, diversamente da Apple, Mozilla non obbliga a utilizzare il proprio canale di distribuzione - lasciando ognuno libero di esprimere la propria creatività. In questo capitolo impareremo come distribuire la nostra app **al di fuori del canale ufficiale di [Firefox Marketplace](http://marketplace.firefox.com)**. 

A mio modesto avviso, non utilizzare il canale ufficiale Mozilla per distribuire un'app è conveniente in questi due casi:

 1. Si sta sviluppando un'app per uso interno aziendale o per una ristretta cerchia di utenti. Pubblicandola su Firefox Marketplace, renderà l'app disponibile a chiunque e renderà necessario implementare un sistema di autenticazione, tramite, ad esempio, un back end su server remoto, per consentire il suo utilizzo solo agli utenti autorizzati. Ad esempio, nelle prime versioni dell'app *Evernote* era richiesta l'identificazione sui loro server prima di poterla utilizzare.
 2. Si dispone già di un grosso bacino d'utenza che è possibile sfruttare per distribuire l'app. Un esempio potrebbe essere un giornale, come il *Financial Times*, che può limitarsi a rendere disponibile l'app sul proprio sito per raggiungere la quasi totalità dei propri utenti. È bene ricordare che è possibile distribuire l'app sia su Firefox Marketplace, sia su un canale esterno, in questo modo sarà possibile sfruttare il canale di marketing preesistente e utilizzare Firefox Marketplace per raggiungere nuovi utenti.

Il processo di distribuzione delle app pacchettizzate e delle app ospitate è simile, anche se utilizzano delle funzioni differenti. Ecco perché tratterò i due casi separatamente. Indipendentemente dal fatto che l'app sia pacchettizzata o ospitata, il procedimento è più o meno lo stesso: sarà necessario rendere disponibile un pulsante o un link nella pagina, denominato **Fai clic per installare l'app**, o utilizzare un particolare URL che quando aperto attiva l'esecuzione della routine di installazione. In entrambi i casi, all'utente finale verrà presentata una finestra di dialogo in cui gli verrà chiesto di confermare l'installazione.

## App ospitate

<<[Code for hosted app installation](code/distribution/hosted_apps_distribution.js)

Nell'esempio riportato qui sopra `manifestURL` riporta l'indirizzo del file manifesto. All'esecuzione di questo codice, il sistema chiederà all'utente se desidera installare l'app e, a seconda della risposta dell'utente, richiamerà la callback appropriata: `success` in caso di risposta affermativa e `error` in caso contrario.

Per ulteriori informazioni su questa API consulta [la pagina su MDN sull'installazione delle app](https://developer.mozilla.org/docs/Apps/JavaScript_API).

## App pacchettizzate

L'installazione di app pacchettizzate funziona in modo analogo, però in questo caso anziché utilizzare la funzione `mozApps.install()` useremo `mozApps.installPackage()` come mostrato nel codice d'esempio riportato qui di seguito.

<<[Code for packaged app installation](code/distribution/packaged_apps_distribution.js)

W> Nota: ho il sospetto che l'installazione di app pacchettizzate da siti diversi da Firefox Marketplace non sia consentita nella versione 1.0.1 di Firefox OS. Nonostante l'API sia documentata, non ho mai provato di persona, quindi se hai l'oppurtunità di verificare questa mia supposizione, ti prego di contattarmi affinché passa aggiornare questo libro.

## Riassunto

In questo capitolo sono stati trattati i metodi di distribuzione delle app alternativi al sito Firefox Marketplace grazie all'utilizzo della API di *Installazione e gestione* delle *app web aperte*. Esistono molte altre routine disponibili, ad esempio per controllare se l'applicazione è installata (in questo modo ti sarà possibile nascondere il pulsante **Fai clic qui per installare**). Per ulteriori informazioni su queste API consulta [la pagina di MDN dedicata all'installazione delle app](https://developer.mozilla.org/docs/Apps/JavaScript_API) (si, hai ragione, questo link non è nuovo, però ci sono informazioni importanti che devi assolutamente conoscere).

Nel prossimo capitolo impareremo come distribuire la nostra app attraverso il sito Firefox Marketplace.

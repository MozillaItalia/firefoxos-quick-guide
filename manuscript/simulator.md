# Il Simulatore Firefox OS 1.1 {#simulator}

![Gestore App](images/originals/simulator-dashboard.png)  

W>Attenzione: Questo capitolo è presente solo per una compatibilità per i dispositivi con Firefox OS 1.1. Il metodo attuale per provare e fare il debug delle applicazioni è il **WebIde** di cui abbiamo parlato nel capitolo precedente. Il contenuto di questo capitolo è per quelle persone che devono provare le applicazioni sulla versione 1.1 di Firefox OS.

W>Attenzione: Se stai usando **Firefox 29 o successive** e dispositivi con **Firefox OS 1.1 o precedenti** hai bisogno di un'altra versione del **Simulatore Firefox OS 1.1** che non è disponibile nell'add-ons marketplace. Questa versione è una **BETA** ma al momento non ci sono alternative. Puoi scaricarla per [Mac OS X][1], [Linux][2] o [Windows][3]. Scarica il file xpi e caricalo in Firefox e segui le istruzioni. Se vuoi seguire la questione del supporto per il **simulatore Firefox OS 1.1** su **Firefox 29** dai un'occhiata alla [bug request #1001590][4].  

Abbiamo installato il Simulatore Firefox OS nel capitolo [*Ambiente di sviluppo per Firefox OS*](#setup) e lo abbiamo utilizzato nel capitolo [*La prima app*](#firstapp). È giunta l'ora di approfondire la conoscenza del simulatore e imparare come effettuare le operazioni più comuni.

Per ulteriori informazioni fare riferimento alla [documentazione di Firefox OS Simulator][5] su MDN.

## Aggiungere Applicazioni

È possibile aggiungere sia applicazioni *hosted* che *packaged* al simulatore. Vediamo come fare.

### Aggiungere applicazioni packaged

È già stata trattata l'aggiunta di un'*app packaged* nel capitolo [*La prima app*](#firstapp), ma vediamo di richiamare i concetti in modo da mostrare tutte le opzioni possibili.

Per aggiungere una nuova applicazione *packaged* fare clic sul pulsante **+** nel **Gestore App**, come è mostrato nella schermata sottostante. 

![Aggiungere un'applicazione packaged al simulatore](images/originals/simulator-add-directory.png)

Dopo aver fatto clic sul pulsante evidenziato nell'immagine,si aprirà una finestra di dialogo di selezione file. Per aggiungere l'app prescelta al simulatore, sarà sufficiente trovare la cartella dell'applicazione. Se non ci sono errori nel file manifesto e nel file che avvia l'app, essa verrà avviata nel simulatore. Se il file manifesto contiene degli errori verranno riportati nel Gestore App. 

![Esempio di un file manifesto non valido](images/originals/simulator-invalid-manifest.png)

Ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare l'applicazione nel simulatore in esecuzione (in alternativa è possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

### Aggiungere applicazioni hosted

Se si sta sviluppando un'applicazione hosted è necessario provarla utilizzando un server web. Non utilizzare il metodo descritto in precedenza con le *app hosted* in quanto alcuni errori potrebbero non essere rilevati, ad esempio un MIME Type non valido del file manifesto. 

Per caricare un'*app hosted* nel simulatore, inserire nella casella di testo, nel box in basso a sinistra, l'URL completa del manifesto dell'app e fare clic sul pulsante **+**.

![Aggiungere un'applicazione hosted al simulatore](images/originals/simulator-add-directory.png)

Dopo aver fatto clic sul pulsante, il simulatore verificherà il file manifesto e, se non verranno rilevati errori, l'app verrà eseguita all'interno del simulatore. Eventuali errori, analogamente a quanto avviene per le *app packaged*, verranno riportati nel Gestore (ad esempio, "app submission to the Marketplace needs at least an 128 icon").

Come per le *app packaged*, ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare la versione in esecuzione nel simulatore (è anche possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

## Debug

Una volta che l'app è stata aggiunta al simulatore, accedendo al Gestore sarà possibile effettuarne il debug facendo clic sul pulsante **Avvia Simulatore** che si trova in basso nel gestore applicazione, al clic apparirà la schermata che permette di eseguire una versione specifica del simulatore (se presente) e di installarne altri. Facendo clic su **Debug** accanto al pulsante **Aggiorna** verrà lanciata l'applicazione sul simulatore. A questo punto, si aprirà un'istanza della **Console JavaScript** connessa all'app in esecuzione nel simulatore. In basso sarà possibile vedere il contenuto nel file manifest tramite visualizzazione ad albero.

![Il pulsate da premere](images/originals/simulator-press-connect.png)

Alla pressione del pulsante scelto verrà mostrata una schermata simile a quella di questa immagine:

![Developer Tools connessi all'applicazione nel simulatore](images/originals/simulator-connected.png)

Con gli strumenti di sviluppo connessi all'applicazione sarà possibile verificarne il funzionamento Javascript, effettuare il debug del DOM, modificare lo stile ecc. Come amano dire i ragazzi delle startup *Provare finché non è pronta*.

Quando l'app risulterà funzionante nel simulatore, sarà tempo di provarla su un vero dispositivo.

## Provare l'applicazione su un dispositivo reale

Fare riferimento alla sezione del capitole precedente su questo argomento.

## Connessione con un dispositivo Firefox OS

Avendo a disposizione un dispositivo Firefox OS (con i driver installati) connesso al computer, è possibile fare un push delle applicazioni direttamente dal simulatore al dispositivo. Facendo clic nella barra laterale dove è scritto **Dispositivo** si passa al gestore del dispositivo (che può essere anche il simulatore stesso). Quando il simulatore riconosce che un dispositivo con Firefox OS phone è collegato, verrà mostrato un messaggio **Dispositivo Connesso**.

![Dispositivo connesso!](images/originals/simulator-device-connected.png)

Se lo smartphone è connesso e riconosciuto, il simulatore mostrerà un nuovo pulsante chiamato **Push** accanto ai pulsanti **Aggiorna** e **Connetti**. Premendo questo pulsante, una **finestra di richiesta per i permessi** apparirà sul dispositivo chiedendo la conferma per poter procedere con l'installazione dell'applicazione.

![Il pulsante da premere per fare il push delle app sul dispositivo](images/originals/simulator-press-push.png)

Nell'immagine sottostante è possibile vedere la finestra di richiesta permessi:

![Non è la foto migliore del mondo ma mostra la finestra dei permessi (scusate per la faccia ma erano le 4:25 di mattina)](images/originals/simulator-remote-push.jpg)

Con l'applicazione in esecuzione nel dispositivo è possibile usare il *remote debugging* per aprire un'istanza della **Console JavaScript** collegata con l'app in modo da effettuare il debug.  

Da questo dispositivo si possono debuggare le applicazioni installate tra cui anche quelle di sistema.  

## Riassunto

Riassumendo, il simulatore Firefox OS è spettacolare per creare applicazioni specifiche per Firefox OS - ma ha alcuni limiti se si vuole sviluppare un'app che funzioni su una maggior gamma di dispositivi (ad esempio al momento non è possibile emulare il comportamento di Firefox OS su un tablet). 

A questo punto del testo, oltre a una sensazione di incredibile forza, si dovrebbe, o così mi auguro, riuscire a comprendere il workflow necessario per sviluppare un'app Firefox OS. Nel prossimo capitolo vedremo come distribuire un'applicazione agli utenti.

[1]: http://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-5.0pre7-mac.xpi
[2]: http://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-5.0pre7-linux.xpi
[3]: http://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-5.0pre7-windows.xpi
[4]: https://bugzilla.mozilla.org/show_bug.cgi?id=1001590 "Bug simulatore"
[5]: https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator

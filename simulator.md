# Il Simulatore Firefox OS {#simulator}

![Firefox OS Simulator Dashboard](images/originals/simulator-dashboard.png)

Abbiamo installato il Simulatore Firefox OS nel [capitolo sulla preparazione dell'ambiente di sviluppo](#setup) e lo abbiamo utilizzato nel [capitolo in cui abbiamo creato la prima app](#firstapp). È giunta l'ora di approfondire la conoscenza del simulatore e imparare come effettuare le operazioni più comuni.

Per ulteriori informazioni fare riferimento alla [documentazione di Firefox OS Simulator](https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator) su MDN.

## Aggiungere Applicazioni

È possibile aggiungere sia applicazioni *hosted* sia *packaged* al simulatore. Vediamo come fare.

### Aggiungere applicazioni packaged

È già stata trattata l'aggiunta di un'*app packaged* nel capitolo [creazione della nostra prima applicazione](#firstapp), ma vediamo di richiamare i concetti in modo da mostrare tutte le opzioni possibili.

Per aggiungere una nuova applicazione *packaged* fare clic sul pulsante **Aggiungi Directory** nella **Dashboard del Simulatore** come è possibile vedere nella schermata sottostante. Se non ci sono errori nel file manifesto e nel file che avvia l'app, essa verà avviata nel simulatore. Se il file manifesto contiene degli errori o se viene rilevato qualche altro errore, essi verranno riportati nella Dashboard del simulatore. 

![Ecco il pulsante *Aggiungi Cartella* che aggiunge l'applicazione al simulatore](images/originals/simulator-add-directory.png)


![Esempio di un file manifesto non valido](images/originals/simulator-invalid-manifest.png)

Ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare la versione in esecuzione nel simulatore (è anche possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

### Aggiungere applicazioni hosted

Se si sta sviluppando un'applicazione hosted è necessario testarla utilizzando un server web. Non utilizzare il metodo descritto in precedenza con le *app hosted* in quanto alcuni errori potrebbero non essere rilevati, ad esempio un MIME Type non valido del file manifesto. Si noti che il simulatore non segnala errori, anche di una certa rilevanza, come un MIME Type non valido, ma è importante verificare che tutto funzioni se si vuole pubblicare l'app su Firefox Marketplace.

La maggior parte delle applicazioni non sono realizzate specificatamente per Firefox OS ma il design responsive permette  di adattare l'interfaccia a più dispositivi e risoluzioni. Queste applicazioni web hanno un backend complesso che permette di far funzionare l'applicazione e quindi è necessario provarla su un server web vero. 

Per avviare un'*app hosted* nel simulatore, inserire nel campo testuale posto nella parte superiore del simulatore l'URL completa del manifesto dell'app e fare clic su **Aggiungi URL**.

![Aggiungere un'applicazione hosted al simulatore](images/originals/simulator-add-url.png)

Dopo aver cliccato il pulsante **Aggiungi URL**, il simulatore verificherà il file manifesto e se non vengono rilevati errori l'app verrà eseguita all'interno del simulatore. Eventuali errori, come avviene per le *app packaged*, verranno riportati nella Dashboard (ad esempio, "app submission to the Marketplace needs at least an 128 icon").

Come per le *app packaged*, ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare la versione in esecuzione nel simulatore (è anche possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

## Debug

Una volta che l'app è stata aggiunta al simulatore, sarà possibile effettuarne il debug facendo clic sul pulsante **Connetti** posto accanto al nome dell'app nell'elenco delle app in esecuzione sul simulatore. A questo punto, si aprirà un'istanza della **Console JavaScript** connessa all'app in esecuzione nel simulatore.

![Il punsate da premere](images/originals/simulator-press-connect.png)

Alla pressione del pulsante sarà mostrata una cosa come questa:

![Developer Tools connessi all'applicazione nel simulatore](images/originals/simulator-connected.png)

Con gli strumenti di sviluppo connessi all'applicazione sarà testare Javascript, effettuare il debug del DOM, modificare lo stile ecc. Come quei ragazzi delle startup che dicono *testare finchè non è pronta*.

Quando l'app risulterà funzionante nel simulatore sarà tempo di testarla su un vero dispositivo.

## Testare l'applicazione su un dispositivo reale

Niente può sostituire il testing su un dispositivo reale. Nel simulatore i test vengono effettuati facendo clic con un mouse su uno schermo di computer, mentre con un dispositivo reale i test si effettuano toccando uno touchscreen e premendo con le dita dei pulsanti reali.  Un'esperienza utente e sviluppatore completamente diversa.

Per sottolineare l'importanza di effettuare dei test su un dispositivo reale, racconterà un fatto personale: Alcuni anni fà Raphael Eckhardt  (il designer della copertina di questo libro) ed io stavamo realizzando un puzzle game simile a  Bejeweled. Il nostro gioco consisteva nel trascinare e posizionare dei pezzi su una tavola e funzionava abbastanza bene sul simulatore. 

Quando abbiamo testato il gioco su un telefono reale ci siamo resi conto che i componenti del gioco non erano ottimizzati per la piattaforma *mobile*: quando posizionavamo la mano sullo schermo tutto scompariva dietro la mano. Inoltre i componenti di gioco erano troppo piccoli per le dita degli utenti quindi gli utenti non potevano cosa succedeva, in poche parole l'interfaccia non era un granchè. Il problema era che noi abbiamo testato con il mouse che ha un cursore piccolo. Quando abbiamo provato con le nostre dita ciccione ci siamo resi conto che dovevamo rielaborare l'interfaccia.  
Per evitare dei problemi dopo il rilascio provate sempre su un dispositivo reale... o due. Testate spesso con dei prototipi per risparmiare tempo e denaro senza dover rimodificare tutto ogni volta. 

È possibile acquistare un developer preview phone Firefox OS dal [Geeksphone Shop](http://shop.geeksphone.com/en/). Consiglio di usare il [Geeksphone Keon](http://www.geeksphone.com/) perchè è quello con le specifiche più simili ai dispositivi lanciati dai partner di Mozilla.  

È sempre possibile acquistare un dispositivo per l'utente finale se abiti in un paese in cui vengono già commercializzati. Un'altra soluzione è sostituire Android con Firefox OS su alcuni dispositivi (alcuni dispositivi lo supportano!) non lo consiglio se non sei un utente avanzato e non ti piace perdere troppo tempo in hacking.  

## Connessione con un dispositivo Firefox OS

Se si è connesso un dispositivo Firefox OS (e se i driver sono installati) è possibile fare un push delle applicazioni direttamente dal simulatore al dispositivo se il dispositivo è connesso al computer. Quando il simulatore riconosce che hai collegato un dispositivo con Firefox OS phone, verrà mostrato un messaggio **Dispositivo Connesso**.

![Dispositivo connesso!](images/originals/simulator-device-connected.png)

Se lo smartphone è connesso e riconosciuto il simulatore mostrerà un nuovo pulsante accanto ai pulsanti **Aggiorna** e **Connetti** chiamato **Push**. Premendo questo pulsante una **finestra di richiesta per i permessi** apparirà sul dispositivo chiedendo la conferma ed installando l'applicazione.

![Il pulsante da premere per connettersi al dispositivo](images/originals/simulator-press-push.png)

Qui è possibile vedere la finestra di richiesta permessi.

![Non è la foto migliore del mondo ma mostra la finestra dei permessi (scusate per la faccia ma erano le 4:25 di mattina)](images/originals/simulator-remote-push.jpg)

Con l'applicazione avviata sul dispositivo è possibile usare il *remote debugging* per connetterti alla console JavaScript e effettuare il debug l'applicazione.

## Riassunto

Riassumendo il simulatore Firefox OS è spettacolare per costruire applicazioni FireFox OS - ci sono alcune limitazioni se stai provando su molti dispositivi (e.g., attualmente non è possibile emulare FirefoxOS come su un tablet). 

Oltre alla sensazione di potere a questo punto del libro hai le conoscenze per realizzare un'applicazione per Firefox OS. Nel prossimo capitolo vedremo come distribuire un'applicazione agli utenti.

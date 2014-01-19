# Il Simulatore Firefox OS {#simulator}

![Firefox OS Simulator Dashboard](images/originals/simulator-dashboard.png)

Abbiamo installato il Simulatore Firefox OS nel capitolo [*Ambiente di sviluppo per Firefox OS*](#setup) e lo abbiamo utilizzato nel capitolo [*La prima app*](#firstapp). È giunta l'ora di approfondire la conoscenza del simulatore e imparare come effettuare le operazioni più comuni.

Per ulteriori informazioni fare riferimento alla [documentazione di Firefox OS Simulator](https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator) su MDN.

## Aggiungere Applicazioni

È possibile aggiungere sia applicazioni *hosted* che *packaged* al simulatore. Vediamo come fare.

### Aggiungere applicazioni packaged

È già stata trattata l'aggiunta di un'*app packaged* nel capitolo [*La prima app*](#firstapp), ma vediamo di richiamare i concetti in modo da mostrare tutte le opzioni possibili.

Per aggiungere una nuova applicazione *packaged* fare clic sul pulsante **Aggiungi Directory** nella **Dashboard del Simulatore**, come è mostrato nella schermata sottostante. 

![Ecco il pulsante *Aggiungi Cartella* che aggiunge l'applicazione al simulatore](images/originals/simulator-add-directory.png)

Dopo aver fatto clic sul pulsante evidenziato nell'immagine,si aprirà una finestra di dialogo di selezione file. Per aggiungere l'app prescelta al simulatore sarà sufficiente trovare e aprire il **file manifesto dell'app** dal proprio hard disk. Se non ci sono errori nel file manifesto e nel file che avvia l'app, essa verrà avviata nel simulatore. Se il file manifesto contiene degli errori o se viene rilevato qualche altro errore, essi verranno riportati nella Dashboard del simulatore. 

![Esempio di un file manifesto non valido](images/originals/simulator-invalid-manifest.png)

Ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare la versione in esecuzione nel simulatore (in alternativa è possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

### Aggiungere applicazioni hosted

Se si sta sviluppando un'applicazione hosted è necessario provarla utilizzando un server web. Non utilizzare il metodo descritto in precedenza con le *app hosted* in quanto alcuni errori potrebbero non essere rilevati, ad esempio un MIME Type non valido del file manifesto. Si noti che il simulatore non segnala errori, anche di una certa rilevanza come, appunto, un MIME Type non valido, ma è importante verificare che tutto funzioni se si vuole pubblicare l'app su Firefox Marketplace.

La maggior parte delle applicazioni *hosted* non sono realizzate specificatamente per Firefox OS, si tratta piuttosto di veri e propri siti web che sfruttano il design responsive per adattarsi a più dispositivi e risoluzioni. Solitamente queste app web funzionano grazie a un complesso back end che deve essere in esecuzione per consentire un loro corretto funzionamento ed è proprio per questo motivo che si rende necessario verificarne il funzionamento con un vero server web per assicurarsi che tutto funzioni correttamente.

Per caricare un'*app hosted* nel simulatore, inserire nella casella di testo, posta nella parte superiore del simulatore, l'URL completa del manifesto dell'app e fare clic su **Aggiungi URL**.

![Aggiungere un'applicazione hosted al simulatore](images/originals/simulator-add-url.png)

Dopo aver fatto clic sul pulsante **Aggiungi URL**, il simulatore verificherà il file manifesto e, se non verranno rilevati errori, l'app verrà eseguita all'interno del simulatore. Eventuali errori, analogamente a quanto avviene per le *app packaged*, verranno riportati nella Dashboard (ad esempio, "app submission to the Marketplace needs at least an 128 icon").

Come per le *app packaged*, ogni volta che l'app verrà aggiornata sarà necessario fare clic sul pulsante **Aggiorna** per aggiornare la versione in esecuzione nel simulatore (è anche possibile utilizzare la scorciatoia da tastiera CMD/CTRL+R dalla finestra del simulatore).

## Debug

Una volta che l'app è stata aggiunta al simulatore, accedendo alla Dashboard sarà possibile effettuarne il debug facendo clic sul pulsante **Connetti** che si trova accanto al nome di ogni app in esecuzione nel simulatore. A questo punto, si aprirà un'istanza della **Console JavaScript** connessa all'app in esecuzione nel simulatore.

![Il pulsate da premere](images/originals/simulator-press-connect.png)

Alla pressione del pulsante **Connetti** verrà mostrata una schermata simile a quella di questa immagine:

![Developer Tools connessi all'applicazione nel simulatore](images/originals/simulator-connected.png)

Con gli strumenti di sviluppo connessi all'applicazione sarà possibile verificarne il funzionamento Javascript, effettuare il debug del DOM, modificare lo stile ecc. Come amano dire i ragazzi delle startup *testare finché non è pronta*.

Quando l'app risulterà funzionante nel simulatore sarà tempo di testarla su un vero dispositivo.

## Testare l'applicazione su un dispositivo reale

Niente può sostituire il testing su un dispositivo reale. Nel simulatore i test vengono effettuati facendo clic con un mouse su uno schermo di computer, mentre con un dispositivo reale i test si effettuano toccando uno touchscreen e premendo con le dita dei pulsanti reali. Un'esperienza utente e sviluppatore completamente diversa.

Per sottolineare l'importanza di effettuare dei test su un dispositivo reale, racconterò un fatto personale. Alcuni anni fa Raphael Eckhardt  (il designer della copertina di questo libro) ed io stavamo realizzando un puzzle game simile a  Bejeweled. Il nostro gioco consisteva nel trascinare e posizionare dei pezzi su una tavola e funzionava abbastanza bene sul simulatore. 

Quando abbiamo provato il gioco su un telefono reale ci siamo resi conto che i componenti del gioco non erano ottimizzati per la piattaforma *mobile*: quando posizionavamo la mano sullo schermo tutto scompariva dietro la mano. Inoltre i componenti di gioco erano troppo piccoli per le dita, quindi gli utenti non potevano rendersi conto di quello che stavano facendo, in poche parole l'interfaccia non era un granché. Il problema era che noi avevamo effettuato i nostri test utilizzando il mouse e il puntatore del mouse è molto piccolo. Quando abbiamo provato con le nostre dita "cicciotelle" ci siamo resi conto che dovevamo rielaborare l'interfaccia.  

Per evitare di avere un'esperienza così frustrante è indispensabile verificare sempre l'app su un dispositivo reale… O ancora meglio su qualunque dispositivo si abbia a disposizione. Effettuare dei buoni test su dei semplici prototipi è molto importante per non dover perdere tempo e denaro a rimodificare tutto ogni volta.

È possibile acquistare un developer preview phone Firefox OS dal [Geeksphone Shop](http://shop.geeksphone.com/en/). Consiglio di usare il [Geeksphone Keon](http://www.geeksphone.com/) perché è quello con le specifiche più simili agli smartphone messi in commercio dai partner di Mozilla.

Inoltre, nel caso si risiedesse in un paese in cui i dispositivi Firefox OS sono già in commercio, è possibile acquistare direttamente un dispositivo per l'utente finale. Un'altra soluzione è sostituire Android con Firefox OS su alcuni dispositivi (alcuni dispositivi lo supportano!) ma, a meno di non essere esperti e disposti a perdere del tempo con l'hacking, non è una cosa che mi sento di consigliare.

## Connessione con un dispositivo Firefox OS

Avendo a disposizione un dispositivo Firefox OS (con i driver installati) connesso al computer, è possibile fare un push delle applicazioni direttamente dal simulatore al dispositivo. Quando il simulatore riconosce che un dispositivo con Firefox OS phone è collegato, verrà mostrato un messaggio **Dispositivo Connesso**.

![Dispositivo connesso!](images/originals/simulator-device-connected.png)

Se lo smartphone è connesso e riconosciuto, il simulatore mostrerà un nuovo pulsante chiamato **Push** accanto ai pulsanti **Aggiorna** e **Connetti**. Premendo questo pulsante una **finestra di richiesta per i permessi** apparirà sul dispositivo chiedendo la conferma ed installando l'applicazione.

![Il pulsante da premere per fare il push delle app sul dispositivo](images/originals/simulator-press-push.png)

E nell'immagine sottostante è possibile vedere la finestra di richiesta permessi:

![Non è la foto migliore del mondo ma mostra la finestra dei permessi (scusate per la faccia ma erano le 4:25 di mattina)](images/originals/simulator-remote-push.jpg)

Con l'applicazione in esecuzione nel dispositivo è possibile usare il *remote debugging* per aprire un'istanza della **Console JavaScript** collegata con l'app in modo da effettuare il debug.

## Riassunto

Riassumendo, il simulatore Firefox OS è spettacolare per creare applicazioni specifiche per FireFox OS - ma ha alcuni limiti se si vuole sviluppare un'app che funzioni su una maggior gamma di dispositivi (ad esempio al momento non è possibile emulare il comportamento di Firefox OS su un tablet). 

A questo punto del libro, oltre a una sensazione di incredibile forza, si dovrebbe, o così mi auguro, riuscire a comprendere il workflow necessario per sviluppare un'app Firefox OS. Nel prossimo capitolo vedremo come distribuire un'applicazione agli utenti.

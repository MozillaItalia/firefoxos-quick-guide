# Il Simulatore Firefox OS {#simulator}

![Firefox OS Simulator Dashboard](images/originals/simulator-dashboard.png)

Abbiamo installato il Simulatore Firefox OS nel [prossimo capitolo dopo la preparazione del sistema](#setup) e letto [il capitolo il primo capitolo della nostra prima applicazione](#firstapp). Diamo un'occhiata alle caratteristiche del simulatoree vediamo le funzioni più comuni.

Per saperne di più, diamo un'occhiata [la documentazione di Firefox OS Simulator](https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator) su MDN.

## Aggiungere Applicazioni

Puoi aggiungere applicazioni sia hosted e packaged al simulatore. Vediamo come aggiungere queste applicazioni.

### Aggiungere applicazioni packaged

Hai già visto come aggiungere applicazioni durante la [creazione della nostra prima applicazione](#firstapp), ma facciamo un riassunto così vediamo le potenzialità.

Per aggiungere una nuova applicazione packaged clicca **Aggiungi Directory** nella **Dashboard del Simulatore** come puoi vedere nella schermata sottostante.

![Ecco il pulsante *Aggiungi Cartella* che aggiunge l'applicazione al simulatore](images/originals/simulator-add-directory.png)

Quando clicchi sul pulsante evidenziato nell'immagine, Firefox aprirà la finestra di selezione file. Sfoglia l'hard disk e seleziona il **file app manifest** dell'applicazione che vuoi provare. Se il tuo file non ha problemi  la tua appliczione verrà aggiunta e il simulatore lanciato. Se c'è qualche errore o problema verrà segnalato verrà segnanalato nella dashboard. 

![Esempio di un file manifest](images/originals/simulator-invalid-manifest.png)

Ogni volta che aggiornerai l'applicazione devi cliccare su **Refresh** per aggiornare la versione dell'applicazione nel simulatore (puoi anche premere CMD/CTRL+R  nella finestra del simulatore). 

### Aggiungere applicazioni hosted

Se stai costruendo un'applicazione hosted devi testarla con un web server. Non provare il metodo citato sopra perchè non funziona con le app hosted generando degli errori perchè il *MIME type* del file manifest è sbagliato. Da notare che il simulatore non segnala questo errore ma è molto importante per inviare l'applicazione al marketplace Mozilla. 

La maggior parte delle applicazioni non sono realizzate specificatamente per Firefox OS ma il design responsive permette di di adattare l'interfaccia a più dispositivi e risoluzioni. Queste applicazioni web hanno un backend complesso che permette di far funzionare l'applicazione e quindi è necessario provarla su un web server vero. 

Per far funzionare l'applicazione nel simulatore, compila il campo con la URL completa dell'applicazione e poi clicca sul pulsante **Aggiungi URL**.

![Aggiungere un'applicazione hosted al simulatore](images/originals/simulator-add-url.png)

Dopo aver cliccato il pulsante il manifest è verificato e se è corretto l'applicazione sarà aggiunta al simulatore e lanciato. Come nelle applicazione packaged se ci sono degli errori verrà segnalato (e.g., "app submission to the Marketplace needs at least an 128 icon").

Come con le applicazioni packaged, ogni volta che aggiornerai l'applicazione devi cliccare su **Refresh** per aggiornare la versione dell'applicazione nel simulatore (puoi anche premere CMD/CTRL+R  nella finestra del simulatore). 
As with packaged apps, whenever you update your application you should click **Refresh** to update the version of the app on the simulator (you can also press CMD/CTRL+R on the simulator window).

## Debugging

Dopo l'applicazione è aggiunta al simulatore e potrami debuggarla cliccando su **Connetti** . Questo lancerà il simulatore con l'applicazione aperta e la **JavaScript Console** aperta e connessa alla tua applicazione.

![Il punsate da premere](images/originals/simulator-press-connect.png)

Dopo aver premuto il pulsante vedrai qualcosa come questo:

![Developer Tools connessi all'applicazione nel simulatore](images/originals/simulator-connected.png)

Con gli strumenti connessi alla tua applicazione puoi testare Javascript, debuggare il DOM, modificare lo stile ecc. Come quei ragazzi delle startup che dicono *testare finchè non è pronta*.

Quando la tua applicazione è funzionante è ora di testarla su un dispositivo.

## Testare l'applicazione su un dispositivo reale

Niente sostituisce il testing su un dispositivo reale. Nel simulatore potrai testare cliccando sullo schermo del computer mentre con un dispositivo reale potrai provare con le tue dita usando pulsanti reali. Una esperienza di debugging completamente diversa. 

Facciamo un'esempio sulla necessità di queste prove raccontandoti una storia: Alcuni anni fà Raphael Eckhardt  (il seigner della copertina di questo libro) ed io stavamo realizzando un puzzle game simile a  Bejeweled. Il nostro gioco consisteva nel trascinare e posizionare dei pezzi su una tavola e funzionava abbastanza bene sul simulatore. 

Quando abbiamo testato il gioco su un telefono reale ci siamo resi conto che i componenti del gioco non erano ottimizzati per il modile: quando posizionavamo la mano sullo schermo tutto scompariva dietro la mano. Inoltre i componenti di gioco erano troppo piccoli per le dita degli utenti quindi gli utenti non potevano cosa succedeva, in poche parole l'interfaccia non era un granchè. Il problema era che noi abbiamo testato con il mouse che ha un cursore piccolo. Quando abbiamo provato con le nostre dita ciccione ci siamo resi conto che dovevamo rielaborare l'interfaccia.  

Per evitare dei problemi dopo il rilascio provate sempre su un dispositivo reale... o due. Testate spesso con dei prototipi per risparmiare tempo e denaro senza dover rimodificare tutto ogni volta. 

Puoi comprare una developer preview phone con Firefox OS dal [Geeksphone Shop](http://shop.geeksphone.com/en/). Consiglio di usare il [Geeksphone Keon](http://www.geeksphone.com/) perchè è quello con le specifiche più simili ai dispositivi lanciati dai partener di Mozilla.  

Puoi sempre comprare un dispositivo per i consumatori se sei in un paese in cui è già disponibili. Un'altra soluzione è sostituire Android con Firefox OS su alcuni dispositivi (alcuni dispositivi lo supportano!) non lo consiglio se non sei un utente avanzato e non ti piace perdere troppo tempo in hacking.  

## Connessione con un dispositivo Firefox OS

Se hai connesso un dispositivo Firefox OS device (ed hai i driver installati) puoi fare un push delle applicaizoni direttamente dal simulatore al dispositivo se il dispositivo è connesso al computer. Quando il simulatore riconosce che hai collegato un dispositivo con Firefox OS phone, verrà mostrato un messaggio **Dispositivo Connesso**.

![Dispositivo connesso!](images/originals/simulator-device-connected.png)

Se il tuo telefono è connesso e riconosciuto il simulatore mostrerà un nuovo pulsante vicino ad **Aggiorna** e **Connetti** chiamato **Push**. Quando premi questo pulsante una **finestra di richiesta per i permessi** apparirà sul dispositivo chiedendo la conferma ed installando l'applicazione.

![Il pulsante da premere per connettersi al dispositivo](images/originals/simulator-press-push.png)

Qui puoi vedere la finestra di richiesta permessi.

![Non è la foto migliore del mondo ma mostra la finestra dei permessi (scusate per la faccia ma erano le 4:25 di mattina)](images/originals/simulator-remote-push.jpg)

Con l'applicazione avviata sul dispositivo puoi usare il *remote debugging* per connetterti alla console JavaScript e debuggare l'applicazione.

## Riassunto

Riassumendo il simulatore Firefox OS è spettacolare per costruire applicazioni FireFox OS - ci sono alcune limitazioni se stai provando su molti dispositivi (e.g., attualmente non è possibile emulare FirefoxOS come su un tablet). 

Oltre alla sensazione di potere a questo punto del libro hai le conoscenze per realizzare un'applicazione per Firefox OS. Nel prossimo capitolo vedremo come distribuire un'applicazione agli utenti.

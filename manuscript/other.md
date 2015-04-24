# Altro

In questo capitolo vedremo in modo veloce alcune tecnologie che ci possono essere utili nello sviluppo per Firefox OS.

## Gaia Building Blocks

Per chi è abituato ad utilizzare i framework CSS sarà molto semplice capire l'utilità di Building Blocks. Questo framework già citato è utilizzato nel boilerplate e in molte applicazioni presenti sul marketplace.  
Si tratta di un framework CSS basato sulle release giornaliere di Gaia che permette di avere sempre le ultime novità.  
Come si può vedere dal sito [http://buildingfirefoxos.com/][1] ci sono moltissimi esempi riguardanti:  

* [Action menu][2]
* [Buttons][3]
* [Confirm][4]
* [Drawer][5]
* [Edit Mode][6]
* [Filters][7]
* [Headers][8]
* [Input Areas][9]
* [Lists][10]
* [Progress And activity][11]
* [Scrolling][12]
* [Seek Bars][13]
* [Status][14]
* [Switches][15]
* [Tabs][16]
* [Toolbars][17]
* [Value Selector][18]

Come si può vedere ci sono molte interfacce e opzioni possibili per avere la stessa grafica del sistema un modo semplice. Inoltre è presente una sezione dedicata alle icone tramite Font Icon.  
Non è finita qui ci sono anche le [transizioni][19] e per chi lavora con Photoshop ci sono anche i file [psd][20] per un'approccio grafico al lavoro.  

## Web Components

I Web Components sono una tecnologia emergente che è attualmente nello stato di [Working Draft][21] dal W3C ma già supportata da Chrome e Firefox.

La caratteristica principale di questa nuova tecnologia è la **personalizzazione** di HTML, possiamo creare dei nuovi tag, definendone il comportamento, e questi verranno aggiunti alla nostra pagina.

Questa idea permette di avere ad esempio un tag `<map>` per visualizzare una mappa tramite Google Maps o OpenStreetMap, un tag `<calendar>` per permettere all'utente di scegliere un giorno dal calendario, `<qr>` o `<barcode>` per mostrare un codice qr o un codice a barre personalizzati, etc, etc...

Questa tecnologia **è retrocompatibile** infatti se volete essere compatibili con una versione datata di un browser e usare i Web Components basta usare una **polyfill** che vi viene data dal progetto **Polymer** di Google.

La libreria [Polymer][22] è integrata nella raccolta di Web Components [Brick 2.0][23], sponsorizzata da Mozilla. In questa guida li introdurremo semplicemente senza andare nei dettagli (un po' come abbiamo fatto con Gaia Building Blocks).

Attualmente sono disponibili in Brick i seguenti componenti, che potete già utilizzare.

* [Barra dell'applicazione][24] - una comoda barra per contenere titolo e pulsanti
* [Calendario][25] - un calendario per selezionare una data
* [Deck o schermata][26] - un "mazzo di carte" che è possibile scorrere per visualizzarle tutte
* [FlipBox][27] - per avere fronte e retro di una schermata, come un foglio
* [Layout (un contenitore)][28] - comodo per isolare parti di una schermata
* [Action][29] - hai bisogno di controllare cosa succede?
* [Barra delle schede][30] - la classica barra delle schede
* [Form][31] - nome, cognome e indirizzo? Eccoti servito
* [Menu][32] - vi serve un menu?
* [Storage-IndexdDB][33] - per conservare informazioni sul dispositivo dell'utente

Per mostrare l'uso di questi componenti, Daniele ha realizzato un boilerplate di nome [Brickly][37] che potete studiare per prendere confidenza con i Web Components.

Non è nell'interesse della guida approfondire questa libreria ma solo pubblicizzare questo materiale già disponibile all'uso.

## Hosting App su Github

Github offre sui suoi server un servizio di web hosting, questa sezione tratterà di come sfruttare Github per distribuire la propria applicazione sulla rete.

Come prima cosa è necessario registrarsi su Github ed affettuare l'accesso. Nella schermata che troverete davanti (detta *Dashboard*) alla destra della vostra immagine di profilo c'è un icona "+" che permette di creare una *repository*.  

Un repository può essere descritto semplicemente come una cartella che contiene un progetto e la storia dei suoi file da quando l'avete creato. Questo ci permette di tenere traccia delle modifiche ai file nel tempo.  

![Aggiungi un repository][addRepo]

Verrete indirizzati alla schermata di creazione della repository; qui dovrete inserire il nome della vostra applicazione e una breve descrizione della stessa, lasciando i restanti campi immodificati premete **create repository**. La repository sarà quindi creata automaticamente e vi troverete nella pagina del progetto.

![Crea un nuovo repository][createRepo]

In questa nuova schermata è presente una barra sulla destra che permette di gestire il progetto, fate click su **Settings**.  

![Impostazioni][settings]  

Scorrete fino alla sezione che ha per titolo **Github Pages** dove troverete il pulsante **Automatic Page Generator**, premetelo. In questo modo verrà generato il ramo **gh-pages** con del contenuto già pronto ideale per questo esempio. 

![Genera il ramo gh-pages automaticamente][gitpages]

La pagina che verrà creata servirà come base per l'applicazione, motivo per cui non dovremo perdere tempo a modificare i contenuti o a scegliere il layout: la pagina generata verrà scartata in favore della nostra applicazione.

Nella prima pagina **New project site** fate click su **continue to layouts** senza modificare nulla e nella pagina di scelta del layout premete **publish page**.  

Github creerà quindi un sito per il vostro progetto che sarà visitabile da chiunque all'indirizzo: `http://miousername.github.io/nomedelprogetto`. Potete trovare l'indirizzo completo nella pagina Settings della vostra repository. Seguendo i passaggi sopra elencati il sito sarà così realizzato (titolo e sottotitolo dipenderanno dal nome e dalla descrizione):

![Una delle pagine disponibili][defaultPage]

Per far si che l'app sia effettivamente installabile occorre modificare il file **manifest.webapp**. In particolare bisogna sostituire nel campo "launch_path" il nuovo indirizzo del vostro file **index.html**.

Se ricordate l'indirizzo che avrà il vostro progetto sarà circa: `http://miousername.github.io/nomedelprogetto`, il manifesto deve quindi essere così modificato.
    
     "launch_path" : "/nomedelprogetto/index.html" 
     
Per la corretta visualizzazione delle icone è necessario aggiornare anche il campo "icons"

    "icons" : {
        "128" : "/nomedelprogetto/cartellaIcone/icona128.png",
        "60" : "/nomedelprogetto/cartellaIcone/icona60.png"
        }
     
Infine per caricare l'applicazione è necessario installare sul computer un software distribuito da Github.

Per Windows tale programma è disponibile con interfaccia grafica o tramite un terminale apposito (Git Power Shell), mentre per GNU/Linux è disponibile solo su terminale, questa guida per semplicità farà riferimento ai comandi da eseguire da terminale.

Per iniziare è necessario clonare la repository sul proprio pc digitando questi comandi nel terminale:    
    
    $ git clone https://github.com/miousername/nomedelprogetto.git
    
Ora bisogna sostituire il contenuto della cartella **nomedelprogetto** con i file che compongono la vostra applicazione, questa operazione per semplicità può essere eseguita tramite il file manager.

W> Attenzione: Dovete copiare solamente i file, non la cartella che li contiene

Quindi per aggiornare i file su GitHub digitare:

    $ cd nomedelprogetto
    $ git add -A
    $ git commit -m "hosting app"
    $ git push origin gh-pages
    

Inserite le vostre credenziali per avviare il caricamento dei file. Una volta finito il caricamento visitando l'indirizzo del vostro progetto vedrete anzichè la pagina generata automaticamente l'*Homepage* della vostra applicazione.

W> NOTA: Può capitare che a volte la modifica della pagina impieghi anche 30 minuti, nel caso pazientate.

Ultima tappa è la pubblicazione sul Firefox Marketplace. Accedete o registratevi al Firefox Marketplace come sviluppatori, nella pagina **Carica un'app** selezionate **Hosted app** e inserite l'indirizzo del **manifesto** ossia: `http://miousername.github.io/nomedelprogetto/manifest.webapp`

### Concierge

Tra gli strumenti a nostra disposizione se vogliamo pubblicare la nostra app come **hosted** c'è [**Concierge**][34], una libreria che si occupa di:

* rilevare se la nostra app è installata
* proporre l'installazione
* creare un bottone di installazione semplice e di buon gusto

Potete vedere la demo su [questa pagina][35].

Per usare **Concierge** basta includere il suo file JavaScript, il file CSS e aggiungere il seguente codice alla nostra pagina su cui troviamo l'applicazione.

```
var install = new Concierge({
    onSuccess: successCallback,
    onError: errorCallback
});

function successCallback () {
    console.log('App installed!');
}

function errorCallback (error) {
    console.error('Concierge() error: ' + error);
}
```

Questo è tutto, se vi doveste trovare in imbarazzo e non funzionasse controllate per bene di aver seguito tutti i passaggi elencati sulla [pagina del progetto][34].

### Firefox Developer Edition

Per i 10 anni di Firefox, il browser indipendente che mette l'utente al centro, Mozilla ha fatto un enorme balzo in avanti verso la comunità degli sviluppatori web come noi (si, anche tu!). La versione [Firefox Developer Edition][36] include **TUTTI** gli strumenti su cui Mozilla lavora per aiutare gli sviluppatori web, compresi quelli ancora non inclusi nelle versioni generiche, ed è compatibile con i più nuovi standard.

Se continuerai questo percorso da Web Developer non potrai fare a meno di sporcarti le mani e questi strumenti sono i migliori disponibili al momento!

[addRepo]:images/originals/git-addRepo.png
[createRepo]:images/originals/git-createRepo.png
[settings]:images/originals/git-settings.png
[gitpages]:images/originals/git-gitpages.png
[defaultPage]:images/originals/git-defaultPage.png

[1]: http://buildingfirefoxos.com/building-blocks/
[2]: http://buildingfirefoxos.com/building-blocks/action-menu.html
[3]: http://buildingfirefoxos.com/building-blocks/buttons.html
[4]: http://buildingfirefoxos.com/building-blocks/confirm.html
[5]: http://buildingfirefoxos.com/building-blocks/drawer.html
[6]: http://buildingfirefoxos.com/building-blocks/edit-mode.html
[7]: http://buildingfirefoxos.com/building-blocks/filters.html
[8]: http://buildingfirefoxos.com/building-blocks/headers.html
[9]: http://buildingfirefoxos.com/building-blocks/input-areas.html
[10]: http://buildingfirefoxos.com/building-blocks/lists.html
[11]: http://buildingfirefoxos.com/building-blocks/progress-and-activity.html
[12]: http://buildingfirefoxos.com/building-blocks/scrolling.html
[13]: http://buildingfirefoxos.com/building-blocks/seek-bars.html
[14]: http://buildingfirefoxos.com/building-blocks/status.html
[15]: http://buildingfirefoxos.com/building-blocks/switches.html
[16]: http://buildingfirefoxos.com/building-blocks/tabs.htm
[17]: http://buildingfirefoxos.com/building-blocks/toolbars.html
[18]: http://buildingfirefoxos.com/building-blocks/value-selector.html
[19]: http://buildingfirefoxos.com/transitions/app-invokes-app.html
[20]: http://buildingfirefoxos.com/downloads/
[21]: http://w3.org/TR/2013/WD-components-intro-20130606/
[22]: http://polymer-project.org/ "Polymer"
[23]: http://mozbrick.github.io/ "MozBrick"
[24]: http://mozbrick.github.io/docs/brick-appbar.html
[25]: http://mozbrick.github.io/docs/brick-calendar.html
[26]: http://mozbrick.github.io/docs/brick-deck.html
[27]: http://mozbrick.github.io/docs/brick-flipbox.html
[28]: http://mozbrick.github.io/docs/brick-layout.html
[29]: http://mozbrick.github.io/docs/brick-action.html
[30]: http://mozbrick.github.io/docs/brick-tabbar.html
[31]: http://mozbrick.github.io/docs/brick-form.html
[32]: http://mozbrick.github.io/docs/brick-menu.html
[33]: http://mozbrick.github.io/docs/brick-storage-indexeddb.html
[34]: https://github.com/alexgibson/concierge "Concierge"
[35]: http://alxgbsn.co.uk/concierge/ "Concierge Demo"
[36]: https://mozilla.org/it/firefox/developer/ "Firefox Developer Edition"
[37]: http://mte90.github.io/Brickly

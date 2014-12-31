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
Non è finita qui ci sono anche le [transizioni][19] e per i grafici ci sono anche i file [psd][20].  

## Web Components

Sono in [Working Draft][21] dal W3C e supportati da Chrome e Firefox.  
Si tratta di nuovi elementi (i widget in poche parole) con tag HTML personalizzati che sfruttano lo Shadow DOM per simulare nuove tag HTML.  
La libreria [Polymer][22] di Google è integrata in [Brick 2.0][23] di Mozilla e ne includono già pronte come un calendario o la barra di stato.  
In questa guida li introdurremo semplicemente senza andare nei dettagli (un po' come abbiamo fatto con Gaia Building Blocks).  
Queste interfacce sono degli oggetti che espongono dei metodi a seconda delle necessità e funzionalità dell'elemento che stiamo utilizzando.

Attualmente sono disponibili: 

* [Barra dell'applicazione][24]
* [Calendario][25]
* [Deck o schermata][26]
* [FlipBox][27]
* [Layout (un contenitore)][28]
* [Action][29]
* [Barra di schede][30]
* [Form][31]
* [Menu][32]
* [Storage-IndexdDB][33]

Per mostrare l'API e la facilità d'uso di alcuni di questi componenti, Daniele ha realizzato un'interfaccia interattiva che mostra il codice Javascript e HTML di nome [Brickly](http://mte90.github.io/Brickly).  
Non è nell'interesse della guida approfondire questa libreria ma solo rendere a conoscenza di questo materiale già disponibile all'uso.

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
[21]: http://www.w3.org/TR/2013/WD-components-intro-20130606/
[22]: http://www.polymer-project.org/
[23]: http://mozbrick.github.io/
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


##Hosting App su Github
Github offre sui suoi server un servizio di web hosting, questo capitolo tratterà di come sfruttare Github per distribuire la propria applicazione hosted sulla rete. 
Come prima cosa è necessario registrarsi su Github ed affettuare l'accesso. Nella schermata che troverete davanti (detta *Dashboard*) alla destra della vostra immagine di profilo c'è un icona a forma di "più" che permette di creare una *repository*.  

Una repository può essere descritta semplicemente come una cartella che contiene un progetto e la storia dei suoi file da quando l'avete creata. Questo ci permette di tenere traccia delle modifiche ai file nel tempo.  

![aggiungi una repository][addRepo]

Verrete indirizzati alla schermata di creazione della repository; qui dovrete inserire il nome della vostra applicazione e una breve descrizione della stessa, lasciando i restanti campi immodificati premete **create repository**. La repository sarà quindi creata automaticamente e vi troverete nella pagina del progetto.

![crea nuova repository][createRepo]

In questa nuova schermata è presente una barra sulla destra che permette di gestire il progetto, fate click su **Settings**  
![settings][settings]   
e scorrete fino alla sezione che ha per titolo **Github Pages** dove troverete il pulsante **Automatic Page Generator**, premetelo.

![genera pagina automatica][gitpages]

La pagina che verrà creata servirà come base per l'applicazione, motivo per cui non dovremo perdere tempo a modificare i contenuti o a scegliere il layout: la pagina generata verrà scartata in favore della nostra applicazione. Nella prima pagina **New project site** fate click su **continue to layouts** senza modificare nulla e nella pagina di scelta del layout premete **publish page**.  

Github creerà quindi un sito per il vostro progetto che sarà visitabile da chiunque all'indirizzo: ``http://miousername.github.io/nomedelprogetto``. Potete trovare l'indirizzo completo nella pagina Settings della vostra repository.
Seguendo i passaggi sopra elencati il sito sarà così realizzato (titolo e sottotitolo dipenderanno dal nome e dalla descrizione):

![Alt text][defaultPage]

Per far si che l'app sia effettivamente installabile occorre modificare il file "manifest.webapp". In particolare bisogna sostituire nel campo "launch_path" il nuovo indirizzo del vostro file index.html  
Se ricordate l'indirizzo che avrà il vostro progetto sarà circa: ``http://miousername.github.io**/nomedelprogetto**``,
il manifesto deve quindi essere così modificato
    
     "launch_path" : "/nomedelprogetto/index.html" 
     
Per la corretta visualizzazione delle icone è necessario aggiornare anche il campo "icons"  

    "icons" : {
        "128" : "/nomedelprogetto/cartellaIcone/icona128.png",
        "60" : "/nomedelprogetto/cartellaIcone/icona60.png"
        }
     
Infine per caricare l'applicazione è necessario installare sul computer un software distribuito da Github; Per Windows tale programma è disponibile con interfaccia grafica o tramite un terminale apposito (Git Power Shell), mentre per GNU/Linux è disponibile solo su terminale, questa guida per semplicità farà riferimento ai comandi da eseguire da terminale.

Per iniziare è necessario clonare la repository sul proprio pc digitando questi comandi nel terminale:    
    
    $ git clone https://github.com/miousername/nomedelprogetto.git
    
Ora bisogna sostituire il contenuto della cartella *nomedelprogetto* con i file che compongono la vostra applicazione, questa operazione per semplicità può essere eseguita tramite il file manager.-**ATTENZIONE: Solo i file, non la cartella che li contiene** -.  

In seguito per aggiornare i file digitare:  
    
    $ cd nomedelprogetto
    $ git add -A
    $ git commit -m "hosting app"
    $ git push origin gh-pages
    
Inserite le vostre credenziali per avviare il caricamento dei file. Visitando l'indirizzo del vostro progetto ora vedrete anzichè la pagina generata automaticamente l'*Homepage* della vostra applicazione. **NOTA:Può capitare a volte che la modifica della pagina mostrata impieghi anche 30 minuti.**

Ultima tappa è la pubblicazione sul Firefox Marketplace. Accedete o registratevi al Firefox Marketplace come sviluppatori, nella pagina "Carica un'app" selezionate "Hosted app" e inserite l'indirizzo del **manifesto** ossia: ``http://miousername.github.io/nomedelprogetto/manifest.webapp``

[addRepo]:images/originals/git-addRepo.png
[createRepo]:images/originals/git-createRepo.png
[settings]:images/originals/git-settings.png
[gitpages]:images/originals/git-gitpages.png
[defaultPage]:images/originals/git-defaultPage.png

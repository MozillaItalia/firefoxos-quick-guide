#Altro

In questo capitolo vedremo in modo veloce alcune tecnologie che ci possono essere utili nello sviluppo per Firefox OS.

##Gaia Building Blocks

Per chi è abituato ad utilizzare i framework CSS sarà molto semplice capire l'utilità di Building Blocks. Questo framework già citato è utilizzato nel boilerplate ed in molte applicazioni presenti sul marketplace.  
Si tratta di un framework CSS basato sulle release giornaliere di Gaia che permette di avere sempre le ultime novità.  
Come si può vedere dal sito [http://buildingfirefoxos.com/](http://buildingfirefoxos.com/building-blocks/) ci sono moltissimi esempi riguardo:  

* [Action menu](http://buildingfirefoxos.com/building-blocks/action-menu.html)
* [Buttons](http://buildingfirefoxos.com/building-blocks/buttons.html)
* [Confirm](http://buildingfirefoxos.com/building-blocks/confirm.html)
* [Drawer](http://buildingfirefoxos.com/building-blocks/drawer.html)
* [Edit Mode](http://buildingfirefoxos.com/building-blocks/edit-mode.html)
* [Filters](http://buildingfirefoxos.com/building-blocks/filters.html)
* [Headers](http://buildingfirefoxos.com/building-blocks/headers.html)
* [Input Areas](http://buildingfirefoxos.com/building-blocks/input-areas.html)
* [Lists](http://buildingfirefoxos.com/building-blocks/lists.html)
* [Progress And activity](http://buildingfirefoxos.com/building-blocks/progress-and-activity.html)
* [Scrolling](http://buildingfirefoxos.com/building-blocks/scrolling.html)
* [Seek Bars](http://buildingfirefoxos.com/building-blocks/seek-bars.html)
* [Status](http://buildingfirefoxos.com/building-blocks/status.html)
* [Switches](http://buildingfirefoxos.com/building-blocks/switches.html)
* [Tabs](http://buildingfirefoxos.com/building-blocks/tabs.html)
* [Toolbars](http://buildingfirefoxos.com/building-blocks/toolbars.html)
* [Value Selector](http://buildingfirefoxos.com/building-blocks/value-selector.html)

Come si può vedere ci sono molte interfacce ed opzioni possibili per avere la stessa grafica del sistema un modo semplice. Inoltre c'è una sezione dedicata alle icone tramite Font Icon.  
Per non finire qui ci sono anche le [transizioni](http://buildingfirefoxos.com/transitions/app-invokes-app.html) e per i grafici ci sono anche i file [psd](http://buildingfirefoxos.com/downloads/).  

##Web Components
Sono in [Working Draft](http://www.w3.org/TR/2013/WD-components-intro-20130606/) dal W3C e supportati da Chrome e Firefox.  
Si tratta di nuovi elementi (i widget in poche parole) con tag HTML personalizzati che sfruttano lo Shadow DOM per simulare nuove tag HTML.  
La libreria [Polymer](http://www.polymer-project.org/) di Google è integrata in [Brick] 2.0(http://mozbrick.github.io/) di Mozilla e ne includono già pronte come un calendario o la barra di stato.  
In questa guida li introdurremo semplicemente senza andare nei dettagli (un po come abbiamo fatto con Gaia Building Blocks).  
Queste interfacce sono degli oggetti che espongono dei metodi a seconda delle necessità e funzionalità dell'elemento che stiamo usando.   
Attualmente sono disponibili: 

* [Barra dell'applicazione](http://mozbrick.github.io/docs/brick-appbar.html)
* [Calendario](http://mozbrick.github.io/docs/brick-calendar.html)
* [Deck o schermata](http://mozbrick.github.io/docs/brick-deck.html)
* [FlipBox](http://mozbrick.github.io/docs/brick-flipbox.html)
* [Layout (un contenitore)](http://mozbrick.github.io/docs/brick-layout.html)
* [Action](http://mozbrick.github.io/docs/brick-action.html)
* [Barra di schede](http://mozbrick.github.io/docs/brick-tabbar.html)
* [Form](http://mozbrick.github.io/docs/brick-form.html)
* [Menu](http://mozbrick.github.io/docs/brick-menu.html)
* [Storage-IndexdDB](http://mozbrick.github.io/docs/brick-storage-indexeddb.html)

Per mostrare l'API e la facilità d'uso di alcuni di questi componenti Daniele ha realizzato un'interfaccia interattiva che mostra il codice Javascript ed HTML di nome [Brickly](http://mte90.github.io/Brickly).  
Non è nell'interesse della guida approfondire questa libreria ma solo rendere a conoscenza di questo materiale già disponibile all'uso.
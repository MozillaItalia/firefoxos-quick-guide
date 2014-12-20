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

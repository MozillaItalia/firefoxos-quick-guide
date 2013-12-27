# Ambiente di sviluppo per Firefox OS {#setup}

## Il motore Gecko
I browser utilizzano diversi motori di rendering per le pagine web: Google Chrome ed Opera usano Blink (un fork di WebKit), Internet Explorer usa Trident, mentre Safari usa WebKit. Mozilla ha il suo engine, chiamato Gecko che viene usato da Firefox desktop, Firefox per Android, e Firefox OS. Poichè questi prodotti usano lo stesso motore o engine, è possibile sviluppare per Firefox OS usando il browser Firefox per il desktop (con alcuni svantaggi[^engine]).

[^engine]: Anche se utilizzano lo stesso motore è usato per tutti i prodotti di Mozilla, la versione del motore in Firefox OS è basato generalmente sulla versione  desktop del browser. Questo perchè il ciclo di rilascio di Firefox OS è più lento della versione Desktop. In pratica, questo vuol dire che alcune funzionalità non sono disponibili (o non funzionano come immaginato) quando si prova ad usarli su Firefox OS - quindi verifica sempre che la tua applicazione funzioni su un dispositivo con Firefox OS. Inoltre, bisogna ricordarsi che gli utenti possono usare versioni differenti di Firefox OS, quindi potrebbero non avere tutte le funzionalità richieste. Assicurati di fornire sempre un'alternativa in caso alcune di queste funzionalità non sia disponibile.

## Di cosa hai bisogno?

Per sviluppare e testare le applicazioni realizzate per Firefox OS hai bisogno di:

 * Una versione recente di [Firefox desktop](http://getfirefox.com).
 * [Firefox OS Simulator](https://addons.mozilla.org/en-US/firefox/addon/firefox-os-simulator/). 
 * Un editor testuale per programmare[^editor].
 
[^editor]: Ci sono molti buoni editor con diversi livelli di complessità e caratteristiche. Uno veramente popolare che io consiglio per chi non ne ha uno preferito è [SublimeText](http://sublimetext.com/). Personalmente, io uso [WebStorm](http://www.jetbrains.com/webstorm/) che è un IDE completo per la realizzazione di web app.
  
## Installare il Simulatore di Firefox OS

Dopo aver installato Firefox,  il passaggio successivo è l'installazione del simulatore di Firefox OS che può essere usato per testare le proprie applicazioni. Con Firefox installato e funzionante, vai nel menu **Strumenti** e seleziona **Add-on**.

![*Strumenti* con *Add-ons** selezionato](images/originals/tools.png)

Usando il campo di ricerca nell'angolo in altro a destra, cerca per **Firefox OS Simulator** e installa l'add-on cliccando il pulsante di installazione.

![Gestore degli addon con la ricerca](images/originals/addons-simulator.png)

Dopo l'installazione dell'add-on, potrai accedere al simulatore andando al menu **Strumenti -> Web Developer -> Firefox OS Simulator**. 

![Dove puoi trovare il simulatore una volta installato](images/originals/tools-web-developer-simulator.png)

Altrimenti, puoi andare nella pagina del [Firefox OS Simulator](https://addons.mozilla.org/en-US/firefox/addon/firefox-os-simulator/), scarica il simulatore da qui. 

## Riassunto

In questo capitolo abbiamo imparato come sviluppare applicazioni per Firefox OS con Firefox browser e Firefox OS Simulator (con un buon editor).

Ora hai configurato il tuo ambiente di sviluppo, adesso vedremo i concetti base per costruire la tua prima applicazione.

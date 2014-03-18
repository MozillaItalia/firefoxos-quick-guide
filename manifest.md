# Il Manifest

## Che cos'è e a cosa serve

Il manifest è un file centrale nell'ecosistema di un applicazione FirefoxOS, poichè rappresenta i **metadati** dell'applicazione.
Questi metadati servono al sistema per vari scopi, come conoscere quali funzionalità vuole utilizzare l'applicazione o le credenziali dell'autore o dell'applicazione stessa da parte del sistema e del Mozilla Marketplace.
Tecnicamente il manifest è definito in un file chiamato *manifest.webapp* ed è costituito da codice **JSON**, ovvero un linguaggio di descrizione con una sintassi più leggera rispetto al XML e simile al Javascript.

## Il nostro primo Manifest

Questo è un manifest di esempio fornito dalla documentazione ufficiale del Mozilla Developer Network
```JSON
{
  "name": "My App",
  "description": "My elevator pitch goes here",
  "launch_path": "/index.html",
  "icons": {
    "128": "/img/icon-128.png"
  },
  "developer": {
    "name": "Your name or organization",
    "url": "http://your-homepage-here.org"
  },
  "default_locale": "en"
}
```
Come possiamo notare, il manifest è composto da una serie di campi chiave/valore, che descrivono le proprietà dell'applicazione.
Il sistema richiede obbligatoriamente solo *name*, *description* e *icons*, ma è buona norma inserire anche il campo *launch_path* che indica il collegamento al file da avviare e il campo *developer* che con le sue proprietà *name* e *url* definiscono, rispettivamente, nome e url dello sviluppatore dell'applicazione (utili nel caso vogliate pubblicare la vostra app sul Mozilla Marketplace)

## Le proprietà del Manifest

Il manifest supporta una marea di proprietà, perciò cercerò di spiegarvi il funzionamento e l'utilità di ogni campo.

**activities**

la proprietà *activities* specifica quali *Web Activities* supporta la nostra applicazione, in sostanza una web activities è un task richiamato da un'altra applicazione, che si appoggia alla vostra per un determinato compito.
Volendo fare un esempio, se voi sviluppate un applicazione che permette di condividere le vostre foto su di un sito, potreste implementare la web activities *share*, in questo modo, quando l'utente prova a condividere una foto dall'app galleria, apparirà anche la vostra applicazione tra quelle che possono svolgere questo compito.
La sintassi di questo campo è un po' complessa, per questo vi rimando alla pagina di documentazione sull' [MDN] (https://developer.mozilla.org/en-US/docs/WebAPI/Web_Activities)

**appcache_path**

questa proprietà vi consente di specificare il percorso del manifest della cache della vostra app, dovete specificarla solo se utilizzate questa tecnologia per il mantenimento di alcune funzione dell'applicazione quando il terminale va offline.
[documentazione] (https://developer.mozilla.org/en-US/docs/HTML/Using_the_application_cache)

**chrome**

il campo *chrome* indica se la vostra applicazione fa uso dei pulsanti di navigazione predefiniti dal sistema come nell'immagine
![chrome](https://github.com/giammyjet/firefoxos-quick-guide/blob/0.3/images/new/nav-both2.png?raw=true)
*nota*: tieni presente che questa funzionalità va utilizzata se e solo se non si può fare altro, poichè le linee guida di user experience prevedono l'inserimento di un tasto *back* da parte dell'applicazione
la sintassi della proprietà è la seguente:
```JSON
"chrome": { "navigation": true }
```

**csp**

Applica una "Content Security Policy" all'applicazione.
[Per ulteriori informazioni] (https://developer.mozilla.org/en-US/Apps/CSP)

**default_locale**

necessaria quando è presente la proprietà *locales*, indica qual'è la lingua predefinita dell'applicazione e quella che verrà usata se nel sistema è impostata una lingua non presente nella vostra app.
Esempio per l'inglese
```JSON
"default_locale": "en"
```

**description**

La descrizione dell'applicazione (massimo 1024 caratteri)

**developer**

Abbiamo incontrato questa proprietà nel manifest di prova, indica chi è lo sviluppatore e qual'è il suo sito web

**fullscreen**

Se impostata a *true*, metterà la vostra applicazione a schermo intero (utile per i giochi)

**icons**

Anche questa proprietà era presente nell'esempio, serve ad impostare le icone dell'applicazione

**installs_allowed_from**

indica una serie di siti a cui è permesso installare l'applicazione (diciamo che è inutile se pubblicate la vostra app solo nel mozilla marketplace)

**launch_path**

il file home della vostra applicazione

**locales**

indica altri dati del vostro manifest specifici per determinate lingue.
esempio:
```JSON
"locales": {
"es": {
  "description": "¡Acción abierta emocionante del desarrollo del Web!",
  "developer": {
    "url": "http://es.mozillalabs.com/"
  }
},
"it": {
  "description": "Azione aperta emozionante di sviluppo di fotoricettore!",
  "developer": {
    "url": "http://it.mozillalabs.com/"
  }
}
}
```

**messages**

indica quali messaggi del sistema la vostra app può leggere
esempio:
```JSON
"messages": [
  { "telephony-new-call": "/dialer/index.html#keyboard-view" },
  { "bluetooth-dialer-command": "/dialer/index.html#keyboard-view" },
  { "headset-button": "/dialer/index.html#keyboard-view" },
  { "notification": "/dialer/index.html#keyboard-view" },
  { "alarm": "/facebook/fb_sync.html" }
]
```

La documentazione di mozilla spiega che quando, ad esempio, avviene l'evento *telephony-new-call* si apre la pagina /dialer/index.html con *anchor* impostato a #keyboard-view

**name**

indovinate? il nome della vostra app 

**orientation**

questa proprietà

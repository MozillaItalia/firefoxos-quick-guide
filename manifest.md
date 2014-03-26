# Il Manifest

## Che cos'è e a cosa serve

Il *manifest.webapp* è un file importante in Firefox OS, poichè contiene i **metadati** dell'applicazione.
Questi metadati servono al sistema per sapere il nome dello sviluppatore, la versione, i permessi richiesti per le varie API, l'icona, le lingue in cui è disponibile e molto altro.
QUesto file è scritto in **JSON**, ovvero un linguaggio di catalogazione di dati con una sintassi più leggera rispetto al XML e derivata da Javascript.

## Il nostro primo Manifest

Questo è un manifest di esempio fornito dalla documentazione ufficiale del Mozilla Developer Network:

```
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
Il sistema richiede obbligatoriamente solo *name*, *description* e *icons*, il campo *launch_path* indica il collegamento al file da avviare (necessario se è di tipo *packaged*) e il campo *developer* che con le sue proprietà *name* e *url* definiscono, rispettivamente, nome e url dello sviluppatore dell'applicazione (utili nel caso vogliate pubblicare la vostra app sul Mozilla Marketplace).

## Le proprietà del Manifest

Il manifest supporta una marea di proprietà, perciò vediamo il funzionamento e l'utilità di ogni campo.

**activities**

la proprietà *activities* specifica quali *Web Activities* supporta la nostra applicazione.  
Una web activities è un task richiamato da un'altra applicazione, che si appoggia alla vostra per un determinato compito.
Volendo fare un esempio, se voi sviluppate un applicazione che permette di condividere le vostre foto su di un sito, potreste implementare la web activities *share*, in questo modo, quando l'utente prova a condividere una foto dall'app galleria, apparirà anche la vostra applicazione tra quelle che possono svolgere questo compito.  
La sintassi di questo campo è un pò complessa, per questo vi rimando alla pagina di documentazione su [MDN](https://developer.mozilla.org/en-US/docs/WebAPI/Web_Activities).

**appcache_path**

Questa proprietà vi consente di specificare il percorso del manifest.appcache, dovete specificarla solo se utilizzate AppCache all'interno della vostra applicazione.  
AppCache è uno standard W3C che permette di mettere in cache alcuni file e molto altro per maggiori informazioni vi rimando alla documentazione su [MDN](https://developer.mozilla.org/en-US/docs/HTML/Using_the_application_cache).

**chrome**

Il campo *chrome* indica se la vostra applicazione fa uso dei pulsanti di navigazione predefiniti dal sistema come nell'immagine  
![chrome](images/originals/nav-both2.png)  
*Nota*: tieni presente che questa funzionalità va utilizzata solo se non è possibile implementare una soluzione propria, poichè le linee guida per l'user experience prevedono l'inserimento di un tasto *back* da parte dell'applicazione.  
La sintassi della proprietà è la seguente:
```
"chrome": { "navigation": true }
```

**csp**

Applica una "Content Security Policy" all'applicazione, per ulteriori informazioni vi rimando alla pagina di documentazione su [MDN](https://developer.mozilla.org/en-US/Apps/CSP)

**default_locale**

Questo parametro è necessario quando è presente la proprietà *locales*, indica qual'è la lingua predefinita dell'applicazione e quella che verrà usata se nel sistema è impostata una lingua non presente nella vostra app.  

Esempio per l'inglese
```
"default_locale": "en"
```

**description**

La descrizione dell'applicazione (massimo 1024 caratteri), siate il più chiari e sintetici possibile perchè è il tasto che verrà visualizzato sul Mozilla Marketplace (successivamente si può modificare).

**developer**

Abbiamo incontrato questa proprietà nel manifest di prova, indica chi è lo sviluppatore e qual'è il suo sito web.

**fullscreen**

Se impostata a *true*, metterà la vostra applicazione a schermo intero (utile per i giochi) nscondendo la barra delle notifiche.

**icons**

Anche questa proprietà era presente nell'esempio, serve ad impostare le varie dimensioni delle icone dell'applicazione.  
CI sono più versioni dela stessa icona a dimensioni diverse perchè a seconda dell'interfaccai o della schermata che mostra l'applicazione verrà usata quella più idonea.  
Alcune dimensioni sono obbligatorie per il Mozilla Marketplace.

**installs_allowed_from**

Indica una serie di siti a cui è permesso installare l'applicazione (questo campo è inutile se pubblicate la vostra app solamente nel Mozilla Marketplace).

**launch_path**

Ne abbiamo già parlato nel codice di esempio più in alto.  
Questo campo indica il percorso di lancio dell'applicazione che deve essere relativo ed è obbligatorio per le app packaged.

**locales**

QUesta proprietà ci permette di impostare i dati come URL o description per le varie lingue in cui è rilasciata l'app.  
Esempio:
```
"locales": {
"es": {
  "description": "¡Acción abierta emocionante del desarrollo del Web!",
  "developer": {
    "url": "http://es.mozillalabs.com/"
  }
},
"it": {
  "description": "Emozionati nello sviluppo libero del Web!",
  "developer": {
    "url": "http://it.mozillalabs.com/"
  }
}
}
```

**messages**

Indica quali messaggi del sistema la vostra app può leggere per eseguire del codice specifico.  
esempio:
```
"messages": [
  { "telephony-new-call": "/dialer/index.html#keyboard-view" },
  { "bluetooth-dialer-command": "/dialer/index.html#keyboard-view" },
  { "headset-button": "/dialer/index.html#keyboard-view" },
  { "notification": "/dialer/index.html#keyboard-view" },
  { "alarm": "/facebook/fb_sync.html" }
]
```
Come si può vedere, per esempio, con *telephony-new-call* allo scatenarsi di questo evento verrà aperta la pagina /dialer/index.html all'ancora #keyboard-view.

**name**

Indovinate? Il nome della vostra app!

**orientation**

Questa proprietà imposta l'orientamento predefinito dell'applicazione, i due valori ammessi sono "landscape" e "portrait" (predefinito).  

**origin**

Indica un'URL che l'applicazione può utilizzare al posto dell'UUID, è raro utilizzare questo valore.  

**permissions**

Proprietà molto importante, permette di chiedere all'utente il permesso di utilizzare elementi specifici del telefono, come la geolocalizzazione.
Esempio:  
```
"permissions": {
  "contacts": {
    "description": "Required for autocompletion in the share screen",
    "access": "readcreate"
    },
  "alarms": {
    "description": "Required to schedule notifications"
  }
}
```
Come potete vedere richiede due permessi: ovvero l'accesso all'elenco dei contatti in modalità lettura/creazione e la possibilità di usare la sveglia.  
Inoltre bisogna fornire due ulteriori campi, un campo *description* in cui bisogna spiegare all'utente a cosa ci serve il permesso e un campo *access* opzionale in cui specificate il grado d'accesso.
I valori possibili sono *readonly*, *readwrite*, *readcreate* e *createonly*.

**redirects**

Permette di impostare un redirect da un sito esterno, per esempio per ragioni di autenticazione.  
Richiede un campo *from* di input e uno *to* di elaborazione.

**type**

Indica se la vostra app è *web*, *privileged* o *certified*. Le certified sono particolari e la loro certificazione avviene solo tramite il Mozilla Marketplace o tramite il debug remoto.

**version**

Il numero di versione della vostra app sotto forma di stringa.

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

prova
-----

# HTTP

HTTP è lo standard base con cui vengono spediti i documenti attraverso la rete ovvero è la base stessa della rete come la conosciamo adesso. Quando digiti www.google.com nella barra degli indirizzi stai dicendo al tuo browser fare una richiesta HTTP ad un secondo computer che si chiama www.google.com e di mostrarti ciò che torna indietro.

Capisci subito che dovremo fare la stessa cosa se vogliamo ottenere dei dati per la nostra applicazione e questi dati si trovano su internet. Fare una richiesta, aspettare una risposta, leggere i dati, scegliere quali servono e visualizzarli.

Ma come diavolo faccio a ottenere un browser che vada prendere questi dati e farlo funzionare dentro alla mia app? Ecco che arriva il nostro eroe: XMLHttpRequest.

# XMLHttpRequest

XMLHttpRequest è uno strumento disponibile attraverso JavaScript che si comporta come il browser del nostro PC; fa richieste, ottiene risposte e se non ci sono problemi espone i dati delle risposte al resto del codice.

Per tutta la documentazione del caso puoi controllare su [MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) la Mozilla Developer Network, un'enciclopedia per sviluppatori web scritta da sviluppatori web.

HMLHttpRequest è un costruttore, noi gli passiamo dei parametri, come l'indirizzo da controllare, i dati da inserire nella richiesta..., e lui ci restituisce un oggetto con dei metodi che possiamo usare per fare la nostra richiesta e ottenere dei dati.

~~~~~~~~
// adesso la variabile xhr contiene un oggetto XMLHttpRequest che possiamo usare
var xhr = new XMLHttpRequest();
~~~~~~~~

# Richieste Cross-Domain

Putroppo XMLHttpRequest è uno strumento che fa molta gola ai malviventi perché può indipendentemente spedire e ricevere dati quindi è stato fin da subito limitato a fare richieste esclusivamente sul dominio d'origine della pagina. Questo vuol dire che sulla pagina www.google.com possono esserci richieste tramite XMLHttpRequeste solo alla pagina www.google.com .

Questo comportamento può essere cambiato da lato server ovvero se voi gestite i dati su due domini diversi allora potete scambiarveli indipendentemente da dove siate ma questo non è il nostro caso.

Noi abbiamo una pagina web che viene presentata su di un telefono, non un server con i dati che mi interessano, quindi dobbiamo richiedere i permessi di fare richieste a enti esterni alla nostra app.

## systemXHR

Apriamo quindi il nostro file manifest.webapp e aggiungiamo alla parte "permission" un nuovo attributo.

```JSON
...
"permissions": {
        "systemXHR": {
            "description": "Inserire motivazione per richiedere il permesso"
        }
}
...
```
Il campo "description" è facoltativo ma io consiglio di inserirlo perché in questo modo l'utente sa cosa fate con il suo permesso.

## mozSystem

Dobbiamo quindi prepararci a fare la richiesta, ci serve XMLHttpRequest:
```javascript
var xhr = XMLHttpRequest();
```
Solo che così non è ancora funzionante, abbiamo bisogno di settare la proprietà __mozSystem__ a true.

```javascript
var xhr = XMLHttpRequest({ mozSystem: true });
```

Adesso `xhr` può essere usato per fare la richiesta che vogliamo ad un qualsiasi indirizzo sul web.

## mozAnonim

Questa è una nuova proprietà dell'oggetto XMLHttpRequest che potete assegnare a true se volete che non vengano mandati cookies o riferimenti all'utente della vostra app al dominio a cui fate richieste.

```javascript
var xhr = XMLHttpRequest({ mozAnonim: true });
```
Adesso sapete come attivare le richieste nella vostra app e come anonimizzarle per proteggere la privacy dei vostri utenti, è venuto il momento di sporcarsi le mani e lavorare.

# Caso di studio: dati meteo

Adesso impareremo a chiedere dei dati tramite la libreria jQuery; perché jquery e non XMLHttpRequest?

Il confronto si vede subito:

### jQuery
```javascript
$.get('http://www.google.com', function () {
    console.log('ricevuta risposta');
});
```
### JavaScript puro
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'http://www.google.com', true);
xhr.onreadystatechanged = function () {
    if(xhr.readyState === 4 && xhr.status === 200){
    console.log('ricevuta risposta');
    }
};
xhr.send(null);
```

La scrittura di codice tramite la libreria jQuery è molto più succinta e meno esoterica quindi più leggibile e meno soggetta ad errori. Niente vi ferma da usare JavaScript allo stato puro ma ben presto capirete che è meglio concentrare le forze su altri problemi.

## OpenWeatherMap

OpenweatherMap è un progetto che mette a disposizione su internet i dati meteo raccolti da centraline sparse per il mondo e, indovinate un po', le richieste si fanno tramite il protocollo HTTP!

esempio: il meteo a [Firenze](http://api.openweathermap.org/data/2.5/weather?q=Firenze,it). Se clicci su questo link vieni indirizzato ad una pagina in cui trovi del testo simile a questo:

```JSON
{"coord":{"lon":11.25,"lat":43.77},"sys":{"type":1,"id":5861,"message":0.1951,"country":"IT","sunrise":1413437464,"sunset":1413476992},"weather":[{"id":803,"main":"Clouds","description":"broken clouds","icon":"04d"}],"base":"cmc stations","main":{"temp":294.01,"pressure":1015,"humidity":73,"temp_min":293.15,"temp_max":295.15},"wind":{"speed":2.6,"deg":220,"var_beg":200,"var_end":270},"clouds":{"all":75},"dt":1413468951,"id":3176959,"name":"Firenze","cod":200}
```

Questo testo assomiglia molto all'oggetto _Object_ che abbiamo a disposizione in JavaScript e infatti non è altro che [JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON) ovvero una stringa di testo nella notazione JavaScript Object Notation.

Adesso vedremo come fare la richiesta tramite jQuery e come fare il parsing della risposta, ovvero come riusciremo ad includere questi dati in una pagina web.

```javascript
$.get('http://http://api.openweathermap.org/data/2.5/weather?q=Firenze,it', function (response){
   console.log(JSON.stringify(response));
});
``` 

Questo frammento di codice effettua la richiesta al sito e, quando riceve una risposta stampa nella console la rappresentazione in forma di stringa dell'oggetto che ci hanno mandato come risposta.

## Usare jQuery in Firefox OS

Il motivo per cui usiamo jQuery è che sotto il cofano, nascosto alla vista, quando noi scriviamo $.get('qualche sito', function (){...}) in realtà chiediamo a jQuery di configurare al posto nostro un oggetto XMLHttpRequest per fare la richiesta; quindi possiamo modificare il risultato di questa operazione per fare il modo che XMLHttpRequest venga configurato in modo corretto con le proprietà __mozSystem__ e __mozAnonim__.

Prima di fare una qualsiasi richiesta configuriamo una volta per tutte jQuery, in modo da non dovercene più preoccupare.

```javascript
$.ajaxSetup({
    xhr: function () {
    return new XMLHttpRequest({ mozSystem: true, mozAnonim: true});
}
});
```
Queste cinque righe di codice istruiscono jQuery dicendo: "quando andrai a fare una richiesta web, usa questo oggetto XMLHttpRequest per lavorare".

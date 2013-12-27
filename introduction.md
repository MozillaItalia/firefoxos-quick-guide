# Introduction {#introduction}

## Firefox OS

![Firefox OS](images/originals/firefox_os_simulator.png)

[Firefox OS](http://www.mozilla.org/firefox/os/) è una nuova piattaforma mobile sviluppata da [Mozilla](http://mozilla.org) e i suoi partner. Dispositivi con Firefox OS sono già disponibili in molti paesi e arriveranno anche in molti altri posti entro la fine di quest'anno.

Mirato per lo sviluppo di nuovi mercati, Firefox OS ha la missione di portare il prossimo bilione di persone online. Per raggiungere questo obiettivo, i dispositivi con Firefox OS sono costruiti per fornire un *ottimo primo smartphone* con prezzi competitivi. I dispositivi con Firefox OS non devono essere confrontati con smartphone di fascia alta come Apple iPhone 5S e Samsung Galaxy S4; sono realizzati per essere un'alternativa ai telefoni avanzati così le persone che usano questi dispositivi possono fare il passaggio a Firefox OS ad un costo accessibile e ricevere una *esperienza smartphone completa*.

Nei mercati in sviluppo come il Brasile o la Colombia, smartphone con prestazioni decenti sono solitamente troppo costosi per il consumatore medio.
Le persone possono comprare telefoni a basso costo, le piattaforme di questi telefoni sono pensate per dispositivi di fascia alta - quindi hardware del telefono tende ad avere problemi di performance, che comporta una terribile esperienza utente. Firefox OS è progettato specificamente per funzionare su hardware limitato fornendo una'esperienza utente decente. 

Un'altro fattore per la sua unicità è l'apertura di Firefox OS. Considera che i sistemi operativi mobile attuali sono dei silos proprietari, dove ogni produttore ha il privilegio di obbligare gli sviluppatori ed utenti ai loro desideri a prescindere della loro volontà (ricordi quando la Apple ha vietato dei linguaggi diversi da Objective-C nel suo app Store). In questi ecosistemi proprietari puoi distribuire le applicazioni solo su canali autorizzati - e il venditore ottiene una commessa sugli acquisti effettuati dal dispositivo.

Oltre a bloccare gli sviluppatori su canali di sviluppo proprietari, questi sistemi bloccano gli sviluppatori sui loro software development kits (SDK). Se vuoi realizzare una app nativa sia per iOS e Android usando i sistemi ufficiali sarà necessario programmare un'app in Objective-C ed un'altra in Java rispettivamente. Questo significa che uno sviluppatore saggio riutilizzerà poco tra i vari progetti (magari riutilizzare anche del materiale multimediale). Questo significa che uno sviluppatore conosca due linguaggi e realizzi lo stesso software due volte. 

Firefox OS si differenzia usando "HTML5" come piattaforma di sviluppo. HTML5 è un termine di marketing usato per indicare la la continua evoluzione degli standard web noto come HTML, CSS e JavaScript. Questi standard royalty free sono supportate dai principali browser web, questo permette di rendere le web app possibili. Sfruttando le tecnologie che includono HTML5, milioni di sviluppatori possono programmare per FireFox OS. Le applicazioni create per FireFox OS sono facili da portare  ad'altre piattaforme usando dei wrapper come [Phonegap](http://phonegap.com).

## The Platform That HTML5 Deserves

The web is everywhere. Its on your computer, mobile phone, smart TV, and even in your video game consoles. The programming language of the web, JavaScript, is one of the most popular languages in the world. As already mentioned, when people talk about HTML5 they usually mean the collection of three technologies known as HTML, CSS and JavaScript. Recent advances in HTML have brought in a range of new features - advanced form controls, Web sockets, and more semantic markup - when compared to XHTML 1.0 and HTML 4.01. Advances in CSS have also introduced lots of new features, such as Flexbox and CSS Animations, that make it a lot easier to create beautiful responsive layouts. And recent advances in JavaScript have brought significant performance improvements and new capabilities, all while remaining easy to use for both beginners and seasoned developers alike.

Firefox OS is in essence, an extension of the mobile web. By making HTML5 a first class citizen, Mozilla has opened its platform to millions of web developers. Even if some other browser vendors implement HTML5 in their mobile offerings, Firefox OS goes beyond that by offering a collection of APIs to access the underlying hardware and system using JavaScript. These APIs are collectively known as the WebAPIs.

## Accessing The Hardware Using The WebAPI

Some earlier platforms also tried to create operating systems that used web technologies for app creation. For example, when the iPhone was introduced to the world, the only way to create apps was using web technologies. However, those web apps were limited in that they had no hardware or device access - meaning that only a limited range of applications could be built. When Apple then allowed developers to code apps in Objective-C, and also access the device's capabilities, it spurred a huge amount of innovation. Sadly, web apps did not gain access to the device's capabilities, and were thus left as "second-class citizens" - this made them unattractive to both users and developers alike, and unable to compete with native apps in that system.

When we say device capabilities we actually mean accessing hardware and OS level features and services: We're talking about things such as updating the address book, sending SMS, and accessing the camera and media gallery. On Firefox OS, the [WebAPI](https://wiki.mozilla.org/WebAPI)s are the means by which you will access many of those capabilities. 

Another earlier platform, WebOS, also offered hardware access via JavaScript but never tried to standardize its APIs. Mozilla is working with the W3C and other stakeholders to make sure that the WebAPIs are an open standard and that other browsers adopt them too. As these APIs are implemented by other browsers, your apps will require less and less changes to work across different platforms.

It's important to emphasize that the WebAPIs are not exclusive to Firefox OS devices. Mozilla is implementing it for the other platforms on which Firefox runs, such as desktop and android. This way, you can use your *open web app* in Firefox OS, Firefox on the desktop and Firefox for Android.

## Freedom to Develop and Distribute

Like everything that Mozilla does, Firefox OS is developed in the open and is free. All development can be followed on [the Mozilla B2G repository](https://github.com/mozilla-b2g/B2G) on GitHub. With Firefox OS you have the freedom to follow and contribute with the development of the system and you also have the freedom to distribute your applications on your own channels or on [The Firefox Marketplace](https://marketplace.firefox.com/). What's really awesome is that all the system applications are written in HTML5, so you can check them out and see how the are put together. 

The main idea is that you're not locked to Mozilla for anything. If you want to pick the source code for the system and change it for your own needs, so be it. If you need to build apps for internal use on your company, or if you want to distribute your creations only on your own web site, you're free to do it. Usually, in other platforms you're locked into the official app store as the only channel to distribute your apps. Firefox OS also has an official market called Firefox Marketplace which has an approval process but you're free to distribute your app outside this store if you want. Like in the web where you can host your web site anywhere you want, on Firefox OS you can do the same with your applications. 

This comes with a small caveat, sadly: some of the WebAPIs are too security sensitive to just allow anyone to use them. To distribute apps that use some of the more "privileged" APIs, you will need to get your applications signed and reviewed by Mozilla's staff. 

## Summary

HTML5 is here to stay and will only get better. Firefox OS is the new open mobile operating system by Mozilla completely based on web technologies. This system is built on the open and offers a robust HTML5 implementation that goes beyond the other platforms by offering the WebAPI which is a collection of APIs to access *hardware and operating system services using JavaScript*. These new APIs are being standardized through the World Wide Web Consortium (W3C) and will hopefully be adopted by other browsers in the future.

In the next chapter we'll quickly get you set up with every you need to develop for Firefox OS. 

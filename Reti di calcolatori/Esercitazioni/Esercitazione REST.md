# Caratteristiche
I Web Service RESTful si basano sullo scambio di messaggi tramite HTTP (GET, POST, PUT e DELETE), il cui contenuto è solitamente JSON o XML. 
REST è un acronimo di Representational State Transfer, un tipo di architettura software per i sistemi di hypertext distribuito

L'architettura REST, come tutti i Web Service operano in modalità client-server, dove un insieme di interfacce separa i client dai server. È Stateless, cioè la comunicazione client-server è ulteriormente vincolata in modo che nessun contesto client venga memorizzato sul server tra le richieste. Ogni richiesta da ogni client contiene tutte le informazioni necessario per richiedere il servizio e lo stato della sessione è contenuto sul client.

Infine come nel caso del World Wide Web, i client possono fare caching delle risposte. Le risposte devono in ongi modo definirsi implicitamente o esplicitamente cacheable o meno, in modo da prevenire che i client possano riusare vecchi dati oppure dati errati. Quindi i principali vincoli dell'architettura REST sono:
- Basata su client-server
- Stateless
- Cacheable

# Elementi fondamentali
Gli elementi fondamentali di un Web Service basato su RESTful sono:
- risorse
- rappresentazione delle risorse
- operazioni sulle risorse

Un servizio RESTful gestisce un insieme di risorse. Una risorsa può rappresentare una collezione di altre risorse.
Ogni risorsa è identificata attraverso un URL specifico, questo rende semplice trasferire l'indirizzo di una risorsa ad un'altra applicazione.

Le risorse sono entità astratte caratterizzate da uno stato che può cambiare nel tempo. Il client e server comunicano scambiandosi rappresentazioni dello stato delle risorse. Per utilizzare le risorse, le componenti di una rete comunicano attraverso un'interfaccia standard e si scambiano rappresentazioni di queste risorse. La rappresentazione di un oggetto può cambiare nel tempo.

Nell'approccio REST si usa un numero limitato di operazioni per leggere o modificare lo stato delle risorse. Le operazioni corrispondono ai "metodi" definiti nel protocollo HTTP, in particolare:
- GET consente di ottenere una rappresentazione della risorsa
- PUT modifica lo stato della risorsa o crea la risorsa se l'URL specificato non ha una risorsa corrispondente
- DELETE cancella una risorsa dal server
- POST aggiunta di nuove risorse in una collezione

# Definizione di un Web Server lato server e client
Nella definizione del web service, occorre specificare:
- Quali operazioni sono permesse per ciascun URL
- Quali formati sono accettati per il body della richiesta e della risposta
- I codici di stato restituiti

Un client RESTful deve:
- individuare la risorsa di cui vuole consultare o modificare lo stato
- Preparare una richiesta indicando l'operazione da effettuare e le altre informazioni aggiuntive
- Inviare la richiesta ed ottenere la risposta
- Esaminare lo status della risposta ed estrarre le informazioni di interesse dal body e dagli header
- 


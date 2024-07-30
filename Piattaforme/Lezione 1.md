---
tag: #piatta
created: 2023-02-27 14:03:15
updated: 2023-02-27 14:03:15
---
#piatta 
# Requisiti delle applicazioni e tier
Le applicazioni web a livello enterprise hanno i seguenti requisiti:
- Portabilità: ogni applicazione ormai è sia desktop che mobile, e su diversi sistemi operativi
- Interoperabilità: ambienti diversi comunicano
- Supporto e gestione runtime: tolleranza ai guasti, affidabilità e risorse gestite bene 
- Time to market: facilità di sviluppo per essere immessa nel mercato
- Integrazione
- Scalabità: risorse richieste e gestite opportunamente

 Gli elementi costitutivi logici di ogni applicazione sono:
- Presentation logic: come si mostra l'applicazione all'utente
- Business logic: orientamento dell'azienda
- Data access logic: logica con il quale si accede ai dati
- Servizi di sistema: meccanismi trasparenti per implementare le transazioni

Le applicazioni enterprise nel corso degli anni sono passate da un modello single tier, dove c'è un mainframe alla base che rende il tutto molto centralizzato e difficile da scalare, ad un modello two tier, client fat ovvero client che interagiscono direttamente con il database e questo come visto a basi di dati è pesante da aggiornare per tutti i client. Si è passati poi ad un modello three tier, dove i client sono alleggeriti tramite uno strato di back-end tra il database ed il client e tale strato, è basato su remote procedural call (chiamata a procedure) ma presentando scarsa riusabilità. Infine si è arrivati ad un modello three tier web server, dove un web client si interfaccia con il web server che tramite RMI accede ai dati.

Un modello molto impiegato è poi quello a container dove si fa girare applicazioni che forniscono servizi in contesti separati. Una soluzione invece basata su standard aperti è Java Enterprise Edition. Spring è un framework che esprime un modello a container leggero e molte funzionalità sono delegate al container tramite politiche di default abbastanza forti. Gli URI, Uniform Resource Identifier forniscono un meccanismo semplice ed estensibile per identificare una risorsa. Gli URI hanno una sintassi standard ed uniforme e questo ha diversi vantaggi quali:
- Convenzioni sintattiche comuni
- Comune semantica per l'interpretazione
- Estensibilità facilitata

Gli URI hanno come identificatori stringhe con una sintassi definita come: `<scheme>:<scheme-specific-part>`. Esiste anche un sottoinsieme di URI per rappresentazioni gerarchi quale `<scheme>://<authority><path>?<query>`, dove a parte `<scheme>` le altre parti possono essere omesse. Esistono due specializzazioni del concetto di URI:
1. URN: specifica il nome della risorsa ma non come trovarlo
2. URL: specifica come trovare una risorsa attraverso un meccanismo d'accesso

Nella sua forma più comune la sintassi di un URL è `<protocol>://[<username>:<password>@]<host>[:port][/<path>[?<query>][#fragment]]` dove host indica il server su cui risiede la risorsa, port definisce la porta da utilizzare di default e path identifica la risorsa nel file system. Tutto ciò che è dentro parentesi quadre è opzionale.

---
# HTTP
È un protocollo client-server generico e stateless utilizzato per lo scambio di documenti ma anche da parte di molte applicazioni. HTTP è indipendente dal formato dati con cui vengono trasmesse le risorse, ricordando che stateless vuol dire che il server non è tenuto a mantenere informazioni persistenti. Caratteristiche di HTTP sono:
- La negoziazione del formato di dati per l'Indipendenza del sistema dal formato di rappresentazione dei dati.
- Specifiche di politiche di caching sofisticate a seconda del tipo di connessione.
- Specifiche di autenticazione dell'utente di varia sofisticazione.

La connessione HTTP è composta da una serie di richieste e risposte, che contengono vari header quali:
- Date: data ed ora
- MIME-Version: versione MIME
- Transfer encoding: formato di codifica
- Cache control: tipo di meccanismo di caching
- Connection: tipo di connessione

Si hanno poi gli header dell'identità che danno informazioni sul corpo del messaggio o sulla risorsa specifica e sono:
- Content type: tipo MIME dell'entità
- Content lenght: lunghezza in byte del corpo
- Content encoding: codifica della risorsa
- Content language: linguaggio della risorsa
- Content location: URL della risorsa
- Expires: data dopo la quale la risorsa non è più valida
- Last modified: data ed ora ultima modifica
- Content MD5: valore di digest MD5 usato per verificare la presenza di errori

Poi ci sono gli user-agent e referer che contengono informazioni quali, da quale pagina web è generata la richiesta, l'host che contiene il nome di dominio e la porta a cui viene fatta la connessione.

---

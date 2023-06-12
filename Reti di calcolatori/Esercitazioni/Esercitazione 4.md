## Perché usare stringhe e non Object?
Il motivo per cui si usano le stringhe invece di oggetti è per interoperabilità. Telnet ad esempio non permette di mandare oggetti, ma di mandare stringhe. Quindi si preferisce compatibilità ed interoperabilità a codice di più alto livello.

---
# Connessione remota in presenza di NAT e firewall
Il NAT è una tecnica che consiste nel modificare indirizzi IP contenuti negli header dei pacchetti in transito su un sistema che agisce da router all'interno di una comunicazione tra 2 o più host. All'interno di una rete domestica tutti i dispositivi hanno un indirizzo IP interno assegnato dal router. Dall'esterno tutti i dispositivi sono raggiungibili con lo stesso indirizzo IP pubblico
Per accedere ad un computer di una rete domestica, in presenza di NAT dinamico è necessario configurare delle regole di redirect delle chiamate sul router. La discriminazione dei dispositivi locali avviene tramite porte logiche. Questa operazione è detta Port forwarding, per cui le connessioni verso una determinata porta TCP o UDP può essere indirizzato verso un particolare host della rete interna. Ogni regola del port forwarding è caratterizzata da:
- una porta
- un protocollo (TCP o UDP)
- un host destinazione

Prima di configurare tali regole bisogna però sapere l'indirizzo IP pubblico del router a cui inviare le chiamate, tuttavia gli indirizzi di solito sono dinamici e bisogna quindi conoscerli. 
I servizi di Dynamic DNS possono fornire un ponte per conoscere l'IP pubblico del router tramite nome host. Ad ogni cambiamento di IP, il router comunica l'IP al DNS dinamico.

La presenza di firewall potrebbe impedire connessioni remote agli host della rete, quindi vanno anche loro tenuti di conto.

# Web Service
I web service sono un meccanismo che rende dei servizi o risorse disponibili attraverso la rete. I primi standard furono:
- SOAP: (Simple Object Access Protocol) definisce i meccanismi con cui un web service è invocato ed il formato dell'input e dell'output.
- WSDL: (Web Service Definition Language) descrive l'interfaccia esterna di un web service affinché uno sviluppatore possa creare un client capace di invocarlo.
- UDDI: (Universal Discovery Description and Integration) è un registro contenente informazioni utili per la scoperta e l'accesso ai web service.

Gli standard utilizzati per i Web service sono tutti dialetti di XML.

Lo scopo dei web service è quello di fare interagire macchine eterogenee per poter comunicare si parla quindi di integrazione di applicazioni. I web service, sono applicazioni messe a disposizione da una macchina e, di solito sono accessibili attraverso protocolli standard di Internet, di solito HTTP e porta 80. I web service presentano le seguenti caratteristiche:
- Interoperabilità: un web service può essere invocato da un client con una tecnologia diversa da quella su cui il web service sta eseguendo
- Incapsulamento: i dettagli di implementazione del software sono inaccessibili da chi usa un web service
- Accessibilità: un web service può essere reso pubblico per l'utilizzo anche limitando eventualmente l'accesso tramite username e password

Un grande vantaggio dei web service è la capacità di integrare applicazioni sviluppatte in maniera indipendente all'interno di sistemi diversi. L'integrazione è però resa difficile dalle politiche di sicurezza.
Le richieste SOAP viaggiano su Internet tramite HTTP e questo è il punto di forza dei web service che fornisce l'interoperabilità.
I web service sono una tecnica di Remote Procedure Call (RPC), ovvero chiamata di una procedura remota.

Una volta creato un Web Service di tipo SOAP, esso è descritto tramite il file WSDL. Il file viene pubblicato sul registro UDDI, il quale lo mette a disposizioni di tutti i client. Un client una volta ottenuto il WSDL, ha ottenuto tutte le informazioni necessarie per creare un client per usare il web service SOAP.

---
## Parentesi su XML
Essendo XML un linguaggio molto propenso ad errori di sintassi, è nato XML Schema linguaggio usato per descrivere il contenuto di un file XML. Gli array in XML sono rappresentati come una sequenza ordinata di elementi ripetuti dello stesso tipo di dati. Esempio:

``` xml
<xs:complexType name="ItemListType">
<xs:sequence>
	<xs:elementname="item" type="xs:string" minOccurs=0 maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>
```

- sequence indica l'ordine in cui devono apparire i parametri
- maxOccurs indica il numero massimo di occorrenze
- minOccurs indica il numero minimo di occorrenze

Esempio traduzione XML Schema:
![[xmlschema.png]]

---
## Struttura messaggi e documenti
Lo standard SOAP contiene:
- la specifica dei messaggi di input e output
- le regole di codifica per i tipi di dati

All'interno di un messaggio SOAP è formato da:
- SOAP Envelope: che è la sovrastruttura del messaggio che contiene l'header e il body
- Header: che contiene informazioni su sicurezza, routing, formati, pagamente ed autenticazione
- Body: contenuto vero e proprio del messaggio
- Fault element (parte specifica del body): contiene errori ed informazioni di stato del messaggio SOAP
- Attachments: allegati della richiesta

Le regole principali per realizzare un messaggio SOAP sono le seguenti:
1. Deve essere codificato in XML
2. Deve utilizzare il SOAP Envelope namespace (utile per usare gli array che non sono nativi di XML)

---
Il file WSDL è un file assocciato ad un web service ed è sufficiente ad un client per invocare il servizio.
Un file WSDL (file descrittore) contiene i seguenti blocchi:
- Types: indica i tipi di dati complessi, che possono essere scambiati con il web service.
- Messages: indica i messaggi che possono essere scambiati tra il web service ed il client, ovvero la struttura di ogni richiesta e risposta. Sono definiti come aggregazione o composizione dei tipi elementari
- Port Types: definisce  punti di connessione verso il web service, cioè le operazioni che si devono invocare ed i loro messaggi di richiesta e risposta
- Bindings: fornisce i dettagli implementativi per il tipo di porta, informazioni su come realizzare la porta ed il metodo di trasporto.
- Services: indica dove le porte sono fisicamente realizzate, fornisce una descrizione testuale di ciascuna porta ed informa i client da dove accedere.

---
Un registro UDDI contiene i documenti WSDL associati ad un insieme di servizi, ed informazioni addizionali riguardanti le credenziali d'accesso richieste dai servizi. L'accesso al registro UDDI può essere:
- Pubblico: chiunque può effettuare ricerche
- Privato: ricerca limita ad una sola azienda
- Ibrido: disponibile con restrizioni di accesso per la ricerca

---





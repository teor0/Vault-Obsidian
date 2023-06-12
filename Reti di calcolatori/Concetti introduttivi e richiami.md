#rdc 
# Richiami
Internet può essere vista come un insieme di host, ovvero computer che ospitano le applicazioni di rete. Gli host sono collegati tramite un'infrastruttura costituita da router che si occupano di instradare i messaggi sulla rete, che sono connessi in diversi modi, ad esempio fibra ottica e satellite. Per comunicare gli host sfruttano protocolli.

Un protocollo definisce formalmente il formato e l'ordine dei messaggi scambiati tra 2 o più entità in comunicazione, cosi come le azioni intraprese in fase di trasmissione e/o ricezione di un messaggio o di un altro evento.
I protocolli sono standardizzati da enti specifici che si occupano dello sviluppo e della manutenzione. Internet si può dire che è l'insieme dell'infrastruttura hardware e dei protocolli software.

I servizi offerti dalle applicazioni possono essere: 
- affidabili, con vantaggi in termini di sicurezza ed appunto affidabilità
- non affidabili, con vantaggi in termini di velocità

---
## Come si perdono i pacchetti e come si verificano ritardi?
Le cause di ritardo di arrivo di un pacchetto possono essere diverse in base ai casi:
1. Ritardo di elaborazione del nodo: ritardo perchè si deve scegliere il canale di inoltro oppure perché c'è un controllo di errore sui bit
2. Ritardo di accodamento: c'è attesa per la trasmissione oppure c'è congestione nel buffer del router

Il ritardo dei pacchetti è influenzato principalmente dal percorso scelto, in quanto più grande è la distanza più tempo è richiesto per l'invio come giusto che sia. 
La perdita di un pacchetto può essere causato in diversi modi, ad esempio il buffer del router è pieno ed il pacchetto viene scartato. Sta poi al protocollo implementato gestire la logica di ritrasmissione, in particolare se si utilizza un protocollo a livello di trasporto affidabile, la ritrasmissione è gestita da esso, altrimenti se si usa un protocollo inaffidabile non si ha un meccanismo di ritrasmissione a livello trasporto. Ovviamente non avere meccanismi a livello trasporto non vuol dire aver perso il pacchetto per sempre, ma sicuramente si è più efficienti avendo un meccanismo a livello trasporto che a livello applicazione.

---

## Throughput
Per [[Controllo di flusso#^9aeebb| throughput]] si intende la frequenza alla quale i bit sono trasferiti da mittente a destinatario. Si può calcolare in modo istantaneo e medio va ottimizzato per avere una comunicazione efficiente. 

In generale basta leggere le prime 4 pagine di appunti di fondamenti di reti (stack TCP e ISO/OSI)

---

## Struttura di Internet
La struttura di Internet è fondamentalmente gerarchica. Al centro vi sono gli ISP (Internet Service Provider) di livello 1 che comunicano in modo internazionale come pari. Sotto ci sono gli ISP di livello 2 che si occupano di un territorio nazionale. Gli ISP di livello 2 possono essere connessi ad 1 o più ISP di livello 1. Gli ultimi sono ISP di livello 3 che si occupano di gestire connessioni in maniera locale. Si capisce che quindi c'è un rapporto gerarchico tra gli ISP e che un ISP di livello 2 o 3 può essere visto come un client di un ISP di livello più alto. 

L'infrastruttura su cui si appoggia una rete può essere basata sul modello:
- Client-server: un host client chiede un servizio al server. Un server ricordiamo, ha un IP fisso, è sempre accesso ed è formato da più calcolatori messi assieme. Un client invece, ha IP dinamico e non comunica direttamente con altri client.
- Peer-to-peer: dove gli host sono tratti come pari e non si coinvolge un server se non per parti del servizio non principali

---

# Concetti introduttivi
Per reti di calcolatori si intende: 
> Un insieme di computer indipendenti ed interconnessi tra loro che possono scambiarsi informazioni 

I cluster però sono un insieme di computer interconnessi che non è una rete di calcolatori. Nel corso degli anni si è passati da sistemi centralizzati a sistemi di rete come le conosciamo adesso. 
Le reti permettono di far comunicare persone, computer e dispositivi. Il trend è quello del IoT (Internet of Things) data la varietà di dispositivi che oggi e nel futuro possono condividere risorse. Altre motivazioni che hanno spinto a sviluppare reti di calcolatori sono:
- Condivisione di informazioni e risorse
- Suddivisione dei compiti
- Affidabilità e scalabilità
- Accesso mobile e pervasivo
- E-Commerce, business to business e business to consumer

Per ridurre la complessità e per ragioni di modularità le reti sono organizzate come una serie di strati o livelli. Ogni livello usa i servizi del livello inferiore. Entità remote dello stesso livello possono comunicare tra loro. L'insieme di servizi forniti da un livello alle entità del livello superiore è detto interfaccia.

Logicamente il livello n di una macchina comunica con il livello n di un'altra macchina, ma in realtà nessun dato viene trasferito direttamente dal livello n  di una macchina al livello n di un'altra macchina, i dati attraversono man mano ogni livello attraverso le interfacce.

---

## Qualità del servizio
La qualità del servizio è data da diversi parametri:
- ordine di consegna dei dati: garantita solo da servizi con connessione
- ricezione garantita dei messaggi: gli ack possono essere usati sia da servizi senza connessione che con connessione
- consegna corretta dei messaggi: utilizzo di checksum per la correzione di errori ad esempio
- tempi di consegna: ritardi (latenza) e jitter (variazione della latenza)

---
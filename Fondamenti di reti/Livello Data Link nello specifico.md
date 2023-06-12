#fondamenti 
[[Struttura dei primi 3 livelli nel ISO-OSI]]
# Di cosa si occupa il livello?
Il livello Data Link ha la responsabilità di trasferire datagrammi da un nodo al nodo adiacente tramite link.
Come tutti i livelli deve fornire servizi al livello superiore, in particolare il livello Data Link si occupa del framing cioè la costruzione del frame ovvero l'organizzazione dei bit o pacchetti, del controllo di errore e di flusso. Il controllo degli errori permette al ricevitore di accorgersi di rumore, interferenze, oppure a causa di propagazione si perdono bit e richiede alla sorgente di ritrasmettere i frame. 
Il controllo di flusso per gestire al meglio il numero di frame componenti il flusso tra sistemi diversi, non sapendo a priori le specifiche della destinazione e può capitare che perdiamo qualità nella velocità di trasmissione dei dati. Per il controllo degli errori si usano delle codifiche per correggere o rilevare gli errori oppure entrambi attraverso lo stesso codice.

Il Medium Access Control ha una interfaccia diretta verso il livello fisico e l'accesso al mezzo cambia in base al canale.

---
## Definizioni
- I nodi sono sia host e router ma anche switch e bridge
- I link sono i canali di comunicazione che connettono nodi adiacenti lungo un percorso e possono essere: link cablati (fibra ottica), link wireless e LAN (di natura broadcast)
- L'unità informativa che prende il nome di frame, più in generale si chiama PDU (Protocol Data Unit) e viene trattata anche nel livello di rete.

Il controllo di flusso ed errore è applicato al collegamento dove viaggiano i dati, quindi è come se per ogni link attivassi un protocollo di collegamento che può essere diverso a seconda dell'interfaccia di rete.
Ci sono 3 tipi di collegamenti: 
1. punto-punto: collega 2 nodi
2. broadcast: vari pc collegati tramite cavo condiviso
3. switched: anche detto collegamento commutato dove c'è uno switch che è selettivo nell'inoltro dei dati e consente di gestire meglio la rete

I rispettivi collegamenti hanno velocità diverse, in particolare:
1. punto-punto: ISDN fino a 56kb/s
2. broadcast: 10Mb/s o più
3. switched: 10Mb/s o più ma la gestione dell'hardware cambia

>[!mezzi] Ogni mezzo fisico quindi ha un protocollo di collegamento su misura per essere sfruttato al meglio

---
# Funzioni e modi trasmissivi livello di collegamento
Il livello realizza 2 funzioni principali:
1. Livello Data Link: framing, controllo errore e flusso
2. Livello MAC: permette accesso al mezzo condiviso fornisce i mezzi per condividere in maniera ottimale le risorse

Ci sono 2 modi di trasmettere i frame:
1. trasmissione seriale con <font color=red> orientamento al carattere</font>
2. trasmissione seriale con <font color=red> orientamento al bit</font>

I protocolli di livello data link, si occupano di scegliere il modo di trasmettere, il colloquio tra half-duplex e full-duplex e devono capire l'organizzazione tra i nodi se master-slave o peer-to-peer.

L'orientamento al carattere è ormai in disuso, e consisteva in una trasmissione a gruppi di 8 bit ad esempio ASCII. L'orientamento al bit consente una trasmissione in modo seriale senza interpretare tutta l'informazione, questo consente una velocità maggiore.

Il tipo di protocollo usato è in relazione con il tipo di velocità della rete, ad esempio su linee a bassa velocità, come quelle usate dai modem è meglio usare un protocollo con orientamento al carattere.
> Il processo che implementa il protocollo gira tramite firmware all'interno dell'adattatore di rete. In base al tipo di scheda di rete si hanno driver che gestiscono il collegamento in modo diverso


---

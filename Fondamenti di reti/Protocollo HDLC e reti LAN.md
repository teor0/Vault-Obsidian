#fondamenti 
[[Framing e codici controllo e recupero di errori]]
# Definizione
Il protocolo HDLC (High level Data Link Communications), è un protocollo standard ISO e deriva dal protocollo proprietario SDLC di IBM. Può essere usato sia in half duplex che full duplex e sia master-slave che P2P. 
La modalità <font color=red> NRM (Normal Response Mode) </font> è di tipo master-slave dove una stazione primaria può inviare comandi e le secondarie trasmettono dopo un permesso.
La modalità <font color=red> ARM (Asynchronous Response Mode)</font> è una sorta di master-slave solo che le stazioni secondarie non necessitano di permessi espliciti.
La modalità <font color=red> ABM (Asynchronous Balanced Mode)</font> dove il traffico si cerca di averlo bilanciato, avviene in full duplex dove le stazioni sono viste come paritarie (peer to peer) e possono inviare informazioni in modo asincrono.

---
## Formato trama
![[tramahdlc.png]]

Per quanto riguarda Address, l'ultimo bit di ogni byte è usato per indicare se segue un ulteriore byte del campo A. In base alla modalità che usiamo l'indirizzo è quello della destinazione o sorgente. Il campo controll è di 1 o 2 byte, i primi bit distinguono il tipo: 
- <font color=red> I (information)</font>: sono trame per la trasmissione di informazioni utente
- <font color=red> S (supervisory)</font>: trame numerate per il controllo dell'invio del flusso di informazioni
- <font color=red> U (unnumbered)</font>: trame non numerate per l'invio di informazioni di controllo o per l'invio di informazioni in modalità senza connessione

Information contiene l'informazione d'utente, può essere non presente ed ha lunghezza variabile.
FCS è il codice di rilevazione d'errore. Nello specifico: ![[trames.png]]
Le trame s consentono di gestire le 3 modalità ARQ ed a seconda del campo type posso descrivere:
- RR: receiver ready
- RNR: receiver not ready
- REJ: reject
- SREJ: selective reject

Le trame U hanno funzioni di controllo aggiuntivo. Il campo M in genere è di 4 bit e suddiviso in M(1) e M(2), ed è usato per definire fino a 32 comandi.
Nell'instaurazione della connessione che avviene tramite messaggi, viene definita la modalità di trasferimento tra SNRM, SARM e SABM. Alla fine del trasferimento si ha il comando DISC che sta per disconnection. 

# Reti LAN
Un'importante aspetto delle reti LAN è il protocollo d'accesso al mezzo. La progettazione di una LAN differisce per 3 macrocategorie:
- topologia: come sono collegati i nodi
- sistema di comunicazione: a che banda trasmettere ed a che distanza
- protocolli d'accesso: chi accede in mutua esclusione e chi accede prima?

Queste 3 macrocategorie sono collegate fra loro.
Le caratteristiche di una LAN sono:
- estensione geografica limitata
- rete senza funzionalità
- utilizzo di protocollo di accesso al mezzo
- proprietà e gestione da parte di una singola organizzazione
- unico mezzo trasmissivo a capacità elevata e con basso tasso d'errore

## Topologie di LAN
Le topologie più usate sono bus, stella ed anello.
La tipologia a bus:
- usa un mezzo trasmissivo fisicamente condiviso ed intrisecamente bidirezionale. 
- L'accesso è multi punto
- Non adatto a fibra ottica
- Le stazioni sono collegate con agganci passivi ad un cavo coassiale. Il segnale alla fine del bus viene assorbito da terminatori posti ai lati

Problemi della topologia:
- accessi concorrenti causano collisioni
- necessità di indirizzazione dei frame

Nelle trame quindi vi è posto l'indirizzo MAC associato alla destinazione. La comunicazione usa lo standard di codifica Manchester ed è full duplex. Il cavo coassiale può essere configurato in 2 modi:
1. configurazione split ![[split.png]]
2. configurazione duale ![[duale.png]]

La topologia a <font color=green> stella</font>:
- sfrutta collegamenti punto-punto dedicati
- adatta a tutti i portanti fisici
- adatta a cablagi di tipo strutturati
- necessità di un hub che svolga funzioni di ripetitore
- possibilità di connette anche nodi distanti

La topologia a stella si differenzia in stella diffusiva, dove l'hub rinvia il segnale ricevuto verso tutti i nodi e stella non diffusiva, dove l'hub rinvia il segnale ricevuto solo al destinatario a fronte di performance maggiori e costi maggiori.

La topologia ad <font color=green> anello</font>:
- sfrutta collegamenti punto-punto
- il mezzo è logicamente condiviso: tipicamente una stazione riceve il permesso di trasmettere un frame speciale che le altre stazioni possono solo ascoltare o ricevere, poi ogni stazione a turno trasmette il frame speciale.

Se 2 o più trasmissioni avvengono contemporaneamente si verifica una collisione. I protocolli d'accesso al mezzo gestirà le collisioni ed inoltre gestisce la coda di trasmissione cioè quando un frame deve essere ritrasmesso devo contenere questo frame in un buffer.

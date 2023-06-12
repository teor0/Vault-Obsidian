#fondamenti 
[[Protocollo TCP]]
# Instaurazione della connessione
Prima di comunicare, deve essere instaurata una connessione, questo avviene tramite il three-way-handshake. I pacchetti sono numerati attraverso il clock per numerare i byte generati, il clock incrementa il contatore binario a passi regolari ad esempio con una velocità di 2Mbit/s la cadenza sarà $\displaystyle\Large {1\over{2\over8}}$=4ms diviso 8 perchè si tratta di byte. Il numerare i byte è importante per l'ordine e per evitare obsolescenza nella rete. Il clock quindi deve essere strutturato sulla base della velocità della scheda di rete, per evitare ciclicità nella numerazione e garantire l'ordine.

Il numero di bit del contatore deve essere maggiore o uguale del numero di bit dei numeri di sequenza, in particolare con 32 bit si garantisce unicità del numero. Il numero iniziale non è 1 ma è l'ISN (Initial Sequence Number) per "sicurezza". L'ISN va accordato al momento della connessione lato source-destination e destination-source. Attraverso MSL (Maximum Segment Lifetime) calcoliamo la durata di un ciclo completo di valori di ISN, in particolare avendo $\displaystyle\large 2^{32}$ possibilità, e frequenza di incremento pari a 4ms, sono necessarie 4ms*$\displaystyle\large 2^{32}$=4.7 h per compiere un ciclo completo. 
Per instaurare la sessione (3 way handshake) tra A e B, devono essere mandati i seguenti messaggi:
1. A→B SYN: my sequence number is x
2. A←B ACK: your sequence number is x
3. A←B SYN: my sequence number is y
4. A→B ACK: your sequence number is y

In realtà i passi 2 e 3 sono fusi in uno per questo si parla di three-way-handshake. Quando instauro la sessione la MSS viene scelta come il minimo della massima dimensione supportata tra sorgente e destinazione. La scelta del MSS dipende da:
- la dimensione della memoria a disposizione delle entità TCP
- la dimensione del MTU della sottorete a cui è connesso l'end-system
Il calcolo del MSS avviene sottraendo al MTU la dimensione degli header IP e TCP. Per rilasciare la connessione avviene lo scambio di messaggi:
A→B FIN
A←B ACK
A←B FIN
A→B ACK

La chiusura potrebbe essere anche leggermente asincrono al riscontro di chiusura.

---
# Trasferimento dati
La strategia utilizzata dal TCP per i riscontri è la PAR (Positive Acknowledge with Retransmission) meccanismo di riscontro cumulativo. La window in trasmissione specifica il numero di segmenti che possono essere inviati senza ricevere un riscontro. Analogamente la window in ricezione specifica il numero di segmenti che possono essere accettati fuori sequenza. Le due window ovviamente coincidono. Il meccanismo TCP Advertised Window serve per comunicare dalla destinazione alla source, la grandezza della window nel tempo.

---
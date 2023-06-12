#fondamenti 
[[Protocolli di trasporto]]
# Caratteristiche del protocollo
Il TCP è un protocollo con connessione cioè, prima di consentire l'invio dei dati nel formato TCP, deve instaurare una comunicazione con la destinazione, scambiandosi informazioni per garantirsi alcune caratteristiche e dopo può trasmettere. Si hanno le seguenti funzioni:
- indirizzamento di uno specifico utente all'interno di un host, ovvero multiplexing e demultiplexing
- trasferimento di un flusso informativo continuo e bidirezionale orientato al byte
- gestione delle connessioni
- controllo e recupero di errore
- segmentazione e riassemblaggio delle informazioni
- controllo di flusso e di congestione
- riordinamento delle unità informative

Una connessione TCP è identificata dalla coppia di socket associata ai due processi chiamati anche end point. Un numero di porta può essere usata per più connessioni, ma l'insieme dei socket di sorgente e destinazione identifica univocamente una connessione. L'assegnazione del numero di porta può essere statica o dinamica, dove nell'assegnazione dinamica si chiede al sistema operativo la porta libera. TCP accetta dal livello applicativo un flusso di segmenti continuo, ogni segmento ha lunghezza massima MSS (Maximum Segment Size) non superiore a 64KB, se non è rispettatta la dimensione a livello 3 si innesca un sacco di frammentazione che crea inefficienza.

>MSS dipende dal MTU

---
## Struttura pacchetto TCP
Il TCP utilizza buffer per immagazzinare i byte di dati finché si costruisce il segmento lato source e destination. Il segmento è formato da informazioni di controllo e dati utili. I campi sono divisi come segue:
![[frametcp.png]]
- Source port (16 bit) definisce l'indirizzo logico della sorgente
- Destination port (16 bit) definisce l'indirizzo logico della destinazione
- Sequence number (32 bit) contiene il numero di sequenza del primo byte di dati contenuti nel segmento a partire dall'inizio della sessione
- Acknowledgement number (32 bit) contiene il numero di sequenza del prossimo byte che il ricevitore si aspetta di ricevere
- offset (4 bit) contiene il numero di parole di 32 bit contenute nell'intestazione TCP
- reserved (6 bit) riservato per usi futuri
- window (16 bit) larghezza della finestra per il controllo di flusso
- checksum (16 bit) contiene la sequenza che permette al TCP ricevente di verificare la correttezza del segmento

Il campo control (6 bit) serve a specificare dei tipi di funzione tramite i bit:
- URG vale 1 se urgent pointer contiene un valore significativo
- ACK vale 1 quando Acknowledgement number contien un valore significativo
- PSH vale 1 quando l'applicazione esige che i dati vengono trasmessi dalla sorgente alla destinazione
- RST vale 1 quando un malfunzionamento impone il reset della connessione
- SYN indica l'inizio della connessione
- FIN indica la fine della sessione

- urgent pointer contiene il numero di sequenza degli ultimi byte di dati da consegnare con urgenza al processo ricevente, questo perchè c'è un orientamento al byte per i segmenti. 
- Option può avere lunghezza variabile. MSS serve per comunicare al TCP la dimensione massima dei segmenti da mandare. 
- Padding consente di arrivare ad avere segmenti multipli di 32 bit. 
---
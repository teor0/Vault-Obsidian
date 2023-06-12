#rdc 
[[Criptovalute]]

# Demultiplexing e multiplexing
Il livello di trasporto, si basa sui servizi del livello di rete e li potenzia. La prima funzione importante del livello di trasporto è multiplexing/demultiplexing.
Il demultiplexing nell'host ricevente consiste in consegnare i segmenti ricevuti al socket appropriato. 
Il multiplexing nell'host mittente consiste in raccogliere i dati da vari socket ed incapsularli con l'intestazione.
La struttura di un segmento è in generale la seguente: ![[segmentoTCPUDP.png]]

Il demultiplexing nel caso dell'UDP usa la seguente procedura:
Il  socket UDP è identificato dalla coppia <IP destinazione, porta destinazione>. Quando l'host riceve il segmento UDP, controlla il numero di porta ed invia il segmento UDP al socket con quel numero di porta. Datagrammi IP con IP di origine e/o numeri di porta di origine differenti vengono inviati allo stesso socket. Esempio:![[datagramUDP.png | SP sta per source port]]

Il demultiplexing nel caso del TCP usa la seguente procedura:
Il socket TCP è identificato da: IP di origine, porta di origine, IP destinazione e porta di destinazione. L'host ricevente usa i 4 parametri per inviare il segmento al socket appropriato, questo fa si che un server può avere più socket TCP contemporaneamente aperti. In particolare i server web hanno un socket differente per connessione client. Esempio: ![[datagramTCP.png]]

---

## UDP
Il protocollo UDP è un protocollo senza connessione, ovvero non vi è alcun handshaking tra mittente e destinatario ed ogni segmento è gestito indipendentemente dagli altri. Il protocollo è inoltre senza controllo di congestione. Questo rende il protocollo leggero e semplice quindi più veloce rispetto al TCP. La struttura di segmento è la seguente:
![[Images/headerudp.png]]
La checksum rilevi i bit alterati nel segmento trasmesso. In particolare:
- Il mittente considera il contenuto del segmento come una sequenza di interi di 16 bit. Il valore nel campo checksum è pari alla somma in complemento a 1 del contenuto del segmento. 
- Il destinatario calcola la checksum del segmento ricevuto e la confronta con il valore nel campo del segmento. Se i valori sono non sono uguali il segmento viene scartato.

---

## GO BACK-N e Selective repeat
![[gobackn.png]]
Nel Go back n la sorgente ha una bufferizzazione mentre la destinazione conserva l'ultimo frame ricevuto correttamente e gli altri frame li scarta. 4 non lo conserva in quanto la sequenza essendo sbagliata necessita di 1, 2 e 3. Questo protocollo lato ricevente non accetta buchi nella sequenza in quanto non si conserva i dati. Il Go back n si usa su canali con alto tasso di errore, l'enumerazione è vitale nel Go back n ma come gestirla? 
Se la window in trasmissione è w=n e indichiamo con M il numero di bit per numerare (numero di sequenza) i frame si deve verificare che:
$2^M>n$
se w=4 M=3 per soddisfare la disequazione.

Il selective repeat complica di più le informazioni al ricevitore. Per i frame fuori sequenza indica al trasmettitore l'ack del frame corrotto.
![[selectiverepeat.png]]
Non perdo la memorizzazione di 2 e 3. Serve quindi un buffer ed un meccanismo di riordinamento dei frame, ideale per errori isolati o canali con alta affidabilità.

---

## Principi del trasferimento affidabile
Per il livello applicazione, il livello trasporto è un canale affidabile, dove vengono mandati dati in entrata e ricevuti dati in uscita. Il livello trasporto offre al livello applicazione 2 metodi per l'invio e la ricezione dei dati. Questi metodi sono l'interfaccia del livello trasporto verso il livello applicazione, sono implementati con il protocollo d'invio e protocollo di ricezione che sono in realtà un unico protocollo. Questo protocollo interagisce con il livello di rete che è un canale inaffidabile attraverso altri 2 metodi. ![[trasferimentoaffidabile.png]]

---

## TCP
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
## Struttura pacchetto TCP e RTT
Il TCP utilizza buffer per immagazzinare i byte di dati finché si costruisce il segmento lato source e destination. Il segmento è formato da informazioni di controllo e dati utili. I campi sono divisi come segue:
![[segmentoTCP.png]]

L'RTT tiene conto indirettamente i ritardi di accodamento e processamento dei nodi, serve quindi una formula robusta e considerare la rete come una black box, altrimenti si rischia di ignorare la congestione delle sottoreti. Occorre aver un RTT più stabile e poco variabile, si usa perciò SRTT, lo Smoothed RTT, dove prendo valori di RTT e si fa una media. L'SRTT viene calcolato tramite la seguente formula: 
$\displaystyle\large SRTT(k+1)=aSRTT(k)+(1-a)RTT(k+1)$ con $\large 0\le a\le 1$
Tanto più a è pari a 0 tanto più si da importanza all'ultima osservazione di RTT. Valori minori del peso corrispondono ad un aggiornamento veloce del SRTT, valori maggiori rendono SRTT insensibile a brevi variazioni del ritardo di trasferimento. 

---

## Controllo di flusso, apertura e chiusura connessione
Nel controllo di flusso il mittente non vuole sovraccaricare il buffer del destinatario in poco tempo. Lo spazio disponibile nel buffer è pari a: <font color=red>Dim buffer -(Ultimo Byte ricevuto - Ultimo Byte letto)</font> questo spazio disponibile viene messo nel campo della finestra di ricezione. 
Per instaurare la sessione (3 way handshake) tra A e B, devono essere mandati i seguenti messaggi:
1. A→B SYN: my sequence number is x
2. A←B SYNACK: my sequence number is y
3. A→B ACK: your sequence number is y

Il primo segmento SYN prende il nome di SYN in quanto il campo S è posto a 1 e non contiene dati. B risponde con un SYNACK in quanto il campo A è posto a 1 essendo il campo di riscontro valido.

Per chiudere la connessione viene mandato un messaggio con campo F pari a 1. Dopo la ricezione del ACK, si ha un'attesa temporizzata per evitare che pacchetti ritardatari vengano persi prima di riallocare il socket della connessione.

---

#fondamenti 
[[Protocollo TCP]]
# Teoria del controllo d'errore
Il controllo d'errore è importante nel TCP, quindi anche il trasmettitore deve avere un buffer per i segmenti inviati che vengono scartati quando arrivano alla destinazione. Per capire se il segmento va ritrasmesso si usa l'RTO (Retrasmission Time Out) che attende l'ACK della destinazione per la ricezione. Se l'RTO scade e non arriva l'ACK in tempo, il segmento verrà ritrasmesso, mentre il riscontro fa scartare il segmento dal buffer. Il meccanismo del controllo dell'errore funzione come segue:
1. A invia verso B, l'invio del segmento viene indirizzato e bufferizzato.
2. B effettua la verifica dell'integrità tramite checksum
3. B genera l'ACK se la verifica va a buon fine, altrimenti non lo genera.
4. A riceve il riscontro e continua oppure ritrasmette.

L'RTO è importante per ricevere il riscontro, se troppo piccolo la trasmissione si interrompe prima, se troppo grande la trasmissione è poco reattiva e si perde efficienza. Per stimare un buon RTO si usa uno schema adattivo in base al Round-Trip time, ovvero il tempo di andate e ritorno di segmento e riscontro. RTT è somma di 3 contributi:
- ritardo di trasferimento sorgente→destinazione
- ritardo di trasferimento destinazione→sorgente
- tempo necessario per rispondere

---
## Calcolo SRTT
L'RTT tiene conto indirettamente i ritardi di accodamento e processamente dei nodi, serve quindi una formula robusta e considerare la rete come una black box, altrimenti si rischia di ignorare la congestione delle sottoreti. Occorre aver un RTT più stabile e poco variabile, si usa perciò SRTT, lo Smoothed RTT, dove prendo valori di RTT e si fa una media. L'SRTT viene calcolato tramite la seguente formula: 
$\displaystyle\large SRTT(k+1)=aSRTT(k)+(1-a)RTT(k+1)$ con $\large 0\le a\le 1$
Tanto più a è pari a 0 tanto più si da importanza all'ultima osservazione di RTT. Valori minori del peso corrispondono ad un aggiornamento veloce del SRTT, valori maggiori rendono SRTT insensibile a brevi variazioni del ritardo di trasferimento. Andando a sviluppare la formula troveremo che:
$\large SRTT(k+1)=(1-a)RTT(k+1)+a(1-a)RTT(k)+a^2(1-a)RTT(k-1) ...$
$\large +a^k(1-a)RTT(1)+a^{k+1}RTT(0)$
dato che a e (a-1) sono $\le$ per ogni termine successivo è più piccolo. Per a=0,8 si ha:
$\large SRTT(k+1)=0,2RTT(k+1)+0,16RTT(k)+0,128RTT(k-1) ...$

L'RTO deve essere proporzionale al SRTT secondo:
$\displaystyle\large RTO(k+1)=min[upperbound,max[lowerbound,bSRTT(k+1)]]$
Dove:
- lowerbound e upperbound sono tipicamente prefissati a 1s e 1m.
- b p una costante tale che 1,3<b<2,0.
- Il lowerbound dovrebbe essere misurato in frazioni di secondo e l'upperbound dovrebbe essere 2MSL cioè 240s.

--- 
## Problematiche 
Ci sono 2 problemi legati al calcolo del RTO:
1. misura accurata del RTT è difficile quando ci sono ritrasmissioni
2. algoritmo per calcolare SRTT è inadeguato perchè assume erroneamente che la varianza nei valori di RTT è piccola e costante

Questi problemi sono rispettivamente risolti dall'algoritmo di Karn e Jacobson.

---

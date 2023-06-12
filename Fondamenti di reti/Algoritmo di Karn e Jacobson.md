#fondamenti 
[[Controllo d'errore]]
# Algoritmo di Jacobson
L'algoritmo di Jacobson incorpora la misura della varianza del RTT ed è importante soprattuto su link a bassa velocitò dove la variazione delle dimensioni dei pacchetti, causa un'ampi variazione di RTT. L'algoritmo migliora l'utilizzo di un link da 9,6kbps dal 10 al 90%. L'idea è trovare una formula più generale rispetto al SRTT. Quindi:
- se la variazione è molto ridotta si può ricadere nel SRTT
- se la variazione è ampia si calcola la deviazione standard: $\displaystyle\large S^2={1\over n}S|RTT-SRTT|^2$

Il calcolo della deviazione standard può essere molto complesso quindi Jacobson sfrutta la deviazione media dei campioni di RTT. Chiamiamo la deviazione media MDEV allora:
$\large MDEV(x)=E[|x-E[x]|]$
$\displaystyle\large MDEV^2(RTT)={1\over n}(S|RTT-SRTT|)^2$

Dimostrato che MDEV=$\displaystyle\large{({p\over 2})^{1\over2}}$SDEV è quindi abbastanza fedele.
Si calcola RTO come $\large RTO(k+1)=SRTT(k+1)+u\times MDEV(RTT)$ dove u=4.
Se c'è poca differenza tra RTT e SRTT per lungo tempo si può pensare che SRTT è una buona stima di RTT, se RTT ha un'alta varianza allora la stima non è molto affidabile ed è opportuno avere un margine di sicurezza proporzionale all'incertezza. La procedura dinamica di RTO è:
- calcolo stima di RTT, SRTT(k+1): 
  $SRTT(k+1)=aSRTT(k)+(1-a)RTT(k+1)=SRTT(k)+aSRTT(k+1)-SRTT(k)$
- calcolo dell'errore nella predizione di RTT, SERR(k+1):
  $SERR(k+1)=RTT(k+1)-SRTT(k)\Rightarrow SRTT(k+1)=SRTT(k)+aSERR(k+1)$

La nuova predizione è basata sulla vecchia più una frazione dell'errore nella predizione. Jacobson conclude che: 
$SDEV(k+1)=(1-h)SDEV(k)+h|SERR(k+1)|$
$RTO(k+1)=SRTT(k+1)+u\times SDEV(k+1)$ con a=0,125 h=0,25 e u=4

---
# Algoritmo di Karn e backoff esponenziale
Quando scade il timeout relativo ad un segmento, il TCP sender ritrasmette il segmento stesso secondo la specifica RFC 793. Il sender usa sempre lo stesso valore di RTO di tutte le successive ritrasmissioni del pacchetto. Questa tecnica non è consigliabile se la scadenza del timeout è legato ad uno stato di congestione di rete perché lo aggraverebbe. È consigliabile variare il valore di RTO delle sorgenti che sono coinvolte nella congestione per evitare ritrasmissioni contemporanee.

> È consigliabile aumentare RTO ogni volta che il TCP sender ritrasmette lo stesso segmento

La congestione comprende più nodi ed il TCP cerca di capire le situazioni in maniera indiretta redendo difficile la comprensione dell'errore. Una tecnica semplice per implementare il backoff è il backoff esponenziale, dove ogni volta che deve ritrasmettere un segmento, TCP moltiplica il valore di RTO precedentemente calcolato per un opportuno valore q, finché il segmento non vada a buon fine. La sorgente TCP aumenta il valore di RTO per ogni ritrasmissione come segue: $\large RTO_{i+1}=qRTO_j$.
Di norma l'RTO viene raddoppiato ad ogni ritrasmissione fino al raggiungimento di un fattore moltiplicativo pari a 64. TCP usa l'algoritmo di Karn per sceglie i campioni di RTT da usare per la stime di SRTT. In caso si ritrasmissione TCP non distingue se il riscontro si riferisce alla prima trasmissione del segmento o alla ritrasmissione del segmento. Un errore di attribuizione può causare un timeout troppo elevato o troppo breve.

>Secondo Karn, nel calcolo di SRTT e SDEV non devono essere inseriti i campioni di RTT relativi a segmenti ritrasmessi e, nel calcolo del RTO bisogna impiegare la procedura di  backoff esponenziale

---
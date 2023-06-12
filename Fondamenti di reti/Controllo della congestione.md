#fondamenti 
[[Protocollo TCP]]
# Tecniche di controllo della congestione
Il controllo della congestione ha lo scopo di evitare o risolvere eventuali situazioni di sovraccarico nella inter-rete, limitando il traffico offerto alla rete. Il meccanismo della sliding window non è sufficiente per il controllo della congestione, si sono sviluppati cosi altri meccanismi. La perdita di segmenti o lo scadere del RTO, porta la sorgente a diminuire l'invio di segmenti. Le principali tecniche per gestire la congestione sono slow start e congestion avoidance.

La tecnica slow start, tende ad evitare la congestione durante la fase di avvio di una connessione perciò, espande gradualmente la finestra del sender ad ogni riscontro fino a raggiungere pieno regime senza causare congestione. L'ampiezza della allowed window usata dal sender è pari a: $awdn=min[RW,cwnd]$
dove RW è il numero di segmenti concessi dalla destinazione e cwnd è la congestion window che vale inizialmente 1. La cwnd cresce fino a raggiungere lo slow start threshold, ovvero la dimensione della finestra dopo la quale si entra in congestion avoidance. Nella congestion avoidance ad ogni riscontro, la cwnd aumenta di 1 fino a tornare al massimo.
Quando avviene ritrasmission timeout slow start fisserà la slowstart threshold pari a $\large ssthresh={cwnd\over 2}$ per cautela. La finestra crescerà esponenzialmente da 1 a 4, poi attenderà 4 riscontri per essere incrementata di 1. Arrivo a 5 aspetta 5 ACK per salire e cosi via.

Esempio:
A t=0 viene trasmesso 1 segmento di lunghezza MMS, al tempo RTT 2 segmenti MSS, al tempo 2RTT 4 segmenti e cosi via. Al tempo kRTT si inviano $\displaystyle\large 2^k$ segmenti che corrispondono a $\displaystyle\large 2^k$MSS byte. 
In un tempo pari a N\*RTT, assumendo che si mantenga valida la condizione CW\<RW con CW=$\displaystyle\large 2^k$MSS, il numero totale di byte trasmessi è pari a:
$\displaystyle\large S_k=1...N(2^kMSS)=MSS\times S_{k=1...N}2^k=MSS\times (2^{N+1}-1)$ byte
Supponiamo che RW=m\*MSS e che la rete non si congestioni, il regime di slow start finisce quando CW>RW ovvero:
$\displaystyle\large 2^nMSS>m\times MSS\Rightarrow 2^n>m\Rightarrow n>log_2m$ dove n rappresenta il numero di RTT dopo il quale, il numero di byte trasmessi è costante cioè il numero di RTT necessari affinché CW raggiunga il valore di regime. Definiamo $\displaystyle\large n_{inf}$ il numero intero subito inferiore a $\displaystyle\large log_2m$: $\displaystyle\large n_{inf}=\lfloor log_2m\rfloor$

A regime di slow start TCP trasmette: 
$\displaystyle\large {MSS(2^{n_{inf}+1}-1)=MSS(2^{\lfloor log_2m\rfloor+1}-1)}$

Per $\displaystyle\large n>n_{inf}$ ad ogni RTT saranno trasmessi m\*MSS byte, per cui in un tempo pari a h\*RTT verranno trasmessi h\*m\*MSS byte. In generale il numero di byte trasmessi in L\*RTT secondi nel caso in cui RW=m\*MSS è dato da: 
$\displaystyle\large L\le n_{inf}\Rightarrow MSS(2^{L+1}-1)$ quindi
$\displaystyle\large 2>n_{inf} \Rightarrow MSS(2^{\lfloor log_2m\rfloor+1}-1)+(L-n_{inf})\times mMSS$

Nelle condizioni in cui il timeout non scatti mai ed il ricevitore dia sempre la massima RW disponibile, il tempo impiegato per trasmettere un file di B byte è L\*RTT con L intero. In particolare:
- $\displaystyle\large B\le MSS(2^{n_{inf}+1}-1)\Rightarrow B=MSS(2^{L+1}-1)\Rightarrow L=\lceil log_2(1+{B\over MSS}-1\rceil$
- $\displaystyle\large B>MSS((2^{n_{inf}+1}-1)\Rightarrow B-MSS(2^{\lfloor log_2m\rfloor+1}-1)=(L-n_{inf})\times mMSS$


## TCP TAHOE e RENO
Per TAHOE se l'RTO è scaduto $\large SSTH={cwnd\over 2}$ e cwnd=1. Si riparte quindi con slowstart per poi passare a congestion avoidance.
Nel RENO, se avviene una perdita SSTH$\large ={cwnd\over 2}$ e $\large cwnd= {cwnd\over 2}$ e si passa immediatamente a congestion avoidance.

## Fast retransmit e fast recovery
Una volta che la sorgente riceve 3 ACK duplicati, si intende che il segmento è stato perso, per ottimizzazione  nel fast retransmit si pone SSTH=${cwnd\over 2}$, si ritrasmette il segmento senza aspettare lo scadere del RTO e si pone $\large cwnd= {cwnd\over 2}$ e si aumenta linearmente la cwnd. Per quanto riguardo il fast recovery invece si pone SSTH=${cwnd\over 2}$ viene ritrasmesso il segmento perso e per tenere conto i segmenti già ricevuti si pone cwnd=SSTH+3 e, per ogni altro ACK duplicato si aumenta di 1 la cwnd e si trasmette un segmento, mentre al arrivo di un ACk si pone cwnd=SSTH.

---



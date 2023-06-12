#fondamenti 
[[Framing e codici controllo e recupero di errori]]
[[Distanza di Hamming e codici a ridondanza ciclica]]
# Diagramma di timing e stop & wait
Un diagramma di timing è uno strumento impiegato per spiegare la logica di funzionamento di un protocollo. Il diagramma usa due linee temporali per rappresentare cosa accade tra le 2 stazioni ed esprimere dettagli diversi.
![[timing.png]]
$\large\tau$=tempo di propagazione $\large\tau_t$=tempo di ritardo. 
![[stopnwait.png| diagramma stop & wait]]
Supponiamo di dover mandare un frame F tra 2 stazioni. Sia $t_E$ il tempo di elaborazione. Una volta mandato il frame la stazione B verifica tramite il codice di rilevazione se c'è stata un'alterazione o no. Questo avviene nel tempo di elaborazione e dopo aver mandato il riscontro positivo, A può mandare un altro frame. Il frame che deve essere mandato deve essere bufferizzato ed avere un time che fa capire se qualcosa è andato storto. Quindi:
A bufferizza F ed inizializza il timer di F per attendere il riscontro di B. Il fatto di avere rumore ci pone delle regole di affidabilità. Se dopo aver mandato F il riscontro non arriva da B anche se B aveva ricevuto F precedentemente lo scarta e manda comunque il riscontro.
Il timeout va dimensionato per bene, vediamo graficamente cosa va tenuto conto:
![[timeoutdiagram.png]]
Il timeout $\large t_{out}$ deve essere tale che $\large t_{out}\ge 2\tau + 2t_E + t_R$. Un'altra questione da chiarire è se bisogna numerare i frame oppure no. Quando arriva un frame, B deve capire se è lo stesso o meno, per farlo si usa un numero di sequenza di 1 bit in quanto è necessario e sufficiente a discriminare frame nuovi. 

## Calcolo efficienza
Sia E l'efficienza dello stop & wait, la formula per calcolarla é: $E=\Large{t_F\over t_{Tot}}$ dove $t_F$ è il tempo di trasmissione del frame e $t_{Tot}$ è il tempo che tengo il canale occupato.

Se E=1 allora l'efficienza è ideale. In realtà si ha $0<E\le 1$. Sviluppiamo $t_{Tot}$ come $\Large t_{Tot}=\tau + t_F+t_E+\tau +t_R+t_E=2\tau + t_F+2t_E+t_R$ quindi:
$E=\displaystyle\Large{{t_F\over 2\tau +t_F+2t_E+t_R}=\large{1\over 2{\tau\over t_F}+1+2{t_E\over t_F}+{t_R\over t_F}}}$

è un valore ottimistico in quanto non si pensa ad uno o più possibili ritrasmissioni. Nel caso più realisitco con errori sul canale: 
$E=\displaystyle\large{t_F\over E[n_t]\times t_{Tot}}$ dove $\large E[n_t]$ è il numero medio di ritrasmissioni ed è pari a $\displaystyle\large E[n_t]={1\over 1-p}$ dove p è la probabilità che un frame arrivi errato alla destinazione dopo la sua immissione sul canale.

Dato per buono questo la formula per il calcolo dell'efficienza diventa: $E=\displaystyle\large{{1\over {1\over 1-p}(2{\tau\over t_F}+1+2{t_E\over t_F}+{t_R\over t_F})}={1-p\over2{\tau\over t_F}+1+2{t_E\over t_F}+{t_R\over t_F}}}$
assumendo che $\displaystyle\large{t_E\over t_F}$ e $\displaystyle\large{t_R\over t_F}$ siano trascurabili rispetto gli altri termini abbiamo che l'efficienza è data infine da:
$E\displaystyle\large\approxeq{1-p\over 1+{2\tau\over t_F}}$.
>Anche con un canale ideale, cioè p=0 il sistema non ha E=1!

Esempio: consideriamo un canale con $V_T=1Gbit/s$ con $L_F=1000bit$ (lunghezza frame), $V_P=2\times 10^8$ e d=10km.

$\displaystyle\large \tau_P={d\over V_P}=0,5\times 10^{-4}s$
$\displaystyle\large t_F={L_F\over V_T}=10^{-6}s$
$\displaystyle\large a={\tau\over t_F}=50 \Rightarrow E_{MAX}={1\over 1+2a}=0,01=1\%$
uno schifo. La destinazione riceve $10^7bit/s$ mentre la sorgente ne manda $10^9bit/s$! Se la sorgente riducesse la sua velocità a $V_T=10^8bit/s$ si avrebbe $E_{MAX}\approxeq 0,091=9\%$ meglio ma comunque efficienza bassissima. Se $V_T=10^6bit/s$ $E_{MAX}\approxeq 99\%$

Quindi un protocollo deve essere adeguato per impiegare al meglio il canale.
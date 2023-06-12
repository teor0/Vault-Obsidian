#asd 
# Nozioni di base
Iniziamo con il dare qualche definizione.  Nei corsi precedenti si è capito che un algoritmo è un insieme passi svolti in sequenza, ma è davvero così? 

- Definizione di algoritmo
>  
Un algoritmo si dice tale quando dato un input genera un output data una sequenza di istruzioni da interpretare.

Gli algoritmi si prefissano di risolvere dei problemi, ma che cos'è un problema?
 
	

- Definizione di problema
>  Dati due insiemi: <font color=red>$I$</font> l'insieme di possibili input e  <font color=blue> $O$</font> insieme di possibili output, un problema <font color=orange>P</font> è una funzione $I→O$. $P:I→O$ scritto in modo matematico, cioè ha come dominio $I$ e codominio $O$.

Un problema può essere risolvibile o meno, ad esempio io posso contare tutte le dita di una mano, ma non posso contare il numero di stelle dell'universo. Insomma
quando un algoritmo risolve un problema?

- Dato un problema <font color=purple>P</font> ed un algoritmo <font color=orange>A</font>, A è detto risolutore, se ogni possibile input x risolve il problema. Perciò se <font color=red> almeno in un caso l'algoritmo non risolve il problema o non termina</font>, non sarà risolutore del problema.


Non tutti i problemi sono risolvibili e non tutti i problemi si possono risolvere tramite algoritmo. I problemi risolvibili sono quelli per i quali esiste un algoritmo risolutore.
Capito cos'è un algoritmo e cos'è un problema resta da capire ancora 2 concetti, perchè progettare algoritmi e soprattutto perchè analizzarli?  

- Perchè progettare algoritmi?

    Vogliamo progettare algoritmi che <font color=green>producano correttemente</font> il risultato desiderato del problema e che <font color=green>siano efficienti</font> in termini di esecuzione ed occupazione di memoria e non degli algoritmi inefficienti e super costosi.

- Perchè analizzare algoritmi?

    L'analisi teorica sembra più efficace ed affidabile di quella sperimentale, ovvero testare l'algoritmo lanciandolo con vari input. L'analisi teorica vale su tutte le istanze di dati su cui l'algoritmo opera, ci aiuta a scegliere tra diverse soluzioni allo stesso problema e permette di predirre le prestazioni di un programma. Quando si analizza un algoritmo si parla quindi di [[Nozioni e tipi di analisi di complessità#Analisi di complessità| analisi di complessità]] e di [[Nozioni e tipi di analisi di complessità#Analisi complessità spaziale | analisi di complessità spaziale]]

Tipicamente l'analisi di un algoritmo si fa rispetto alla dimensione dell'input

---

# Analisi di complessità

Per calcolare la complessità di un algoritmo dovremmo utilizzare la macchina di Turing, ma questo richiederebbe un processo molto oneroso. Possiamo direttamente studiare la complessità ad alto livello, sapendo che quando un linguaggio ad alto livello è tradotto in assembly, linguaggio macchina o un qualsiasi linguaggio a basso livello, esiste una proporzione che collega ad ogni istruzione di alto livello ad un numero di istruzioni di basso livello.

L'analisi di complessità è in genere il calcolo della <font color=red> complessità temporale </font> di un algoritmo, ovvero il tempo necessario per essere eseguito. Si può anche però fare un'analisi di complessità per quanto riguarda lo spazio di memoria occupato, ovvero la [[Nozioni e tipi di analisi di complessità#Analisi complessità spaziale| complessità spaziale]]. Non sempre esiste però, una funzione che associa la dimensione dell'input al costo di esecuzione di un algoritmo, come si può ovviare a questo problema?

Chiamiamo $T(x)$ il costo di esecuzione di un algoritmo A su $x$ e con $k$ la dimensione. Avremo due funzioni:

<font color=red> $\displaystyle\large T_w(x)=max\{T(x) | x \in I ∧ k=n\}$</font>
- Worst case/caso peggiore, ovvero il costo del caso peggiore è pari al costo massimo di $T(x)$ tale che la dimensione è $n$ preso un input $x$.

<font color=blue> $\displaystyle\large T_b(x)=min\{T(x) | x \in I ∧ k=n\}$</font>
- Best case/caso migliore, ovvero il costo del caso migliore è pari al costo minimo di $T(x)$ tale che la dimensione è $n$ preso un input $x$.

Se si considera la distribuzione di probabilità che le istanze siano effettivamente date in input all’algoritmo (in gergo $Pr(x)$) allora si può definire anche la funzione:

$\displaystyle\large T_m(x) = \sum_{x\in I∧k=n}T(n) \times Pr(x)$ 
- Caso medio, ovvero la sommatoria della probabilità $Pr(x)$ per il costo di esecuzione $T(n)$

Lo studio della complessità quindi si esplica lavorando per casi, caso migliore, caso peggiore e caso medio.

---

# Analisi complessità spaziale

La complessità spaziale è <font color=red> il costo della memoria che viene utilizzata da un algoritmo </font>. Le istruzioni di base tipo <font color=grey>`int i=0;`</font> hanno un costo "dipendente", cioè se devo memorizzare una variabile sulla RAM o sul registro della CPU, avrò un grosso cambio in termini di costo, per questo motivo alcune istruzioni si possono "ignorare". Per programmi iterativi è sufficiente esaminare il costo di allocazione di una struttura dati e la dichiarazione delle variabili per calcolare l'effettivo costo di memoria. 

Per quanto riguarda gli algoritmi ricorsivi, lo spazio usato in un certo momento è lo spazio totale usato da tutte le chiamate ricorsive attive in quell'istante. Questo perchè, ad ogni chiamata di un metodo siamo costretti a tenerci qualche informazione, al minimo l'indirizzo di ritorno.


>Una procedura occupa spazio quando è attiva e libera spazio quando termina.

Abbiamo visto quindi l'analisi di complessità e l'analisi di complessità spaziale, andiamo adesso a studiare l'analisi teorica per eccellenza ovvero [[Analisi asintotica| l'analisi asintotica]].


---


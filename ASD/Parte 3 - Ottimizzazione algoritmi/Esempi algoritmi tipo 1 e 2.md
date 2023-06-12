[[Teorema delle ricorrenze]]
#asd 
# Esempi tipo 1

Alcunia esempi di algoritmi dividi et impera di tipo 1 sono la ricerca binaria, merge sort, la moltiplicazione tra matrici e la moltiplicazione di interi con dimensione infinita. Prendiamo in esame la ricerca binaria definita dal seguente algoritmo:

```java
public static int ricercaBinaria(int[] v, int x){
	return ricerca(v,x,0,v.length-1);
}

public static int ricerca(int[] v, int x, int inf, int sup){
	if(sup<inf)
		return -1;
	int med=(inf+sup)/2;
	if(v[med]==x)
		return med;
	if(v[med]>x)
		return ricerca(v,x,inf,med-1);
	return ricerca(v,x,med+1,sup);
}
```

- Il test `if(sup<inf)` è il controllo della dimensione banale.
- Le 2 chiamate ricorsive sono "dividi" e dividono a metà v.
- med non dipende dall'input
- Si crea solo una sottoistanza.

Quindi abbiamo per il teorema master, che $a$=1 perché cerchiamo solo un elemento su una metà, c=2 perché dividiamo il vettore in 2 metà, d=0 perché dividendo il vettore in metà e comprendere su quale spostarci, è un'operazione costante.

Quindi $\displaystyle\large {a\over c^d}$=$\displaystyle\large{1\over 2^0}$=1 quindi dato il teorema delle ricorrenze la complessità sarà uguale a: $\displaystyle\large\theta(n^dlog_cn)\Rightarrow \theta(n^0log_2n)\Rightarrow \theta(log_2n)$.

Adesso prendiamo in esame il merge sort:

![[mergesort.jpg]]

![[merge.jpg]]

- a=2 perché si hanno 2 sottoistanze di mergeSort
- c=2 dividiamo il vettore a metà ed ogni sottoistanza ha dimensione $\displaystyle {n\over 2}$
- d=1, questo perchè precedentemente si è visto che il merge ha complessità intrinseca $\theta(n)$ anche perché il merge ha istruzione dominante l'incremento per scorrere tutto il vettore che è lungo n.

Quindi si ha $\LARGE {a\over c^d}$=$\LARGE {2\over 2^1}$=1 perciò il mergeSort ha complessità pari a $\theta(n^dlog_cn)\Rightarrow \theta(n^1log_2n)\Rightarrow \theta(nlog_2n)$

Esaminiamo la complessità spaziale:

Per quanto riguarda il metodo merge si ha complessità spaziale al più n. Per quando riguarda il metodo mergeSort invece, quando la prima chiamata ricorsiva finisce il suo spazio sarà liberato e lo spazio occupato in memoria sarà solo quello della seconda chiamata. Ci serve quindi capire al più quante istanze si hanno attive sullo stack. Visto che ogni chiamata divide in 2 la dimensione, si avranno al più $log_2n$ istanze. La complessità totale è data dalla somma tra le 2 complessità spaziali perciò $\displaystyle\large\theta(n+log_2n)$ ovvero $\displaystyle\large\theta(n)$ che è tanto. Si capisce perciò che il merge sort è un algoritmo di ordinamento adatto alla memoria secondaria.

---
# Quicksort come miglioramento

Esaminiamo adesso il quick sort come possibile miglioramento del merge sort data la sua grande presenza in memoria:

![[quicksort.jpg]]

Nel caso peggiore il pivot che si sceglie è l'elemento più piccolo e la complessità è pari a:

$T(n)=b$  se n≤1

$T(n)=T(n-1)+bn$ se n>1

>Il quicksort si capisce che è di tipo 2, quindi srotoliamo

$T(n)=T(n-1)+bn=T(n-2)+b(n-1)+bn$=$T(n-2)+b\displaystyle\sum_{j=0}^1n-j$=$T(n-3)+b(n-2)+b\displaystyle\sum_{j=0}^1n-j$=$T(n-3)+b\displaystyle\sum_{j=0}^2n-j$ perciò al k-esimo passo $T(n)=T(n-k)+b\displaystyle\sum_{j=0}^{k-1}n-j$.

Quando $n-k=1$ $k=n-1$ perciò $T(n)=T(1)+b\displaystyle\sum_{j=0}^{n-2}n-j=b(n-(n-1))+b\displaystyle\sum_{j=0}^{n-2}n-j=b\displaystyle\sum_{j=0}^{n-1}j=b*{{n(n-1)}\over {2}}={{bn^2-bn}\over 2}$ perciò $T(n)\in \theta(n^2)$.

Si usa il quick sort, perché se capita il caso peggiore, dove il pivot è l'elemento più piccolo allora sarà il caso dove si è più vicini alla disposizione ordinata del vettore.

## Analisi caso medio:

Supponendo che la scelta random del pivot abbia sempre la stessa probabilità, avremo la seguente equazione di ricorrenza:

$T(n)=\displaystyle\sum_{p=0}^{n-1}{1 \over n}(n+T(p)+T(n-p-1))$ dove $\Large {1\over n}$ indica la probabilità della scelta, e T(n-p-1) è il costo di questo caso di quicksort. I termini T(p) e T(n-p-1) hanno lo stesso contributo quindi riscriviamo T(n) come, $T(n)=n+\displaystyle\sum_{p=0}^{n-1}{2\over n}T(p)$.

Ipotizzando che l'algoritmo abbia complessità ricorsiva, si vuole dimostrare che $T(n)\le 2nlogn$. Applicando il metodo della sostituzione, ipotizziamo che esiste una costanze $\alpha$ tale che $T(n)\le \alpha nlogn$. Dimostriamolo attraverso l'induzione:

Per n=1 T(n)=0, per tutti i p tale che p<n vale $T(p)\le \alpha plogp$ sostituiamo in T(n):

$\displaystyle\large T(n)=n-1+\sum_{p=0}^{n-1}{2\over n}\alpha plogp=n-1+{2\alpha\over n}\displaystyle\sum_{p=2}^{n-1}plogp$ adesso poniamo $\displaystyle\large n-1+{2\alpha\over n}\sum_{p=2}^{n-1}plogp\le n-1+{2\alpha\over n}\int_{p=2}^nplogp$

Applichiamo il metodi di risoluzione per parti,

$\displaystyle\int_2^nplogp\space dp$ $g(p)=p$ $F(p)=logp$$\displaystyle\Rightarrow {p^2\over 2}logp-\displaystyle\int_2^n{p^2\over 2}{1\over p}dp={p^2\over 2}logp-{1\over 2}\displaystyle\int_2^np\space dp={p^2\over 2}logp-{1\over 2}{p^2\over 2}$$\displaystyle\huge\vert_2^n$$\displaystyle\large={p^2\over 2}logp-{p^2\over 4}\displaystyle\huge\vert_2^n$=$\displaystyle\large{n^2 logn\over 2}-\large{n^2\over4}-2log2+1$

Perciò data la risoluzione dell'integrale:

 $\displaystyle T(n)\le n-1+{2\alpha\over n}({n^2logn\over2}-{n^2\over4}-2log2+1)\simeq n-1+\alpha logn-{\alpha n\over2}-\alpha {4log2\over n}+{2\alpha\over n}$
 $\large\simeq n-1+\alpha nlogn-{\alpha n\over2}\le\alpha nlogn$ quando $\alpha$≥2 come volevasi dimostrare.

Abbiamo poi [[Algoritmo di Strassen e per moltiplicazioni di interi|ulteriori esempi]].

---


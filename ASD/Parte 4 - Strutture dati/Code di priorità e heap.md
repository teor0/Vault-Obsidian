#asd
[[Albero binario di ricerca e AVL]]
# Code di priorità
Si basano sulle code FIFO, realizzate con Linked List dove si fa append in coda e si rimuove dalla testa, oppure su array circolari e la differenza è che l'array può essere pieno mentre la lista no. Nelle code con priorità gli elementi sono rimossi dalla coda secondo l'ordine stabilito dalla loro proprietà. Consideriamo le seguenti caratteristiche:
1. Le priorità sono elementi di un dominio totalmente ordinato
2. Il dominio delle priorità sia finito e "piccolo" (ovvero indipendente) rispetto alla dimensione della coda.

Bisogna perciò implementare metodi in ed out efficienti alla stessa maniera di una coda tradizionale. Se usassimo un albero AVL avremmo:
- costo operazione in pari a $\theta(logn)$
- costo operazione out pari a $\theta(logn)$ predendo il nodo più a sinistra e si rimuove.
- costo operazione top pari a $\theta(logn)$ si prende il nodo più a sinistra 

Ma perché si prende il nodo più a sinistra? Cambiamo l'ordinamento dell'albero AVL per rendere la ricerca più efficiente, poniamo perciò il minimo nella radice dell'albero binario in modo da abbattere il costro della ricerca. Finiamo cosi nel caso della struttura dati Heap, in questo caso un <font color=red> Heap binario</font>. 
Ricordiamo che l'heap è un albero dove <font color=red>ogni nodo ha un valore minore uguale dei valori nei sottoalberi</font>, non sappiamo però se il sottoalbero sinistro è minore del figlio destro della radice.
Le condizioni da rispettare quindi sono:
1. $\forall$ nodo $u$ dell'heap, il valore contenuto in $u$ è minore dei valori contenuto nei sottoalberi
2. L'heap deve essere completo fino al penultimo livello e con l'ultimo livello riempito da sinistra verso destra

![[invalid.jpg|non valido]]
![[valid.jpg| valido]]

---
## Inserimento e rimozione
Vediamo un esempio di inserimento:
![[esempio.jpg]]
Se dovessimo inserire 7 ci aspetteremo che data la seconda condizione il 7 sia figlio destro di 10, ma questo viola la prima condizione. Per transitività vale che ogni radice deve essere < dei figli, quindi scambiando 7 con 10 e inserendo il 10 come suo figlio destro, verificheremo entrambe le condizioni. 
![[postins.jpg]]
Questo però potrebbe rendere non verificate le condizioni per 1 il padre di 7. Bisogna quindi effettuare un confronto che in questo caso è verificato. 
La rimozione avviene rimuovendo la radice, quindi il minimo o massimo che viene sostituito con l'ultimo nodo aggiunto, ed effettuando eventualmente accorgimenti.

Il costo di una insert è pari a $\theta(logn)$ mentre la rimozione comporta togliere la radice. Il costo delle remove è al più l'altezza quindi $\theta(logn)$, abbiamo perciò migliorato top ma alzato la complessità di in e out. 
Per capire dove effettuare l'inserimento o la rimozione è sufficiente mantenersi il numero di nodi. Fino al penultimo livello si hanno $2^3-1$ nodi. Il numero di nodi che abbiamo è pari a 10 nell'esempio che andremo a trattare. Il numero dei nodi nell'ultimo livello è pari a 10 - $2^3-1$=3. Il numero massimo di nodi nell'ultimo livello è 8. Esempio di inserimento:

![[Tree.png]]
Se voglio inserire un nodo dove dovrei inserirlo? A destra o sinistra? Per capire dove inserire il nodo bisogna scandire l'albero seguendo una logica. Nell'ultimo livello in questo caso si hanno $2^3$=8 nodi e ogni metà ha 8/2=4 nodi. Quindi se voglio inserire un nodo esso sarà il quarto nodo del livello che quindi appartiene al sottoalbero sinistro. Calcolato ciò vado a scandire l'heap ed inserisco il nodo come figlio destro del figlio destro nel sottoalbero sinistro.

---

## Heap basato su array
Innanzi tutto si prende la struttura dell'albero e si indicizzano i nodi:
![[heaparray.png]]

successivamente indicizziamo gli elementi secondo l'ordine in cui saranno nell'array quindi:
```
i= 0 1 2 3 4  5 6  7  8
e= 0 2 6 7 20 8 12 11 10
j= 1 2 3 4 5  6 7  8  9
```
Interpretiamo adesso l'albero dall'array:
padre(j)=$j/2$
figlioS(j)=$j*2$
figlioD(j)=$(j*2)+1$ 
padre(i)=$(i+1)/2-1$
figlioS(i)=$(i+1)*2-1$
figlioD(i)=$(i+1)*2$ 
con $j=i+1$ e $i=j-1$.

---
# Algoritmo di ordinamento heap sort
Vediamo adesso un algoritmo di ordinamento basato su code di priorità, ovvero l'heap sort che consiste in:
1. Prendere tutti gli elementi del vettore da ordinare ed inserirli nella coda di priorità.
2. Scorrere il vettore da sinistra verso destra e per ogni posizione estrae un elemento dalla coda e lo ricopia nella posizione corrente del vettore

L'implementazione è la seguente:

``` java
public static void ordina(Comparable[] v, boolean crescente){
	Heap<Comparable> heap = new Heap(v.length,crescente);
	for(int i =0; i<v.length;i++)
		try {
			heap.in(v[i]);
		} catch (CodaPiena e) {
			e.printStackTrace();
	}
	for(int i =0; i<v.length;i++)
		v[i]=heap.out();
	}
}
```
Essendo il costo di in e di out pari a $\theta(logn)$, ed essendo eseguiti entrambi al più n volte, la complessità è pari a quella del mergeSort ovvero, $\theta(nlogn)$

Se invece di riempire il vettore originario, riempissi la porzione dell'heap che sto svuotando per riordinare senza usare memoria aggiuntiva, ottengo un ottimizzazione che ci porta alla seguente implementazione. Da notare è che se si vuole un ordinamento crescente bisogna usare un vettore con ordinamento opposto, in quanto si usa la parte finale dell'heap per l'ordinamento.

``` java
public static void ordina(Comparable[] v, boolean crescente){
	Heap<Comparable> heap = new Heap(v,!crescente);
	for(int i =0; i<v.length;i++)
		try {
			heap.in(v[i]);
		} catch (CodaPiena e) {
			e.printStackTrace();
	}
// togliere ad uno ad uno gli elementi e metterli nel vettore
// dalla prima posizione verso l'ultima
	for(int i =v.length-1; i>=0;i--)
		v[i]=heap.out();
	}
}
```
Quindi abbiamo un algoritmo che ordina in $\theta(nlogn)$ senza utilizzare memoria aggiuntiva.

---

# Code di priorità con livelli di priorità finiti
Utilizziamo una rappresentazione che assume di avere un array di code FIFO, dove quindi la coda ad indice 0 ha più priorità della coda ad indice 5, che ha più priorità della coda ad 9.

![[codeprioarray.jpg]]

Gli oggetti che si inseriscono sono descritti da coppie del tipo <4,"io">, quindi nella coda associata alla posizione 4 inserisco l'elemento "io". Risulta chiaro che l'inserimento avviene in tempo costante. La rimozione invece richiede 2 operazioni:
1. ricerca nell'array di una coda non vuota $\theta(Dominio\  priorità)$, in particolare la verifica della coda vuota è costante e viene eseguita un numero di volte pari al dominio delle priorità che però essendo indipente dal numero di elementi presenti nella coda si ha complessità $\theta(1)$ 
2. rimozione dalla coda FIFO $\theta(1)$

In sostanza si rimuove il primo elemento della coda più prioritaria non vuota.

---


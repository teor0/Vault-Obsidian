#fondamenti 
[[Instradamento]]
[[Algoritmi di instradamento e protocolli di instradamento]]

# Instrademento come cammino su grafo
L'instradamento equivale a cercare il cammino del grafo distinguendo la ricerca del cammino a distanza minima (grafo non pesato), da ricerca del camminimo a minima lunghezza (grafo pesato).

Gli algoritmi si basano sul costo, però dobbiamo capire che cosa si intende per costo. Se il criterio è il numero di hop questo corrisponde a trovare il cammino di distanza minima. Se ad un hop è associato un costo, una metrica corrisponde a trovare il cammino di lunghezza minima.
La maggior parte degli algoritmi si basano sull'algoritmo di Dijkstra e di Bellman-Ford
Per Dijkstra è importante conosce la topologia di rete e che ogni nodo la conosca.

# Algoritmo di Bellman-Ford
L'algoritmo di Bellman-Ford, individua il cammino a lunghezza minima tra un nodo s e tutti gli altri nodi di un grafo G, aumentando progressivamente il numero di archi. L'algoritmo procede secondo i seguenti passi:
1. individua i cammini minimi tra il nodo sorgente e gli altri nodi raggiungibili con un solo arco.
2. individua i cammini minimi tra il nodo sorgente e gli altri nodi raggiungibili con al più 2 archi.

Si itera il procedimento fino al valore massimo di archi possibili in un cammino.
Vediamo la funzione di aggiornameto. Si considerano comunque i pesi degli archi solo che, il vettore dei cammini a costo minimo è funzione vincolata con il numero di archi non superiore a h, dove h è il massimo numero di archi in un cammino.

$\displaystyle\Large L_0(n)=\infty$ per tutti $\large n\neq S$
$\displaystyle\Large L_h(S)=0$ per tutti i valori di h
La funzione di aggiornamento per $\large h\ge 0$ è:
$\displaystyle\Large L_{h+1}(n)=min_j[L_h(j)+W(j,n)]$

In sostanza il processo è: connettere il nodo n con il nodo predecessore j che raggiunge il minimo, ed eliminare le connessioni di n con altri nodi predecessori individuati in precedenti iterazioni. 
L'algoritmo termina quando h+1 non cambia il valore dei percorsi minimi rispetto all'iterazione precedente cioè: $\displaystyle\Large L_{h+1}(n)=L_h(n)$ $\large\forall n$.
I passi influiscono i successivi in quanto conosco il costo migliore allo step precedente. La complessità dell'algoritmo è nel caso peggiore $\displaystyle\large O(|V^3|)$ dove |V| è il numero di nodi. Questo avviene se la rete è molto connessa, mediamente la complessità è $\displaystyle\large O(|V^2|)$.

Il vantaggio di Bellman-Ford sta nel prestarsi di più ad un'implementazione distribuita nella rete, per cui se si vuole calcolare il costo dei cammini minimi pur non avendo le informazioni aggiornate da nodi distanti dalla nostra rete, con Bellman-Ford si può fare mentre con Dijkstra no. 

---
# Algoritmo di Dijkstra
L'algoritmo di Dijkstra individua il cammino a lunghezza minima tra un nodo s e tutti gli altri nodi di un grafo G aumentando progressivamente la distanza. L'algoritmo procede secondi i seguenti passi:
- Al passo k-esimo sono individuati tutti i k nodi raggiungibili dal nodo sorgente tramite i cammini a costo minimo. Tali nodi formano l'insieme T
- al passo k+1 è aggiunto un altro nodo all'insieme T caratterizzato dal cammino a costo minimo dal nodo s che transita solo in nodi del insieme T
- l'algoritmo termina quando sono esplorati tutti i nodi

Notazioni:
- N: insieme dei nodi del grafo
- s: nodo sorgente
- T: insieme nodi raggiunti dall'algoritmo
- w(i,j): peso del ramo(i,j)
- L(n): costo del cammino a costo minimo tra s e n

All'inizio T={s} L(n)=w(s,n) con $\large n \ne s$. Al passo k, bisogna trovare il nodo $x \notin T$ a distanza minima da s, tale che $\large L(x)= min_{j\notin T}L(j)$, si aggiunge x a T e si aggiornano i cammini minimi, $\large L(n)=min[L(n),L(x)+w(x,n)]$ $\forall n \notin T$ 

La complessità dell'algoritmo è $O(V^2)$, perché ci sono |V|-1 iterazioni e per ogni iterazione il numero di operazioni effettuate è proporzionale a |V|.

---

# Differenze tra Bellman-Ford e Dijkstra
I due algoritmi convergono alla stessa soluzione, solo che Bellman-Ford nel caso peggiore è più complesso ma a differenza di Dijkstra non presuppone che un nodo conosca tutta la topologia della rete ed il peso di tutti i rami, ma necessita di un colloquio solo tra nodi adiacenti. Come visto nelle definizioni inoltre, Dijkstra calcola il camminimo a lunghezza minima aumentando progressivamente la distanza, mentre Bellman-Ford aumenta progressivamente il numero di rami. 

---
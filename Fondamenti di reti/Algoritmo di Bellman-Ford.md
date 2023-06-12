#fondamenti 
[[Instradamento]]
[[Algoritmi di instradamento e protocolli di instradamento]]

# Instrademento come cammino su grafo
L'instradamento equivale a cercare il cammino del grafo distinguendo la ricerca del cammino a distanza minima (grafo non pesato), da ricerca del camminimo a minima lunghezza (grafo pesato).

Gli algoritmi si basano sul costo, però dobbiamo capire che cosa si intende per costo. Se il criterio è il numero di hop questo corrisponde a trovare il cammino di distanza minima. Se ad un hop è associato un costo, una metrica corrisponde a trovare il cammino di lunghezza minima.
La maggior parte degli algoritmi si basano sull'algoritmo di Dijkstra e di Bellman-Ford
Per Dijkstra è importante conosce la topologia di rete e che ogni nodo la conosca. L'algoritmo di Bellman-Ford individua il cammino a lunghezza minima tra un nodo S e tutti gli altri nodi di un grafo G, aumentando progressivamente il numero di archi. 

# Algoritmo di Bellman-Ford
L'algoritmo di Bellman-Ford procede secondo i seguenti passi:
1. individua i cammini minimi tra il nodo sorgente e gli altri nodi raggiungibili con un solo arco.
2. individua i cammini minimi tra il nodo sorgente e gli altri nodi raggiungibili con al più 2 archi.

Si itera il procedimento fino al valore massimo di archi possibili in un cammino.
Vediamo la funzione di aggiornameto. Si considerano comunqeu i pesi degli archi solo che, il vettore dei cammini a costo minimo è funzione vincolata con il numero di archi non superiore a h, dove h è il massimo numero di archi in un cammino.

$\displaystyle\Large L_0(n)=\infty$ per tutti $\large n\neq S$
$\displaystyle\Large L_h(S)=0$ per tutti i valori di h
La funzione di aggiornamento per $\large h\ge 0$ è:
$\displaystyle\Large L_{h+1}(n)=min_j[L_h(j)+W(j,n)]$

In sostanza il processo è: connettere il nodo n con il nodo predecessore j che raggiunge il minimo, ed eliminare le connessioni di n con altri nodi predecessori individuati in precedenti iterazioni. 
L'algoritmo termina quando h+1 non cambia il valore dei percorsi minimi rispetto all'iterazione precedente cioè: $\displaystyle\Large L_{h+1}(n)=L_h(n)$ $\large\forall n$.
I passi influiscono i successivi in quanto conosco il costo migliore allo step precedente. La complessità dell'algoritmo è nel caso peggiore $\displaystyle\large O(|V^3|)$ dove |V| è il numero di nodi. Questo avviene se la rete è molto connessa, mediamente la complessità è $\displaystyle\large O(|V^2|)$.

Il vantaggio di Bellman-Ford sta nel prestarsi di più ad un'implementazione distribuita nella rete, per cui se si vuole calcolare il costo dei cammini minimi pur non avendo le informazioni aggiornate da nodi distanti dalla nostra rete, con Bellman-Ford si può fare mentre con Dijkstra no. 


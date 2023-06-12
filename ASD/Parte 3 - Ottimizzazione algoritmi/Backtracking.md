
---
created: 2022-10-03 16:32:02
updated: 2022-10-03 17:56:22
---
#asd 
[[Alberi di decisione]]
# Backtracking
Il backtracking è una tecnica algoritmica, che si presta bene a risolvere problemi del tipo: assegna un valore preso da un dominio K a ciascuno degli $n$ elementi di un vettore soluzione V in modo che siano soddisfatti un'insieme di vincoli su tali valori.

$V=[v_0,v_1,...v_n]$ con $v_i\in K$

Dato un problema P, l'obiettivo di una tecnica backtracking è trovare una soluzione $V\in V_P$ (dove $V_P$ è l'insieme delle possibili soluzioni candidate) tale che $X_P(V)=true$ ovvero i vincoli imposti dal problema siano soddisfatti. 
Per risolvere un problema abbiamo utilizzato la ricerca esaustiva, dove generiamo tutte le possibili soluzioni e verifichiamo se una di essa soddisfa i requisiti, quindi ho una complessità del tipo $|K|^n$, in pratica per ogni $n$ scelte ho |K| possibilità ovvero il numero di elementi che devo assegnare.

Il backtracking è una sorta di ricerca esaustiva ma "furba", in quanto ad ogni assegnamento verifica se i requisiti sono soddisfatti. I problemi di backtracking in genere sono di ricerca e le soluzioni si possono rappresentare graficamente attraverso alberi di ricerca. Importante per un problema di backtracking è individuare quali sono: le scelte, i punti di scelta ed i vincoli!

---
## Esempio
Vediamo adesso il problema delle sottostringhe adiacenti uguali di dimensione n. In sostanza dato un insieme di caratteri, si vuole generare una stringa di dimensione $n$ tale per cui non esistano delle sottostringhe adiacenti che sono uguali. Se K={0,1,2} ed n=3 la stringha x=001 non è valida mentre y=010 si.

L'albero di ricerca rappresenta lo spazio delle soluzioni, in particolare ogni nodo rappresenta un punto di scelta, ogni arco rappresenta una scelta fatta in una specifica posizione. Le soluzioni candidate sono sulle foglie e possono essere raggiunte percorrendo il cammino che va dalla radice ad esse.

---

# Branch & bound (facoltativo)
La tecnica del branch & bound si può usare su problemi di ottimizzazione per trovare la soluzione $V^*= max|min{f(V)}$ dove $ $V\in V_P$ tale che $X_P(V)=true$. Vogliamo quindi trovare la funzione obiettivo massima o minima. La tecnica esplora l'albero di ricerca in modo furbo, cioè quando una porzione dell'albero non porta ad una soluzione ottima smette di visitare quella porzione. Ovviamente si ha bisogno di un indice che rappresenta la qualità della soluzione che dipende però dal problema.

Esempio: voglio cambiare una moneta da 8 centesimi avendo a disposizione le monete da 1, 4 e 5 centesimi in modo tale da effettuare il cambio utilizzando il minor numero di monete. 
![[branchnbound.jpg]]
Mentre il backtracking necessita di una visita in profondità, il branch & bound può adoperare sia una visita in profondità, sia una visita in ampiezza.

---



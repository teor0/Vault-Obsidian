---
tag: #basi 
created: 2023-01-13 11:08:14
updated: 2023-01-13 11:08:14
---
#basi 
[[Tecniche basate su B-Tree]]
# B+-Tree
Nei database commerciali si usano i $B^+-Tree$ dove i nodi non foglia sono fatti come di seguito:
![[bplustreenode.jpg]]
non c'è per ogni chiave il puntatore dov'è memorizzata la tupla. I nodi foglia invece hanno la seguente struttura:
![[bplustreeleaf.jpg]]
non hanno le barrette laterali per i figli, essendo appunto foglie ed hanno il puntatore alle pagine con i dati a differenza dei nodi non foglia. Tutti i nodi a livello foglia hanno dei puntatori che generano una lista concatenata, questo vuol dire che nell'ultimo livello sono riportate tutte le chiavi indicizzate, ordinate in senso lessicografico rispetto alla chiave di ricerca.
Nel $B^+-Tree$ i nodi intermedi presentano una serie di chiavi e puntatori con lo stesso criterio di ordinamento del B-Tree ma non presentano il puntatore per trovare la tupla. Questo perché le chiavi in un livello intermedio sono ripetute nel livello foglia. 
Esempio:
![[esempbplustree.jpg]]
Le operazioni cambiano poco da quelle del B-Tree. Novità sono puntatori avanti ed indietro rispetto a foglie che si trovano allo stesso livello, questo lo rende molto idoneo a ricerche per range. Un nodo intermedio di un $B^+-Tree$ può contenere più chiavi di un nodo intermedio di un B-Tree, in quanto si risparmi sul costo dei puntatori quindi il grado del $B^+-Tree$ sarà più grande e $log_m$ più piccolo. Anche se le chiavi nei nodi intermedi sono ripetute, la maggior parte di esse sono in nodi foglia. 

L'indice è staccato dai nodi foglia, se faccio una ricerca per range accedo all'indice e poi alle pagine se uso una chiave primaria. Se non sono ordinate rispetto ad una chiave primaria bisogna scandire l'albero e trovare la chiave che desidero e poi accedere a tutte le pagine indicizzate. L'indice è staccato rispetto a come si memorizzano le chiavi.

>Scandire le pagine è più efficiente di scandire i nodi.

Quando i dati sono memorizzati rispetto alla chiave di ricerca usata nell'indice, si dice che l'indice è <font color=red>clustered</font>, quindi l'indice è definito su una chiave di ricerca che definisce anche l'ordinamento dei dati nelle pagine dati. Se un indice è clustered posso rappresentare alcune tuple e non tutte per forza, rendendo così l'indice sparso. L'indice sparso si può usare solo se l'indice è clustered!
Per gli attributi non chiave si usa un livello intermedio tra i nodi ed i dati attraverso una tabella. La tabella contiene ogni valore del attributo e vengono elencate le pagine, questa tabella a sua volta viene divisa in pagine, a tali pagine punteranno le foglie del $B^+-Tree$.

---


#asd 
[[Cammini minimi per grafi pesati ed albero dei cammini minimi]]
# Caratteristiche dell'algoritmo
Questo algoritmo è un algoritmo goloso come quello di Prim, quindi sfrutta alberi come soluzioni parziali.
Come ipotesi supponiamo:
I: (G,S), O: albero cammini minimi
$\large\forall e\in E$ si ha $\lambda(e)\ge 0$ quindi ogni peso degli archi di G è positivo o 0.
A differenza di Prim cambia la funzione di costo. Parte da A ed anche lui considera un arco in più che parte da nodi appartenenti ad A e che va verso nodi che non appartengono ad A per estendersi.
![[dijkstraA.png|500]]
Fra tutti gli archi come funzione di costo usa il costo dei cammini più costosi che posso percorrere nell'albero dalla radice verso un altro nodo e prende il minimo.
Il taglio resta uguale ma la radice dell'albero è fissata al nodo sorgente. Inizialmente abbiamo un albero con radice il nodo sorgente che ha ovviamente distanza 0. Graficamente:
![[taglioA.png]]
scegliamo l'arco verso 1 inquanto comporta il cammino minore.
![[taglioB.png]]
successivamente sceglia il cammino 0,2 in quanto ha costo 2 a differenza del cammino 0,1,2 che ha costo 3 oppure 0,1,5 che ha sempre costo 3. Andando avanti seguendo il criterio dell'algoritmo si avrà:
![[taglioFinale.png]]

---
## Controesempio per dimostrare che Dijkstra non funziona sempre
Adesso vediamo un esempio per dimostrare che Dijkstra non funziona sempre:
![[ce1.png]]
![[ce2.png]]
costo([0,1,3,4])=4
costo([0,2,3,4])=0

---
## Dimostrazione della buona funzionalità di Dijkstra
Trovo una proprietà invariante per ogni passo per dimostrare la correttezza. La proprietà che andrò ad utilizzare è:
Per $A^i$ $\exists A^*$ tale che $\forall e \in A^i$ $A^*$ li contiene tutti. Dove $A^i$ è l'albero al passo i-esimo e $A^*$ è l'albero dei cammini minimi.

$A^0$ non ha archi quindi vale banalmente per induzione, se la proprietà invariante vale al passo i ed è vera al passo i+1 allora vale per tutti i passi. Per dimostrare ciò consideriamo che esiste $A^{i+1}$ tale che esiste un arco $e^i$ che va verso nodi che non appartengono a $A^i$.
Se $\large e^i\in A^*$ allora tutti gli archi di $A^{i+1}$ sono contenuti in $A^*$.
Se $\large e^i\notin A^*$ esiste un altro cammino che parte dalla radice e finisce nel nodo terminale v dell'arco $e^i$.

Consideriamo $A'^*=A^*-e'+e^i$, dove e' è l'arco finale del cammino che porta al nodo terminale v. Cosa succede nei nodi tra $A'^*$ e $A^*$? Cambia il modo di raggiungere v e tutti i nodi che sono raggiungibili in $A^*$ partendo da v. Basta che il costo per raggiungere v in $A'^*$ sia uguale a quello di $A^*$ affinché anche $A'^*$ sia un albero dei cammini minimi. Dimostrazione:

C=[S,...,u,v]=$\delta$
C'=[S,...,u',v',v'',...,v''',v]
Dove [S,...,u',v']=$\delta$' e [v'',...,v''',v]=$\delta$''
$\large\delta\le\delta '$ perché sono cammini considerati nel taglio quindi per raggiungere v' si aveva una distanza al massimo pari a quella di v. Inoltre $\large\delta ''\ge 0$ il costo(C')=$\large\delta '+\delta ''$ e costo(C)=$\delta$ dalle relazioni posso ricavare: costo(C)$\le$costo(C') quindi il modo di raggiungere v è valido perciò anche $A'^*$ è un albero dei cammini minimi.

---
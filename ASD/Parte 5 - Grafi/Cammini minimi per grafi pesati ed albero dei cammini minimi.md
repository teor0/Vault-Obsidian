#asd 
[[Algoritmo di Kruskal e union find]]
# Cammini minimi per grafi pesati
Dato un certo cammino [$\large u_0,...,u_k$] il costo del cammino C non è altro che:
$\displaystyle\large\sum_{i=0}^{k-1}\lambda((u_i,u_{i+1}))$ assumendo G=<N,E,$\lambda$> 

Dati 2 nodi $u_0,u_k$ ed un cammino C da $u_0$ a $u_k$, C è un cammino di costo minimo detto anche cammino minimo da $u_0$ a $u_k$ se e solo se per ogni cammino C' da $u_0$ a $u_k$ si ha:
costo(C)$\le$costo(C')

Dati 2 nodi $u_0$,$u_k$ la distanza da $u_0$ a $u_k$ d($u_0$,$u_k$)=costo(C), dove C è un cammino minimo da $u_0$ a $u_k$.
Esempio: ![[camminomin.png]]
$C_1$=[0,2,3,4]
costo($C_1$)=2+1+2=5

Nelle definizioni non si è usato il cammino semplice in quanto in alcuni grafi è possibile che $\lambda$ possa ritornare pesi negativi. Quindi $C_1$ è un cammino minimo e la distanza tra 0 e 4 è pari a 5. Prendiamo un cammino $C^*$=[0,2,3]=-1 e sia C'=$C^*$,$C^*$,$C^*$,...$C^*$,[0,2,3,4] dove $C^*$ è ripetuto per 100 volte. Abbiamo perciò che $C^*$x100 =-100 ed essendo [0,2,3,4]=5 abbiamo che C'=-95, le distanze minime fra coppie di nodi non sono definite per ogni grafo. Siamo sicuri che le distanza minime sono definite per ogni coppia nel grafo se e solo se nel grafo non sono presenti dei cicli il cui costo sia negativo. In presenza di esso non si ha certezza in quanto il concetto di distanza non è limitato inferiormente, ossia d=-$\infty$ è possibile.

---
# Albero dei cammini minimi
Dato G=<N,E,$\lambda$> consideriamo S$\in$N (S nodo sorgente), A=<$N_S$,$E_A$,$\lambda_A$> albero "ricoprente" di G tale che $\large\forall u\in N$, $\large u\ne S$ $\large d_A(S,u)=d_G(S,u)$. Dove $N_S$ sono i nodi raggiungibili da S in G. Esempio: 
![[albcammin.png]] dove S=0
![[acm.png]]
> Dato un nodo non è detto che esiste un albero dei cammini minimi ricoprente rispetto al grafo. L'albero che vorremmo è quello che abbia la proprietà rispetto ai nodi raggiungibili dal nodo sorgente.

---
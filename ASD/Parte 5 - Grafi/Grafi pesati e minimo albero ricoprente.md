#asd 
[[Algoritmi per verificare l'aciclicità]]
# Grafi pesati
Usiamo grafi pesati quando vogliamo mantenere informazioni relative ai nodi oppure relative agli archi oppure entrambe le cose. 
Il primo caso è molto semplice, per rappresentare informazioni sui nodi, si può usare un array che mantiene queste informazioni. Si potrebbe usare un array di Object che nella i-esima posizione, contiene informazioni rispetto al nodo i-esimo.
Nel secondo caso si parla di grafi pesanti sugli archi, che tipo di informazione si vorrebbe contenere? Nella visita BFS si voleva tenere conto del numero minore di archi per raggiungere un nodo. Per esempio per raggiungere il nodo 4 il percorso più breve è 0,1,4 ma solo se gli archi hanno costo "uguale". ![[pesi.jpg]]
Se ad ogni arco assocciassimo un costo il percorso più breve potrebbe cambiare. ![[pesato.jpg]]
Per le liste di incidenza e la matrice di incidenza visto che rappresentano l'insieme degli archi per ogni arco basta rappresentare il peso. Per le liste di adiacenza e la matrice di adiacenza invece bisogna fare altro:
![[matricepesi.jpg]] 
![[esempiomatricepesi.jpg]]
Se il peso indica il costo di percorrenza, allora per gli archi mancanti uso 0 e $\infty$ se non ho un arco che arriva al nodo

---

# Minimo albero ricoprente
Dato un grafo, un grafo pesato è formato da N insieme dei nodi, E insieme degli archi e $\lambda$ funzione di etichettatura cioè $\lambda:E\rightarrow P$, dove P sono interi, reali ecc.

Dato un grafo non orientato e pesato sugli archi G=<N,E,$\lambda$>, A=<$N_A$,$E_A$,$\lambda_A$> è un <font color=red>albero ricoprente</font> di G se solo se: ^7ccbee
1. N=$N_A$ insieme di nodi coincidono
2. $E_A\subseteq$ E
3. $\forall$ e $\in$ $E_A$ $\lambda_A(e)=\lambda(e)$ peso uguale
4. A è un albero

Esempio:
![[grafo.jpg]]
![[A.jpg]] valido
![[B.jpg]] non valido in quanto $N\ne$$N_A$
![[C.jpg]] non valido in quanto $\lambda_C(3)$$\ne$$\lambda(3)$
![[D.jpg]] non valido perché non è un albero
Noi però cerchiamo il minimo albero ricoprente, ma per averlo devo confrontare gli alberi e vederne il costo. Il costo di un albero ricoprente è uguale alla sommatoria del costo degli archi:

costo (A)=$\displaystyle\large\sum_{e\in E_A}\lambda_A(e)$
Costo A=1+1+2+1+3=8, in questo caso A è un minimo albero ricoprente per G se: A è un albero ricoprente e se per tutti gli alberi ricoprenti di G costo(A)$\le$costo(B)

---
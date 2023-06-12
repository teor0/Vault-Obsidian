#asd
[[Grafi e problema even path]]
# Strutture per i grafi orientati
Per i grafi orientati una possibilità è la lista di archi di G, modo più semplice ma non molto efficiente. Un altro modo è la lista di adiacenza dove, per ogni nodo manteniamo la lista dei nodi che sono raggiungibili tramite un arco. Esempio adiacenza:
![[lista.jpg]]
Se voglio sapere su quali nodi mi posso muovere partendo da $a$, guardo la lista.
Questo operazione non può mettere un tempo inferiore dal punto di vista asintotico al <font color=red>grado di uscita del nodo</font>, $a$ in questo caso. Per la lista degli archi devo scansionare tutta la lista e segnarmi tutti gli archi con primo nodo a.
Un'altra rappresentazione è quella a liste d'incidenza dove attraverso delle liste, si mantiene il riferimento all'indice di una lista di archi, più flessibile nel caso in cui si hanno informazioni aggiuntive per gli archi, risulta quindi una combinazione tra lista di adiacenza e lista di archi. Anche in questo caso l'operazione per conoscere quali nodi posso raggiungere da $a$ ha un <font color=red>costo lineare rispetto al grado di uscita</font> di $a$. Esempio incidenza:
![[adiacenza.jpg]]
![[incidenza.jpg]]
Poi c'è la matrice d'adiacenza fatta come segue: 
- righe e colonne rappresentano i nodi del grafo
- ogni cella che associa la coppia di nodi assume 0 oppure 1, dove 0 indica l'assenza dell'arco e 1 indica la presenza.
![[matadia.jpg]]

Per sapere quali nodi sono raggiungibili si scandisce la riga di n elementi che potrebbe essere nel caso peggiore proporzionale al grado di uscita ma in realtà è molto di più. 
Verificare un arco tra ad esempio b e d, ha <font color=red>costo costante</font> molto più efficiente del caso in cui si usa la lista di adiacenza.
L'ultima struttura dati che può essere usata è la matrice di incidenza, (matrice n\*m), dove:
- gli indici delle righe sono i nodi
- gli indici delle colonne sono gli archi
![[matinci.jpg]]

Il costo anche in questo caso è quello di scandire la riga e:
- si trova 1 se l'arco è uscente da quel nodo
- si trova -1 se l'arco è entrante in quel nodo
- si trova 0 se l'arco non c'è

Il costo sarà proporzionale al numero di nodi m, la verifica della presenza di un arco è sempre costante, in più la verifica dei nodi dai quali posso raggiungere un altro nodo è compresa.
Questa operazione con le liste è pari alla scansione di tutte le liste quindi proporzionale a n. Nella matrice di incidenza accedo gli archi in cui ho -1, nella matrice di adiacenza ha costo pari ad $n$ perchè scorro tutta la colonna e prendo solo gli 1.

![[grafiorstrutt.jpg]]

---

# Struttere per grafi non orientati
Per i grafi non orientati si usano le stesse strutture ma con degli accorgimenti. La matrice di adiacenza ad esempio è simmetrica e questo può favorire alcuni "trick".
![[strutt.jpg]]
Prestazioni lista di archi:
![[prelarchi.jpg]]
Prestazioni lista di adiacenze:
![[preladia.jpg]]
Prestazioni matrice di adiacenza:
![[premadia.jpg]]
Le più utilizzate sono la lista e matrice di adiacenza.

---
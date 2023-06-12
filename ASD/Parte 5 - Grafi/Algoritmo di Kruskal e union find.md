#asd
[[Algoritmo di Prim e tecnica invariante]]
# Algoritmo di Kruskal
L'algoritmo di Kruskal è sempre una tecnica golosa, che calcola il minimo albero ricoprente come Prim.  A differenza di Prim rinuncia alla quarta condizione, ovvero A è un albero e mantiene le prime 3. 
1. N=$N_A$ insieme di nodi coincidono
2. $E_A\subseteq$ E
3. $\forall$ e $\in$ $E_A$ $\lambda_A(e)=\lambda(e)$ peso uguale

Per Kruskal A deve essere una foresta, la foresta quindi viene utilizzata per le soluzioni parziali.

Kruskal presa una foresta F, considera le varie foreste che ottiene aggiungendole a F. Come politica di costo si sceglie la foresta che contiene il costo più piccolo (dopo aver aggiunto un arco).
Inizialmente considera una foresta senza archi, perciò costo 0. Poi aggiungendo un arco prende la foresta di costo minimo. Considero quindi gli archi con peso minore. Esempio:
![[foresta.jpg]]
prendo ad esempio![[f1.png]]
poi prendo ![[f2.png]]
poi ![[f3.png]]
infine arrivo a ![[f4.png]]
L'arco tra 5 e 7 non può essere aggiunto in quanto aggiungerei un ciclo. Per capirlo basta verificare se si può aggiungere 7 partendo da 5 nella foresta corrente, anche se c'è un modo più semplice. Alla fine avrò una foresta dopo tutti i passaggi quale:
![[ff.png]]
Dimostrazione per assurdo è triviale in quanto basta il modo in cui considera gli archi per dimostrare che restituisce un minimo albero ricoprente.

>Ricorda che la foresta è un grafo non orientato aciclico

---
# Union find
L'implementazione non è efficiente al punto da avere una complessità pari a quella di Prim. Serve una struttura dati aggiuntiva, la union find.

La union find consente di rappresentare una partizione di un insieme, ricordando che una partizione è:
> Dato un insieme S, una partizione P di S è un insieme di sottoinsiemi di S che ha le seguenti proprietà: $\forall S_i,S_j\in P$ | $S_i$ $\cap$ $S_j$= $\oslash$ ovvero coppie disgiunte di sottoinsiemi.
$\displaystyle\large\bigcup_{S_i\in P}$$S_i=S$ preso qualunque insieme di S questo appare in almeno un sottoinsieme che appartiene a P.

Queste 2 proprietà ci dicono che preso un elemento di S questo appare in uno ed un solo elemento di P. ![[insieme.png]]
A,B e C sono sottinsiemi che formano P.

La union find rappresenta la partizione. Operazioni applicabili a union find:
- find: come input si prende un elemento x appartenente ad S. Output l'insieme $S_i\in P$ tale che $x\in S_i$
- union: riceve in input 2 insiemi $S_i$,$S_j$ $\in P$, e modifica la partizione P in modo che $P=P-${$S_i,S_j$} $\cup$ {$S_i$ $\cup$ $S_j$}

Esempio find(3):
![[find.png]]
Esempio union($S_0,S_1$):
![[union.png]]
Un'altra operazione è makeSet, un'operazione di inizializzazione, che riceve in input un elemento ed inserisce l'insieme che contiene quel elemento in P.

Usiamo ora questa foresta: ![[funion.png]]
per prendere la foresta vuota F e le sue componenti massimali che su una union find equivale alla makeSet di ogni nodo. ![[fcompmass.png]]
Prendiamo adesso gli archi con peso minimo ed eseguiamo Kruscal:
- (0,1) 1
- (2,5) 1
- (3,6) 1
- (0,2) 2
- (2,3) 2
- (1,3) 2
- (1,4) 2

prendiamo il primo arco, essendo 0 e 1 componenti connesse massimali a parte, non ci sono cammini quindi senza lanciare la visita capisco che non c'è un ciclo se aggiungo (0,1). Eseguite le 2 find verifico se sono 2 insiemi diversi, se si metto l'arco nel grafo.
Adesso 0 non è una componente connessa massimale. L'idea è che una volta inserito l'arco, si va a chiamare la union dei 2 insiemi. Quindi avremo:
![[makeset.png]]
Prima avevo l'insieme di tutte i nodi connessi a 0 e 1, adesso ho l'insieme di tutti i nodi connessi a 0 e 1 per ogni arco chiamo quindi 2 find ed eventualmente anche una union. Tengo aggiornate le componenti connesse massimali fino a che, quando trovo 2 find uguali (1 e 3) non eseguo una modifica.
> Nel caso peggiore eseguo: 2m find e (n-1) union

L'obiettivo diventa trovare strutture dati per rendere efficienti find ed union. Però c'è un problema, non si può avere una struttura che rende efficaci entrambi, abbiamo quindi strutture di tipo QuickFind e QuickUnion. 

Per le QuickFind vogliamo che la complessità sia $\theta(1)$. Tipicamente dal punto di vista logico, associamo ad ogni sottoinsieme un albero in cui la radice ha il nome dell'insieme e le foglie rappresentino gli elementi dell'insieme. 
Per QuickUnion voglio creare per forza l'albero d'altezza 1, per farlo accedo a $S_j$, itero i suoi figli e cambio il puntatore al padre. Anche qui ho un numero di operazioni costanti. In alcuni casi potrei avere un costo proporzionale al costo di tutta la partizione ovvero $\theta(n)$ si nota che se devo fare union($S_i,S_j$) con $|S_i|$=1, $|S_j|=n-1$ faccio n-1 spostamenti quando basterebbe fare 1. 
> Nel caso peggiore con $|S_i|=\displaystyle{n\over 2}$ e $|S_j|=\displaystyle{n\over 2}$ per come mi muovo sposto $\displaystyle{n\over 2}$ elementi

Quindi nel caso peggiore di una union nella QuickFind si ha complessità lineare, ma tornando indietro mi accorgo che si fanno (n-1) di union. 
Posso fare 2n union in un algoritmo? No, perché se faccio union tra $S_i$ e $S_j$, avrò che:
Sia $S_{ij}$ la union tra loro: $|S_{ij}|\ge$ $2*minimo(|S_i|,|S_j|)$,
se $|S_i|\lt |S_j|$ allora $|S_{ij}|$=2$|S_i|$+$|S_j|-|S_i|$, dove la differenza $|S_j|-|S_i|$ è al più =0.
Quindi ogni union raddoppia la cardinalità. Indichiamo con $S^*$ l'insieme dove abbiamo fatto (n-1) union quindi avremo 1x2x2x2... quindi $|S^*|\ge|S^{n-1}|$ quindi per forza non faremo 2n union. 

Quanto costano queste n-1 operazioni di unione nel caso peggiore? Prendiamo union($S_i$,$S_{MAX}$) dove $|S_i|=1$ e $|S_{MAX}|$ è quella con più elementi nella partizione.  Il numero di spostamenti fatti durante n-1 union è pari a:
$\displaystyle\large\sum_{i=1}^{n-1}i$=$\displaystyle\large{n\times (n-1)\over 2}$ ovvero $\theta(n^2)$

Una banale ottimizzazione della QuickFind è QuickFind con bilanciamento sull'unione. Se union($S_i,S_j$) con $|S_i|\le |S_j|$ sposta gli elementi di $S_j$ in $S_i$ altrimenti sposta gli elementi di $S_i$ in $S_j$ e rinomina $S_j$ in $S_i$. Se l'applichiamo al caso esaminato farò n-1 spostamenti. Per realizzare ciò devo essere in grado di calcolare la cardinalità degli insiemi in tempo costante. Semplicemente nella radice mi tengo il numero di elementi. 
Il caso peggiore ha $\large{n\over 2}$ spostamenti per $log_2n$ altezza dell'albero. Quindi $\displaystyle\large {n\over 2}log_2n$ $\Omega(nlogn)$. Dimostriamo come arrivare a $O(nlogn)$.

Utilizziamo il metodo dei crediti assegnando $log_2n$ crediti ad ogni elemento sotto ipotesi che, spendo un credito per spostare un elemento da un insieme ad un altro. 
>Tecnica usata per la complessità ammortizzata per array estendibili.

Prendiamo un generico elemento x e denotiamo con $S_x^i$ l'insieme dove x è stato spostato dopo $i$ unioni. Per ipotesi $\displaystyle\large|S_x^i|\gt log_2n$. 

$|S_x^0|$ ha almeno un elemento, ovvero x quindi $|S_x^0|\ge 1$
$|S_x^1|$ quanto vale? In una generica union($S_x^0,S^*$) si ha che 
$|S_x^0|\le |S^*|$ $\Rightarrow$ $|S_x^1|$=$|S_x^0|+|S^*|$ $\Rightarrow$ $|S_x^1|$=2$|S_x^0|+|S^*|-|S_x^0|$ dove $|S^*|-|S_x^0|$ è $\ge 0$, quindi $|S^1|\ge 2|S_x^0|$ ed andando avanti avremo che $\displaystyle\large|S_x^i|\ge 2|S_x^{i-1}|$ $\Rightarrow$ $\displaystyle\large|S_x^i|\ge 2^i|S_x^0|\ge2^i$

Per $\large|S_x^{log_2n}|\ge 2^{log_2n}\ge n$ quindi non può mai succedere che abbia un valore di i > $log_2 n$. Quindi per assurdo si è dimostrato che più di $log_2 n$ non può essere spostato ed arrivato a $log_2 n$ avrò un insieme che contiene tutti gli elementi della partizione. 

Costo di Kruskal senza union find è di $\theta(m*n)$ con la union find è $\theta(m log n)$

---

#asd
[[Grafi pesati e minimo albero ricoprente]]
# Algoritmo di Prim
Si basa sulla tecnica golosa, parte di tecniche esplorative che esplorano uno spazio delle possibili soluzioni (anche parziali) ad un certo problema, finché non trovano la soluzione desiderata. Per esplorare lo spazio iteriamo fino a che ci troviamo in una soluzione, se questa non è la soluzione cercata ci spostiamo in una delle altre soluzioni e ripetiamo ciò finché o si trova la soluzione o se non ce ne sono altre possibili. 

Le tecniche golose hanno bisogno delle soluzioni su cui spostarsi definite per spostarsi. Queste tecniche hanno in comune il modo in cui decidono in quale fra le possibili soluzioni raggiungibili dalla soluzione corrente mi sposto. Associamo ad ognuna delle possibili soluzioni in cui mi posso muovere un costo. La tecnica golosa prevede di spostarsi nella soluzione in cui, in quel momento per spostarmi pago di meno e non rivedere questa scelta in futuro. 

>La tecnica backtracking è esplorativa ma non è golosa.

Prim dato un grafo ha come spazio delle possibili soluzioni alberi A=<$N_A$,$E_A$,$\lambda_A$> per cui valgono le condizioni 2,3 e 4 della definizione di [[Grafi pesati e minimo albero ricoprente#^7ccbee| albero ricoprente]], la prima quindi può non valere.
Se la soluzione corrente è A=<$N_A$,$E_A$,$\lambda_A$> mi posso spostare in alberi che hanno struttura A=<$N_A\cup{u}$, $E_{A'}\cup <u',u>$, $\lambda_{A'}$> dove u$\in$N ma u$\notin$$N_A$ inoltre:
- u' $\in$ $N_A$, <u',u>$\in$E
- $\forall$e$\in$$E_A$: $\lambda_A(e)\equiv$$\lambda_{A'}(e)$ e $\lambda_A(<u',u>)$=$\lambda(<u',u>)$

Come costo prendiamo il costo dell'albero. Esempio:
![[esprim.jpg]]
La prima soluzione è l'albero vuoto, poi si aggiunge un nodo qualunque con il costo minore, in questo caso aggiungo i nodi albero nel seguente ordine: 0,1,4,5. Si arriva poi ad una situazione del tipo
![[taglio.jpg]]
La linea descrive il taglio del grafo, che è una partizione dei nodi del grafo originale, in nodi che fanno parte della soluzione corrente ed i rimanenti nodi del grafo. Tutti gli archi <u,v> che hanno come nodo u, un nodo della soluzione corrente e nodo v un nodo che non lo fa, costituiscono il taglio. Scegliere la soluzione minore, consiste nel prendere l'arco di costo minore che attraversa il taglio. Alla fine avremo speranzosamente l'albero ricoprente minimo perchè la tecnica golosa non da assicurazioni. È possibile dimostrare che Prim trova un minimo albero ricoprente se il grafo in input è connesso, ovviamente ci possono essere più di uno come di seguito
![[alberoricoprente.jpg]]
in questo caso ci sono 4 alberi ricoprenti.

# Formalizzazione pratica di Prim
Dato $\lambda$, $\lambda_X$ è la restrizione tale che X-P ovvero, $\lambda:N\rightarrow P$ $\lambda_X:X\rightarrow P$ 
$\forall x$ $\in$ X $\lambda(x)=\lambda_X(x)$

Sia G un grafo non orientato pesato, sia A l'albero soluzione parziale, allora:
G=<N,E,$\lambda$>
A=<{$n_0$, $\oslash$, $\lambda_{\oslash}$}
generalmente: A=<$N_A$,$E_A$,$\lambda_{E_A}$>

Prim usa la funzione di taglio di G rispetto ad A ovvero:
Taglio(G,A)={(u,v)|(u,v)$\in$E con u $\in$ $N_A$, v$\in$ N-$N_A$}

Sono tutti archi che partono da nodi che sono stati inclusi nella soluzione e vanno verso nodi del grafo originario non inclusi. Poi Prim calcola un arco $e_{min}$, ovvero l'arco in Taglio(G,A) tale che $\lambda(e_{min})$ è $\le$ di $\lambda(e)$ $\forall e$$\in$Taglio(G,A) ovvero l'arco con peso più piccolo in Taglio(G,A). Mentre al passo i-esimo avremo $A^{i+1}$=<$N_A^i$$\cup${v},$E_A^i$$\cup$(u,v), $\lambda_{E_A^i}$$\cup$(u,v)> con $e_{min}(u,v)$.
Rivediamo l'esempio:
![[tagliprim.jpg]]
partiamo da 5, ed otteniamo il tagli risultante:
![[tag1.jpg]]
scelgo l'arco che verso 1 tanto gli archi hanno peso uguale. Successivamente scelgo l'arco che va verso 7 e poi verso 4 ottenendo il taglio: ![[tag2.jpg]]
poi verso 6, verso 2, verso 3 ed infine 0.

---
# Correttezza di Prim attraverso la tecnica invariante
Andiamo a dimostrare che l'algoritmo ritorna un albero ricoprente di costo minimo attraverso la tecnica invariante, tecnica solo per algoritmi iterativi.

Osserviamo che non ha senso avere che ad ogni passo l'albero $A^i$ sia minimo ricoprente, ma solo alla fine deve esserlo, bisogna trovare quindi una proprietà invariate.  Abbiamo inizialmente $A^i$ e G, si vuole che:
$\exists$ $A^*$ di G tale che $A^*$=<N,$E^*$,$\lambda_{E^*}$> e che $A^i$ $E_{A^i}\subseteq$ $E^*$ $\forall$ e $\in$ $E_{A^i}$, $\lambda_{E_{A^i}}$(e)=$\lambda_{E^*}$(e), in altri termini vogliamo che $A^i$ sia un sottoalbero di $A^*$.
Dimostrare la proprietà invariante per ogni passo dell'algoritmo di Prim dimostra la sua correttezza.

Sapendo che $|E^*|=n-1$ ovvero la cardinalità del insieme degli archi in un albero se ci sono n nodi, è pari a n-1, allora se partiamo dalla soluzione 0 e poi aggiungiamo un arco ad ogni soluzione $A^i$ abbiamo che:
$A^{n-1}$$\Rightarrow$$|E_{A^{n-1}}|=n-1$
$\displaystyle E_{A^i}\subseteq$ $E^*$$\Rightarrow$$E_{A^{n-1}}\equiv$ $E^*$

quindi l'albero coincide con l'albero minimo ricoprente.
Bisogna dimostrare che la proprietà invariante valga ad ogni passo, usiamo quindi il principio d'induzione.

Caso base:
$A^0$=<{$n_0$},$\oslash$,$\lambda_{\oslash}$>,vale $E_{A^i}\subseteq$ $E^*$? 
Per ipotesi $\exists$ $A^*$ qualunque tale che $\oslash\subseteq$ $E^*$ quindi la condizione è verificata.

Caso induttivo:
$\large A^i=<N_{A^i},E_{A^i},\lambda_{E_{A^i}}$>
$\large A^{i+1}=<N_{A^i}\ \cup\ \{v\},E_{A^i}\ \cup\ \{u,v\},\lambda_{E_{A^i}}$>
Sappiamo che se $E_{A^i}\nsubseteq$ $E^*$$\Rightarrow$(u,v)$\notin$ $E^*$
Supponiamo di essere nella situazione in cui $E_{A^i}\nsubseteq$ $E^*$ e che quindi l'arco {u,v} non appartiene al albero ricoprente.
Graficamente:
![[correttezzaprim.jpg]]
Indichiamo uno dei due archi diversi da {u,v} con e' e sappiamo che
$\lambda(e')$$\ge$$\lambda((u,v))$ perché $e_{min}=(u,v)$. Consideriamo ora l'albero $A'^*$
$A'^*=<N,E^*-\{e'\}$$\ \cup\  \{e_{min}\}$, $\lambda$> e l'albero $A^*$=<N,$E^*$,$\lambda_{E^*}$>
Come costo abbiamo:

costo($A'^*$)=$\displaystyle\large\sum_{e\in E^* -\{e'\}}$ $\lambda(e)$ + $\lambda(e_{min})$

costo($A^*$)=$\displaystyle\large\sum_{e\in E^*}$ $\lambda(e)$= $\displaystyle\large\sum_{e\in E^* -\{e'\}} \lambda(e)$ + $\lambda(e')$

costo($A'^*$)$\le$costo($A^*$)

$\displaystyle\large\sum_{e\in E^* -\{e'\}}$ $\lambda(e)$ + $\lambda(e_{min})$ $\le$ $\displaystyle\large\sum_{e\in E^* -\{e'\}}$ $\lambda(e)$ + $\lambda(e')$

sottraendo $\displaystyle\large\sum_{e\in E^* -\{e'\}}$ $\lambda(e)$ da entrambi i membri si ottiene,

$\lambda(e_{min})$ $\le$  $\lambda(e')$ è vero quindi $A'^*$ è un minimo albero ricoprente, contiene tutti gli $A^{i+1}$, quindi la proprietà è valida al passo i+1-esimo come volevasi dimostrare.

Prim ha costo $\theta(n*m+log n)$ se utilizzo un heap ed una lista d'adiacenza, con array ho $\theta(n^2)$

---
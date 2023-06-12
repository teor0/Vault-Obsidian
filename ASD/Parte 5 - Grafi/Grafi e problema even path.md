#asd 
[[Counting sort e radix sort]]
# Caratteristiche dei grafi
I grafi sono collezioni che permettono di mantenere relazioni qualsiasi, che coinvolgono più elementi, ma ci concentreremo su relazioni binarie. Ogni entità ha un identificativo ad esempio un numero. Per memorizzare una relazione esistono 2 modi:
1. Attraverso un grafo orientato, dove gli archi sono orientati e monodirezionali
2. Attraverso un grado non orientato, dove gli archi sono bidirezionali

![[grafoor.png]]
![[grafonor.png]]
Le entità sono contenute in nodi che sono relazionati tramite archi. Un grafo può essere rappresentato sottoforma di struttura matematica:
>Dato N l'insieme di nodi, un grafo G è una coppia <N,E> dove E è l'insieme di archi o meglio E $\subseteq$ $N\times N$ (sottoinsieme del prodotto cartesiano dei nodi). Ad esempio: <{0,1,2,3,4},{<1,0>,<0,2>,<3,0>,<3,2>,<3,4>,<4,2>}>

Per un grafo non orientato invece vale la stessa condizione data più:
>$\forall$ x,y $\in$ N, <x,y> $\in$ E $\Rightarrow$ <y,x> $\in$ E. Ovvero: <{0,1,2,3,4},{<1,0>,<0,1>,<0,2><2,0>,<3,0>,<0,3>,<3,2>,<2,3>,<3,4>,<4,3>,<4,2>,<2,4>}>

Si può dare una definizione diversa per E nel caso di grafo non orientato. 
>Un arco è un insieme, E $\subseteq$ P(N) (power set di N), dove ogni arco ha cardinalità 2, ovvero i valori che sono collegati.

Formalmente si potrebbe avere un grafo di dimensione infinita. Esempio: 
N= insieme dei numeri interi
E={<x,y>| x $\in$ N, y $\in$ N, y=x+1} che rappresenta la relazione del successore ovvero: {<0,1>,<1,2>,<2,3>...}.
Tuttavia a noi interessano i grafi finiti.

---

## Definizioni proprietà grafi
- Per i grafi non orientati, dato un arco a=<x,y> a è incidente su x e y.
- x è adiacente al nodo y se e solo se <x,y> $\in$ E.
- Per i grafi orientati, un arco a=<x,y> si dice uscente da x ed entrante in y.
- y è adiacente ad x se e solo se <x,y> $\in$ E.

Il grado di un nodo è il numero di archi che incidono su di esso, si tratta ovviamente di un grafo non orientato quello su cui si stabilisce il grado dei nodi.

Il grado di entrata di un nodo è il numero di archi entranti nel nodo, mentre il grado di uscita è il numero di archi uscenti dal nodo. 

![[gradi.jpg]]
![[entrante.jpg]]

---
# Percorsi interconnessi
È naturale impiegare i grafi per le reti o comunque delle interconnessioni ad esempio le strade che collegano delle città, si vuole quindi sapere quale nodo posso raggiungere a partire da un altro.
Introduciamo il concetto di <font color=red> cammino in un grafo</font>. 
![[cammino.jpg]]
Un cammino potrebbe essere rappresentato da una sequenza di nodi: $n_0,n_1,n_2,...,n_k$. Non tutte le sequenze sono possibili perciò bisogna aggiungere a questa definizione le successioni: $\forall$i $\in$ {0,1,...,k-1} <$n_i$,$n_i$+1> $\in$ E. Un cammino si dice non vuoto se ha almeno 2 nodi.

Definizione alternativa:
>Un cammino in un grafo è una sequenza di archi, <$n_0$,$n_1$>,... <$n_{k-1}$,$n_k$> dove ogni arco successivo al primo inizia con il secondo nodo dell'arco di prima. Un cammino si dice non vuoto se ha almeno un arco.

In entrambe le definizioni si può definire <0,0>.

---

## Lunghezza di un cammino, ciclo nei grafi orientati e ciclo nei grafi non orientati
Se si segue la definizione alternativa, la lunghezza di un cammino è data dal numero di archi della sequenza. Mentre seguendo la prima definizione, la lunghezza di un cammino è data dal numero di nodi della sequenza meno 1.
Un ciclo è un cammino $n_0,n_1,...n_k$ non vuoto in cui $n_0=n_k$. Se un ciclo ha lunghezza 1, si chiama self-loop.
Un ciclo nei grafi non orientati, è un cammino da $n_0,n_1,...n_k$ non vuoto in cui: 
$n_0=n_k$ $\forall$ i $\in$ (0,1,...,k-1) $\nexists$ j $\in$ (0,1,...,k-1) | <$n_i$,$n_{i+1}$>=<$n_{j+1}$,$n_j$>

Controesempio di ciclo:
![[notciclo.jpg]]
Il cammino 101 non è un ciclo. 
Modifichiamo adesso la definizione di cammino, un cammino semplice è un cammino senza cicli ad esempio: 1,0,2,3,4 è semplice. Un cammino $n_0,...n_k$ si dice semplice se $\nexists$ i $\in$ (0,1,...,k) e j $\in$ (0,1,...,k) con i<j tale che $n_i$=$n_j$.
Sia $c_1$=1,0,2,3,0,2,3,4 un cammino non semplice e $c_2$=1,0,2,3,4 un cammino semplice e$c_2$ sembrerebbe più efficiente da percorrere di $c_1$.

---

# Problema even path
Dato un grafo ed una coppia di nodi $n_i$, $n_j$, esiste un cammino da $n_i$ a $n_j$ di lunghezza pari? Questo problema ha 2 varianti:
1. Variante dove si richiede un cammino semplice pari.
2. Variante dove si richiede di verificare l'esistenza del cammino.

Questo problema è molto complesso e ha classe di complessità np. Nel caso di cammino generale si ha complessità molto bassa e polinomiale, il cammino semplice invece richiede un costo alto che necessità enumerazione dei cammini. Esempio:
![[evenpath.jpg]]
Nodi pari a 3k+1, archi pari a 4(k-1). Per andare da $\large n_0^0$ a $\large n_0^k$ si hanno $2^k$ cammini semplici ed è molto caro enumerarli.

---
#asd
[[Algoritmi visita grafi]]
# Obiettivi degli algoritmi
Verificare l'aciclicità è un'operazione costosa e differente se il grafo è orientato o no. Un grafo G=<N,E> è ciclico se $\exists$ un ciclo $n_0,...n_0$ composto usando gli archi di G, è aciclico altrimenti. 


Definiamo un algoritmo inefficiente dove, in un grafo orientato $\forall$(x,y)$\in$E verifico se x è raggiungibile da y, cioè se esiste un cammino e ritorno true altrimenti false, basta verificare che da y, x faccia parte dei nodi marcati. Il costo però è quello della visita per ogni arco quindi costo $\theta(m*n^2)$ per la matrice d'adiacenza e $\theta(m*(m+n))$ per la lista d'adiacenza.

Nei grafi non orientati serve una proprietà per sapere se ci sono cicli o meno, questa proprietà è la connessione. Un <font color=green>grafo orientato connesso</font> è tale se $\forall$x,y$\in$N esiste un cammino da x ad y, cioè se ogni nodo è raggiungibile da un altro, nei grafi non orientati anche da y a x ovviamente.
Un grafo connesso può essere anche aciclico? Possiamo trovare una relazione fra il numero di nodi n ed il numero di archi m?

![[gca.jpg|100]]
grafo connesso ed aciclico
![[gcc.jpg|100]]
grafo ciclico e connesso
![[gnca.jpg]]
grafo non connesso ed aciclico
![[gcnc.jpg]]
grafo connesso ed aciclico

Ipotizziamo di avere un grafo n, scegliamo un arco che può dividere in due il grafo in n' e n'' con almeno un nodo e sono porzioni connesse ed acicliche. 
Per induzione:
$n'-1=m'$ 
$n''-1=m''$

Abbiamo quindi che $n'+n''=n$  perciò
$n'+n''-2=m'+m''\Rightarrow n-2=m-1$ da ciò segue che $n-1=m$. 
Quindi se un grafo di dimensione $n-1$ ha m archi ed è connesso ed aciclico allora anche un grafo di n nodi lo sarà. 
>Se $n-1=m$ ed il grafo è connesso allora il grafo è aciclico, inoltre se il grafo è aciclico allora $n-1=m$ e quindi risulta connesso.


Un grafo non orientato connesso ed aciclico in realtà è un albero dato che posso scegliere tranquillamanete la radice.
Per verificare se un grafo è un albero si può usare il metodo:
``` java
public boolean eAlbero{
	return(n==m+1) && eConnesso();
}
```
Il metodo eConnesso essenzialmente verifica se da un nodo posso raggiungere tutti gli altri ed ha costo $\theta(n^2)$ per matrice di adiacenza e $\theta(n+m)$ per le liste di adiacenza.

Il metodo costa dipendemente dal fatto se eConnesso viene chiamato, cioè se fosse la prima condizione dell'and allora la return sarebbe più lenta dato che se $n\ne m+1$ subito evitiamo di chiamare eConnesso. Se il numero di archi ha numero proporzionale al numero di nodi, la complessità è pari a $\theta(n)$. Un grafo orientato e non connesso si può suddividere in porzioni connesse. Esempio:
![[porzioni.jpg]]
Tra C1, C2 e C3 non possono esserci archi. Le porzioni perciò devono essere separate, in componenti di un grafo, dove una componente di un grafo è un sottoinsieme di N. Una componente C si dice connessa se <font color=red>$\forall x,y \in C\ |\  x \ne y$ esiste il cammino da x a y e viceversa</font>. Una componente si dice fortemente connessa nel caso dei grafi orientati, si dice componente debolmente connessa se da un grafo orientato ricaviamo un grafo non orientato togliendo l'ordinamento degli archi.

![[compenteconnessa.jpg]]
{0,2} è una componente connessa.

Una componente connessa C è <font color=red>massimale se non esiste una componente connessa</font> C' tale che C$\subset$C'. In questo caso {0,2} non è massimale.

>C1,C2 e C3 sono componenti connesse massimali.


Siano C1,C2,...,CK tutte le componenti connesse massimali del grafo, {C1,...,CK} è una partizione di N, cioè $\displaystyle\large\bigcup_{i=1}^k C_i=N$ inoltre, $\forall i,j$ $C_i\cap C_j=\oslash$, quindi l'intersezione tra 2 componenti connesse massimali diverse da un'insieme nullo.
>In un grafo il numero massimo di componenti massimali sono al più i nodi. 

Prendiamo un grafo con CK componenti connesse massimali. Affinché il grafo sia aciclico, tutte le componenti devono essere acicliche. I nodi di ogni componente sono a pari a $n_i=m_i+1$.
Esempio:
![[componenti.jpg]]
(n1+n2+...+nk)=(m1+m2+...+mk)+k $\Rightarrow$ n=m+k
dove m+k sono le componenti connesse massimali.

Come capire quante sono k? Realizziamo un algoritmo che conta il numero di visite che compie sulle componenti
``` java
public boolean eAciclico(){
	int k=nComponentiConnesseMassimali();
	return n==m+k;
}

public int nComponentiConnesseMassimali(){
	int k=0;
	boolean[] visitati=new boolean[n];
	List<Integer> l=new LinkedList<>();
	for(int i=0; i<n;){
		k++;
		depthFirstSearch(i,l,visitati);
		for(i++; i<n && visitati[i]; i++)
			//ricerca prossimo indice
	}
	return k;
}
```
costo $\theta(n^2)$ matrice $\theta(n+m)$ lista per depthFirstSearch
Il caso in cui si fanno n volte le operazioni è il caso in cui si hanno n componenti connesse massimali cioè un grafo senza archi. Si ha perciò costo $O(n^3)$ per matrice e $O(n*(n+m))$ per lista come costo.
>Una foresta è un grafo non orientato aciclico dove le componenti connesse massimali sono grafi non orientati aciclici e non connessi

---

# Caso grafi orientati
Nei grafi orientati come si può fare di meglio dell'algoritmo di base? Si può usare una proprietà di grafi con numero finito di nodi. Tale proprietà è: 
Se $\forall$x $\in$ N il grado di entrata di x è >0 allora il grafo è ciclico. Vediamo perchè:
![[progrado.jpg|150x650]]
Due casi sono possibili per avere grado d'entrata >0, per $x_0$ un arco di selfloop oppure da un arco che parte da $x_1$. Per $x_1$ può esserci un arco di selfloop oppure un arco che parte da $x_0$ o $x_2$ e cosi via fino a $x_{n-1}$. Quindi arrivati a $x_{n-1}$ dovrò per forza avere un ciclo.
Un esempio non ciclico: N=numeri interi E={(x,y)|y=x+1}

Ipotiziamo di avere un grafo dove esiste un nodo x con grado d'entrata 0. Possiamo suddividere il grafo G in due parti: il nodo x ed il grafo G-x. Potrei dimostrare che: G è aciclico $\Longleftrightarrow$ G-x è ciclico. La presenza di un ciclo in G non la pressupone in G-x, supponiamo di avere un ciclo in G: ![[ciclo.jpg]]
tutti questi nodi hanno un grado d'entrata >0 perciò saranno sicuramente nodi di G-x. Queste 2 proprietà sono utili per definire un algoritmo dove, o trovo che i gradi sono tutti >0 oppure rimuovo un nodo fino a quando non ho un grafo vuoto e rispondo che è aciclico. 
Il calcolo dei gradi d'entrata richiede di scorrere interamente l'iteratore su gli archi ed ha costo $\theta(n^2)$ per matrice e $\theta(n+m)$ per lista. Un nodo da rimuovere è un nodo con grado d'entrata =0 e costa $\theta(n)$, tutto il ciclo per rimuovere tutti i nodi costa n e la ricerca di un nodo con grado 0 da rimuovere ha costo $\theta(n)$ perciò $\theta(n^2)$. Il costo totale dell'algoritmo dove tolgo tutti i nodi con grado d'entrata 0 è $\theta(n^2)$.

---
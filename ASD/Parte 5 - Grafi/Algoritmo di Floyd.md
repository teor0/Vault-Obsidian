#asd
[[Algoritmo di Dijkstra]]
# Caratteristiche dell'algoritmo
L'algoritmo di Floyd funziona anche con pesi negativi e si basa sulla tecnica della programmazione dinamica. La programmazione dinamica, possiamo vederla come l'opposto di divide et-impera si basa anche lei sul concetto di dimensione dell'istanze del problema, ma segue una strategia diversa. Con <font color=orange>Ist(i) </font>indichiamo l'insieme di tutte le istanze di dimensione $i$. La programmazione dinamica prevede un "modo" per calcolare Ist(i+1) a partire da Ist(i). Chiamiamo con <font color=orange>Sol(Ist(i))</font> l'insieme delle soluzioni delle istanze con dimensione $i$. Perciò:

Sol(Ist(i+1))$\large\Leftarrow$Sol(Ist(i))

Quindi parte da soluzioni a dimensioni 0 e va avanti. L'algoritmo per calcolare il fattoriale oppure Fibonacci iterativamente segue questo modo di procedere. Bisogna però capire bene cosa considerare come dimensione delle istanze.

Floyd, si pone di risolvere questo problema: 
Dato un grafo G, calcolare le distanza tra tutte le coppie di nodi di G, senza nodo sorgente.
Lo potrei risolvere con Dijkstra ma dovrei iterare per ogni possibile nodo sorgente. Anche Floyd però non può calcolare la distanza nel caso in cui ci sono cicli con risultati negativi. Prima di vedere l'algoritmo di Floyd, vediamone uno simile ma con complessità più alta. 

Come input si ha: G=<N,E,$\lambda$> come output: $\large D^{n\times n}$ dove $n=|N|$ tale che D[x,y] è la distanza tra x e y. Calcoliamo $\large D_i^{n\times n}$ come la distanza da x a y considerando solo cammini minimi da x a y con al più, $i$ (inteso come variabile) nodi intermedi.
Esempio:
![[Floyd.png]]
Oltre ad essere matrice d'adiacenze è $\large D_0^{n\times n}$ 
Il cammino [0,2] non è ammissibile in $\large D_0^{n\times n}$ in quanto c'è 1 nodo intermedio. Definiamo una strategia divide et-impera:
$\large D_{i+1}[x,y]=min_{z\in N}(D_i[x,z]+D_0[z,y])$

Faccio un cammino con al più $i$ nodi intermedi per arrivare da x a z e sommo il costo da z a y che però non attraversa nessun nodo intermedio. ![[dividefloyd.png]]
Allora la strategia divide et-impera consiste in calcolare $D_0$ per calcolare con un passo $D_1$ per ogni x e y della matrice devo trovare il minimo di $D_i[x,z]+D_0[z,y]$ che costa $\theta(n^3)$ ovvero 3 for. Quindi:
$\large D_{1}[x,y]=min_{z\in N}(D_0[x,z]+D_0[z,y])$
$\large D_{2}[x,y]=min_{z\in N}(D_1[x,z]+D_0[z,y])$
fino a n-2 perché i cicli hanno somma di pesi sugli archi positiva, e non può essere un cammino minimo che contiene un ciclo. Il costo di tutto è $\theta (n^4)$ ovvero $\theta(n^3)$ ripetuto n-2 volte.

---
## Perchè i cicli hanno somma positiva?
![[cicli.png]]
costo(C1)=C'+C''
costo(C2)=C'+C+C'' 
Essendo $C\ge 0 \Rightarrow$ costo(C1)$\le$costo(C2) ecco perchè mi perfo a $D_{n-2}$, perchè non considero cammini con cicli in quanto ho già calcolato cammini senza cicli. Questo algoritmo quindi funziona supponendo cicli con cammini $\ge$ 0. Però con Dijkstra avrei costo $\theta(n^3)$ quindi converrebbe lui, questo perché la dimensione è stata presa male.

---

# Algoritmo di Floyd
L'unica cosa che si può fare per migliorare la strategia è evitare di calcolare un minimo in un insieme di n elementi disordinati, ovvero un costo $\theta(n)$ e sostituirlo con un costo costante. Tuttavia la dimensione della dimensione del problema, costringe a procedere così. Floyd considera come dimensione del problema, non il numero di nodi intermedi che appaiono in un cammino, ma gli indici dei nodi intermedi che appaiono in un cammino, introducendo il concetto di <font color=green>cammino k-vincolato</font>.

>Un cammino da x a y si dice k-vincolato, se gli indici dei nodi intermedi del cammino sono tutti minori di k, con indici dei nodi che vanno da 0 a n-1.

Se considero un cammino 0-vincolato trovo nodi intermedi? No perchè qualunque indice è >0, ed associato a questo concetto c'è il concetto di <font color=green>distanza k-vincolata</font> tra 2 nodi.

> La distanza da x a y che ottengo considerando solo cammini k-vincolati prende il nome di distanza k-vincolata.
> La distanza da x a y è il costo del cammino k-vincolato da x a y con costo più piccolo.

![[Floyd.png]]
Definiamo la matrice delle distanza k-vincolate $\large D_v^k$ M=$\large D_v^k$ non posso considerare i nodi intermedi, considero solo gli archi come prima. Procedura di aggiornamento:
$\large D_v^{k+1}[x,y]=min(D_v^k[x,y],D_v^k[x,k]+D_v^k[k,y])$
Se voglio calcolare la distanza minima k+1 vincolata da un nodo x ad un nodo y, basta prendere il minimo tra la distanza minima k vincolata x,y e la somma delle distanze da x a k e da k a y. Ma perché? 

Prima vediamo cosa facciamo. Attraverso $\large D_v^0$ calcoliamo $\large D_v^1$ poi tramite esso calcoliamo $\large D_v^2$ e cosi via fino a $\large D_v^n$ perché i nodi vanno da 0 a n-1. Arrivato a $\large D_v^n$ ammetto cammini intermedi con qualunque indice. Calcolare il minimo è costante perché non dipendende dal numero di celle della matrice. Per l'intera matrice ho costo $\theta(n^2)$, questo lo faccio n volte quindi l'intera strategia costa $\theta(n^3)$, costo alto ma ragionevole. Per vedere che questo è il calcolo corretto consideriamo quale può essere un cammino da x a y k+1-vincolato. Possiamo avere cammini del tipo:
![[camminoK.png]]
cammini da x a y che attraversano nodi intermedi con indici $\lt$k. I cammini k+1 vincolati sono raggruppabili in 3 categorie:
![[camminiK.png]]
1. Cammini k vincolati
2. Faccio 2 cammini da x a k e da k a y, dove attraverso solo nodi intermedi con indici $\lt$k. Se i cammini k-vincolati fossero riportabili ad una di queste 2 forme l'equazione sarebbe corretta, ma non è così
3. Faccio 3 cammini, da x a k è k-vincolato, da k a k è k+1 vincolato e da k a y è k-vincolato.

Ho scontato che qualunque cammino da x a y con nodi intermedi con indici $\le$k ricade in una delle 3 forme.
L'ultima forma non viene tenuta di conta da Floyd perchè da k a k si ha un ciclo. Se rimuovo il ciclo ottengo un cammino di tipo 2, e questo cammino ottenuto rispetto al cammino originale ha un costo più piccolo. Ecco perchè non viene considerato, perché poi dovrò prendere il cammino con costo minimo.

Sarebbe bello anche calcolare i cammini minimi. Uno pseudo codice sarebbe:
``` 
Set<cammino>[][] c
for(k da 0 a n){
	for (i=0; i<n)
		for(j=0; j<n){
			if(distanze[i][j]>distanze[i][k]+distanze[k][j])
				distanze[i][j]=distanze[i][k]+distanze[k][j]
				cammini[i][j]=concatena(cammini[i][k],cammini[k][j])
			else if(distanze[i][j]==distanze[i][k]+distanze[k][j])
				cammini[i][j]=unisci(cammini[i][j],concatena(cammini[i][k],cammini[k][j]))
		}
}
```

purtroppo l'unione fa crescere la complessità a livello esponenziale, costo che nella pratica non si paga considerando solo i cammini più corti.

---


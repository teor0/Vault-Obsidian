#asd 
[[Hash map]]
# Caratteristiche degli insiemi
Gli insiemi sono strutture dati di m oggetti che offrono il vantaggio di verificare se un elemento appartiene all'insieme con costo basso. La memore occupata da un insieme è pari a $O(m)$ e viene implementato tramite un vettore di boolean. 
L'unione tra 2 insiemi A e B ha costo $\theta(m_A+m_B)$ dove $m_A$ è il numero di elementi in A e $m_B$ è il numero di elementi in B. Il costo delle operazioni caratteristiche sono:

La differenza: $\theta(n_A)$.
Intersezione tra A e B: $\theta(min(n_A,n_B))$
In Java si usa la classe BitSet che usa un array di bit invece di boolean. 

Per set basati su liste o vettori non ordinati si hanno prestazioni:
- Inserimento, ricerca e cancellazione: $O(n)$
- Inserimento assumendo l'assenza: $O(1)$
- Unione, intersezione e differenza: $O(n*m)$

Se si usano liste o vettori ordinati si hanno prestazioni:
- Ricerca nella lista: $O(n)$
- Ricerca nel vettore: $O(logn)$
- Inserimento e cancellazione nella lista: $O(n)$
- Inserimento e cancellazione nel vettore: $O(n)$
- Unione, intersezione e differenza: $O(n)$
- Unione, intersezione e differenza nel caso in cui A e B hanno gli stessi elementi: $O(n+m)$

Ci sono poi insiemi basati su alberi bilanciati ed hash table. Gli alberi sono ordinati mentre l'hash table no.
Prestazioni rispettive:
- Ricerca, inserimento e cancellazione nell'albero: $O(logn)$
- Iterazione sull'albero: $O(n)$
- Ricerca, inserimento e cancellazione nell'hash table: $O(1)$
- Iterazione nell'hash table: $O(m)$

In realtà per ricerca e rimozione la complessità è $O(1+\alpha)$ nel caso medio, dove $\alpha$ è il fattore di bilanciamento.
Facciamo un riassunto di quello che abbiamo visto:
![[riassuntoinsiemi.jpg]]
> Per la tabella hash (memoria esterna), si intende una tabella hash con liste di collisione, mentre per la tabella hash (memoria interna) si intende quelle ad indirizzamento diretto.

![[suntoinsiemi.jpg]]
> Nel caso del Bit Set, $m_A$ e $m_B$ indicano la capacità dell'insieme non il numero di elementi effettevi, in particolare $m_A\ge n_A$ e $m_B\ge n_B$

In Java si usano rispettivamente TreeSet, HashSet e LinkedHashSet per avere un HashSet ordinato.

---
## Esempio applicativo e problema
Per calcolare il powerset è molto utile il vettore di booleani. Supponiamo di avere un insieme $v=[1,2,3,15,25]$ e creiamo un sottoinsieme associato ad un vettore booleano. 
$S=[2,15]→[0,1,0,1,0]$ dove 1 indica true e 0 false. Quindi se utilizzo un vettore di questo tipo, se parto da $[0,0,0,0,0]$ parto dall'insieme vuoto e se prendo il vettore e lo tratto come un numero binario ed ogni volta sommo 1, otterrò il power set che voglio calcolare in modo semplice.
Il costo di generare tutti i possibili sottoinsiemei è pari a $\theta(2^n)$.

Problema subsetsum, ovvero generare tutti i sottoinsiemi:
Dato un insieme $S$ ed un intero k trovare $S'\subseteq S$ tale che $\displaystyle\large\sum_{i\in S'}x=k$, ovvero la somma degli elementi di $S'$ mi dia k. Ciò si può risolvere in modalità brute force generando tutti gli insiemi. L'implementazione è la seguente:
```java
public static boolean subset(int[] v, int k){
	boolean[] b=new boolean[v.length];
	while(!tuttiuno(b)){
		if(somma(v,b)==k)
			return true;
		incremento(b);
	}
	return somma(v,b)==k; //ultimo check con tutto l'array
}

private static int somma(int[] v,boolean[] b){ //theta(n)
	int sum=0;
	for(int i=0; i<b.length; i++)
		if(b[i])
			sum+=v[i];
	return sum;
}

private static void incremento(boolean[] b){ //O(n)
	boolean riporto=true;
	int i=0;
	while(riporto && i<b.length){
		if(b[i])
			b[i]=false;
		else{
			b[i]=true;
			riporto=false;
		}
		i++;
	}
}

private static boolean tuttiuno(boolean[] v){ //O(n)
	for(int i=0; i<v.length; i++)
		if(!v[i])
			return false;
	return true;
}
```
La complessità totale dell'algoritmo risolutore del problema è data da $\theta(n*2^n)$ dato che calcolo tutti i sottoinsiemi e faccio la somma per verificare il risultato.

---
 #asd
[[Dettagli sulle strutture dati classiche ed alberi]]
# Esercizio Stack

Ipotizziamo di avere uno stack dinamico che memorizza i dati su un array che a seconda della capacità varia. Effettuiamo adesso la sua implementazione.

```java
class DynamicStack<T>{

	private int top; //cima stack
	private int cap; //capacità
	private T[] arr;

	public DynamicStack(int cap){
		this.cap=cap;
		arr=(T[])new Object[cap];
		top= -1;
	}

/*caso migliore push: non bisogna espandere l'array theta(1)*/
/*caso peggiore push: bisogna espandere l'array theta(n)*/
	public void push(T el){
		if(isFull())
			expandArray();
		arr[top+1]=el;
	}
	/*caso migliore e peggiore isFull: theta(1)*/
	private boolean isFull(){
		return top+1==cap;
	}
	/*costo di expandArray: theta(n)*/
	private void expandArray(){
		int currentSize=top+1;
		T[] nArr=(T[]) new Object [currentSize*2];
		for(int i=0; i<currentSize; i++)
			nArr[i]=arr[i];
		arr=nArr;
		cap=nArr.length;
	}
	/*caso migliore e peggiore isEmpty: theta(1)*/
	public boolean isEmpty(){
		return top==-1;
	}
/*caso migliore pop: non bisogna ridurre la dimensione theta(1)*/
/*caso peggiore pop: bisognare ridurre la dimensione theta(n)*/
	public T pop(){
		if(isEmpty())
			return null;
		T ret=arr[top];
		arr[top]=null;
		top--;
		reduce();
		return ret;
	}
	/*caso migliore e peggiore reduce: theta(n)*/
	public void reduce(){
		int currentSize=top+1;
		if(currentSize<=cap/4){
			T[] nArr = (T[]) new Object [cap/2];
			System.arrayCopy(arr,0, nArr, 0, nArr.length);
			arr=nArr;
			cap=nArr.length;
		}
	}
}
```

Calcolo complessità spaziale: 
sia h la dimensione dell'array di supporto. Sia n il numero di elementi dello stack. Vogliamo capire la quantità di memoria che viene utilizzata. Supponiamo che creiamo un array di dimensione 1 ed avere 0 elementi. Quando n=h, h diventa 2h. Quando n=h/4, h diventerà h/2.

Possiamo dire che $\forall n>0$  abbiamo $\dfrac{h}{4} \le n \le h$ cioè $n \le h \le 4n$

Chiamiamo $S(n)$ lo spazio utilizzato per ospitare n elementi, $S(n)=\theta(h)= \theta(n)$

Se al posto di utilizzare un array, si usasse una linked list, nel caso peggiore di push e pop avremo complessità $\theta(1)$.

---

# Iteratore non nulli

Vogliamo inizializzare un iteratore su un vettore generico, che può contenere anche null nelle posizioni. Ecco adesso il nostro iteratore non si basa sulla posizione, ma su gli elementi non nulli. Perciò se l'iteratore trova un elemento nullo, non lo ritorna ma va avanti.

```java
private class IteratorNonNulli implements Iterator<T> {

		protected boolean hasNext;
		protected int pos = -1;

		public IteratorNonNulli() {
			succ();
		}

		public T next() {
			if(!hasNext()) 
				return null;
			Object tmp = items[pos];
			succ();
			return (T) tmp;
		}

		public boolean hasNext() {
			return hasNext;
		}

		public void remove() {
			throw new UnsupportedOperationException();
		}

		private void succ() {
			hasNext = false;
			pos++;
			while (pos < items.length) {
				if (items[pos] != null) {
					hasNext = true;
					return;
				}
				pos++;
			}//while
		}
	}
```

Il metodo succ() è in realtà quello che permette di evitare gli elementi nulli, infatti il metodo succ() ritorna la posizione del prossimo elemento non nullo.

>Molto importante per questo genere di iteratori è evitare di occupare altra memoria.

---

# Esercizi metodi su albero

Vediamo adesso la complessità di alcuni metodi disponibili su gli alberi. Prendiamo il metodo `eRipetuto(Albero a, int x)` che ritorna true, se vi è almeno un nodo n nell'albero tale che l'intero x sia nel sottoalbero destro e sinistro. Allora abbiamo 3 casi dove si può trovare x:

1. x sta nella radice
2. x sta nel sottoalbero sinistro
3. x sta nel sottoalbero destro

Posso richiamare il metodo ricorsivamente nei 2 sottoalberi. Quindi vediamo come implementare il metodo con uno schema risolutivo:

- Chiamiamo a, la radice dell'albero. Se `a==null` allora ritorna false, in quanto l'albero non esiste
- Altrimenti x sta nella radice o nei sottoalberi perciò: bisogna ritornare il caso il cui (appare a destra && appare a sinistra) oppure richiamare eRipetuto a sinistra oppure richiamare eRipetuto a destra.

Utilizziamo quindi un metodo che svolge la vera e propria ricerca, il metodo appare che:
- Se `a==null return false`
- Altrimenti x è contenuto in questo nodo oppure a sinistra o destra: `return a.val==x || appare a sinistra || appare a destra`.

```java
public static boolean eRipetuto(Albero a, int x){
	if(a==null)
		return false;
	return (appare(a.fS)) && appare(a.fD)) || eRipetuto(a.fS) || eRipetuto(a.fD);
}

public static boolean appare(Albero a, int x){
	if(a==null)
		return false;
	return a.val==x|| appare(a.fS, x)|| appare(a.fD, x);
}
```

Il caso peggiore temporale di questo metodo è $O(n^2)$ e $\Omega(n^2)$ perché calcolo prima sul sottoalbero sinistro che ha $n-1$ nodi e poi scendo ancora a $n-2$ e così via fino ad 1. 
Tutto ciò è pari a $\large\displaystyle\sum_{i=0}^{n-1} {n(n-1)\over 2}$ che asintoticamente è pari a $n^2$. Caso migliore temporale è pari a $\theta(1)$, caso spaziale peggiore $\theta(n)$ e caso spaziale migliore $\theta(1)$.

Vediamo adesso un metodo che deve calcolare il numero di nodi foglia pari. I casi possibili sono:

- Se `a==null` allora return 0.
- Altrimenti il nodo può avere figli nulli, quindi siamo in presenza di un nodo foglia e ritorniamo 1 se è pari altrimenti 0.
- Oppure si può avere il caso in cui il nodo ha figli quindi si richiama contaFigliPari su i figli.

```java
public static int contaFigliPari(Albero a){
	if(a==null)
		return 0;
	if(a.fS==null && a.fD==null){
		if(a.val%2==0)
			return 1;
		else
			return 0;
	}
	return contaFigliPari(a.fS)+contaFigliPari(a.fD);
}
```

Essendo un'algoritmo di ricerca non ho caso migliore e peggiore temporale, quindi la complessità temporale è pari a $\theta(n)$ in quanto guarda ogni nodo dell'albero sempre cercando gli elementi pari. La complessità spaziale peggiore si presenta quando si ha un albero _degenere_ ed è pari a $\theta(n)$. La complessità migliore spaziale si ha invece con un albero completo ed è pari a $\theta(logn)$, perchè ogni volta ho $2^i$ nodi, dove i indica il livello dell'albero, quindi se ho un albero di altezza pari a 4 ho $2^3$ foglie.

---

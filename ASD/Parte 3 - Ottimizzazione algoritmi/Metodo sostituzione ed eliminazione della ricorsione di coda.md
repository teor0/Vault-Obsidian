[[Teorema delle ricorrenze]]
#asd 
# Metodo sostituzione

Per gli algoritmi di tipo 1, bisogna risolvere l'equazione di ricorrenza con il metodo dello srotolamento, ma questo non è l'unico modo. Esiste anche il metodo di sostituzione.

Si parte dall'idea di "indovinare" una soluzione ed usare l'induzione matematica per provare che è vera. Esempio:

$T(n)=n+T(\large{n\over 2})$ con n generico

$T(1)=1$ se n=1

assumiamo che la soluzione sia $T(n)\le cn$ dove c è una costante.

se $n=1$ $T(1)=1\le c*1$ per ogni $c$

$\displaystyle\large T(n)=n+T({n\over 2})\le n+c({n\over 2})=({c\over 2}+1)n$ perciò,

$T(n)\le cn$  per $c\ge 2$

---

# Eliminazione della ricorsione di coda

Questa tecnica permette in particolari casi di sostituire l'ultima chiamata, che deve anche essere l'ultima istruzione, con un while, riducendo lo spazio occupato in memoria. Nel caso del quicksort, nel caso peggiore la complessità spaziale è pari $T(n)=T(n-1)b$.

Esempio di eliminazione:

```java
static void metodo(parametri){
	if(dimBanale)
		return casoBase(dimBanale);
	corpo(parametri);
	return metodo(parametri);
}
//diventa
static void metodo(parametri){
	while(parametri di dimensione non banale){
	corpo(parametri);
	parametri=parametriModificati;
	}
	return casoBase(parametri);
}
```

Applichiamo questa tecnica al quicksort:

```java
static void quickSort(int[]v, int inf, int sup){
	if(sup<inf)
		return;
	int p=partiziona(v,inf,sup);
	quickSort(v,inf,p-1);
	quickSort(v,p+1,sup);
}
//diventa
static void quickSort(int[]v, int inf, int sup){
	while(!(sup<=inf)){
		int p=partiziona(v,inf,sup);
		quickSort(v,inf,p-1);
		inf=p+1;
		sup=sup;
	}
	return;
}
```

Purtroppo la complessità spaziale resta la stessa più o meno. Proviamo adesso a non eliminare l'ultima chiamata ma quella più grande.

```java
static void quickSort(int[]v, int inf, int sup){
	while(!(sup<=inf)){
		int p=partiziona(v,inf,sup);
		if(p<((inf+sup)/2)){
			quickSort(v,inf,p-1);
			inf=p+1
		}
		else{
			quickSort(v,p+1,sup);
			sup=p-1;
		}
	}
	return;
}
```

Cosi facendo si è ridotto il costo a $log(n)$ perché al massimo la chiamata avrà dimensione $\large {n\over2}$ perché al massimo si divide il vettore a metà. Adesso l'equazione di ricorrenza diventa:

$\large T(n)=T({n\over2})+b$ se n>1

T(n)=b se n≤1

applicando il teorema della ricorrenza si trova:

- a=1 appunto una sottoistanza
- c=2 perché si ha dimensione pari alla metà al più nella sottoistanza
- d=0 perché capire su quale metà andare è un'operazione costante e facile

Quindi $\displaystyle {a\over c^d}={1\over1}=1$ perciò $T(n)\in\theta(logn)$.

---

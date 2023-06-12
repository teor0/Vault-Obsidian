#asd 
[[Modello a costi logaritmici e complessità ammortizzata]]
# Metodo Srotolamento
Le equazioni di ricorrenza vengono utilizzate per calcolare la complessità di funzioni ricorsive in modo semplice ed accurato. Vediamo un esempio:

```java
public static int fat(int n){
	if(n<=1)
		return 1;
	return n*fat(n-1);
}
```

Chiamiamo T la complessità rispetto n:

$\large T(n)=2$ se $\large n≤1$

$\large T(n)=2+T(n-1)$ se $\large n>1$

Dobbiamo calcolare la complessità di T(n-1), per semplicità 2 che è costante chiamiamola b e consideriamo n>1 quindi passiamo a:

$\large T(n)=b$ se $\large n≤1$

$\large T(n)=b+T(n-1)$ se $\large n>1$

Usiamo il cosidetto metodo dello srotolamento e consideriamo $\large (n-1)>1$ allora:

$\large T(n)=b+(b+T(n-2))=2b+T(n-2)$

consideriamo ancora n-2>1

$\large T(n)=2b+(b+T(n-3))=3b+T(n-3)$

si vede perciò che ad ogni passo i avremo

$\large T(n)=ib+T(n-i)$ che asintoticamente è $\large \theta(n)$.

---
## Dimostrazione

Ricordiamo che:
- $\large T(n)=b$ se $\large n≤1$

- $\large T(n)=b+T(n-1)$ se $\large n>1$

Se $\large n-i>1$ allora: 
$\large T(n)=ib+(b+T(n-i-1))=(i+1)b+T(n-(i+1))$

finché $\large n-i>1$ si avrà $\large T(n)=ib+T(n-i)$

quando $\large n-i=1$ cioè $\large i=n-1$ si avrà $\large T(n)=b$.

Se $\large i=n-1$ sostituendo alla prima formula ricavata ovvero $\large T(n)=ib+T(n-i)$ si ha:

$\large T(n)=(n-1)b+T(n-(n-1))=$
$\large (n-1)b+T(1)=(n-1)b+b=$
$\large nb-b+b=nb$.

Perciò $\large T(n)=nb$ cioé $\large T(n)\in \theta(n)$.

---

# Limitazioni - bound

Ha senso cercare un algoritmo migliore di un altro per tutti i problemi che magari, hanno già un algoritmo risolutore? 
No, per alcuni algoritmi non è possibile fare di meglio, ma possono venire in aiuto i concetti di limite superiore ed inferiore.

Per il <font color=yellow> limite superiore </font> è sufficiente conoscere un algoritmo risolutore e non per forza il migliore. La conoscenza di esso tuttavia, fornisce la quantità di tempo o memoria sufficiente per risolvere il problema ma, non dà nessuna informazione completa sulla complessità intrinseca del problema.

Il <font color=yellow> limite inferiore</font> è determinabile quando nessun algortimo, anche quelli non noti, per la risoluzione può fare a meno di utilizzare una quantità definita di memoria o tempo o di eseguire un certo numero di operazioni, almeno in qualche caso particolarmente difficile.

Passiamo alle definizioni:

Un problema P ha <font color=red> un limite superiore</font> (upper bound) di complessità O(g(n)), se e solo se esiste un algoritmo A risolutore di P che ha complessità O(g(n)) nel caso peggiore.

Un problema P ha <font color=red> un limite inferiore</font> (lower bound) di complessità $\Omega(g(n))$ se e solo se tutti gli algoritmi A risolutori di P hanno complessità $\Omega(g(n))$ nel caso peggiore.

Il limite inferiore è anche detto complessità intrinseca del problema. La definizione del limite inferiore non può essere usata per calcolare la complessità intrinseca subito a causa della mole di dati e del fatto che alcuni dati non sono noti. Propriamente la definizione di complessità intrinseca è la seguente:

> Dato un problema P ed una funzione f, si dice che P ha complessità intrinseca $\Omega(f)$ se tutti gli algoritmi risolutori di P hanno complessità $\Omega(f)$.


Praticamente se analizzo un algoritmo e trovo che la complessità al caso migliore è $\theta(1)$ e, la complessità al caso peggiore è $\theta(n)$ allora posso dire che, la complessità dell'algoritmo è dominata superiormente da $n$.
Vediamo un [[Esercizio equazione ricorrenza|esempio]] per capire la loro utilità nel pratico.

---


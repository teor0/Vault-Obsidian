[[Notazioni asintotiche e proprietà transitiva]]
#asd
# Metodo a costi uniformi

Come appunto specifica il metodo, assumiamo che ogni operazione elementare abbia costo unitario, il costo dell'algoritmo quindi è dato dalla somma del numero di volte che le operazioni vengono ripetute durante l'esecuzione dell'algoritmo. Ovvero:

$\displaystyle\large T(n)=\sum_{ist_i\in Ist} num(ist_i)$

Dove <font color=yellow> Ist</font> è l'insieme di tutte le istruzioni elementari dell'algoritmo e <font color=yellow> $num(ist_i)$</font> rappresenta il numero di volte che l'istruzione <font color=green> $\large ist_i$</font> è eseguita durante l'esecuzione dell'algoritmo.

Esempio:

```java
public static boolean presente(int[] v, int x){
		for(int i =0; i<v.length; i++)
			if(v[i]==x)
				return true;
		return false;
	}
```

Eseguendo i calcoli si ha che:

$T_w(n)$=2+3n+1=3n+5, in particolare:
- 2 è dato da l'inizzializzazione di $i$ ed una return
- 3n si ha perchè si effettua `v[i]==x`, `i++` e `i<v.length` quindi 3 istruzioni, per n volte ovvero la dimensione dell'array
- 1 sarebbe il caso di uscita dal for quando `i>v.length`

$T_b(n)$=1+1+1+1=4, in particolare si esegue l'inizzializzazione, il test del for, il test del if e la return

applicando l'analisi asintotica

$T_b(n) \in \theta(1)$

$T_w(n) \in \theta(n)$

---
# Metodo istruzione dominante

^d8b418

Se riprendiamo l'algoritmo di prima:

```java
public static boolean presente(int[] v, int x){
		for(int i =0; i<v.length; i++)
			if(v[i]==x)
				return true;
		return false;
	}
```

La complessità T(n) è data dalla somma del numero di volte che ogni istruzione è fatta. Numeriamo e definiamo le istruzioni:

- $i_0$= int i=0;
- $i_1$= i<v.length;
- $i_2$= i++;
- $i_3$= v[i]\==x;
- $i_4$= return true/false;

Notiamo che l'istruzione $i_1$ viene effettuata il maggior numero di volte ed inoltre da essa dipendono sia $i_2$  sia $i_3$. Detto ciò il numero di volte che viene eseguita $i_1$ è pari a n+1, quindi possiamo concludere che $T(n)=\theta(n+1)$ ovvero $T(n)=\theta(n)$. Come si è trovato con il metodo a costi unitari.

>Se ho più funzioni che crescono rapidamente allo stesso passo, ne scelgo una e la caratterizzo asintoticamente per $\theta$(num volte eseguita). In questo si è scelto il test del for

>Se si ha una somma di funzioni per la caratterizzazione di $T_w(n)$, voglio sapere il comportamento della funzione che cresce più rapidamente.

---

# Metodo istruzione dominante per algoritmi ricorsivi
Consideriamo il seguente algoritmo:

```java
public static int fat(int n){
	if(n<=1)
		return 1;
	return n*fat(n-1);
}
```

Possiamo utilizzare uno stratagemma che però può ingigantire il limite.

Ignoriamo per il momento la chiamata ricorsiva ed ipotizziamo sempre uguale, il costo della singola chiamata, considerando così il confronto ed una delle due return. Chiamiamo $g(n)$ il costo del if e una return che è quindi costante, chiamamo poi $h(n)$ il numero di chiamate di fat(n-1).

Abbiamo perciò che $\large T(n)=g(n)*h(n)$, dato che $g(n)$ è costante, sostituiamolo con c. Per quanto riguarda $h(n)$, il suo valore è proprio n perchè, chiamo il metodo n-1 volte finchè non arrivo ad avere n≤1, infatti se parto da n per arrivare ad 1 devo decrementare n volte. Abbiamo perciò che $\large T(n)=c*n$ in notazione asintotica $\large \theta(n)$.

Tuttavia questo ragionamento funziona per questo caso, perché valuto il costo della singola chiamata imputandolo al valore dell'input iniziale. Questo ragionamento se applicato al merge sort ad esempio, me la fa sparare moooooolto grossa.

---
## Importanza della rappresentazione dell'input
Sappiamo che per memorizzare un numero interno n servono al più $\large log_2 (n)$ bit. Quindi la dimensione dell'input per il fattoriale non è n ma $\large log_2(n)$. Se voglio calcolare n rispetto alla dimensione dell'input, chiamiamola d, applicando la proprietà inversa del logaritmo si ha che $\displaystyle\large n=2^d=2^{log_2(n)}$.

Quindi $\large T(d) \in \theta(2^d).$

Ecco perchè si è detto che ingigantiamo il risultato. Quindi è importante rappresentare l'input per bene senza dargli una taglia fissa. Capiamo insomma che il modello a costi uniformi non è molto sensato, essendo gli operandi possibilmente collegati alla dimensione dell'input ed a sua volta le istruzioni potrebbero avere una dimensione a seconda dell'input.
Passiamo adesso ad introdurre, il [[Modello a costi logaritmici e complessità ammortizzata| metodo a costi logaritmici e la complessità ammortizzata]]

---


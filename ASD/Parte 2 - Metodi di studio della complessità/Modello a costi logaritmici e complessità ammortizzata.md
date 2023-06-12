[[Metodi di studio della complessità]]
#asd 
# Modello a costi logaritmici

Questo modello assume per le istruzioni elementari un costo pari al logaritmo del valore degli operandi su cui lavorano.
Tuttavia non è sempre necessario utilizzare questo modello, in quanto se la dimensione bene o male resta uguale, con stessa proporzione per l'input, basterebbe moltiplicare il costo trovato con il modello a costi unitari per il logaritmo del valore per rendere il risultato più preciso.

Adesso prendiamo un esempio per cui non è semplice utilizzare questo modello:

```java
public static int fact(int n){
	int fatt=1;
	for(int i=1; i<=n; i++)
			fatt*=i;
	return fatt;
}
```

Analizziamo inizialmente il costo singolo rispetto all'input:

- int fatt=1 $\theta(1)$ quindi costante rispetto all'input
- int i=1 $\theta(1)$
- i≤n $\theta(log(n))$ perché i sarà al più n
- i++ $\theta(log(n))$ incremento al più n volte
- fatt*=i $\large \theta(log(n)+log(n))$ perché i al più arriva ad n e fatt può essere priorio $n!$. Applicando la proprietà dei logaritmi abbiamo $\large \theta(log(n)+log(n))=\theta(log(n!))$
- return fatt $\theta(log(n!))$

Il confronto e l'incremento vengono eseguiti un numero di volte maggiore di 1, in particolare il loro contributo è pari a:

$\large T(n) \in \theta(n *log(n))$.

il contributo di fatt*=i è pari a:

$\large T(n) \in \theta(n*log(n!))$.

Applicando il metodo dell'istruzione dominante, si ha che:

$\large T(n) \in \theta(n*log(n!))$ essendo che $\large n! \approxeq n^n$ avremo che:

$\large T(n) \in \theta(n*log(n^n))$ che applicando la proprietà dei logaritmi è

$\large T(n) \in \theta(n*n*log(n))$ infine $\large T(n) \in \theta(n^2*log(n))$

Quindi bisogna utilizzare questo modello quando supponiamo interi che abbiano dimensione variabile, ma anche quando il valore degli interi delle variabili nell'algoritmo può essere esponenzialmente più grande del valore dell'input iniziale.

---

# Complessità ammortizzata
 Si tratta di calcolare la complessità di una sequenza di operazioni. Ad esempio n volte la next in una linked list. Verrebbe da dire che la complessità è pari a $O(n^2)$, ma in realtà la next() non sarà sempre nel caso peggiore, e quindi non costerà sempre $\large \theta(n)$.

 Esempio ideale, la next() di un iteratore su un albero n volte, anche in questo caso si pensa abbia complessità $O(n^2)$ ma in realtà ha complessità di $\large \theta(n)$. E sapendo ciò, possiamo trovare che la complessità di una singola chiamata è data da $\large \dfrac{\theta(n)}{n}=\theta(1)$
 >Perciò per calcolare la complessità ammortizzata bisogna calcolare la complessità della sequenza delle istruzioni e divederla per il numero di operazioni della sequenza!
---

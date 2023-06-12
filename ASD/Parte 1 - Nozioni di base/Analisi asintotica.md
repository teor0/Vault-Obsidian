[[Nozioni e tipi di analisi di complessità]]
#asd 
# Analisi asintotica

Ipotizziamo di avere un algoritmo con complessità temporale pari a:

$T(n)=3n+4$

A seconda della potenza di calcolo della CPU, cambia la velocità di esecuzione e che se dividiamo le righe di codice in 2 cambiamo il numero di linee da eseguire costanti. Per evitare di considerare tutti questi dettagli ci avvaliamo dell'analisi asintotica. L'idea dietro è la seguente, scrivere già i tempi in funzione dell'input $n$ e trattare 2 funzioni come uguali in prima istanza, se una è $C$ volte l'altra, dove $C$ è una costante <font color=red>indipendente</font> da $n$, oppure perchè magari hanno stesso coefficente per quanto riguarda $n$ e sono diversi per il termine costante. Ad esempio:

$\displaystyle T(n)=4n+2$

$\displaystyle T'(n)=8n+4$

$\displaystyle T''(n)=4n+50$

in questo caso $T'(n)$ è 2 volte $T(n)$ e $T''(n)$ è "simile" con $T(n)$ in quanto hanno stesso coefficiente per $n$ ma termine costante diverso.

## Piccoli suggerimenti per i costi asintotici
Quando si hanno operazioni logico-artimetiche o assegnamenti abbiamo costo $O(1)$ ovvero unitario, quindi in un if-else, il costo è dato dalla valutazione della condizione e dal massimo tra il blocco if o il blocco else. Quando si ha un ciclo del tipo, `for(int i=0; i<n; i++)`: si ha un costo $\displaystyle\large\sum_{i=0}^{n-1}t_i$ costo della i-esima iterazione, più il costo dell'assegnazione, il controllo della condizione e l'incremento.

Quando si ha un ciclo del tipo, while(condizione){...}. Abbiamo che il costo è pari a: $\displaystyle\large\sum_{i=0}^nt_i$ + $\displaystyle\large\sum_{j=0}^{n-1} t_j$ , dove $n$ è il numero di volte che la condizione è valutata. 
La prima sommatoria è il costo della valutazione della condizione, mentre la seconda è costo dell'j-esima iterazione. Quando si ha una sequenza di blocchi il costo è dato dalla somma fra i costi dei blocchi. 

Vediamo un esercizio per capire meglio

---
# Esercizio analisi asintotica
Vediamo il costo della chiamata di un metodo insertionSort(A) quanto costa.
Codice insertionSort(A):

``` 
1	for j=2 to A.length{
2		key=A[j]
		//inserisci A[j] nel segmento A\[i,...,j-1\]
3		i=j-1
4		while i>0 and A[i]>key{
5			A[i+1]=A[i]
6			i=i-1
		}
7		A[i+1]=key
	}
```

Abbiamo che n è la dimensione di A. Calcoliamo il costo delle istruzioni:

1. n
2. n-1
3. n-1
4. $\displaystyle\large\sum_{j=2}^n t_j$
5. $\displaystyle\large\sum_{j=2}^n t_j-1$
6. $\displaystyle\large\sum_{j=2}^n t_j-1$
7. n-1

$T(n)$= somma dei costi delle istruzioni.

<font color=green> Costo caso migliore</font>

Il caso migliore è quando l'array è già ordinato. Il costo è pari a $\large T(n)=\theta(n)$

<font color=green> Costo caso peggiore </font>

L'array è disordinato in modo tale che il numero di scambi è pari a $n-j$, quindi il numero di confronti del while è $j$. Il costo è pari a $\large T(n)=\theta(n^2)$. Vediamo velocemente perchè:

Se sostituisco $j$ a $\large t_j$ abbiamo che la prima sommatoria è uguale a $\displaystyle\large\sum_{j=2}^nj$ ma questa altro non è che la sommatoria fino n di Gauss, che è pari a $\dfrac{n(n+1)}{2}$. 
Le altre due sommatorie sarebbero $\displaystyle\large\sum_{j=2}^nj-1$ che altro non è che $\dfrac{n(n-1)}{2}$. Sommando assieme agli altri costi si avrà un polinomio di secondo grado, che analizzando asintoticamente porta a $\large\theta(n^2)$.

Abbiamo visto usati $O(1)$ e $\theta(n)$, ma cosa sono? Andiamo a parlare di [[Notazioni asintotiche e proprietà transitiva| notazione asintotiche]]

---
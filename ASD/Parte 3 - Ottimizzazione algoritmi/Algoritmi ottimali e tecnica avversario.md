[[Metodo srotolamento e limitazioni]]
#asd
# Algoritmi ottimali

>Dato un problema P avente complessità intrinseca $\Omega(g(n))$, un algoritmo A risolutore di P che abbia complessità $O(g(n))$ per P nel caso peggiore è detto ottimale.

Come determinare però la complessità intrinseca? Ci sono 2 metodi:

Il primo metodo consiste nell'osservare che ogni algoritmo risolutore di un problema <font color=red>deve produrre l'output previsto</font> dal problema. Esempio, la somma di 2 matrici quadrate ha come output una matrice quadrata. La complessità intrinseca dell'algoritmo per svolgere la somma è $\Omega(n^2)$. L'algoritmo utilizzato ha complessità $O(n^2)$ perciò è ottimale.

Il secondo metodo parte dal fatto che per alcuni problemi, l'algoritmo risolutore <font color=red>deve leggere tutto l'input</font> e non una porzione di esso per risolvere il problema. Un controesempio tipico è la ricerca binaria.

```java
//ipotiziamo di volere cercare il valore 8 in un array
int[] a={1,2,3,4,5,6,7,8,9,10};
ricercaBinariaIncompleta(a,8);
//ipotiziamo per assurdo che il metodo ricercaBinariaIncompleta non
//guardi la seconda metà di a e che quindi non possa proprio
//trovare la posizione di 8
```

---
## Tecnica avversario

La tecnica dell'avversario ci aiuta per il secondo metodo ed altri casi simili. La tecnica consiste nel supporre che dato un ipotetico algoritmo che risolve il problema con un certo costo, se altero i dati e cerco di far sbagliare l'algoritmo rivelo un costo maggiore, siccome l'output è dato dalla parte dell'input che l'algoritmo guarda. Esempio:

Sia dato un problema P ed una funzione f(n) vogliamo dimostrare che la complessità intrinseca di P è $\Omega(f(n))$. Per assurdo supponiamo che vi sia un algoritmo A risolutore di P che risolve P in "meno" di $\theta(f(n))$ passi. Questo implica che per ogni input $x$ di dimensione $n$, A impiega $\theta(f(n))$ passi per risolvere x. 

Sfruttando il fatto che, l'esecuzione di A su $x$ dipende esclusivamente dalla porzione di $x$ su cui A accede e che restituisce un output $y$, quando viene lanciato su un input $x*$ identico ad $x$ sulla porzione $x'$ restituirà $y$. Se possiamo scegliere un input $x*$ tale per cui si ha $P(x)\mathrlap{\,/}{=}P(x*)$, dimostriamo che A non è risolutore per P arrivando ad un assurdo e quindi portando la complessità intrinseca di P a $\Omega(f(n))$.

>[!warning]
>Il limite inferiore della complessità per algoritmi di ordinamento basato su confronti è $\Omega(n log n)$

---

# Esercizio tecnica avversario e calcolo complessità intrinseca.

Dati 2 vettori ordinati u e v, produrre un vettore w ordinato che contenga tutti gli elementi di u e v comprese le eventuali ripetizioni. La complessità intrinseca è $\Omega(n+m)$ con n dimensione di u e m dimensione di v. Questo è facilmente verificabile grazie al primo metodo per calcolare la complessità intrinseca, in quanto se le dimensioni sono n ed m, allora ho complessità intrinseca n+m per fonderli assieme senza guardare l'ordine.

Dimostrare che servono 2n-1 confronti e non 2n-2 confronti per attuare merge di 2 vettori. Prima cosa definiamo 2 vettori:

x=$(x_0,x_1,x_2,x_3)$ y=$(y_0,y_1,y_2,y_3)$ tale che

$x_0<y_0<x_1<y_1<x_2<y_2<x_3<y_3$

4 elementi ciascuno e 7 confronti ed output $(x_0,y_0,x_1,y_1,x_2,y_2,x_3,y_3)$.

Ipotizziamo adesso un input del genere:

y=$(y_0,y_1,y_2,x_3)$ x=$(x_0,x_1,x_2,y_3)$ ed ignoriamo l'ultimo confronto quindi $x_0<y_0<x_1<y_1<x_2<y_2<y_3$ e dopo? Se non considero l'ultimo confronto ho che l'output che si verrà a creare sarà uguale fino $y_2$, perché i confronti singolarmente sono uguali, sia prima avevo che $x_3$ era maggiore di $y_2$ sia adesso. Solo che ignorando l'ultimo confronto il risultato sarebbe $(x_0,y_0,x_1,y_1,x_2,y_2,y_3,x_3)$.

Avrei perciò un output diverso da quello su x. Perciò è dimostrato che 2n-2 confronti non bastano.

---
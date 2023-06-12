[[Analisi asintotica]]
#asd 
# Notazioni asintotiche

Per l'analisi asintotica andiamo a sfruttare 3 notazioni che servono a comparare funzioni al tendere dell'argomento a +$\infty$:

$\large O(n)$, $\large\theta(n)$ e $\large\Omega(n)$

- <font color=green> $\large O(n)$ </font>: date 2 funzioni f e g, diciamo che, se f è $\large O(g)$ (f appartiene $\large O(g)$) intuitivamente questo vuol dire che, al tendere dell'argomento a $\infty$, g cresce più velocemente di f (a partire da un certo valore dell'argomento, g si mantiene sempre maggiore di f). In formula:

$\large O(g)=\{f |  \exists n_0$ tale che $\large\forall n \ge n_0$ allora $\large f(n) \le g(n)$}

>In sintesi, se f appartiene a $O(g)$, la funzione g cresce più velocemente di f.


Esempi:
1. $\large2n+5=O(n)$ perché $\large2n+5\le 7n\ \forall n$
2. $\large2n+5=O(n^2)$ perché $\large2n+5\le n^2$  $\forall n\ge4$
3. $\large2n+5=O(2^n)$ perché $\large2n+5\le 2^n \ \forall n\ge4$

Se f(n)=$\large 3n^2+2$, g(n)=$\large 2n^3$ e h(n)=$4n^2+2$:
- f appartiene $\large O(g)$ è vero per n=10 f(10)=302, g(10)=2000, anche perchè $n^2<n^3$.
- g non appartiene $O(f)$
- g appartiene $O(g)$ è vero perchè si considera ≤.
- f appartiene $O(h)$ è vero
- h appartiene $O(f)$ è falso

Quest'ultimo caso ci fa capire che la definizione data è errata, perchè una costante può influire. Corregiamola in:

<font color=blue>$\large O(g)=\{f | \exists n_0$ e $c$ tale che $\large\forall n \ge n_0$ allora $\large f(n)\le c*g(n)\}$</font>

Vediamo adesso la definizione di $\large\Omega(n)$:

- <font color=green> $\large \Omega(n)$</font>: date 2 funzioni f e g, diciamo che, se f è $\Omega(g)$ (f appartiene $\Omega(g)$) questo vuol dire che, al tendere dell'argomento all'infinito f cresce più velocemente di g.

In sintesi: f appartiene $\Omega(g)$ allora f cresce più velocemente di g.

$\large \Omega(g)=\{f |\exists n_0$ e $c$ e $\large \forall n \ge n_0$ allora $\large f(n) \ge c*g(n)\}$

<font color=green> $\large \theta(n)$</font>: f appartiene a $\theta(n)$ se e solo se f appartiene sia a  $O(g)$ e $\Omega(g)$.

Esempio:

f(n) = $3n^2+10n$ abbiamo che $O(n^2)$

Troviamo $c$ e $n_0$ tale che f(n)≤ c*$n^2$ $\forall n\ge n_0$

$3n^2+10n \le 13n^2$ perciò c=13, $n_0$=0

$f(n)$ appartiene $\Omega(n^2)$ infatti 
$3n^2+10n \ge 3n^2$ perciò c=3, $n_0=0$
>Quando O(1) allora si dice che il numero di istruzioni non dipendono dalla dimensione dell'input.

---

# Proprietà transitiva
Siano f, g e h funzioni, abbiamo allora che:

se $\large f \in O(g)$ e $\large g \in O(h)$ allora $\large f \in O(h)$ 

In parole povere, se $g$ cresce più velocemente di $f$ e $h$ cresce più velocemente di $g$, allora $h$ cresce più velocemente di $f$.

Nel dettaglio:

$\large f \in O(g): \exists c,n_0\  |\  \forall n \ge n_0 \ f(n) \le c*g(n)$
$\large g \in O(h): \exists c',n_0'\ |\  \forall n \ge n_0'\  g(n) \le c'*h(n)$
$\large f \in O(h): \exists c^*,n_0^*\  |\ \forall n \ge n_0^*\  f(n) \le c^**h(n)$

Piccola dimostrazione:

$\large f(n) \le c*g(n)$ e $\large g(n) \le c'*h(n)$

Se moltiplicando per c i due membri della seconda disequazione, abbiamo: $\large c*g(n) \le c*c'*h(n)$.
Infine se prendo $n$ il $\large max\{n_0,n_0'\}$ e $\large c^*=c*c'$ allora ho verificato la seguente disequazione:

$\large f(n) \le c*g(n) \le c^**h(n)$.

La stessa proprietà è facilmente dimostrabile per $\Omega(n)$.

$\large f(n) \ge c*g(n)$ e $\large g(n) \ge c'*h(n)$

Riprendiamo $\large g(n) \ge c'*h(n)$ e moltiplichiamo entrambi i membri per $c$ $\large c*g(n) \ge c*c'*h(n)$. Poi prendo $n$ il $\large max\{n_0,n_0'\}$ e $\large c^*=c*c'$ allora ho verificato la seguente disequazione:

$\large f(n) \ge c*g(n) \ge c^**h(n)$.

---

##  Ulteriore proprietà per la caratterizzazione di una funzione

Se ho 3 funzioni f, g e h tale che <font color=blue>$\large f(n)=g(n)+h(n)$</font> e <font color=green>$\large g \in O(h)$</font> e voglio caratterizzare la funzione più veloce posso dedurre che $\large f \in O(h)$. Dimostrazione:

$\large g \in O(h): \exists c,n_0\  | \ \forall n \ge n_0\  g(n) \le c*h(n)$
prendendo $\large g(n)=c*h(n)$ e sostituendolo in $\large f(n)=g(n)+h(n)$ allora si ha che $\large f(n) \le c*h(n)+h(n)$ cioè $\large f(n) \le h(n)*(c+1)$.

---

## Classificazione degli algoritmi in modo pratico
Se ho che un problema P ha classe di complessità pari a $O(n^2)$, vuol dire che ad un qualsiasi algoritmo risolutore è richiesto di compiere al più $O(n^2)$ passi. Quindi se vengono proposti un algorimo A con costo $O(n)$ ed un algoritmo B con costo $O(n^4)$, l'algoritmo A non è risolutore di P mentre B si.

Se ho che un problema P ha classe di complessità pari a $\Omega(n^2)$, vuol dire che ad un qualsiasi algoritmo risolutore è richiesto di compiere almeno $\Omega(n^2)$ passi. Se vengono proposti un algoritmo A con costo $O(n)$ ed un algoritmo B con costo $O(n^2)$, l'algoritmo A non è risolutore di P mentre B si.

---
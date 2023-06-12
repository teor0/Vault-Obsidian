[[Esempi algoritmi tipo 1 e 2]]
#asd
# Algoritmo moltiplicazioni di interi con n cifre.

Per effettuare la moltiplicazione $x*y$, indichiamo $\large x_i$ e $y_i$ la i-esima cifra di x e y. Decomponiamo il tutto in:

$\displaystyle\large \sum_{i=0}^{n-1}x*y*B^i$ dove B è la base del sistema di numerazione (10 in genere ma anche 2 per il binario). Ogni moltiplicazione ha complessità temporale $\theta(n)$, di queste operazioni se ne fanno n e poi sommiamo n numeri, perciò abbiamo che l'algoritmo ha complessità temporale pari a $\theta(n^2)$. Si può fare di meglio con la tecnica dividi et impera?

Decomponiamo i 2 interi x e y ognuno in 2 parti aventi lo stesso numero di cifre:

$\displaystyle\large x=x_1*B^{n\over\Large2}$ + $x_0$ e $\displaystyle\large y=y_1* B^{n\over2}$+$y_0$. Dove $x_1$ sono le prime $\displaystyle {n\over2}$ cifre più significative di x ed $x_0$ sono le restanti $\displaystyle {n\over2}$ meno significative. Stesso discorso per $y_1$ e $y_0$.

$\displaystyle\large x*y=(x_1*B^{n\over2}+x_0)*(y_1*B^{n\over2}+y_0)=$
$\displaystyle\large=x_1y_1B^n+x_0y_1B^{n\over2}+x_1y_0B^{n\over2}+x_0y_0=$
$\displaystyle\large=x_1y_1B^n+(x_0y_1+x_1y_0)B^{n\over2}+x_0y_0$.

Nel caso peggiore si ha complessità $\theta(n)$ per la suddivisione e 4 sottoistanze. Le operazioni del tipo $x*B^n$ hanno costo $\theta(n)$ con lo shift sinistro. Le somme hanno costo proporzionale al più 2n cioé $\theta(n)$. L'algoritmo perciò è di tipo 1 con a=4, c=2 e d=1. Quindi $\Large {a\over c^d}$=$\large{4\over2^1}$=2, perciò complessità pari a $\theta(n^{log_ca})\Rightarrow\theta(n^{log_24})\Rightarrow\theta(n^2)$ non conviene dunque. Provando a dividere in 3 o 4 o 5 ecc. non converrà mai. Dobbiamo trovare il modo di abbassare il numero di moltiplicazioni così da abbassare il numero di sottoistanze.

Poniamo adesso $\large m_3=x_1y_1$ e $\large m_1=x_0y_0$ abbiamo perciò:

$\displaystyle\large {m_3B^n+(x_0y_1+x_1y_0)B^{n\over2}+m_1}$

bisogna trovare una sostituzione per $(x_0y_1+x_1y_0)$. Poniamo ora $\large M=m_1+m_2+m_3$. $\large M=x_0y_1+x_1y_0\Rightarrow m_1+m_2+m_3=x_0y_1+x_1y_0$ ovvero $\large x_1y_1+m_2+x_0y_0=x_1y_1+x_1y_0\Rightarrow m_2=x_0y_1+x_1y_0-x_1y_1-x_0y_0$ 
$\large \Rightarrow m_2=y_1(x_0-x_1)+y_0(x_1-x_0)\Rightarrow m_2=(x_0-x_1)*(y_1-y_0)$

Abbiamo perciò un prodotto tra $\displaystyle{n\over2}$ cifre, 5 somme e 3 moltiplicazioni: 
$\displaystyle\large m_3B^n+(m_3+m_2+m_1)B^{n\over2}+m_1$ leggermente più complicata ma con efficienza di minore $\theta(n^2)$ perché:

$a$=3, c=2 e d=1
$\Rightarrow\displaystyle\Large {a\over c^d}$=$\displaystyle\large{3\over2}>1\Rightarrow$$\displaystyle\large\theta(n^{log_ca})\Rightarrow\displaystyle\large\theta(n^{log_23})\Rightarrow\displaystyle\large\theta(n^{1,585})$.

---

# Algoritmo di Strassen per le moltiplicazioni tra matrici

Possiamo progettare un algoritmo divide et impera basandoci sull'osservazione che una matrice $n*n$ può essere vista come una matrice 2\*2 ove ciascun elemento è a sua volta una matrice $\displaystyle{n\over2}*{n\over2}$.

![[strassen.jpg]]

Come parametri abbiamo quindi:

- $a$=8 perché 8 sottoistanze
- c=2 perché dimensione pari alla metà
- d=2 bisogna eseguire 4 somme di matrici

Quindi $\displaystyle{a\over c^d}={8\over2^2}=2>1$ perciò $\large\theta(n^{log_ca})=\theta(n^{log_28})=\theta(n^3)$ non conviene ma Strassen, trovò un modo per calcolare r,s,u e t con 7 moltiplicazioni di matrici $\displaystyle{n\over2}*{n\over2}$.

![[metodostrass.jpg]]

Abbiamo perciò come parametri $a$=7, c=2 e d=2 che ci danno $\displaystyle{a\over c^d}={7\over4}>1$, perciò $\large T(n)\in\theta(n^{log_ca})=\theta(n^{log_27})=\theta(n^{2,807})$ che conviene.

---
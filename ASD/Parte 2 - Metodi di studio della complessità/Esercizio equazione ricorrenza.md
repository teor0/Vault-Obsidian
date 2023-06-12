#asd 
# Esercizio equazione ricorrenza

Vediamo un altro esempio per quanto riguarda l'equazione di ricorrenza:

```java
public static int fib(int n){
	if(n<=1)
		return 1;
	return fib(n-1)+fib(n-2);
}
```

Calcoliamo la complessità T rispetto n:

$\large T(n)=c$ se $n≤1$

$\large T(n)=c+T(n-1)+T(n-2)$ se $n>1$

assumiamo una limitazione superiore, essendo $\large fib(n-1)>fib(n-2)$ cioè $fib(n-1)$ contiene la chiamata $fib(n-2)$ al suo interno possiamo dire che:

- $\large T(n)=c+2T(n-1)$ quando $\large n>1$
- $\large T(n)=c$ quando $n≤1$

calcoliamo adesso il limite superiore con il metodo dello srotolamento.

Ipotiziamo $n=n-1$ e che $n>1$

$\displaystyle\large T(n)=2(2T(n-2)+c)+c= 2^2T(n-2)+c \sum_{i=0}^1 2^i=$

$\displaystyle\large 2^2(2T(n-3)+c)+c\sum_{i=0}^1 2^i= 2^3T(n-3)+c \sum_{i=0}^2 2^i$

si capisce che al j-esimo passo si ha $\displaystyle\large2^jT(n-j)+c\sum_{i=0}^{j-1} 2^i$.

Quando $\displaystyle\large j≥n-1 → n-j≤1$ perciò

$\displaystyle\large 2^{n-1}c+c  \sum_{i=0}^{n-2}2^i=c \sum_{i=0}^{n-1}2^i$.

Ora si sa che 111111 in binario è pari a $\large 2^5+2^4+2^3+2^2+2+1=63$

e 1000000 è $\displaystyle\large2^6=64$ quindi se $\displaystyle\large2^6-1=63$ allora  $\displaystyle\large c \sum_{i=0}^{n-1}2^i=c(2^n-1)$.

In conclusione applicando la notazione asintotica abbiamo che il limite superiore è $\displaystyle\large T(n)\in O(2^n)$.

Vediamo adesso come calcolare il limite inferiore. Le istruzioni di $fib(n-2)$ è sicuramente minore di quelle di $fib(n-1)+fib(n-2)$.

Abbiamo quindi che:

$\displaystyle\large T(n)=2T(n-2)+c$ se $n>1$

$\displaystyle\large T(n)=c$ se $n≤1$

Utilizzando il metodo dello srotolamento possiamo calcolare il limite inferiore:

$\displaystyle\large T(n)=2T(n-2)+c=$ 
$\displaystyle\large 2(2T(n-4)+c)+c=2^2T(n-4)+3c=$
$\displaystyle\large2^2(2T(n-6)+c)+3c=2^3T(n-6)+7c$

Capiamo quindi che al j-esimo passo 
$\displaystyle\large T(n)=2^jT(n-2j)+(2^j-1)c$

quando $\displaystyle\large 2j≥n-1 → n-2j≤1$ perciò:

$\displaystyle\Large {T(n)=2^{{n-1} \over {2}}c+(2^{{n-1}\over 2} -1)c=c(2^{1+\frac{n-1}{2}}-1)= c(2^{{n+1}\over 2}-1)}$ ovvero asintoticamente $\displaystyle\large{\Omega(2^{n \over 2})}$.

In definitiva possiamo dire che $T(n)$ è compreso tra $\displaystyle\large 2^{n \over 2}$ e $\displaystyle\large2^n$.

---
[[Alberi di decisione]]
#asd
# Divide et impera

La tecnica divide et impera è una tecnica utilizzata per la progettazione di algoritmi efficienti. Gli algoritmi realizzati tramite questa tecnica seguono una tecnica comune:

- Se l'istanza è di dimensione banale allora si risolve direttamente oppure, si utilizzano algoritmi efficienti su problemi di piccole dimensioni.
- Si suddivide l'istanza in J istanze dello stesso problema con dimensioni più piccole del tipo <font color=green>$\displaystyle\large n \over \displaystyle\large c$</font> o <font color=blue>$\large n-k$</font>, con c e k costanti indipendenti da n.
- Le sottoistanze vengono risolte applicando lo stesso algoritmo, le soluzioni poi vengono combinate per ottenere la soluzione al problema.

Gli algoritmi che suddividono il problema in J istanza di dimensione $\displaystyle {n \over c}$ sono detti di <font color=green> tipo 1 </font>.

Gli algoritmi che suddividono il problema in J istanza di dimensione n-k sono detti di <font color=blue> tipo 2 </font>.

> Gli algoritmi di tipo 1 <font color=red>sono più efficienti </font> del tipo 2!


---

# Esempio risolviDI

```java
public SoluzioneDI risolviDI() {
	if (dimensioneBanale())
		return risolviDirettamente();
	ProblemaDI[] sottoproblemi = dividi();
	SoluzioneDI[] sottosoluzioni = new SoluzioneDI[sottoproblemi.length];
	for (int i = 0; i<sottoproblemi.length; i++)
		sottosoluzioni[i] = sottoproblemi[i].risolviDI();
	return combina(sottosoluzioni);
}
```

Abbiamo quindi un algoritmo di tipo 1, in quanto il problema di dimensione n è suddiviso in sottoproblemi di dimensione $\displaystyle {n \over c}$ .
Valutiamo adesso i costi dei metodi:

- risolviDirettamente e dimensioneBanale avranno un costo costante rispetto alla dimensione dell'input.

Se ignoriamo momentaneamente il costo degli algoritmi ricorsivi il numero di passi svolti non dipende dalla dimensione dell'istanza ma dai parametri. Supponiamo che l'algoritmo sia caratterizzato dalle seguenti costanti:

- $a$: numero di sottoistanze
- c: costante che regola la dimensione delle sottoistanze
- d: complessità dei metodi dividi e combina, in questo caso $\theta(n^d)$

La complessità dell'algoritmo (T) è descritta dalla seguente equazione di ricorrenza:

$T(n)=b$ se $n≤1$     
$T(n)=\displaystyle\large aT({n \over c})+bn^d$ se $n>1$ dove

$\large aT({n \over c})$ è il costo di `sottoproblemi[i].risolviDI()`, nello specifico $a$ sarebbe sottoproblemi[i] e $\large T({n \over c})$ sarebbe il costo di risolviDI().

$\large bn^d$ è il costo di dividi e combina con una costante b.

Nel caso in cui risolviDI() fosse stato di tipo 2, l'equazione di ricorrenza sarebbe stata pari a:

$\large T(n)=aT(n-k)+bn^d$ se $n>1$ 
$T(n)=b$ se $n≤1$.

---

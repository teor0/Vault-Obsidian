#asd 
[[Code di priorità e heap]]
# Counting sort
L'algoritmo di ordinamento counting sort viene impiegato per ordinare un vettore di interi V, attraverso un vettore di appoggio A. Il vettore di appoggio avrà una dimensioni pari a: max(V)-min(V)+1.
La prima fase dell'algoritmo corrisponde al contare le occorrenze degli elementi di V e aggiornare il numero di occorrenze nel vettore di appoggio.
La seconda fase consiste nel scansionare l'indice k degli elementi possibili e copiare il valore del'indice finché il contatore non diventa pari a 0. L'esempio risulta più chiaro:

![[countingsort.jpg]]

Il costo della prima fase è $\theta(n)$ in quanto si scansiona il vettore V e si incrementano i contatori nel vettore di appoggio. La seconda fase ha costo $\theta(n+m)$ dove $n$ è il numero di scritture ed $m$ è il numero di celle del vettore di appoggio. Quindi la complessità è dominata dalla seconda fase. Tuttavia il valore di $m$ è influenzato dall'input in qualche modo. La dimensione dell'input è data da $n*c$ dove c è una costante che indica il numero di bit che utilizziamo per memorizzare i nostri valori. Si ha necessità di memorizzare fino a $m$ allora si ha che la dimensione dell'input è pari a $n*log_2m$. 
L'algoritmo quindi non è efficiente, ma rispetto al numero di celle è molto efficiente. 
>Da notare che la complessità spaziale è data da max-min+1!

```java
public static void countingSort(int[] v){
	int min=minimo(v);
	int max=massimo(v);
	int []app=new int[max-min+1];
	for(int i=0; i<v.length; i++)
		app[v[i]-min]++;
	int ins=0;
	for(int j=0; j<app.lenght; j++)
		while(app[j]>0){
			v[ins++]=j+min;
			app[j]--;
		}

}
```
---

# Radix sort
Studiamo adesso il radix sort come miglioramento del counting sort, in particolare la logica dietro il radix sort è quella di eseguire un ordinamento lessicografico, con parità di priorità. Il radix sort ha complessità lineare rispetto alla dimensione dell'input. L'algoritmo sceglie una priorità ed effettua un'ordinamento di quel vettore per quella priorità. Se utilizziamo radix sort per ordinare un vettore di interi, l'ordinamento avviene per cifre partendo dalla cifra meno significativa cosìcché, passando a cifre sempre più significative l'ordinamento fatto in precedenza non perde di importanza. Da notare che gli interi li portiamo ad avere tutti lo stesso numero di cifre eventualmente aggiungendo zeri come prefissi. Esempio:
```
23489 passa a 00100 -- 00100 -- 00100
00100         01234    01234    00385
01234         00385    00385    01234
00385         23489    23489    23489
```

Quindi si fa un ordinamento con code di priorità a priorità fissata, dove ad ogni passo si ha costo pari a $\theta(n)$ e ciò si fa $c$ volte per il numero di cifre, quindi si avrà alla fine $\theta(c*n)$, ma $c*n$ è la dimensione dell'input perciò avremo in definitiva $\theta(n)$

>Questo algoritmo soffre dello stesso problema del merge sort e viene anche lui usato in memoria secondaria, data la complessità della coda di priorità a livello di spazio di memoria.

---
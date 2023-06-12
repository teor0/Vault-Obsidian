[[Storia e base di C]]
# Array statici
Un array in C funziona esattamente come in Java con qualche piccola differenza. Perciò per definire un array si usano istruzioni simili a quelli di Java. Per gli array statici la dimensione deve essere nota a tempo di compilazione. Mentre per gli array dinamici non è necessario sapere a priori la dimensione.
Risulta quindi ovvio che come in Java, in C posso creare un array nel seguente modo:
```c
	int n=10;
	int v[n];
```
per allocare un generico elemento del vettore, in C bisogna usare<font color=yellow> l'operatore unario di indirizzo &, </font> che restituisce l'indirizzo della locazione di memoria dell'operando. L'operatore di indirizzo non va usato come left value, ovvero non deve stare a sinistra dell'uguale in un'operazione. Vediamo nel codice
```c 
	&v=b
	a=&v
```

<font color=yellow> L'operatore unario di dereferenziazione \* </font> di un puntatore restituisce il valore della variabile puntata dall'operando. Se viene usato come right value, si esegue un'operazione di estrazione: ^f56ab0
```c 
	a=*p;
```
assegna ad a il valore della variabile puntata da p.
Se viene usato come left value, si esegue un'operazione di inserimento:
```c 
	*p=a;
```
assegna il valore di a alla variabile puntata da p.
![[value.png]]

## Problema del buffer overflow
Se alloco un vettore buffer di 10 elementi, cosa succede a buffer[10]? Ci sono 2 problemi:
1. sovrascriviamo una cella di memoria già occupata
2. avviene segmentation fault
Anni fa, il segmentation fault era privo di controlli ed era molto sfruttato dagli hacker per eseguire funzioni da loro create. Dentro la memoria lo stack memorizza i valori di una funzione. All'interno dello stack è contenuto l'indirizzo di ritorno del main, attraverso il segmentation fault riesco ad cambiare questo indirizzo di ritorno, per entrare nella funzione malevola.
![bufferoverflow](returnaddress.png)

# Puntatori
Supponiamo di avere un task A, che gira sulla RAM. Il task A occupa la memoria da 4KB a 20KB quindi occupa 16KB di RAM. Questi 16KB poi vengono divisi tra codice , stack ed heap.
![Visualizzazione](task.jpg)
Una variabile di tipo puntatore, è designata a contenere l'indirizzo di memoria di un'altra variabile (variabile puntata), la quale a sua volta può essere di qualunque tipo anche non nativo.

# Array dinamici
Per utilizzare array dinamici bisogna far uso del comando mallock, che alloca memoria non inizializzata (ovvero che non ha assunto valori prima). Vediamo come:
```c 
	int *v;
	int i;
	int n;
	printf("inserisci la dimensione n del vettore "); 
	scanf("%d", &n); 
	v=(int*)malloc(n*sizeof(int)); 
	if(v==NULL){ 
	printf("ERRORE NELLA MALLOC\n"); 
	return 1; 
	} 
	for(i=0; i<n; i++){ 
	printf("inserisci v[%d]",i); 
	scanf("%d", &v[i]); 
	} 
	free(v);
```

Una volta terminato di utilizzare il vettore, si utilizza la funzione free() che libera memoria puntata dal vettore v. È importante notare che non bisogna utilizzare la memoria liberata da free, in quanto è memoria inizializzata!
## Errori che possono sorgere con l'utilizzo
Ci sono 2 tipi di errori che possono sorgere quando si utilizza un puntatore:
- <font color=blue> Segmentation fault</font>: tentativo di accedere a locazioni di memoria esterni al programma ![segmentationfault](segmentation_fault.png)
- <font color=blue> Memory override</font>: cambio erroneo di valori di variabili all'interno del programma

Esempio segmentation fault:
```c 
	px=(int*)500;
```
in questo modo si cambia l'indirizzo a cui punta px andando fuori dall'area di memoria del programma.
Esempio di memory override:
```c 
	px++;
	*px=50;
```
potrebbe capitare che si cambi il valore di un'altra variabile e non della variabile x.

---
Un vettore v è composto da vari elementi, l'elemento v[0] ha un indirizzo 0x7b...0, il vettore v ha indirizzo uguale a quello dell'elemento v[0]. Perciò se ho un puntatore \*p e faccio le seguenti istruzioni:
```c 
	*p=x;
	*p=&v[0];
```
l'assegnazione è la stessa. \*p punterà in entrambi i casi all'indirizzo 0x7b...0.

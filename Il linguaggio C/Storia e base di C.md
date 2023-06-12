# Storia di C

Il C è un linguaggio <font color=red> imperativo </font> legato a Unix, adatto all'implementazione di compilatori e sistemi operativi. 
Per imperativo si intende che un programma viene inteso come un insieme di istruzioni ciascuna delle quali è eseguita in ordine.

È stato progettato da Dennis Ritchie per il PDP-11 all'inizio degli anni '70. Nel 1983 l'ANSI ne ha definito una versione standard portabile (ANSI C). A differenza dei linguaggi da cui ha tratto le idee fondamentali ovvero B, è un linguaggio tipato. Il C è un linguaggio <font color=red>compilato </font> a differenza magari di Java, che può girare ovunque grazie alla Java Virtual Macchine.  ^b3d029

La compilazione è preceduta da una fase di <font color=red> preprocessing </font>, dove avviene la sostituzione di macro, inclusione di file sorgenti ausiliari ed altro ancora. La compilazione avviene tramite [gcc](https://gcc.gnu.org/) il compilatore fornito da GNU. Per installare il compilatore tramite shell:
```ad-info

sudo apt-get install build-essential

```


---
Il linguaggio C è considerato di alto livello, ma non "troppo", in quanto fornisce le primive per manipolare numeri, caratteri ed indirizzi di memoria, ma non oggetti composti come ad esempio stringhe, liste ecc. Per effettuare operazioni di input/output si deve ricorrere alla libreria standard.
## Compilare in C
C ha assunto uno [[#^b3d029|standard]] nel corso del tempo, quindi per essere in linea con la comunity si dovrebbe utilizzare lo standard di compilazione tramite il comando:
`gcc -std=c11 helloworld.c`
in questo modo usiamo lo standard di C11 ovvero il più recente. All'interno del corso evitiamo di utilizzare uno standard e quindi compiliamo il codice tramite
`gcc helloworld.c`
compilare helloworld.c restituisce il file binario a.out, che contiene l'immagine dell'eseguibile da caricare in memoria. Digitando nella shell `a.out` apparira a schermo l'output Hello world! Per rinominare il file binario basta utilizzare l'opzione -o e digitare il nome che si vuole.

---
## Struttura di un programma C
La struttura di un programma C contiene un main, con all'interno una sezione di dichiariazione e poi una sezione di corpo. Vediamo l'esempio classico di Hello World! ed uno di un programma semplice
```c
#include<stdio.h>
int main(){
	printf("Hello World!");
	return 0;
}
```
```c
#include<stdio.h>
#include<stdlib.h>
int main(){
	//sezione dichiarativa
	int x;
	
	//sezione di corpo
	scanf("%d", &x);
	printf("Valore asseganto ad x:%d\n", x);
	return 0;
}
```
All'interno del secondo programma abbiamo diviso il codice in, sezione dichiarativa e sezione di corpo.

---
## Tipi base di C
A differenza di Java, C ha meno tipi di base:

Tipo | Rappresenta
--| -
int | interi
short | intero corto
long | intero lungo
float | numero con la virgola a singola precisione
double | numero con la virgola a doppia precisione
char | carattere

A ben vedere manca il tipo <font color=yellow>bool</font> che tuttavia si può "integrare" attraverso gli int, oppure attraverso la libreria <span style="font-family:default; font-size:default; color:yellow"> stdbool</span> si può utilizzare normalmente.

In C esistono 2 tipi di conversioni: 
1. Promozioni, ovvero come in Java uno short sarà sicuramente rappresentabile come int e così via. La gerarchia in C è la seguente: char→int→long→float→double
2. Casting, uguale a quello di Java
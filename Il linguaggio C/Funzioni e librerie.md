[[Storia e base di C]]
# Funzioni
In C le funzioni sono caratterizzate da un nome, dal tipo della variabile ritornata e da una lista di parametri, insomma tale e quale a Java. Il return è solo 1 come in Java! All'interno di un file c si ha di solito una struttura del genere:
1. sezione di dichiarazione delle funzioni
2. corpo del main
3. sezione di implementazione delle funzioni

Per stampare su standard output, si utilizza la funzione <span style="font-family:default; font-size:default; color:yellow">printf </span>, che può essere utilizzata in 2 modi possibili:
1. 
```c
	printf("Hello world! \n");
```
dove sostanzialmente si stampa una stringa.
2. 
``` c
	printf("Valore di x =%d", x);
```
Si stampa una stringa ed il valore della variabile x. Per stampare i valori memorizzati nelle variabili, bisogna specificare il formato per il tipo della variabile:

Formato | Tipo argomento
------- | --------------
%d, %i  | integer
%f | float o double fino a 6 cifre
%c | char
%s | string e bool
%p | puntatori

Sempre all'interno della printf si possono usare <font color=yellow> caratteri di escape </font> per stampare caratteri speciali. Vediamo quali sono i più utili:

Escape | Descrizione
-------|-----------
\n | ritorno a capo
\b | backspace
\t | tabulazione
\\" | doppi apici
\\\ | backslash

---
La funzione malloc serve ad allocare una porzione di memoria.
La funzione calloc svolge la funzione della malloc, ma in più inizializza la memoria a zero, quindi riserva ed inizializza memoria. 
La funzione realloc ridimensione l'area di memoria
``` c
	realloc(ptr, new_size);
```

## Passaggio di parametri
In C a differenza di Java un parametro può essere passato sia per valore, sia per riferimento, tramite [[Array, puntatori, operatori di indirizzo e dereferenziazione e buffer overflow#^f56ab0|l'operatore di dereferenziazione]] *.

# Librerie
Le librerie in C sono di 2 tipologie:
1. librerie standard che sono contenute in <> ad esempio stdio.h
2. librerie non standard che sono contenute in "" ad esempio mylib.h
Le librerie sono divise in 2 file, il file header .h ed il file contenente tutte le implementazioni delle funzioni di tipo .c

Per creare una propria libreria occore svolgere i seguenti passi:
1. creare un file header con tutte le intestazioni delle funzioni
2. creare un file contenente le implementazioni delle funzioni ed aggiungere all'inizio la clausola `#include"fileheader"`
3. creare il codice oggetto del file contenenti le implementazioni tramite `gcc -c impl.c` che crea impl.o
4. creare il codice oggetto del file che utilizza le funzioni desiderate ad esempio `gcc -c main.c` che crea main.o
5. infine compilare passando i codici oggetto creati `gcc -o main main.o impl.o`

Le intestazioni delle funzioni normalmente si mettono in un file .h, mentre in un altro file con lo stesso nome di tipo .c si trovano le implementazioni. Per poi sfruttare le librerie fatte da utenti si utilizza:
```c 
	#include "mylib.h"
```
in quanto tra <> si mettono le librerie standard.
Nel caso di programmi più grandi è conveniente suddividere il codice in più file. C consente 3 modi di suddividere il codice:
1. <font color=blue> Inclusione diretta di file sorgente</font>: effettuata dal preprocessore mediante una direttiva `#include "mylib.c"`. Prima della compilazione il preprocessore inserisce il contenuto del file mylib.c nel codice. Questo è il metodo più semplice ma meno efficiente, dato che la modifica di uno solo dei file richiede la ricompilazione del intero programma
2. <font color=blue>Header file</font>: anziché includere tutto il file sorgente, si può includere il file mylib.h, che contiene solamente le inclusioni di altri header file, definizione di strutture e tipi e le intestazioni funzioni. L'implementazione delle funzioni va scritto in un file .c che deve includere l'header. Durante la compilazione deve essere effettuato il linking.
3. <font color=blue>Creazione di librerie statiche o dinamiche</font>: la fase di linking, è l'ultima nella creazione di un eseguibile ed aggiunge ai file oggetto il codice delle librerie esterne necessarie per il programma. Il linking può essere statico (l'eseguibile contiene una copia del codice della libreria) o dinamico (l'eseguibile contiene un riferimento alla libreria). Un link statico non presuppone la presenza delle librerie sul PC, è più veloce nel caricamento del programma, ma consuma più memoria. Un link dinamico invece presuppone la presenza delle librerie sul PC, è più lento nel caricamento, ma consuma meno memoria.


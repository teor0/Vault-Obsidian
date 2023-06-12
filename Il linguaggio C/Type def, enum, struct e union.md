[[Storia e base di C]]
Attraverso type def si possono definire dei tipi, per poi impiegarli.
``` c
	#define true 1
	#define false 0
	typedef int boolean;
	//definisco il tipo boolean che memorizza interi
	//le define fatte prima sono fatte apposta che il compilatore sostituisca 
	//a true 1 e false 0. cosi posso scrivere in modo molto più leggibile
```
Una variabile boolean può essere anche definita attraverso enumerazione. L'enumerazione di C è molto simile a quella di Java. Il tipo enumerativo, enum può essere impiegato in 2 modi:
1. attraverso la definizione di un tipo enum con una sua lista di valori, e successivamente la definizione di una variabile di quel tipo enum
2. attraverso una typedef, in modo più "astratto", senza dover definire una variabile per il tipo enum che si vuole utilizzare. Quindi appunto una sorta ti definizione di un tipo che può assumere una lista di valori definiti.
``` c
	enum boolean {false,true};
	enum boolean trovato;
	typedef enum {false,true} boolean;
```
Il compilatore assegna di default ai valori della lista, dei valori interi a partire da 0. Tuttavia si possono assegnare dei valori arbitrari attraverso un normale assegnazione.
``` c
	typedef enum {true=1, false=0} boolean;
```

# Struct
Le struct sono quello che in Java sono gli oggetti, ovvero sono strutture dati aggregate, dove non ci sono metodi ed altri dettagli che ad alto livello come in Java è possibile trovare. 
``` c
	struct nome_struct{
	tipo campo;
	}
	struct nome_struct variabile;
	variabile.campo=...;
	//per non portarci dietro la parola chiave struct si può usare typedef
```
Per i puntatori a struct è possibile utilizzare l'operatore `->`. 

La union è un dato strutturato che permette di manipolare diversi tipi di dati. La union è una variabile che può contenere più tipi. Esempio per capire:
``` c
	union n{
		int int_val;
		float f_val;
	} number;
```
La variabile number potrebbe quindi assumere un valore intero oppure float. 
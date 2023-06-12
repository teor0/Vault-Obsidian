[[Algoritmi ottimali e tecnica avversario]]
#asd 
# Alberi di decisione

La tecnica degli alberi di decisione, si può tenere conto solamente per algoritmi che producono il loro output <font color=red>esclusivamente</font> sulla base dei confronti effettuati, ad esempio: bubble sort e selection sort. 

La tecnica si basa sulla rappresentazione di un algoritmo mediante un albero di decisione. Un albero di decisione è un albero in cui ogni nodo interno rappresenta un'operazione di confronto, i rami da esso uscenti corrispondono ai 2 esiti possibili (> oppure ≤) ed ogni foglia rappresenta l'esito di una serie di confronti ovvero una risposta. Vogliamo perciò contare il numero minimo di confronti che un algoritmo di confronto compie, contando tutte le possibili risposte in modo tale che consideriamo tutti gli input possibili. 

Se un algoritmo è risolutore di un problema, il numero di foglie presenti nell'albero, corrispondente alle possibili esecuzioni su input di dimensione n, deve essere ≥ al numero di risposte diverse che per questi input devono essere date. Un qualsiasi algoritmo che fa al più x confronti su un input di dimensione n al massimo può dare $\large 2^k$ risposte. Quindi per il problema dell'ordinamento di un vettore deve risultare $2^k\ge n!$ dove n! è il numero totale di tutti i possibili input.

Siccome $\large n!\sim n^n$ abbiamo che se si estrae $log_2$ da entrambi i lati si ottiene $\large 2^k\ge n^n$ → $\large k\ge nlog_2n$ perciò il lower bound è $\Omega(nlog_2n)$. Su domini ordinati invece $2^k\ge n+1$ ovvero $k\ge log_2(n+1)$ da questo capiamo che il lower bound è $\Omega(log_2n)$, essendo più basso di $\Omega(nlog_2n)$.

Perciò dato un problema di ordinamento, il numero di risposte è dato da <font color=red> $\large confronti^{possibili esiti}$</font> ed il numero di possibili risposte è dato da <font color=red>numero elementi*possibili risposte</font>.

---

# Esercizio monetine

Siano date 12 monete tra cui una di peso diverso dalle altre ed una bilancia a 2 piatti. Con 3 pesate si riesce a stabile quale sia la moneta con peso diverso. Dimostrare che con 14 monete è impossibile stabilire quale sia la moneta di peso diverso, se c'è e se più leggera o più pesante. Analizzare anche il caso in cui le monete siano 13.

Il numero di possibili esiti a pesate è 3 cioè, monete uguali, moneta più pesante o più leggera, indipendentemente dal numero di monete che si utilizza a pesata. Il numero di confronti è 3, perciò si ha che il numero di risposte che possiamo dare è $3^3$=27. C'è una possibile moneta di peso diverso abbiamo perciò 2 risposte a moneta: leggera\pesante o uguale a quella sull'altro piatto. Il numero di possibili risposte perciò è 14\*2+1, dove 1 sta ad indicare la risposta che dice che tutte le monete sono uguali. Quindi abbiamo risposte pari a 29 e possibili risposte che possiamo dare pari a 27. 29>27 quindi è inutile pensare un algoritmo per dare una risposta efficiente in quanto i confronti non bastano.

Per quanto riguarda il caso delle 13 monete, si hanno sempre 27 risposte possibili da dare e numero di risposte pari a 13\*2+1 che è proprio 27.

---
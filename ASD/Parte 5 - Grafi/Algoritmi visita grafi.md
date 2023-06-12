#asd 
[[Strutture dati per rappresentare grafi]]
# Tecniche di visita
Gli algoritmi per visitare i grafi comportano un problema di base per molte applicazioni. Esistono 2 tecniche principali:
- BFS: visita in ampiezza, corrispondente negli alberi alla visita per livelli
- DFS: visita in profondità, corrispondente negli alberi alla visità anticipata

``` 
visititaGenerica(vertice S){
	//rende tutti i vertici non marcati
	//inizializza T, albero formato solo dal nodo S
	//inizializza F, insieme vuoto di vertici detto frangia
	//marca il vertice S ed aggiunge S a F
	while(F!=0)do{
		estrai un qualsiasi vertice u da F
		visita il vertice u
		for each(arco(u,v)in G)do
			if(v non ancora marcato)then
				marca v ed aggiunge v a F
				rendi u padre di v in T
			else
				eventualmente rendi u padre di v in T
	}
	return T
}
```

F sarebbe l'insieme dei vertici per i quali non abbiamo ancora esplorato i vicini
Il while ha costo $\theta(n)$.
Le 2 istruzioni dell'if hanno costo unitario.
Il costo della visita è dato dal for each per tutti i nodi.

Un vertice viene marcato solo la prima volta. La marcatura può essere mantenuta tramite un vettore di bit di marcatura. La visita genera un albero di copertura, inoltre l'insieme F$\subseteq$T mantiene la frangia di T, ovvero la porzione da esplorare.

Se v$\in$T e v$\notin$F, v è detto chiuso e tutti gli archi incidenti su v sono esaminati.
Se v$\in$F, v è aperto ed esistono archi incidenti su v ancora da esaminare.

Il costo sarà:
- per matrice di adiacenza $O(n^2)$
- per liste di adiacenza $O(m+n)$
- per lista di archi $O(m*n)$

Perchè? Perché eseguo il while al massimo $O(n)$, se da S tutti i nodi hanno un cammino che parte da S per raggiungerli.

>Se la frangia è implementata come coda si ha una visita in ampiezza.
>Se la frangia è implementata come pila si ha una visita in profondità.

Accade quello che accade negli alberi tramite la struttura iterativa. Vediamo adesso l'implementazione:

``` java
visititaInAmpiezza(vertice S){
	rende tutti i vertici non marcati
	inizializza T, albero formato solo dal nodo S
	inizializza F come coda
	marca il vertice S ed aggiunge S a F
	while(! F.isEmpty())do{
		estrai un qualsiasi vertice u da F
		for each(arco(u,v)in G)do
			if(v non ancora marcato)
				marca v ed aggiunge v a F
				rendi u padre di v in T
	}
	return T
}
```
Per ogni nodo v, il livello di v nell'albero BFS è pari alla distanza di v dalla sorgente S.
Per ogni arco (u,v) di un grafo non orientato gli estremi u e v appartengono allo stesso livello oppure a livelli consecutivi dell'albero.
Se il grafo è orientato, possono esistere archi (u,v) che attraversano all'indietro più di un livello.

La visita DFS può essere fatta ricorsivamente:
``` java
visitaDFS(vertice S){
	crea un albero vuoto T
	visitaDFSricorsiva(S,T)
	return T
}

visititaDFSricorsiva(vertice v, albero T){
	marca e visita il vertice v
	for each(arco(v,W))do
		if(w non è marcato)
			aggiunge l'arco (v,w) a T
			visitaDFSricorsiva(W,T)
}
```

---
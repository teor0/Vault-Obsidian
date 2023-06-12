[[Metodo sostituzione ed eliminazione della ricorsione di coda]]
#asd 
# Dettagli sulle strutture dati

La gestione di collezioni di oggetti è definita da 2 particolari:

1. Il tipo di dato che specifica le operazioni di interesse su una collezione di oggetti ad esempio inserimento, cancellazione e ricerca.
2. Le strutture dati, ovvero l'organizzazione dei dati che permette di supportare le operazioni di un tipo di dato usando meno risorse di calcolo possibile.

Esistono 2 modi per rappresentare le strutture dati:

1. Rappresentazione <font color=red>indicizzata</font>: è una rappresentazione statica che ha come pro l'accesso diretto ai dati mediante indici ma come contro una dimensione fissa.
2. Rappresentazione <font color=red>collegata</font>: è una rappresentazione dinamica che ha come pro la dimensione variabile che offre aggiunta e rimozione degli elementi in tempo costante, come contro l'accesso sequenziale ai dati.

Ci sono dei casi in cui la rappresentazione collegata non può essere gestita, in quanto ad esempio: l'heap non esiste perché la gestione della memoria a basso livello non è supportata o nel caso in cui non è implementata. Ovviamente paghiamo sempre la riallocazione.

Per quanto riguarda array ordinati abbiamo che:
```java

search(Object x)
//ricerca tramite ricerca binaria. costo O(log n)
insert(Object x)
//inserisce un elemento spostando a destra gli elementi successivi
//costo O(n)
delete(Object x)
//cerca la chiave tramite search, elimina x e sposta a sinista
//gli elementi successivi costo O(n)
```

Per quanto riguarda il tipo di dati vediamo ad esempio il tipo Map:

```java
//il dato è un insieme S di coppie (elem,key)
//le operazioni sono
insert(elem e, key k);
//aggiunge ad S una nuova coppia (e,k)
delete(key k);
//rimuove da S una key k
search(key k);
//se la key è presente in S restituisce l'elemento e ad essa associato
//null altrimenti
```

il tipo Pila o stack:

```java
//il dato è una sequenza S di n elementi
//le operazioni sono
isEmpty();
//ritorna true se S è vuota, false altrimenti O(1)
push(elem e);
//aggiunge e come ultimo elemento di S costo O(n)
pop();
//toglie da S l'ultimo elemento e lo restituisce O(n)
top();
//restituisce l'ultimo elemento di S senza toglierlo O(1)
```

ed il tipo Coda o queue:

```java
//il dato è una sequenza S di n elementi
//le operazioni sono
isEmpty();
//ritorna true se S è vuota, false altrimenti O(1)
enqueue(elem e);
//aggiunge e come ultimo elemento di S O(1)
dequeue();
//toglie l'ultimo elemento da S e lo restituisce O(1)
first();
//restituisce l'ultimo elemento di S senza toglierlo O(1)
```

Esempi di strutture dati collegate sono le liste concatenate semplici, le liste concatenate doppie e le liste circolari doppiamente collegate, ovvero liste concatenate dove l'ultimo nodo punta al primo come successivo e viceversa.

---

# Alberi

Sono strutture dati collegate che presentano l'organizzazione gerarchica dei dati. I dati sono contenuti nei nodi, e le relazioni gerarchiche sono definite dagli archi che li collegano.

![[Alberi/alberi.jpg]]

Se altezza 0 allora l'albero è vuoto. I figli possono essere illimitati o limitati e sono posizionati in ordine. Se ho una rappresentazione in cui i figli sono illimitati, allora assumo un ordine non assoluto, invece se ho figli limitati posso assumere un ordine assoluto. Esempio:

![[Alberi/nodiill.jpg]]

rappresentazione figli illimitati

![[Alberi/nodilim.jpg]]
rappresentazione figli limitati.

Abbiamo poi le rappresentazioni collegate di alberi, dove la rappresentazione con puntatori ai figli è tipica, quando ho nodi con numero limitato di figli. La rappresentazione con liste di puntatori ai figli quando ho nodi con numero illimitato di figli. Infine la rappresentazione di tipo primo figlio-fratello successivo dove si ha nodi con numero arbitrario di figli.

![[rappr.jpg]]
![[primofiglio.jpg]]
Abbiamo poi il concetto di visita degli alberi, ovvero algoritmi che consentono l'accesso sistematico ai nodi ed agli archi di un albero. Questi algoritmi si distinguono in base al particolare ordine di accesso ai nodi. La visita può essere effettuata in profondità partendo dalla radice e procedendo di figlio in figlio e richiede tempo $O(n)$. Di visita in profondità esisteno 3 tipi:

- <font color=red> Visita in ordine o infissa</font>: figlio più a sinistra, padre e figlio destro, se il figlio destro ha figlio sinistro allora si passa direttamente a quello 
- <font color=red> Visita in ordine anticipato</font>: si parte dalla radice dell'albero, poi si scende fino al figlio sinistro e poi si risale per andare verso destra. Se mentre risalgo trovo figli a destra allora riscendo verso sinistra.
- <font color=red> Visita in ordine posticipato</font>: si passa dal figlio sinistro al destro e poi la radice.

![[Alberi/visite.jpg]]

La visita poi può essere effettuata in ampiezza, partendo dalla radice procedendo visitando i nodi per livelli successivi. Un nodo sul livello i può essere visitato solo se tutti i nodi sul livello i-1 sono stati visitati.
ESEMPIO:
![[alberopervisite.jpg]]
```
Risultato visita ordinata:
[0,1,2,3,4,5,6,7,8,9,11,14,17]
Risultato visita anticipata:
[7,3,1,0,2,5,4,6,9,8,14,11,17]
Risultato visita posticipata:
[0,2,1,4,6,5,3,8,11,17,14,9,7]
Risultato visita per livelli:
[7,3,9,1,5,8,14,0,2,4,6,11,17]
```

---
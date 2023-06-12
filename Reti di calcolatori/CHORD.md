#rdc 
[[Problema della ricerca in sistemi P2P, sistemi P2P strutturati e DHT]]
# Chord
Chord è un sistema P2P strutturato, basato su pochi semplici concetti:
- <font color=green>Facilità di implementazione</font> e comprensione
- <font color=green>Eleganza nel codice</font>
- <font color=green>Possibilità di definire ottimizzazioni</font>

Le caratteristiche principali sono:
- <font color=orange>Spazio logico degli indirizzi piatto</font>: gli indirizzi sono ID di m bit invece che indirizzi IP
- Il <font color=orange>routing è efficiente</font>, con costo $log(N)$ con alta probabilità, cioè se la rete non è inconsistente.
- La dimensione delle tabelle di routing di ogni nodo è pari a $log(N)$ <font color=orange>rispetto al numero di nodi</font>.
- C'è <font color=orange>auto organizzazione</font>

Alcune applicazioni che sfruttano CHORD sono:
- <font color=red>cooperative mirroring</font>: tecnica di replicazione su nodi per facile reperibilità
- <font color=red>indici distribuiti</font>: Gnutella
- <font color=red>applicazioni per la condivisione dei dichi</font>: CHORD contiente l'indice di nodi con più spazio  di memoria.

---
## Funzionalità
CHORD usa interfacce per l'accesso, quali PUT e GET come visto nelle DHT. La funzione hash per generare gli ID è SHA-1 e lo spazio degli indirizzi per chiavi ed identificatori è lo stesso. Dato il numero alto di bit (in genere 160), non c'è problema di collisioni. SHA-1 effettua consistent hashing quindi i nodi sono distribuiti uniformemente sull'anello ed il bilanciamento di carico è garantito. L'algoritmo di mapping è seguente:
Una key di valore K viene assegnata al primo nodo dell'anello il cui identificatore ID risulta $\ge$ K: $\large n(key)=successor(key)$
n è il primo nodo individuato partendo da K e proseguendo sull'anello in senso orario. Esempio:
![[chordring.png]]
Bisogna definire anche dei collegamenti tra i nodi che vanno aldilà del semplice successore. L'overlay è determinato dai link stabiliti tra i nodi. I link sono memorizzati nella tabella di routing di ogni nodo. La topologia più semplice è la lista circolare, dove ogni nodo conosce il suo successore, molto semplice con tabella di routing $O(1)$ per complessità spaziale, però il routing ha complessità $\displaystyle O({n\over 2})$ ed il fallimento di un nodo interrompe i link sull'anello. Se ogni nodo memorizza i link a z vicini si ha routing $O(1)$ ma tabelle di dimensione $O(n)$. Bisogna trovare un compromesso tra i 2 approcci dove: ogni nodo memorizza diversi link verso i vicini e pochi verso nodi lontani. Cosi si hanno tabelle limitate e routing accurato verso nodi vicini ed approssimato verso nodi lontani. 

---

## Finger table e algoritmo di routing
Definiamo la distanza tra 2 identificatori $\large I_1$ e $\large I_2$ dell'anello come il numero di identificatori compresi tra  $\large I_1$ e $\large I_2$ . Ogni nodo di identificatore <font color=purple>x</font> appartenente all'anello, conosce un insieme di al più <font color=yellow>m</font> nodi costituito da nodi caratterizzati da identificatori la cui distanza da x cresce esponenzialmente. In realtà m è il numero di righe della tabella di routing con $log_2(N)$ con N nodi effettivi presenti nella rete, righe univoche. I vicini sono memorizzati nella finger table di un nodo. Esempio: ![[fingertable.png]]

La finger table viene costruita come segue:
- se m è il numero di bit usati per gli ID, la tabella contiene al massimo m link
- sul nodo n, l'entry finger\[i] punta a $\displaystyle successor(n+2^{i-1})$ con $1\le i\le m$

Un nodo mantiene anche una <font color=red>key table</font>, tabella contenente tutte le key di cui il nodo è responsabile in quel momento.

L'algoritmo di routing consiste in:
Ogni nodo propaga una query per la chiave K al finger più distante che precede k, in senso orario. La propagazione continua fino al nodo n tale che: $\displaystyle\large n=predecessore(K)$ e $\displaystyle\large successore(n)=successore(k)$ 
in questo caso il successore di n possiede la chiave.
![[chordrouting.jpg]]

---
## Inserimento nodi
CHORD è in grado di gestire in modo dinamico i cambiamenti della rete quali:
- fallimento di nodi
- fallimenti nella rete
- arrivo di nuovi nodi
- ritiro volontario di nodi

C'è quindi il problema di mantenere consistente lo stato del sistema, più specificamente, aggiornare tempestivamente le finger table ed il successore di ogni nodo. In particolare:
- Per la correttezza del routing, è necessario che ogni nodo mantenga aggiornato il suo successore effettivo sull'anello
- Per l'efficienza del routing, è necessario l'aggiornamento delle finger table

>Correttezza → successorre aggiornato
>Efficienza → finger table aggiornata

Procedura inserimento di nodi in CHORD:
Il nuovo nodo n sceglie un ID, n contatta un nodo esistente sulla rete, un boostrap node. Individua il suo successore sull'anello e vi si aggancia. Costruisce la propria finger table in modo *lazy*, ovvero in intervalli di tempo costanti aggiunge una riga casuale alla finger table. Ogni riga si crea facendo lookup uguale a quello usato per cercare una key. Fino a che la rete non si stabilizza, solo il successore di n è consapevole della presenza di n sulla rete.
I nodi eseguono periodicamente alcune procedure per stabilizzare la rete, ovvero:
- Stabilize per aggiornare il puntatore al successore
- fix fingers per aggiornare la finger table del nodo

Pseudocode stabilize:
```
stabilize(){
	x=successor.predecessor;
	if( x in range(n,successor))
		successor=x;
	successor.notify(n);
}

notify(nodo n'){
	if(prece==null || prece==n' in range (prece,n))
		prece=n'
}
```

I nodi devono ridistribuire le responsabilità delle chiavi. CHORD non si occupa di questo, ma se ne occupa l'applicazione, ciò avviene attraverso la procedura di PUT che avviene periodicamente.

Pseudocode fix fingers:
```
fix_fingers(){
	next=random entry nella finger table
	finger[next]=find successor(n+2^{next-1})
}
```
Si fa in modo randomico perché la rete è imprevedibile e non conosco quale righe saranno influenzate dal cambiamento.
Tutti i link di un nodo sono correttamente aggiornati quando stabilize e fix fingers, sono stati eseguiti. Il sistema "rincorre" la stabilità che è il fulcro del sistema. La correttezza della ricerca dipende dalla corretta impostazione del nodo successore  di ogni nodo appartenente all'anello.

---

## Approcci per CHORD e stabilità
Ci sono 2 approcci per CHORD:
1. Approccio a livelli: dove CHORD è responsabile del routing mentre la gestione dei dati è demandata alle applicazioni
2. Approccio soft: i nodi cancellano le coppie key-value dopo che è trascorso un intervallo di tempo dall'ultimo inserimento. Le applicazioni effettuano il refresh periodico delle coppie. In questo modo si attribuiscono le informazioni ai nuovi nodi arrivati, se un nodo fallisce occorre aspettare il periodo di refresh per avere le informazioni nuovamente disponibili.

Tutte le operazioni relative all'inserimento/caduta di un nodo sono corrette, se avvengono quando l'anello si trova in uno stato stabile. L'anello deve avere il tempo di stabilizzarsi tra 2 operazioni successive, ma questo è impossibile in una rete molto grande. Il sistema tuttavia continua a funzionare anche se non è in uno stato di perfetta stabilità. Possiamo dire che:
> Se i protocolli di stabilizzazione dell'anello vengono eseguiti con una frequenza opportuna, dipendente dalla frequenza degli aggiornamenti, allora l'anello rimane costantemente in uno stato stabile in cui il routing rimane corretto e veloce.

---

## Casi di fallimento di nodi
Primo caso, ogni comunicazione con i fingers è controllata mediante time-out, se il time-out scade la query viene inviata al finger precedente per evitare di oltrepassare il nodo destinazione. Il finger caduto viene rimpiazzato con il suo successore nella finger table. Questa operazione prende il nome di <font color=red>trigger repair</font>. Esempio:
![[triggerrepair.png]]

Secondo caso, ci si trova in una situazione di incosistenza. Un nodo perde il riferimento al suo successore sull'anello. La corretezza dell'algoritmo di routing è garantita se ogni nodo mantiene aggiornato il riferimento al nodo successivo anche in caso di riferimenti multipli. Ma in caso di fallimenti simultanei questo non è garantito. La soluzione è applicare la ridondanza. Per migliorare la robustezza del sistema:
- ogni nodo matiene una lista dei suoi r successori sull'anello con $r=log N$
- se n rileva la caduta del suo successore, il successore viene sostituito con il secondo elemento della lista e cosi via. La lista è mantenuta consistente mediante la procedura di stabilizzazione
- più alto r, più è robusto il sistema

La lista dei successori di n, include i primi r successori sull'anello in senso orario. Il nodo n, richiede la lista dei successori al suo immediato successore s, rimuove l'ultimo elemento ed inserisce j in testa. Se il successore cade viene sostituito con l'elemento successivo della lista.

---

## Affidabilità

La correttezza della finger table viene verificata periodicamente attraverso:
1. Controllo periodico della caduta dei fingers
2. Sostituzione con nodi attivi
3. Trade-off: traffico aggiuntivo per la gestione dei fallimenti vs correttezza e velocità nel reperimento delle informazioni

Tuttavia CHORD non garantisce l'affidabilità dei dati in presenza di fallimenti, ma fornisce meccanismi per garantire affidabilità. Ogni applicazione che utilizza il livello CHORD, può utilizzare la lista dei successori di un nodo per garantire che un dato venga replicato negli r successori di un nodo. Nel momento che un nodo fallisce, il sistema può usare le repliche per individuare i dati in modo corretto. Nel caso in cui ci sia la partenza volontaria di un nodo, per semplicità si può trattere il tutto come una caduta come si è visto ampiamente oppure si possono usare ottimizzazioni quali notifica dell'abbandono ai successori e predecessori e trasferimento delle proprie chiavi al successore.

In sintesi: ![[sintesichord.png]]

---





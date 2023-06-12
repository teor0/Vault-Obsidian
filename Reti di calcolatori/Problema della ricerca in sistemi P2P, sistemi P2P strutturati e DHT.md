#rdc 
[[Cloud Computing]]
# Ricerca in sistemi P2P
Il problema principale in sistemi P2P dovuto alla mancanza di strutturazione della rete è quello della ricerca. I sistemi strutturati sono basati su assunzioni diverse:
- una informazione condivisa può essere memorizzata su qualsiasi nodo della rete
- l'associazione delle informazioni ai nodi avviene secondo un criterio ben preciso che consente poi un routing "intelligente" della query, verso i nodi che possono soddisfarla

Quali sono i meccanismi usati per decidere dove memorizzare l'informazione e come reperirla? Qualsiasi soluzione deve tenere particolarmente in considerazione:
- <font color=purple>Scalabilità del sistema</font>: occorre controllare l'overload di comunicazione e la memoria usata da ogni nodo in funzione del numero di nodi del sistema
- <font color= purple>Robustezza ed adattabilità</font>: in caso di fault e frequenti cambiamenti

Facciamo un confronto tra approccio centralizzato e approccio completamente distribuito. 
L'approccio <font color=red>centralizzato</font> ha le seguenti caratteristiche:
- Ricerca: $O(1)$
- Quantità di memoria richiesta sul server: $O(N)$ al crescere delle informazioni disponibili, cresce la quantità di memoria richiesta.
- Banda richiesta: $O(N)$
- Possibilità di sottomettere query complesse al sistema


L'approccio <font color=red>distribuito</font> ha le seguenti caratteristiche:
- Ricerca: caso peggiore $O(N^2)$ perché necessità di flooding
- Quantità di memoria richiesta: $O(1)$  in quanto non dipende dal numero di nodi del sistema
- Non sono presenti strutture dati per ottimizzare la query o il flooding
  
Esiste una soluzione che realizza un compromesso tra i 2 approcci, questa soluzione è rappresentata dalla DHT (Distributed Hash Table) che offre:
- Scalabilità nella ricerca e nella memoria richiesta: $O(log N)$
- Falsi negativi eliminati
- Auto organizzazione: i nodi in una DHT tramite le regole di essa si auto organizzano

---

# DHT
I nodi sono distribuiti geograficamente dal punto di vista fisico. Dal punto di vista logico, si tenta di collegarli sottoforma di anello per sottomettere tramite questa infrastruttura le query e trovare rapidamente le risorse.
Gli obiettivi di una DHT sono: 
- <font color=blue>Scalabilità</font>: ricerca e memoria richiesta in $O(log N)$
- <font color=blue>Flessibilità</font>: in senso generale, non solo per il file sharing
- <font color=blue>Affidabilità</font>: realizzata tramite varie tecniche e load balancing tramite funzioni hash crittografiche
- <font color=blue>Adattabilità</font>: a fallimenti, inserimento e rimozione di nodi
- <font color=blue>Bilanciamento delle informazioni tra nodi per efficienza della ricerca</font>

Tuttavia le DHT non supportano le query complesse nativamente, ma attraverso estenzioni che abbasano le prestazioni per supportarle.

---
## Funzionamento DHT
Ai peer sono associati degli identificatori univoci, creati tramite indirizzo IP e porta logica passati ad una funzione hash, che li individuano all'interno del anello. Anche i dati sono dotati di ID all'interno del anello che prende il nome di <font color=red>chiave</font>. Gli ID dei nodi e delle chiavi sono mappati nello stesso spazio degli indirizzi. I nodi sono responsabili della gestione di una porzione dello spazio logico degli indirizzi. Trovare il responsabile del dato significa trovare il nodo responsabile del dato e quindi il dato richiesto. Questo tipo di ricerca si chiama, <font color=orange>Key Based Routing</font>. 

>Senza nome esatto non trovo il file!

L'instradamento dal nodo che vuole trovare il dato verso il responsabile avviene con passi successivi fino alla convergenza in $log N$ passi. Il primo step su una DHT è la definizione degli indirizzi dei partecipanti con m bit con logica modulare da 0 a $2^m-1$. Essendo i nodi su un anello, l'ultimo nodo è il precedente del primo. La topologia reale e logica non sono in genere correlate (overlay network), valgono le stesse considerazioni fatte, in precedenza per i sistemi P2P, dove 2 nodi che sono fisicamente vicini non per forza devono essere vicini logicamente.
Il secondo passo è l'associazione nodi-indirizzi logici, che avviene tramite una funzione hash. Ogni nodo è responsabile di una parte dei dati sulla DHT, in genere una parte contigua dello spazio degli indirizzi dei nodi mediante la funzione hash. Ogni nodo memorizza informazioni relative ai dati mappati sulla propria porzione di indirizzi, che sono mappati mediante la funzione hash. Ad esempio:
Il nodo 2000 copre fino a 2599 perché il nodo 2600 è il prossimo.
Talvolta per motivi di affidabilità ed efficienza si usa l'overlapping cioè, più nodi sono responsabili di una parte dell'anello, cosi da evitare single fault point.

---
### Bilanciamento del carico nella DHT
Una rete si dice <font color=green>popolata</font> se il numero di nodi è maggiore di $2^m$, anche se idealmente una rete non sarà mai pienamente popolata al massimo. La DHT ha come problema il bilanciamento del carico, se la funzione di hashing è consistente, la rete sarà sufficientemente bilanciata. Se si nota che delle risorse sono più popolari di altre si può effettuare overlapping, in modo da garantire sia robustezza che bilanciamento, in quanto più nodi sono responsabili di queste risorse. Cause di possibile sbilanciamento di carico sono:
1. Un nodo deve gestire una grossa porzione dello spazio degli indirizzi
2. Gli spazi degli indirizzi sono distribuiti in modo uniforme tra i nodi, ma gli indirizzi gestiti da un nodo corrispondono a molti dati
3. Un nodo deve gestire diverse queries, perché i dati corrispondenti agli indirizzi gestiti sono molto richiesti

---
### Routing nella DHT
Il routing in una DHT avviene come segue:
- Si parte da un nodo della rete e si calcola l'hash del nome del file
- Ci si rivolge ad un nodo arbitrario della rete e chiedo chi è il responsabile
- La risposta rimanda al nodo responsabile fino a che non si trova il vero responsabile
- Il responsabile risponde con l'indirizzi IP e la porta logica.

Ovviamente il criterio del meccanismo del routing è quello di convergere verso nodi via via più vicini sull'anello al ID del file che viene richiesto. Ma come scelgo il percorso da fare? Attraverso le tabelle di routing e l'assegnazione dei vicini come segue:
Ogni nodo conosce $log N$ nodi di cui molti adiacenti e alcuni distanti esponenzialmente. La DHT memorizza coppia chiave-valore, dove il valore è un dato oppure il puntatore al dato cercato. Il dato viene copiato al inserimento diretto nella DHT nel nodo responsabile, quindi si tratta di indirizzamento diretto, se si memorizza il puntatore è indirizzamento indiretto. L'indirizzamento indiretto è preferibile in quanto è più flessibile al cambianto del dato che può variare nel tempo e non lo copia ogni volta. 

---
### Operazioni nella DHT
Il trasferimento dei dati avviene al di fuori della DHT. 
L'inserimento di un nodo richiede il calcolo del suo ID, il ricalcolo delle responsabilità dei nodi adiacenti ed il bilanciamento del carico. Stessa cosa per la rimozione che può essere voluta o non voluta. Queste operazioni sono definite da opportuni algoritmi della rete. 

La soluzione più semplice per evitare che quando un nodo lascia la rete, di avere informazioni scoperte, è quella di dare la responsabilità di informazioni ad un nodo per un time to live, in questo modo l'assegnamento è ricalcolato allo scadere del time to live e se il nodo non lascia la rete resta la responsabilità a lui, altrimenti passa ad un altro nodo. La DHT offre un'interfaccia per l'accesso, in particolare si usa PUT per inserire informazioni a partire da una coppia chiave-valore, si usa la GET per trovare il valore a partire da una chiave. La DHT offre un servizio generico distribuito per la memorizzazione di informazioni, il valore memorizzato in corrispondenza di una chiave può essere qualsiasi cosa.

---

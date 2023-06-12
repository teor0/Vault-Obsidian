#fondamenti 
[[Algoritmi di instradamento e protocolli di instradamento]]
## Distance Vector
Nel distance vector, i nodi su base periodica calcolano i costi verso i nodi vicini e possono calcolare il percorso parziale tra loro ed i loro vicini. Questi costi poi passano ai nodi vicini, in questo modo i nodi a mano a mano conoscono sempre di più la topologia di rete. Nel distance vector si usa l'algoritmo di Bellman-Ford in versione asincrona, dove c'è la possibilità di avere bad news propagation, cioè variazioni particolari per cui la convergenza (conoscenza totale della rete) è molto lenta.

Un router oltre alla tabella di routing, mantiene una struttura dati detta appunto distance vector contenente informazioni ricavate dalle tabelle di routing quali, indirizzo da raggiungere e la distanza (metrica) verso esso. Ad ogni modifica della tabella i router devono inviare il nuovo distance vector risultante ai nodi vicini, che avverrà allo scadere di un timer periodico.

---

# Passi distance vector
Quando arriva un messaggio da un router vicino si confronta la coppia indirizzo, distanza e:
- se la destinazione non è in tabella si crea una nuova entry
- se la destinazione è in tabella ed il next hop è il router adiacente si aggiorna il costo
- se la destinazione è in tabella ed il costo indica un percorso migliore, si aggiorna costo e next hop

Queste informazioni sono trasmesse ad intervalli regolari solo ai router adiacenti che pian piano, si arricchiscono di informazioni. Se ho una lunghezza massima di k hop la rete convergerà tra k volte il tempo di time out. Ogni nodo al suo interno ha in realtà 3 vettori:
- $W_x$ vettore costi uscenti dal nodo
- $L_x$ vettore distanze minime verso altre reti
- $R_x$ vettore next hop verso altre reti

Si ha poi M, numero di reti a cui il nodo x è direttamente connesso e N, numero di reti nella configurazione. Esempio funzionamento: ogni 30s ogni nodo scambia $L_x$ tra i nodi vicini, sulla base dei distance vector ricevuti il nodo x aggiorna i suoi vettori $L_x$ e $R_x$.

---

# Passi link state
Il link state assume che ogni router dispone della tipologia completa. La topologia completa si costruisce attraverso pacchetti speciali, i link state packet. Una volta raccolti tutti, si costruisce la topologia si applica l'algoritmo di Dijkstra e poi si estraggono le tabelle di instradamento. 
Al boot avviene nel router il <font color=red> neighbour greetings</font>, cioè si crea una topologia parziale dei nodi adiacenti, che forma il link state packet che verrà inoltrato a tutti i nodi della rete in broadcast.
Il link state packet contiene:
- identificativo emittente del packet
- stato di ogni link connesso al router
- costo del link
- identità di ogni vicino connesso all'altro estremo del link
- numero di sequenza del packet

Ogni router crea un database di link state packet aggiornando al numero di sequenza più alto ovvero il più recente. Una volta finita la creazione del database, si crea la topologia e poi si applica Dijkstra per estrapolare la tabella di instradamento. Il packet può essere mandato su base periodica o se varia la topologia.
L'informazione mandata è maggiore rispetto al distance vector.

---
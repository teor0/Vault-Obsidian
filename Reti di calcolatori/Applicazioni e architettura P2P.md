#rdc 
[[Aspetti del protocollo DNS]]

# Architettura P2P pura e velocità di download
L'architettura pura è quella in cui:
- non c'è un server sempre attivo
- coppie di pari comunicano direttamente fra loro
- i peer non devono essere necessariamente sempre attivi e cambiano indirizzo IP

Una domanda nasce data l'architettura della rete. Quanto tempo ci vuole per distribuire file da un server a N peer?

Sia $\large u_s$ la frequenza di upload del collegamento di accesso del server.
Sia $\large u_i$ la frequenza di upload del collegamento d'accesso del peer i-esimo.
Sia $\large d_i$ la frequenza di download del collegamento d'accesso del peer i-esimo.
Nell'architettura client-server, il server invia in sequenza N copie del file in $\displaystyle\large t={NF\over u_s}$
Un client i impiega $\displaystyle\large t={F\over d_i}$ per scaricare il file. Per distribuire F passa un tempo pari a $\displaystyle\large d_{cs}=max\{{NF\over u_s}, {F\over min_i(d_i)}\}$.

Questa funzione cresce linearmente con il valore di N.
Per l'architettura P2P, il server invia una copia in $t=\displaystyle\large{F\over u_s}$ ed un client i scarica in $t=\displaystyle\large{F\over d_i}$. Devono essere scaricati in totale NF bit. Il più veloce tasso di upload è pari a $\displaystyle\large u_s+\sum u_i$ in quanto tutti i peer partecipano all'upload. Il tempo di distribuzione del file tra tutti i peer è pari a
$\displaystyle\large d_{P2P}=max\{{F\over u_s},{F\over min_i(d_i)}, {NF\over u_s+\sum u_i}\}$

L'architettura P2P è più efficiente ma va comunque implementata bene.

---

## BitTorrent
Un sistema di distribuizione P2P di file ben affermanto è BitTorrent, dove un tracker tiene traccia dei peer che partecipano alla condivisione. Il <font color=blue>torrent</font> è un flusso di dati che un gruppo di peer usano per scambiarsi parti di file. Il file viene diviso in parti dette chunk in media di 256kb in modo da sfruttare il parallelismo al meglio per scaricare. Quando un peer entra a far parte del torrent:
- non possiede nessun chunk del file ma li accumula con il passare del tempo
- si registra presso il tracker per avere la lista dei peer

I peer possono uscire ed entrare a piacimento dai torrent separandosi cosi in <font color=green>seeders</font> (chi attivamente carica il file anche se lo ha scaricato) e <font color=red>leechers</font> (chi ha scaricato il file e non è attivo al momento oppure esce dal torrent). Mentre effettua il download il peer carica parti ad altri peer. 
In un dato istante peer diversi hanno parti diverse del file. L'indicizzazione è necessaria per conosce la posizione del file che i peer condividono. I peer comunicano all'indice ciò che possiedono, cosicché i peer che consultano l'indice possono trovare i file. 
I peer periodicamente chiedono ai loro vicini la lista dei chunk che possiedono e ne chiedono il più raro in modo che, da questo comportamento egoistico si abbia una distribuzione uniforme dei chunk.

Un peer poi invia i chunk ai vicini (in genere 4) che attualmente stanno inviando i loro chunk con frequenza più alta e pure ad un peer random, gli altri non ricevono nulla.
Sistemi alla BitTorrent necessitano di un'indice che tiene traccia dei peer che condividono un file.

---

## Napster
Napster era una directory centralizzata P2P. Quando il peer si collega, informa il server centrale del suo indirizzo IP ed i file che possiede. Un peer cerca un file ed il server risponde con l'indice dei peer che contengono tali ad un altro peer.
Tuttavia, avere una directory è un problema in quanto se si guasta la directory centrale non funziona nulla e risulta come collo di bottiglia per le prestazioni.

La soluzione al problema di Napster, con server centralizzato è il <font color=red>query flooding</font>: ogni nodo ha un elenco che rende disponibile per la condivisione oppure nessuno. Un dato peer è connesso con meno di 10 vicini nella rete di copertura. Un arco tra il peer x e y è una connessione TCP, quindi un arco è un collegamento virtuale. Tutti i peer attivi e connessi con gli archi, formano la rete di copertura, il tutto è quindi distribuito. Si chiama query flooding in quanto si ha un'inondazione di query tra i nodi vicini. Esempio:
![[queryflooding.png]]
La rete è rappresentata da un grafo che viene chiamato overlay network (rete di ricoprimento). I nodi vicini è bene averli misti, ovvero sia avere nodi vicini geograficamente vicini, che nodi vicini geograficamente lontani. 
Le risposte arrivano aggregate dal percorso che la query di richiesta ha fatto. Il file è poi scaricato dal nodo che offre velocità migliore tramite HTTP, il download però è diretto dal nodo, non passa attraverso i nodi come la risposta.

Come trovare i peer su Gnutella?
Bisogna prima almeno trovare un peer membro della rete, ciò avviene attraverso i contact server che "indicizza" i membri della rete. Una volta conosciuto un peer, si usano i messaggi ping e pong. Ping si usa come richiesta e pong come risposta contenente i vicini e l'indice dei file a disposizione. L'enorme numero di messaggi però è una criticità, siccome si usa il query flooding, in più il grafo di copertura di Gnutella è ciclico e quindi lo stesso messaggio può arrivare più volte. Ciò si può risolvere con un ID nel messaggio per inoltrarlo o meno, oppure un time to live in funzione dei vicini, il valore del time to live è calcolato in base al numero di vicini di un nodo ed in funzione della dimensione della rete. Data la natura di una rete decentralizzata che di per se è inefficiente, un'altra soluzione è  quella di avere una gerarchia attraverso super peer responsabili di 30 o più peer, inoltre i super peer sono connessi in P2P essendo i più stabili e duraturi. 

---

## Skype
Skype utilizza un protocollo proprietario, è intrinsecamente P2P, in quanto coppie di utenti comunicano tra loro e sfrutta la copertura gerarchica con i supernodi. Skype usa un login server per autenticare un utente e conoscere il suo indirizzo IP e la porta per la comunicazione, si pone un problema però, se entrambi gli utenti hanno NAT, la comunicazione non può avvenire. Per sopperire ciò si fa uso dei relay, intermediari tra gli utenti che non possono ascoltare la comunicazione ma la rendono possibile. 

---
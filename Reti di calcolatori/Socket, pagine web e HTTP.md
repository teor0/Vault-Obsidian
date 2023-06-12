#rdc
[[Concetti introduttivi e richiami]]
# Socket
Le applicazioni di rete si basano sul fondamento dell'indirizzamento, ovvero affinché un processo su un host invii un messaggio a un processo su un altro host, il mittente deve identificare il processo destinatario. Per identificare un host si usa la coppia: indirizzo IP-porta logica. L'indirizzo IP identifica univocamente un host e la porta identifica un processo in esecuzione sul host. 
Ad esempio la porta 80 identifica l'HTTP, quindi se voglio inviare un messaggio HTTP ad un host mi occorre sapere il suo indirizzo IP ed usare la porta 80.

Un processo per inviare/ricevere dati deve utilizzare un socket. Il socket altro non è che una porta d'accesso/invio. Della consegna se ne occupa l'infrastruttura esterna che compone la rete. Quindi possiamo definire il socket come segue:
>[!Socket]
>Un'interfaccia di un host creata dalle applicazioni, gestita dal S.O. in cui il processo di un'applicazione può inviare o ricevere messaggi da un processo di un'altra applicazione.

Esistono socket di tipo TCP, UDP e Multicast dove per socket TCP la connessione è punto-punto mentre per UDP e Multicast la connessione è punto-multipunto.

## Logica di programmazione dei socket
I prerequisiti affinché il cliente possa contattare il server sono: che il processo server deve essere in esecuzione e che il server deve avere un ServerSocket per accettare le richieste di connessione. A questo punto il client per contattare il server crea un socket TCP, specificando indirizzo IP e porta del server socket, quindi stabilisce una connessione con il server TCP. Ora un server socket può gestire solo un socket alla volta, e per gestire più richieste il server socket crea istantaneamente un socket su una porta diversa, che verrà usata per la durata necessaria per comunicare con il client. Questo porta all'utilizzo dei Thread.

Nei socket UDP non c'è handshaking, ovvero non c'è un client specifico da cui ricevere dati, ma è destinato a ricevere dati da chiunque. Questo evita la creazione della creazione di socket ad hoc. Il mittente deve allegare esplicitamente l'indirizzo IP e la porta del destinatario al pacchetto. Il server deve estrarre l'indirizzo IP e la porta del mittente per l'eventuale risposta. Anche se i dati trasmessi possono andare persi o non arrivare con l'ordine originario si ha un vantaggio sostanziale in termine di prestazioni.

---

# Pagina web e HTTP
Una pagina web è costituita da oggetti. Un oggetto può essere un file HTML, un'immagine JPG e un file audio. Una pagina web è formata da un file base HTML che include diversi oggetti referenziati. Ogni oggetto è referenziato da un URL (Uniform Resource Locator) formato da hostname o indirizzo IP.

Il protocollo HTTP è un protocollo a livello applicazione basato sul modello client server, dove il client è il browser che richede, riceve e visualizza gli oggetti dal web, mentre il server è un computer che invia oggetti in risposta ad una richiesta. HTTP usa il protocollo TCP per il livello di trasporto. HTTP si dice senza stato (<font color=red>stateless</font>), in quanto il server non mantiene informazioni sulle richieste fatte dal client. Quindi ogni richiesta è indipendente dall'altra. Un protocollo con stato (<font color=red>statefull</font>) serve per mantenere informazioni. Ovviamente a seconda del caso si usa un protocollo stateless o stateful. 
HTTP può adoperare un modello di <font color=red> connessione persistente</font> o <font color=red> non persistente</font>. Per connessione non persistente si intende quando dopo aver inviato un oggetto al client la connessione viene chiusa. Nella connessione persistente, la connessione rimane aperta e più oggetti di un medesimo insieme possono essere trasmessi.
Esempio connessione non persistente, per una pagina HTML contenente 10 riferimenti a file jpg:
1.  Il client HTTP inizializza una connessione con il server HTTP identificato da hostname e porta 80.
2. Il server HTTP in attesa di una connessione TCP accetta la connessione del client
3. Il client HTTP trasmette un messaggio di richiesta nel socket della connessione TCP, indicando l'oggetto richiesto.
4. Il server HTTP riceve il messaggio di richiesta e forma il messaggio di risposta contenente l'oggetto richiesto e lo invia sul socket.
5. Il server HTTP chiude la connessione TCP
6. Il client HTTP riceve il messaggio di risposta che contiene il file HTML, visualizza il documento e trova i riferimenti ai 10 file jpg.

A questo punto il client HTTP dovrà ripetere tutti e 6 i passaggi per ciascuno dei 10 file jpg.

Per calcolare il tempo di risposta sfruttiamo l'RTT, (Round Trip Time). Il tempo di risposta ad una richiesta HTTP è data da:
- 1RTT per inizializzare la connessione TCP
- 1RTT affinché ritorni la risposta HTTP
- Tempo di trasmissione del file

Quindi per ogni singolo oggetto si impiega: 2RTT+ tempo di trasmissione.
Per risolvere questo problema i browser aprono socket in parallelo per scaricare gli oggetti di risposta HTTP. La vera alternativa e soluzione sarebbe usare connessioni persistenti, tuttavia non è detto che sia migliore, in quanto nelle connessioni persistenti il parallelismo di avere più socket aperti è difficoltoso da gestire rispetto ad avere più socket aperti per connessioni non persistenti. La soluzione impiegata è quella di usare un mix fra le 2 opzioni.

---

## Messaggi HTTP e comandi
I messaggi HTTP si dividono in messaggi di richiesta e di risposta. I messaggi di richiesta fino a HTTP 1.1 erano in formato ASCII leggibile dall'utente. I messaggi sono composti come seguono:
```
GET /somedir/page.html HTTP/1.1
Host: www.myschool.edu
User-Agent: Mozilla/4.0
Connection:close (connessione non persistente)
Accept-language:it


```
La prima riga contiene un comando tra GET, POST e HEAD, successive sono le righe di intestazione, caratterizzate da coppie chiave-valore. In particolare GET non contiene un corpo in quanto si fa una richiesta, mentre ad esempio per POST nel corpo del messaggio di solito si trovano dati che andranno a riempire i form del sito web.
Per mandare un input si può usare anche il cosidetto metodo URL, dove attraverso il comando GET, si manda l'input appendendoli al URL che normalmente la GET manda al server. Esempio:
`https://getcomics.info/?s=batman`
Il metodo URL si usa per mandare piccoli dati in formato testuale sapendo che la lunghezza del URL è fissa. Ovviamente se devo mandare una foto utilizzo il comando POST.
La prima versione di HTTP, HTTP/1.0 forniva solo i metodi GET, POST e HEAD (usata per ottenere l'header di oggetto al fine di consultare facilmente i metadati). A partire da HTTP/1.1 vanno ad aggiungersi PUT (include il file nel corpo dell'entità e lo invia al percoso specificato nel campo URL) e DELETE (cancella il file specificato del campo URL).

I messaggi di risposta seguono una logica simile a quella dei messaggi di richiesta. Un messaggio di risposta è generalmente composto come segue:
```
HTTP/1.1 200 OK
Connection: close
Date: Mon, 06 Aug 2007 07:12:49 GMT
Server: Apache/1.3.0 (Unix) 
Content-Language: it
Content-Lenght: 7241
Content-Type: text/html; charset=utf-8
dati del file html
```
La prima riga è la riga di stato contenente il codice di stato e di seguito ci sono righe di intestazione e dopo eventuali dati richiesti.

---
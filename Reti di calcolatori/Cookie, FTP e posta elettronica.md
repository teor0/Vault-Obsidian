#rdc 
[[Socket, pagine web e HTTP]]
# A cosa servono i cookie?
Essendo HTTP stateless, non si possono memorizzare dati utili del client. I cookie sono lo strumento che viene in aiuto e si basano su 4 componenti:
1. Una riga di intestazione nel messaggio HTTP response
2. Una riga di intestazione nel messaggio HTTP request
3. Un file cookie mantenuto sul computer del client e gestito dal browser dell'utente
4. Un database sul sito che fa uso dei cookie

I cookie possono contenere
- informazioni di autorizzazione
- carta d'acquisto
- raccomandazioni
- stato della sessione dell'utente (e-mail e password)

---

## Cache web
Una cache web è uno spazio di memorizzazione, ovvero un file system in cui memorizziamo delle pagine e degli oggetti html più vicini al client, per evitare di reperirli dal server di origine. Ad esempio se io frequento per la prima volta `www.repubblica.it` andrò a richiedere la pagina al server d'origine. Se frequento spesso il sito dell'università e lui si trova nel server proxy dell'università allora la richiesta non arriverà al server d'origine. Quindi una richiesta passa prima dal server proxy che, nel caso in cui non riesce a soddisfarla andrà a richiedere l'oggetto al server d'origine.

La cache web opera sia come client che server ed è tipicamente installata da un ISP. Quali sono le motivazioni che spingono ad usare una cache web?
- Riduce i tempi di risposta alle richieste dei client
- Riduce il traffico sul collegamento di accesso a internet
- Aiuta i provider "scadenti" a fornire dati con efficacia.

Se l'oggetto sul server d'origine cambia, il proxy potrebbe contenere una versione vecchia dell'oggetto, inoltre la dimensione del server proxy è limitata.
La soluzione per evitare di avere oggetti di versioni "vecchie" è quella di confrontare la data di ultima modifica di un oggetto del server proxy con quella sul server d'origine. Questa soluzione è implementata dalla GET condizionale attraverso il campo di intestazione `If-modified-since: <data>` che verrà mandato tramite una richiesta al server d'origine. Il vantaggio di tale soluzione è che nel caso in cui l'oggetto non è stato modificato, la risposta del server d'origine al server proxy è di gran lunga più veloce del caso in cui l'oggetto ha subito una modifica. Questo perchè appunto il tempo totale della trasmissione è influenzato dalla durata del tempo necessario per trasferire l'oggetto.

---

## Protocollo FTP
Il protocollo FTP è basato su TCP ed è di tipo client-server. Il protocollo FTP (file transfer protocol) serve appunto per trasferire file da un server ad un client o viceversa tramite la porta 21 e 20. FTP sfrutta TCP perchè trasferendo un file serve l'affidabilità nel trasferimento. Per il trasferimento di file si usa l'approccio di controllo fuori banda, cioè sostanzialmente che l'invio e ricezione dei comandi ed il trasferimento del file non avvengono nello stesso socket per evitare che si interferiscano tra loro, in particolare la porta 21 è utilizzata per i comandi e la porta 20 è utilizzata per trasferire i file. 
Un server FTP è un server <font color="red"> stateful</font> che viene acceduto tramite username e password dal file anche se tuttavia i messaggi di richiesta e risposta sono in formato testuale ASCII, ovviamente con le nuovi versioni il formato è cambiato per sicurezza. Alcuni comando sono:
- USER username: inserisci username
- PASS password: inserisci la password
- LIST: elenca i file della directory corrente
- RETR filename: recupera un file dalla directory corrente
- STOR filename: memorizza un file sul server

Codici di ritorno comuni sono:
- 331: username ok, password requested
- 125: data connection already open; transfer starting
- 425 can't open data connection
- 452 error writing file.

---

# Posta elettronica
Nella posta elettronica ci sono 3 componenti principali:
1. Agente utente: software usato dall'utente per scrivere il messaggio ed inviarlo al server ad esempio outlook o gmail.
2. Server di posta: dove finiscono i messaggi scritti tramite l'agente utente, che ha il compito di inoltrarli verso il server di posta del destinatario
3. SMTP (simple mail transfer protocol): il protocollo utilizzato per il trasferimento dei messaggi

Il protocollo SMTP usa TCP per trasferire in modo affidabile i messaggi di posta elettronica tra client e server attraverso la porta 25. Questo trasferimento sulla porta 25 avviene senza crittografia ma ci sono altre porte dedicate ad un trasferimento sicuro tramite SMTP. Il trasferimento è diretto, per quanto riguarda il livello applicazione, quindi dal server di posta del mittente si passa al server di posta del destinatario. 
Il protocollo si basa su 3 fasi a livello applicazione:
- Handshaking
- Trasferimento di messaggi
- Chiusura

L'interazione si basa su comandi e risposte in formato ASCII e, in particolare le risposte sono codici di stato ed espressione. Il protocollo stabilisce che i messaggi siano nel formato ASCII a 7 bit quindi fino a 128 caratteri che può essere un problema. A differenza del HTTP dove il client effettua pull dal server, ovvero richiede informazioni, in SMTP il client fa push al server, invia informazioni. Lo standard per il formato dei messaggi è composto da intestazione, (contenente righe di intestazione come il mittente, il destinatario e l'oggetto della mail) una riga vuota e dal corpo del messaggio contenente solo caratteri ASCII.
Per trasmettere contenuti non ASCII nativi, si usa il formato MIME. MIME è un formato multimediale dei messaggi di posta che richiede alcune righe di intestazione aggiuntive nell'intestazione del messaggio, per indicare il tipo di contenuto ed il formato di codifica usato. 
Esempio:
```
From: alice@cattolica.edu
To: bob@bicocca.edu
Subject: Fototessera per tesserino
MIME-Version: 1.0
Content-Transfer-Encoding: base64
Content-Type: image/jpeg
...
```

---

## Protocolli d'accesso alla posta 
I protocolli d'accesso alla posta per ottenere i messaggi dal server sono 3:
1. HTTP: È il protocollo usato da servizi web mail come gmail o outlook.
2. POP (Post Office Protocol): attualmente alla versione POP3, è un protocollo che permette di scaricare i messaggi dal server
3. IMAP (Internet Mail Access Protocol): è un protocollo che fornisce funzioni più complesse rispetto a POP.

POP3 è un protocollo testuale che si divide in 2 fasi, fase di autorizzazione e fase di transazione. Nella fase di autorizzazione il client comunica i propri dati d'accesso al server tramite dei comandi e riceve risposte dal server ed infine l'accesso al server. Nella fase di transazione il client può usare diversi comandi per: elencare i messaggi ricevuti, scaricare i messaggi, eliminare i messaggi e chiudere la sessione. Esempi di transazioni:
```
C:list
S: 1 498
S: 2 912
.
C: retr 1
S: <message 1 content>
.
```
POP3 è efficiente con solo un client in quanto non permette la sincronizzazione diversi client per un utente. Questo è dovuto ovviamente perché POP3 è un protocollo stateless.

IMAP consente all'utente di organizzare i messaggi in cartelle e mantiene tutti i messaggi sul server. IMAP conserva lo stato dell'utente tra le varie sessioni ed introduce la comunicazione bidirezionale tra client e server, quindi il client può sia scaricare che caricare messaggi. L'agente utente del client contrassegna i messaggi letti sul server affinché possa avvenire la sincronizzazione.

---
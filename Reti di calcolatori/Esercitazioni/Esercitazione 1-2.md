# Richiami
Facciamo un richiamo a delle definizioni date nel corso di fondamenti di reti di telecomunicazione:
Un nodo <font color=red> host</font> indica ogni terminale collegato attraverso un link di comunicazione ad una rete informatica.
Un indirizzo IP è un modo per identificare un host collegato ad una rete informatica che usa il protocollo IP.
<font color=red> L'hostname</font> è il nome identificativo di un dispositivo collegato all'interno di una rete di calcolatori e può far parte di un URL. L'hostname permette di associare una denominazione ad un indirizzo IP ad esempio: google.com associato all'IP 188.114.96.2

Con <font color=red> API (Application Programming Interface) </font>si indica un insieme di procedure disponibili al programmatore.
Un <font color=red> server </font>è computer di elevate prestazioni che in una rete fornisce un servizio ad altri computer collegati detti <font color=red> client</font>.
Un <font color=red> protocollo</font> descrive formalmente il formate dei messaggi e le regole che 2 computer devono adottare per lo scambio di messaggi.

Il package java.net può essere diviso in due sezioni:
1. Low level API che comprende: gli address per identificare una rete, socket per gestire la comunicazione tra 2 computer e interface per le interfacce di rete.
2. High level API che comprende: URL che punta e rappresenta una particolare risorsa sul web e connection che rappresenta una connessione ad un URL.

---
## Classe java.net.InetAddress
La classe sarà utilizzata all'interno del codice e mette a disposizione diversi metodi quali:
![[metodiInetAddress.png]]

---
## Risoluzione Hostname - IP e stream di dati
Ogni computer mantiene informazioni locali per risolvere hostname in indirizzi IP. Nei sistemi Unix il file `/etc/hosts` mantiene tali informazioni mente in Windows sono contenuti in `C:\WINDOWS\system32\drivers\etc\hosts`.
Il DNS è il sistema utilizzato per la risoluzione di hostname in indirizzi IP e viceversa. Il servizio è realizzato tramite un database distribuito costituito dai server DNS.

Gli stream in Java si dividono in:
- <font color=red> byte stream</font>, per stream di caratteri  rappresentati con una codifica di 1 byte
- <font color=red> character stream</font>, per stream di caratteri rappresentati con una codifica a 16 bit UNICODE.

Per stream di input si usa:
- La classe astratta<font color=green> InputStream</font> per i byte stream, che legge un byte alla volta
- La classe astratta<font color=green> Reader</font> per i character stream, che legge un carattere alla volta

Utili sono le classi concrete <font color=green> InputStreamReader</font> che converte uno stream di byte in input in uno stream di caratteri e la classe <font color=green> BufferedReader</font> che legge un carattere alla volta fino al carattere di fine linea.

Per stream di output si usa:
- La classe astratta<font color=green> OutputStream</font> per i byte stream, che scrive un byte alla volta  
- La classe astratta<font color=green> Writer</font> per i character stream, che scrive un carattere alla volta

Utili sono le classi concrete <font color=green> OutputStreamWriter</font> che converte uno stream di caratteri in output in uno stream di byte e la classe <font color=green> PrintWriter</font> che tramite println scrive stringhe terminate da un carattere di fine linea in uno stream di output.

Il metodo `readLine()` della classe BufferedReader è bloccante, quindi fin quando non si legge una linea il client rimane in attesa. L'uso di `println()` della classe PrintWriter è consigliato per non bloccare.

Il metodo `flush()` svuota il flusso di output e forza la scrittura di tutti i byte di output bufferizzati. Il metodo dovrebbe essere chiamato se alcuni byte precedentemente scritti sono stati bufferizzati dall'implementazione del flusso di output. Printwriter mette a disposizione il costruttore `PrintWriter(OutputStream o, boolean autoFlush)` dove se settato true l'autoflush, il metodo flush si attiva automaticamente ogni qual volta si usano i metodi println, printf o format.

---

## Socket
Il socket è un canale di comunicazione che permette a 2 processi che lavora su 2 computer diversi di comunicare fra di loro. Il socket altro non è che un oggetto che viene istanziato e viene utilizzato per trasmetter o ricevere dati. Per far funzionare un socket è importante utilizzare bene le porte TCP. Sono le porte che consentono il multiplexing delle connessioni, ovvero di avere più connessioni a più computer contemporaneamente.
Java permette di creare un socket attraverso l'omonima classe sempre nel package java.net

![[metodiSocket.png]]
![[metodiSocket2.png]]

L'operazione di readline è bloccante quindi il client non fa altro che aspettare finchè non arriva una linea di caratteri. Per evitare un attesa infinita viene implementato un timeout tramite il metodo `setSoTimeout(int timeout)`.
![[metodisocketserver.png]]

---
## HTTP
Il protocollo HTTP è usato per la trasmissione d'informazioni sul web. Un server HTTP generalmente utilizza la porta 80 e sfrutta il protocollo TCP a livello trasporto. L'HTTP funziona su meccanismo richiesta/risposta, dove il client effettua una richesta ed il server restituisce una risposta. 
Ci sono quindi 2 tipi di messaggi HTTP:
1. <font color=red> Messaggio di richiesta</font>, composto in 3 parti, con una request line fatta da metodo, URI e versione del protocollo, la sezione header e il body del messaggio. La richiesta termina con una riga vuota quindi con 2 ritorni a capo. Esempio request line: `GET /wiki.com/Pagina_principale HTTP/1.1`
2. <font color=red>Messaggio di risposta </font>, di tipo testuale anch'esso composto in 3 parti, status line, sezione header e body. Esempio: 
``` 
HTTP/1.0 200 OK
Date: Mon, 28 Jun 2004 10:47:31 GMT
Server: Apache/1.3.29 (Unix) PHP/4.3.4
Content-Language: it
Content-Type: text/html; charset=utf-8
```

Ci sono poi i codici di stato HTTP famoso il codice 404. I codici si dividono nelle seguenti categorie:
- 2xx Success ad esempio 200 è la risposta standard per richieste andate a buon fine
- 3xx Redirezione ad esempio 301 per una redirezione ad un altro URI
- 4xx Client error ad esempio 404 riporta una risorsa non trovata
- 5xx Server error ad esempio 503 riporta che il server non è attualmente disponibile

---

## Serializzazione
La serializzazione consiste nel trasformare un oggetto in una sequenza di Byte, tale sequenza può essere scritta su un file o trasmetterlo tramite una connessione. La trasfromazione può avvernire anche in codifiche quali XML e JSON. Lo scopo della serializzazione  è di trasmettere l'intero stato dell'oggetto in modo che esso possa essere succesivamente ricreato nello stesso identico stato dal processo inverso di deserializzazione.

Un oggetto in Java è serializzabile se la classe a cui appartiene implementa l'interfaccia Serializable. 

---
#fondamenti 
[[Protocollo TCP]]
# Definizione
Gran parte della perdita dei segmenti è da attribuire all'overflow del buffer, per quanto riguarda TCP. I protocolli applicativi come TELNET e HTTP poggiano su TCP, mentre NFS, RIP e DNS poggiano su UDP.
I protocolli applicativi operano a paradigma client-server, dove server è qualunque processo che offre un servizio che può essere raggiunto attraverso internet, mentre cliente è il processo applicativo che richiede il servizio al server ed aspetta il risultato. La maggior parte degli applicativi su internet è client-server. Molti servizi applicativi richiedono un'autorizzazione all'uso trmite account fornito al client dall'amministratore del sistema (server) ed una password.

---
## TELNET
TELNET permette di usare le funzioni di un calcolatore remote come se il terminale che si usa fosse uno dei terminali locali del sistema remoto. L'host di desitnazione deve contenere la componente server di TELNET. Il processo può essere iterativo, cioè ci si può collegare ad un host remoto e da quello ad un altro e cosi via. TELNET consente di aprire sessioni interattive su host ovunque ubicati all'interno della inter-rete, purché il client disponga di un'autorizzazione all'uso. 

---
## ICMP
L'ICMP è un protocollo non orientato alla connessione in quanto poggia su IP. ICMP è usato per:
- segnalare ai sistemi coinvolti situazioni anomale
- controllare il trasferimento delle informazioni
- effettuare misure di prestazioni

Le possibili anomalie riscontrabili sono:
- il router non riesce ad instradare un pacchetto IP
- l'host di destinazione è disconesso dalla rete
- dispositivo non funziona correttamente
- congestione elevata

ICMP consente di notificare gli errori alla sorgente ma non specifica cosa fare ricevuta la notifica. Serve quindi un programma applicativo per gestire cosa fare ricevuta la notifica. La notifica degli errori arriva solo al router o all'host che ha originato i datagrammi, i nodi intermedi non possono ricevere nulla, quindi se il problema è originato da un nodo intermedio l'ICMP non lo identifica.

ICMP è incluso in ogni implementazione di IP. Il messaggio è incapsulato nel payload del datagramma IP ed ha il seguente formato: ![[icmpdata.png]] Sulla base del tipo, capisco cosa mando ed il codice esprime successo o insuccesso. 
>Non vengono generati messaggi ICMP in seguito ad errori causati da datagrammi che trasportano messaggi ICMP.

I messaggi ICMP vengono manipolati dal software IP non dagli applicativi utente. I messaggi sono scambiati tra entità IP remote e da questo punto di vista ICMP dovrebbe essere collogato al di sotto dello strato IP, ma in realtà è al di sopra di IP. Alcuni messaggi sono:
![[icmpmess.png]]
Un host che vuole sapere se un altro host è raggiungibile e attivo manda un echo request, l'host ricevuto echo request risponde con un echo reply rinviando i dati ricevuti. Echo request e echo reply possono fornire anche statistiche. Destination unreachable è mandato da un router ad un host che non è in grado di instradare un datagramma. Source Quench è mandato dal host destinazione per informare la source che la coda sua è piena. Tramite redirect, il router informa la source che l'instradamento scelto era errato o non il migliore e ne notifica uno nuovo. Address Mask Request/Reply sono usati dagli host per richiedere la maschera di sottorete ai router.

---
## Ping
Ping manda messaggi di echo request ICMP, ma non è uno strumento assoluto per verificare la raggiungibilità di un host, in quanto la echo reply potrebbe percorrere un percorso diverso dalla request. Per stabilire se un host è raggiungibile è consigliato usare ping da punti differenti.

---
## Trace route
Trace route, incrementa il time to live ad ogni successivo echo request quindi sfrutta i messaggi ICMP in sequenza.

---
## SMTP
Il protocollo SMTP, è usato per la posta elettronica. SMTP poggia su TCP, l'obiettivo è di fornire i meccanismi per trasferire messaggi in forma elettronica in modo affidabile ed efficiente attraverso internet. SMTP usa TCP a livello di trasporto ed una modalità di trasferimento con connessione ed affidabilità. SMTP usa la porta 25 ed aspetta che il server notifica l'avvenuta comunicazione. Il server avvia la comunicazione inviando al client una linea di testo contenente la propria identità ed informandolo della propria disponibilità a ricevere mail. Quando è pronto, il client annuncia il mittente ed il destinatario della mail. Se un host non è collegato ad internet esso utilizza un mail server per inviare e ricevere posta elettronica.

---
## POP3 e IMAP
Il protocollo POP3 consente di prelevare i messaggi di posta e memorizzarli sul PC locale, IMAP consente all'utente di leggere i messaggi direttamente dal server.

---
## FTP
FTP usa TCP per trasferire i file e consente di visualizzare, modificare e cancellare dalla directory remota i file e consente funzionalità di protezione e compressione dei file, inoltre garantisce l'accesso alla directory tramite autenticazione. FTP gestisce 2 tipi di connessioni:
1. Dedicata al controllo, è instaurata sulla porta 21 e qui client e server comunicano i comandi
2. Dedicata al trasferimento, usa la porta 20 del server

---
## TACK, X-Window, NFS e WWW
TACK consente il dialogo tra 2 utenti in tempo reale, X-Window è simile a TELNET ma il terminale emulato è fornito di GUI, NFS consente di avere un file system remoto e WWW consente ad un utente di acquisire un documento situato in un sistema remoto, usando la componente WWW del client.

--- 
## HTTP
Il webclient (browser) comunica con un web server tramite una o più connessioni TCP. La porta usata è la 80. HTTP è usato dal client e server per comunicare sopra connessioni TCP, il client stabilisce una connessione TCP con il server sulla porta 80, fa una richiesta ed aspetta il documento di risposta che in genere contiene hypertext link ad altri file. Le richieste sono effettuate tramite GET ed il server risponde con un HTTP o indica la fine del documento chiudendo la connessione. Il file, in formato HTML potrebbe risiedere sul server oppure su un altro. 

---
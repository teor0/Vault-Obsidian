# Datagrammi
Le applicazioni che comunicano tramite socket possiedono un canale dedicato, in quanto si usa il protocollo TCP a livello trasporto. Per comunicare un client ed un server stabiliscono una connessione, trasmettono dati, quindi chiudono la connessione. Tutti i dati inviati sul canale sono ricevuti nello stesso ordine in cui sono stati inviati. Le applicazioni che comunicano tramite datagrammi inviano e ricevono pacchetti di informazione completamente indipendenti tra loro. Queste applicazioni non dispongono e non necessitano di un canale di comunicazione punto-punto. La consegna dei datagrammi alla loro destinazione non è garantita e neppure l'ordine del loro arrivo, questo perché si usa il protocollo UDP a livello trasporto.

Il package java.net fornisce le classi che consentono di scrivere applicazioni che usano datagrammi per inviare e ricevere pacchetti sulla rete, queste classi sono: <font color=red> DatagramSocket</font> e <font color=red> DatagramPacket</font>. Elenchiamo adesso i metodi utili della classe DatagramSocket e DatagramPacket:
![[metodiDatragramSocket.png]]
![[metodiDatagramPacket.png]]

---
# MulticastSocket
Per utilizzare il Multicast con i socket, si sfrutta la classe <font color=red> MulticastSocket che estende DatagramSocket</font>. MulticastSocket fornisce la possibilità di introdurre gruppi, caratterizzati da un indirizzo IP ed una porta standard UDP.

``` Java
MulticastSocket(int port)
crea un multicastsocket e lo collega alla porta specificata sulla macchina locale
void joinGroup(InetAddress)
si aggiunge ad un gruppo
void leaveGroup(InetAddress)
esce da un gruppo
void receive (DatagramPacket p)
riceve un pacchetto dal socket
void send (DatagramPacket p)
manda un pacchetto sul socket
void close()
chiude il multicastsocket
```
Un gruppo multicast è identificato da un indirizzo IP ed una porta standard UDP.
Gli standard internazionale hanno previsto una classe di indirizzi predisposti al multicast, tale classe è: 224.0.0.0 - 239.255.255.255 
Gli indirizzi multicast nel corso del tempo sono stati standardizzati, in particolare alcuni standard hanno stabilito dei vincoli quali:
- 224.0.0.0 non è usato da nessun gruppo
- 224.0.0.1 è il gruppo formato da tutti gli host della LAN
- 224.0.0.2 è il gruppo di tutti i router
- 224.0.0.4 è il gruppo di tutti i DVMRP (Distance Vector Multicast Routing protocol) router
- 224.0.0.5 è il gruppo degli OSPF (Open Shortest Path First) router
- 224.0.0.13 è il gruppo dei PIM (Protocol Indipendent Multicast) router
- Il blocco 224.0.0.0 - 224.0.0.255 è usato per scopi amministrativi
- 224.0.1.1 è riservato al NTP (Network Time Protocol)

Il multicast è usato per comunicare in maniera efficente un messaggio da un computer a più computer, senza fare n connessioni singole ma piuttosto una connessione singola. Il multicast è utilizzato per stream multimediali a gruppi di host, ricordando che il multicast è basato su protocolli senza connessione come l'UDP.

---
## URLConnection

Per poter lavorare con gli URL, Java mette a disposizione la classe java.net.URL
``` Java
URL (String spec);
//crea un oggetto URL a partire dalla stringa che lo rappresenta
URL (String protocol, String host, int port, String file)
crea un URL a partire dai componenti specificati
```
solitamente un URL è composto dai seguenti componenti:
\<protocol>://\<userinfo>@\<hostname>:\<port>/\<path>?\<query>#\<references>

``` Java
URLConnection openConnection()
restituisce un oggetto URLConnection che gestice la connessione diretta alla risorsa
InputStream openStream()
apre un flusso di input per la lettura di dati della risorsa. da notare che restituisce un flusso binario

String getRef()
restituisce la reference di un URL
String getHost()
restituisce hostname di un URL
String getQuery()
restituisce la query string di un URL
String getProtocol()
restituisce il protocollo di un URL
String getPort()
restituisce la porta di un URL
String getUserInfo()
restituisce la parte di informazioni utente di un URL
```
Dietro le quinte la classe URL usa i socket, quindi aggiunge un ulteriore livello di astrazine che consente operazioni più potenti. Per connettersi ad un oggetto URLConnection occore usare il metodo connection(), dopo aver aperto la connessione tramite openConnection() su un oggetto URL. Esempio:
``` Java
URL url=new URL("https://the-eye.eu");
URLConnection c=url.openConnection();
c.connection();
```
Gli oggetti URLConnection possono avere diverse proprietà impostate, ad esempio:
- setDoInput(Boolean b): l'utente può ricevere l'input da questo URLConnection
- setDoOutput(Boolean b): l'utente può ricevere l'output da questo URLConnection
- setUseCaches(Boolean b): i dati possono essere recuperati da una cache locale
- setAllowUserInteraction(boolean allowUserInteraction): se true all'utente può essere richiesto un input addizionale
- setRequestProperty(String key, String value): imposta una proprietà della richiesta

Si possono anche richiedere informazioni di intestazione tramite metodi getter quali:
- getDate()
- getContentType()
- getContentEncoding()
- getContentLength()
- getLastModified()
- getExpiration()
- getHeaderFieldKey(int n)
- getHeaderField(int n)
- getInputStream()
- getOutputStream()

---

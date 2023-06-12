#fondamenti 
[[Instradamento]]
# Modalità dei protocolli
Il protocollo di trasporto funge da legame tra i livelli datalink e fisico ed il livello applicazione. I processi sono elementi attivi che producono o consumano messaggi ad esempio, dispositivi I/O comunicano tramite i processi. Un protocollo di trasporto può essere definito:
- affidabile con garanzia di consegna dei messaggi nel corretto ordine
- non affidabile dove si riesce solo ad indirizzare i processi applicativi

Il protocollo TCP (Transmission Control Protocol) è affidabile e orientato alla connessione. Il protocollo UDP (User Datagram Protocol) è senza connessione e non affidabile ma discrimina i processi applicativi.
Le funzionalità di questi protocolli sono implementate solo nei end device, quindi non su router, switch o hub. 

I protocolli di livello trasporto lavorano in una logica end to end, la distinzione per i processi applicativi la fanno tramite SAP (Service Access Point) su cui sono attestati i diversi processi applicativi in esecuzione su un host ad esempio HTTP. Ogni processo applicativo si appoggia su un SAP diverso, l'inframezzamento di informazioni da più entità di livello applicazione ad un processo di livello sottostante è chiamata <font color=red> multiplexing</font>. 
L'ordine si crea, in quanto ogni pacchetto di livello IP può scegliere il processo di livello 4 specifico TCP o UDP, che potrà esaminare dati specifici per smistare i pacchetti. Questa operazione si chiama <font color=red>demultiplexing </font>. ^ba9791

> sorgente→multiplexing destinazione→demultiplexing

I SAP sono distinti da un'etichetta logica detta porta. Le porte logiche risultano essenziali per il multiplexing e demultiplexing. Quindi abbiamo che:
- per il livello 4 indirizzamento tramite porte
- per il livello 3 indirizzamento tramite indirizzo IP
- per il livello 2 indirizzamento tramite indirizzo MAC

---
# Porte logiche
L'indirizzo completo TCP/IP, è costituito da indirizzo IP e numero della porta e identifica univocamente un processo in esecuzione su un host. I compiti si dividono:
- lo strato IP si occupa del trasferimento dei dati tra host collegati
- lo strato UDP/TCP si occupa dello smistamento dei dati tra sorgenti o destinazioni multiple all'interno dello stesso host tramite il numero di porta.

La coppia IP-porta sorgete, e la coppia IP-porta destinazione prende il nome di <font color=red> socket</font>. Se non indicati i socket non si può inoltrare alcun flusso. Il numero di porta è importante per discriminare i processi applicativi ed i numeri più "famosi" sono regolamentati dalla IANA. La porta destinazione è chiamata in genere <font color=green> server port </font>, mentre la porta sorgente è detta <font color=green>client port </font>. I numeri di porta possono essere assegnati in 2 modi:
1. assegnazione universale tramite IANA
2. assegnazione dinamica: assegnazione dal processo applicativo sorgente dopo una fase di negoziazione col processo applicativo destinazione e validi per una determinata sessione

La porta è indiciata con un numero a 16 bit, quindi $\large2^{16}$ porte divise in 2 gruppi:
1. da 0 a 1023 sono porte usate e ben conosciute, tra cui da 0 a 256 sono servizi consolidati nel tempo.
2. da 1024 a 65535 sono porte libere per gli utenti.

Alcune porte conosciute sono:
- Porta 21 per Telnet di tipo TCP
- Porta 25 per SMTP di tipo TCP
- Porta 53 per DNS di tipo sia TCP che UDP
- Porta 80 per HTTP di tipo TCP

---
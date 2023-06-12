#fondamenti 
[[Architettura ISO-OSI e TCP-IP e comunicazione logica]]
# Struttura TCP-IP
## Livello di accesso alla rete
Il livello fisico assieme al livello collegamento formano il livello di accesso alla rete. Questo livello include le funzioni che nel modello OSI sono comprese negli strati fisico, data link e di rete, quest'ultimo per ciò che riguarda gli aspetti connessi al funzionamento di ogni singola rete. 
Comprende le funzionalità per il trasferimento dei dati tra 2 sistemi terminali connessi alla stessa rete e può essere realizzato con gli strati pertinenti di qualunque tipo di architettura.

## Livello rete o internet
Il livello rete anche detto livello internet, gestisce l'instradamento dei datagrammi, fornisce un servizio di strato senza connessione, consente l'interfunzionamento delle varie reti componenti con funzionalità che nel modello OSI sono collocate in un sottostrato di rete alto ed usa il protocollo IP.

## Livello trasporto
Corrisponde allo strato di trasporto ed a parte dello strato di sessione del modello OSI. Un tipo di protocollo di questo strato è TCP (Transmission Control Protocol), dove il servizio dello strato è con connessione e mira all'affidabilità, ma c'è anche UDP (User Datagram Protocol) dove il servizio dello strato è senza connessione, tendente al multiplexing. Il livello trasporto sfrutta una logica E2E.

## Livello applicazione
Corrisponde a parte dello strato di sessione e agli strati di presentazione e di applicazione del modello OSI e consente supporto delle applicazioni di rete, utilizzando processi applicativi come ftp, telnet, dns e http.

---
# Confronto tra i 2 modelli
![[confronto.png]]
Il principale contributo del modello OSI è la distinzione tra servizi, interfacce e protocolli. Il modello OSI è nato prima della definizione dei suoi protocolli, questo porta a:
- pro: il modello è abbastanza generale
- contro: il progetto non teneva conto dei problemi reali specifici di alcune reti come le LAN

I protocolli sono nati prima del modello TCP/IP che è solo una descrizione di questi, e questo porta a:
- pro: i protocolli si adattano perfettamente al modello
- contro: il modello non si adatta a descrivere reti non TCP/IP

In sostanza:
- OSI, supporta a livello di rete servizi con e senza connessioni ed a livello trasporto, servizi con connessioni
- TCP/IP, supporta a livello di rete servizi senza connessioni ed a livello trasporto, servizi con e senza connessioni

---
## Critiche 
Per quanto riguarda OSI:
- tempismo storico errato: agli albori di OSI, TCP/IP era già nelle università ed i produttori decisero di investire su di esso.
- tecnologia errata: alcuni livelli sono sovraccaricati di funzioni, altri non sono necessari ed alcune funzioni sono ripetute tra livelli diversi come il controllo di flusso.
- implementazione errata: data la complessità del modello e protocolli, le prime implementazioni furono pesanti.
- politca errata: OSI era vista come proposta governativa, mentre TCP/IP era una realtà nata nelle università.

Per quanto riguarda TCP/IP:
- mancanza di una chiara distinzione tra servizi, interfacce e protocolli.
- mancanza di generalità ed applicabilità ad altri tipi di reti
- il livello di accesso alla rete non è un vero strato
- non esiste distinzione tra il livello fisico e data link

---


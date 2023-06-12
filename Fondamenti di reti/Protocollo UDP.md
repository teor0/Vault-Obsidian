#fondamenti 
[[Protocolli di trasporto]]
# Caratteristiche del protocollo
Il protocollo UDP è un protocollo semplice in grado di usare il servizio di comunicazione e le funzionalità IP facendo colloquiare processi remoti. UDP aggiunge 2 funzionalità a quelle di IP:
1. Indirizzamento della applicazione, cioè identificazione tramite un numero [[Protocolli di trasporto#^ba9791|SAP]] e di una porta.
2. Un blando controllo d'errore sull'header dei messaggi attraverso una checksum per verificare l'integrità.

UDP fornisce un servizio <font color=red> connectionless</font>, cioè manda pacchetti senza preoccuparsi di predisporre risorse in anticipo e quindi non si preoccupa di garantire l'ordine sequenziale d'arrivo. Inoltra non prevede meccanismi di ritrasmissione e controlli di flusso, eventuali meccanismi di ritrasmissione vengono gestiti dall'applicazione. 

---
## Struttura pacchetto UDP
Un pacchetto UDP è formato come segue:
![[packageudp.png]]
L'unità dati UDP ha lunghezza variabile, l'intestazione di UDP è lunga 8 byte ed è divisa nelle seguenti parti:
![[headerudp.png]]
- port number (16 bit), esprime la porta source o destination
- length (16 bit) è la lunghezza in byte del datagramma UDP (header+dati) dove il minimo valore è di 8 byte quando i dati sono vuoti
- checksum (16 bit), che utilizzerà [[Distanza di Hamming e codici a ridondanza ciclica#^0e219e|codice a ridondanza ciclica]] e tecniche per rilevare certi tipi di errori

La checksum è applicata allo pseudo header

---
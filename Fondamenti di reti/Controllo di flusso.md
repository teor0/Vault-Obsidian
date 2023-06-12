#fondamenti 
[[Protocollo TCP]]
# Definizione
Il controllo di flusso è una procedura attuata in modo esplicito tra sorgente e destinazione, intesa a limitare il flusso dei dati trasmessi in funzione delle risorse a disposizione. Il controllo di flusso avviene durante il trasferimento dei segmenti grazie alla sliding window della destinazione. La dimensione della window è orientata al byte. Un riscontro significa che sono stati riscontrati tutti gli ottetti ricevuti fino a quello numerato con x-1. Il trasmittente è autorizzato a trasmettere senza attendere altri riscontri fino a w ottetti ovvero fino all'ottetto numerato x+w+1. Dove:
Window=w e ACK number =x.
Solitamente la window ha un'ampiezza n\*MSS dove n è un intero per evitare che il TCP trasmittente esegue una segmentazione poco efficiente. Esempio: sia MSS=100 e Receiver Window=3MSS=300 Byte.
Il ricevitore può ricevere da 101 a 400 byte. Il primo segmento va da 101 a 201 il secondo da 201 a 301 la window poi slitta e la finestra rimane di 300 byte altrimenti il riscontro sarà inferiore. 
>Nel controllo di flusso al centro ci sono le risorse del ricevitore!

---
## Problema silly window
Per evitare il problema della <font color=red> silly window</font>, ovvero che 
la sorgente passa dati che il ricevente processa lentamente, c'è un accordo tra source e destination per cui la source deve mandare segmenti grandi almeno $\displaystyle {1\over 2}$MSS e la destinazione non comunica nulla finché non supera una certa dimensione in genere di 1MSS. L'unico caso in cui si può mandare meno di $\displaystyle{1\over 2}$ è per messaggi PUSH o URGENT.

--- 
# Throughput controllo di flusso
Il throughput di una connessione TCP dipende da:
- W: dimensione della window TCP in byte 
- D: ritardo di propagazione in secondi tra sorgente e destinazione TCP
- R: bit rate in byte/s della source TCP

Sia S il throughput, allora:
$\displaystyle\large S=\begin{cases} 1, & \text{se } W>RD \\ {W\over RD}, & \text{se } W<RD \end{cases}$

Dove S=1 significa 100% di utilizzo.
La window essendo che esprime il numero massimo di byte che posso mandare senza riscontro è un limite. Nel calcolo del throughput ignoriamo l'overhead del segmento TCP. Questa formula funziona su reti convenzionali tipo, reti cablate e l'internet classica. Un elevato ritardo di propagazione può inficiare la qualità della connessione, mentre se ho un bit rate spropositato accade che il prodotto RD risulta elevato. 
Quando fu concepito il TCP sembrava a prova di problemi, ma con il tempo si è accorti che il prodotto banda-ritardo su alcuni canli era elevato, questo portò alla nascita di un estensione del protocollo per farlo "sopravvivere" più a lungo. Questa estensione si occupa di fornire una dimensione della finestra di congestione variabile.

---

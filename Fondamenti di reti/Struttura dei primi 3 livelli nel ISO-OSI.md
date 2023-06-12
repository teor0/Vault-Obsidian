#fondamenti 
[[Architettura ISO-OSI e TCP-IP e comunicazione logica]]
[[Struttura dei restanti 4 livelli del ISO-OSI]]
## Livello 1 - fisico
Considera l'informazione come bit, l'interpretazione a più basso livello. Il livello fisico, fornisce i mezzi meccanici, fisici, funzionali e procedurali per attivare, mantenere e disattivare le connessioni fisiche. Ha inoltre il compito di effettuare il trasferimento delle cifre binarie scambiate dalla entità di livello di collegamento.

Il livello fisico ha scopo di fornire un mezzo di trasferimento da un nodo all'altro dell'unità informativa minima, il bit. Fornisce anche procedure per la trasformazione del flusso informativo di bit di segnali da inviare al mezzo:
- <font color=red> modulazione e demodulazione</font>: associare al segnale una forma d'onda e la possibilità di manipolarlo a piacimento
- <font color=red> codifica e decodifica</font>: che tipi di forma d'onda usa per rappresentare i bit
- <font color=red> multiplazione fisica ed accesso multiplo fisico</font>: se si vuole stabilire ogni quanto mandiamo i bit.

Su un nodo si ha una parte d'accesso su cui vengono mandati i bit ed a loro volta vengono mandati sul mezzo fisico. Questa parte, che è il cuore della struttura a livelli, permette lo scambio dìinformazione tra livelli. Il livello fisico si occupa di mandare al meglio i singoli bit per il livello 2.

---
## Livello 2 - collegamento o Data Link
Il livello Data Link, fornisce i mezzi funzionali e procedurali per il trasferimento delle unità dati tra entità di livello rete e per fronteggiare malfunzionamenti del livello fisico, attraverso codici di rilevazione o correzione di errore. Funzioni fondamentali sono:
- rilevazione e recupero degli errori di trasmissione (2 logiche diverse)
- controllo di flusso

> Per i canali broadcast il livello è stato diviso in MAC e LLC

Il livello Data Link si occupa del trasferimento dell'unità logiche di bit (trame) su un collegamento. ![[trama.png|Struttura trama]]

Il payload è l'informazione che si trova al livello superiore ovvero i dati utili del livello superiore più l'iter di quel livello. Al payload si aggiunge l'address, il CRC (Codice a ridondanza ciclica, per rilevazione e correzione di errori) ed i delimitatori. L'informazione viene suddivisa in frame in base alla direzione logica in cui viene trasmesso, se verso su o giù.

Per le reti broadcast, al livello Data Link, viene aggiunta la funzionalità d'accesso multiplo detta MAC (Medium Access Control). Essendo il canale broadcast condiviso, si usano interfacce per smistare i nodi, in questo caso si crea un sottolivello del livello collegamento, il MAC che si preoccupa di gestire l'accesso al canale condiviso. Al MAC si aggiunge LLC (Link Layer Control) che gestice il flusso ed il controllo di errori. ^553691

---
## Livello 3 - Rete
Il livello rete fornisce i mezzi funzionali e procedurali per lo scambio di informazioni tra entità di livello trasporto. Fornisce i mezzi per instaurare, mantenere e abbattere le connessioni di rete tra entità di livello trasporto. Funzioni fondamentali sono:
- instradamento
- indirizzamento
- controllo di connessione

Nel livello 3 del ISO/OSI c'è anche un controllo di congestione e connettività. In questo caso esiste un'unica entità di rete per l'instradamento e risulta evidente che è compito di questo livello creare le tabelle d'instradamento.

---
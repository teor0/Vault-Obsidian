---
tag: #elettronica 
created: 2023-04-26 12:24:52
updated: 2023-04-26 12:24:52
---
#elettronica 
[[Flip flop master-slave, preset-clear e pipeline]]
# Memoria 
I latch, i flip flop e registri sono stati impiegati per memorizzare piccole quantità di dati ma per grandi quantità di dati non sono adatti. Rivediamo brevemente i tipi di memoria:
- RAM: Random Access Memory, permette l'accesso diretto a qualunque indirizzo con tempo costante. Nella RAM vengono caricati programmi e dati, ricordando che è una memoria volatile.
- Cache: è utilizzata dalla CPU per ridurre i tempi d'accesso ai dati presenti nella RAM. La cache ha una capacità di memorizzazione limitata, ma è molto veloce ed è utilizzata per mantenere copia dei dati ai quali si accede più frequentemente.
- ROM: Read Only Memory, è una memoria a sola lettura contenente il BIOS scritto dal costruttore e costituito con un insieme di istruzioni necessarie all'accensione del sistema. 

Storicamente si è passati da ROM non programmabile se non dal produttore, PROM (programmable ROM) permette ad un utente di programmare un chip di memoria vuoto una volta sola, EPROM (Electrically PROM) che permette di cancellare tramite raggi UV il chip e riprogrammarlo però un numero finito di volte, EEPROM (Electrically Erasable PROM) cancellazione grazie a segnali elettrici molto più semplice e veloce, a Flash memory che utilizzano un morsetto specifico per programmazione e cancellazione.

L’organizzazione di una memoria è rappresentabile tramite un’array di parole, l’indice che individua la posizione di una certa parola, viene chiamato <font color=red>indirizzo di memoria</font>.
Ogni parola (word) consiste di $k$ bit dove $k$ è una potenza di 2 chiamata <font color=orange>word length</font> e una potenza di 2 è anche la profondità della memoria ovvero il numero di parole memorizzabili. A meno delle memorie ROM, le memorie possono essere sia lette che scritte e quando si va ad eseguire un accesso è necessario specificare l’indice. Data una memoria ad N indirizzi, con $x=log_2(N)\ bit$ è possibile rappresentare tutti gli indici per accedere alla memoria.
Descriviamo adesso le configurazioni di memoria ROM più commerciali:
- Single port, composta dal segnale di clock, in quanto anche l'accesso in ROM deve avvenire in maniera sincrona al segnale di clock, indirizzo da leggere, l'abilitazione alla lettura ENA, ed il canale di uscita che restituisce la word. Single port perché si legge una sola word alla volta. ![[singleport.jpg]]
- Dual port, dove è possibile specificare 2 diversi indirizzi per accedere parallelamente a 2 word. I due accessi possono essere sincronizzati su 2 segnali di clock differenti, ma non accade di solito. Una dual port può essere anche utilizzata come single port lasciando inutilizzati i segnali di ingresso e di uscita della seconda porta. ![[dualport.jpg|400x400]]

La dual port si usa per massimizzare la velocità d'accesso e ridurre i tempi complessivi.
Descriviamo poi le configurazioni di memoria RAM più commerciali che presentano segnali per la scrittura dei dati.
- Single port, dove troviamo l'indirizzo, il segnale DINA (Data In) che rappresenta il dato da scrivere in ingresso, il segnale di abilitazione per la scrittura e lettura WEA, che se pari a 1 abilita la scrittura e se pari a 0 abilita la lettura. ![[ramsingleport.jpg|500x300]]
- Simple dual port, che abilita l'accesso duplice ovvero una scrittura ed una lettura contemporaneamente tramite un secondo segnale ENB. Non permette di fare due letture o due scritture in quanto si ha un solo segnale di uscita. La scrittura e lettura contemporanee necessitano di gestione di conflitti, di solito gestiti già dal circuito. ![[simpledpram.jpg|300x450]]
- True dual port, che fondamentalmente permette ogni tipo di operazione, sia 2 scritture che 2 letture che una scrittura che una lettura. Anche qui ci sono conflitti da gestire in particolare, se voglio scrivere due valori diversi nello stesso indirizzo si ha una memorizzazione indefinita perciò la gestione degli indirizzi deve essere attenzionata. ![[truedpram.jpg|300x500]]

## Struttura interna
Guardiamo adesso la struttura interna di una RAM single port con profondità $N$, con indirizzi a $x=log_2(N)$ bit. Il suo circuito di controllo comprende un decoder per l'indirizzo ed una porzione di circuito che si occupa dei segnali di abilitazione. Il decoder è la componente circuitale che garantisce l'accesso esclusivamente sulla parola in posizione indicata, si noti che l'uscita del decoder comanda due interruttori/transistor che permettono di collegare la word specifica con l'uscita. ![[structspr.jpg|800x400]] Si ha quindi la sicurezza di chiudere un interruttore in scrittura o lettura per una sola word. 
Per una true dual port si impiegano 2 decoder e due datain e dataout.
Una singola dataword è composta da $k$ celle di memoria (non flip flop o latch!),che può essere realizzata in due modi:
1. Statica - SRAM,  ogni cella di memoria è formata da 2 inverter retroazionati quindi si hanno in totale 4 interruttori.
2. Dinamica - DRAM, la cella è composta da un solo interruttore e da una capacità. Meno costoso in quanto basta un interruttore rispetto ai 4 della cella SRAM ma più lenta, in quanto la lettura è distruttiva quindi o riscrivo il dato o lo perdo.
![[sramdram.jpg]]

Attraverso le celle si ottimizza l'uso di risorse e l'uso di interconnessioni verso l'esterno per operazioni di scrittura e di lettura.
>La cache utilizza la SRAM mentre la ROM utilizza la DRAM.

---



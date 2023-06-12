---
tag: #basi 
created: 2023-02-11 11:48:11
updated: 2023-02-11 11:48:11
---
#basi 
[[Transazioni e schedule]]
# Lucchetti
Nei database si usano 2 diversi tipi di lucchetti:
1. Lock-X: dove X sta per eXclusive
2. Lock-S: dove S sta per Shared

Quando su una risorsa viene messo un Lock-S, vuol dire che ci sono più chiavi per accedervi. Se il lock attivo è di tipo shared, tutte le risorse che devono richiedere un accesso in lettura possono accedere ed il lock rimane attivo, nel momento in cui qualcuno vuole sovrascrivere deve chiedere un lock di tipo eXclusive. Se il lock-S è ancora attivo allora il lock-X deve aspettare, e una volta ottenuto il controllo tutte le altre transazioni devono aspettare.
>Il lock-S garantisce un grado maggiore di parallelismo allo scheduler.


Prendiamo adesso uno schedule non conflict-serializable e non serializzabile:
![[eslock.jpg]]
Stabiliamo adesso che quando una transazione vuole accedere solo in lettura richieda un lock-S e se deve accedere solo in scrittura richieda un lock-X.
Vediamo come risolvere lo schedule visto:
![[eslockx.jpg]]
Quando $T_2$ richiede il lock-X su A, esso non sarà dato e dovrà aspettare a questo punto il controllo dello schedule ritorna a $T_1$ che finisce la transazione rilascia il lock e committa, dopodiché sarà garantito il lock a $T_2$. Ma facendo ciò è garantito l'isolamento? Sembra di si ma in realtà no, vediamo un controesempio:
![[controesempiolucc.jpg]]
Se eseguiamo in serie $T_1,T_2$ otterremo A=220, B=220 e se eseguiamo $T_2,T_1$ otterremo A=210, B=210. Entrambi gli schedule sono ragionevoli e garantiscono l'isolazione, ciò che crea problemi non è la richiesta del lock in sé ma il rilasciare il lock subito se dopo ne serve un altro! Per risolvere ciò utilizziamo il protocollo 2PL (2 Phase Locking).

---
# Protocollo 2PL
La prima fase del protocollo 2PL è la fase di <font color=orange>growing</font>, dove il numero di lucchetti della transazione aumenta. La seconda fase è quella di <font color=orange>shrinking</font> dove il numero di lucchetti della transazione diminuisce. La prima unlock andrà fatta dopo l'ultimo lock che la transazione chiede e dopodiché non potrà solo fare unlock. 
Se le transazioni seguono la semantica dei lucchetti ed il protocollo 2PL lo scheduler garantisce l'isolamento e genera schedule conflict-serializable. 

Dimostrazione tramite esempio su 3 transazioni: supponiamo di avere $T_1,T_2,T_3$ aderenti al protocollo 2PL, voglio di mostrare che qualunque schedule generato dallo scheduler che segue la semantica dei lucchetti sia conflict-serializable. Per assurdo: Sia $S$ schedule generato secondo semantica dei lucchetti, non sia conflict serializable. Si ha quindi che tra $T_1,T_2,T_3$ nel grafo delle precedenze si ha un ciclo. ![[assurdolock.jpg]]
Ma mettendo in cascata le precedenze alla fine si avrà: $unlock^{T1}(A)< lock^{T1}(C)$. Questo è assurdo dato che le transizioni segueno il protocollo 2PL non può accadere che $T_1$ faccia prima unlock e poi lock. 
L'intuizione sta nel dire che dato che si adopera il protocollo 2PL, non si possono mai generare cicli di concatenazione tra lock.

Il protocollo 2PL non garantisce però recuperabilità e cascadeless, nasce così il protocollo variante <font color=green>Strict 2PL</font> dove le transazioni rilasciano il lock-X tramite la commit e non esplicitamente tramite unlock. Ciò permette di avere le condizioni sufficienti per la recuperabilità e cascadeless. Nella pratica si usa un protocollo ancora più forte, lo <font color=green>Strong Strict 2PL</font> dove tutti i lucchetti sono rilasciati tramite commit. Questo alleggerisce il lavoro al DBMS che non deve tenere conto di quali lucchetti sono chiusi e quali aperti. 
Come detto prima, avere tutti questi vincoli porta a limitazioni non potendo generare degli schedule che impiegano unlock abbassando l'efficienza non tenendo di conto delle possibilità, si tende però ad utilizzare il protocollo Strong Strict 2PL data la sua leggerezza.
## Starvation e deadlock negli schedule
L'utilizzo del protocollo Strong Strict 2PL non impedisce però di avere starvation. Se ad esempio ho 10 transazioni dove solo la numero 3 chiede il lock-X e tutte le altre il lock-S, può capitare magari che data la natura del lock-S non bloccante verso richieste di lock-S, $T_3$ attenda all'infinito in quanto il lock-S continua a rinnovarsi dalle altre transazioni. Questo va a peggiorare in quanto nei database molti utenti fanno solo letture e pochi fanno letture e scritture assieme. Per evitare la starvation si può utilizzare il meccanismo dell'ageing.
Per quanto riguarda il deadlock può avvenire all'interno di serie di transazioni, per questo il DBMS ha meccanismi di detection del deadlock in tempo reale proprietari, in particolare un DBMS sceglie di abortire una transazione che attende da troppo tempo per rompere il deadlock.

---
# Livello di isolamento
Quando si crea un database si può settare il livello di isolamento tra:
- Serializable: garantisce la serializzabilità
- Repeatable read: permette la lettura solo di risorse che durante una transazione può cambiare.
- Read committed: permette di leggere solo risorse committate, ma permette pure che tra due letture una abbia aggiornato e committato la risorsa.
- Read uncommitted: permette di leggere risorse uncommittate, quindi non c'è alcun isolamente.

attraverso il comando `SET ISOLATION LEVEL [LV]`. Più il livello di isolamento è alto più il database è lento.

---

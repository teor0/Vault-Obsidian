---
tag: #basi
created: 2022-11-22 11:31:59
updated: 2022-11-22 11:31:59
---
#basi
# Introduzione
All'interno del corso si studia come si tratta la gestione della rappresentazione delle informazioni all'interno di collezioni di dati da diversi punti di vista. L’espressione gestione di dati indica tutte le attività che sono coinvolte nel ciclo di vita 
della rappresentazione dell’informazione: da un lato c’è l’informazione  d'altro c’è il fatto di voler estrarre delle informazioni. Tali informazioni poi andranno ad essere memorizzate in strutture apposite che durano nel tempo, strutture diverse da quelle viste in ASD in quanto il tutto sarà memorizzato in memoria secondaria e non primaria! Tali strutture si aggiornano automaticamente in maniera approppriata, infatti all'interno delle basi di dati il problema di race condition ritorna come parlato nei sistemi operativi.

---

# Concetto d'informazione e concetto di dato
Prima di occuparci di basi di dati però, bisogna distinguere dato da informazione.
Il <font color=orange>dato</font> è la rappresentazione di un concetto mediante una codifica o linguaggio, mentre <font color=blue>l'informazione</font> è qualcosa di primitivo, di cui non si può dare una definizione, insomma l'informazione è un concetto astratto.
> Distinguiamo quindi il livello astratto (informazione) da quello concreto (dati)

Nella teoria dell'informazione, l'informazione è quantificabile, ma non definibile. La misura dell'informazione è quanto viene alterato lo stato di chi la riceve rispetto al momento precedente alla ricezione. 
Il dato di per sé non ha alcun significato, ma, una volta interpretato in modo opportuno, fornisce informazioni.

---
# Concetto di basi di dati e DBMS
Le basi di dati servono a collezionare dei dati, quindi rappresentano delle informazioni in maniera opportuna secondo un particolare linguaggio dove il linguaggio è la codifica delle informazioni. Un Data Base Management System (DBMS), è un sistema software in grado di gestire collezioni di dati. Le caratteristiche delle basi di dati sono:
- <font color=blue>Grande capacità di memorizzazione</font>. Un DBMS ha capacità di migliaia di Terabyte se non di decine di Petabyte.
- <font color=blue>Condivisione</font>. Le basi sono condivise tra utenti e amministratori secondo opportune modalità, evitando la ridondanza.
- <font color=blue>Persistenza</font>. Le basi di dati sono dei veri e propri archivi, ed in quanto tali devono durare nel tempo e non possono cancellarsi con lo spegnimeto della macchina su cui si trovano.
- <font color=blue>Affidabilità</font>. Il sistema deve conservare il contenuto intatto delle basi di dati in caso di malfunzionamenti.
- <font color=blue>Privatezza</font>. Cioè ciascun utente deve essere abilitato opportunamente a determinate azioni sui dati attraverso meccanismi di autenticazione.
- <font color=blue>Efficienza</font>. Le basi sono capaci di svolgere operazioni in modo efficiente senza abusare di risorse o tempo di esecuzione
- <font color=blue>Efficacia</font>. Le basi sono capaci di rendere produttive, le attività dei loro utenti.

Si capisce che attraverso la condivisione e l'affidabilità nasce la concorrezza, in particolare l'accesso concorrente è gestito da una base di dati mentre da Access no.

>Perciò una base di dati è un'architettura che consente di avere atomicità e mutua esclusione dell'accesso alle informazioni. 

---
# Ciclo di vita di un sistema informatico basato su DBMS
Il ciclo di vita di un sistema basato su DBMS è descritto tramite il modello a cascata.
![[ciclovitadbms.jpg]]

Si parte dallo <font color=orange>studio di fattibilità</font>, la fase iniziale dove capiamo se la richiesta è fattibile o meno. Ciò dipende da 3 fattori:
1. Realizzazione: se è realizzabile o no
2. Pagamento: paga proposta
3. Tempo a disposizione: deadline consegna

Ci sono casi in cui ovviamente ci sono dei sistemi già disponibili e robusti che sono preferibili a delle realizzazioni fatte da 0.

Il secondo passo è <font color=orange>l'analisi dei requisiti</font> dova si raccolgono le specifiche funzionali e non. Un requisito non funzionale è ad esempio la volontà da parte del committente di avere software open source. Un requisito funzionale è ad esempio un'operazione specifica che il cliente vuole. Tale analisi avviene attraverso interviste con il committente.

Fase successiva è la <font color=orange>progettazione concettuale</font> dove si affronta la scelta delle informazioni da rappresentare ottenute dall'analisi dei requisiti. Tipicamente in un documento apposito si elencano le informazioni da rappresentare e le relazioni tra esse.

La fase successiva è la <font color=orange>progettazione logica/fisica</font>, dove capire quale struttura dati utilizzare (progettazione logica), e come implementarla (progettazione fisica). Consiste quindi nel guardare la realtà a diversi livelli di astrazione. 

Infine vi sono implementazione e messa in opera che saranno il frutto di tutte le fasi precedenti.

> Da notare, che il modello a cascata non impedisce di tornare ad una fase precedente.
---


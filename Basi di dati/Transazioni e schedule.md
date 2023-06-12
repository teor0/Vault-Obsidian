---
tag: #basi 
created: 2023-02-10 11:01:22
updated: 2023-02-10 19:12:40
---
#basi 
[[XQuery]]
# Transazioni
Il DBMS gestisce le transazioni ovvero programmi che vedono il contenuto del database ed effettuano modifiche. Formalmente:
> Una transazione è un'unità di programma in esecuzione che accede al database e può alterarne lo stato.

Capiamo la differenza tra query e transazioni attraverso un esempio:
Fattura(<u>Numero,Anno</u>,cliente,data)
Cliente(<u>CF</u>,nome,eta,citta)
Composizione(<u>NumFattura,AnnoFattura</u>,prodotto,qta,prezzo)
Prodotto(<u>Codice</u>,nome,marca)

Inserire una fattura nel database comporta:
1. L'inserimento di una tupla in Fattura
2. Un possibile inserimento in cliente
3. Possibili N inserimenti in prodotto
4. Possibili N inserimenti in composizione

Anche se dal punto di vista operativo si fanno più operazioni di basso livello, la transazione è concettualmente un'unica grande operazione. La transazione ha un significato <font color=red>atomico</font> ovvero tutte le operazioni di basso livello devono andare a buon fine, e non essere effettuate parzialmente altrimenti la transazione non va a buon fine. Nel database tramite l'istruzioni `BEGIN transaction` e `END transaction` si possono effettuare transazioni. Quindi essendo atomica la transazione se ho qualcosa del tipo:
```SQL
BEGIN TRANSACTION
INSERT ...
INSERT ...
DELETE ...
END TRANSACTION
```
e la DELETE è errata il database viene riportato ad uno stato <font color=red>consistente</font> dove vengono annullate le operazioni precedenti. In alcuni DBMS non ci sono gli statement di BEGIN/END, ma esiste lo statement COMMIT che eseguirà tutte le operazioni come corpo di un'unica transazione. 
L'operazione di ripristino di uno stato consistente è detta <font color=blue>ROLL BACK</font>.

---
# ACID
Le proprietà che vengono garantite dal motore di un DBMS che supporta le transazioni sono 4 e vengono abbreviate nella sigla ACID:
- <font color=blue>A</font>tomicità: una transazione che consiste in un insieme di statement ha successo se tutti gli statement al suo interno hanno successo.
- <font color=blue>C</font>onsistenza: una transazione agisce su uno stato consistente del database e restituisce uno stato consistente del database.
- <font color=blue>I</font>solamento: le transazioni sono isolate una dall'altra, attraverso la concorrenza delle modifiche. Per garantire la consistenza nella concorrenza le transazioni vengono eseguiti in modo seriale.
- <font color=blue>D</font>urabilità: quando il DBMS gestisce le transazioni, una volta che una transazione è andata a buon fine, le sue modifiche devono durare finché non arriva una nuova transazione che effettua un'ulteriore modifica.

È importante la gestione dell'isolamento delle transazioni, per fare ciò dentro il DBMS c'è uno scheduler che produce una schedule, in modo da usufruire dei benefici del parallelismo. Lo scheduler non genera schedule casuali altrimenti ci sono dei conflitti, ma non generano schedule seriali altrimenti non si sfrutta il parallelismo e l'efficienza è pessima. Uno scheduler di un DBMS genera schedule <font color=red>serializzabili</font>, che sono equivalenti a schedule seriali, portando il DBMS allo stesso stato a cui sarebbe stato portato da uno schedule seriale.

> Uno schedule S è serializzabile se $\exists$ $S'$ sulle stesse transazioni di S tale che: $S\equiv S'$ ossia $\forall$ istanza del database possibile, $S(D)=S'(D)$. 

Essendo uno schedule serializzabile equivalente ad uno schedule seriale dal punto di vista del risultato, si ha una certificazione di certezza e di non creare conflitti. Anche se gli schedule seriali sono ragionevoli non è detto che sono equivalenti tra loro. Esempio:
![[esemptrans.jpg]]
Se A=100 e lo schedule $S_1$ esegue $T_1,T_2$ e lo schedule $S_2$ esegue $T_2,T_1$ anche se corretti i risultati sono diversi!
Diciamo quindi che uno schedule serializzabile è ragionevole perché è equivalente ad uno schedule seriale non a tutti gli schedule seriali possibili.

---
# Scheduler e tipi di schedule
Generare uno schedule equivalente ad uno seriale è complesso. Per questo i database anziché andare a generare schedule che stanno nell'insieme degli schedule serializzabili, si sceglie di generare schedule che appartengono a due sottoclassi:
- Conflict-serializable: uno schedule è conflict-serializable quando da uno schedule ne posso ottenere uno equivalente seriale, facendo uno switch di operazioni che tra di loro non sono in conflitto. 
- View-serializable: consente di catturare casi di serializzabilità in cui avviene una blind write.

>[!Regola]
>Due operazioni sono in conflitto quando avvengono sulla stessa risorsa ed almeno una di loro è una scrittura.

Definizione formale di uno schedule conflict-serializable
> Uno schedule S è conflict-serializable se è conflict-equivalent ad uno schedule seriale S', in notazione $S\equiv_C S'$. $S\equiv_C S'$ se esiste una sequenza di scambi di operazioni non in conflitto tramite la quale si ottiene $S'$ da $S$.

>[!Regola]
Se uno schedule è conflict-serializable è serializzabile, lo dimostra l'insieme di operazioni. Non vale il viceversa.

Esempio di schedule serializzabile ma non conflict-serializable:
![[serianoconfl.jpg|400x550]]
I database usano dei meccanismi che generano conflict-serializable perdendo delle libertà, in quanto gli schedule serializzabili sono complicati da gestire.

Per capire se uno schedule è conflict-serializable utilizzo il seguente metodo: prese tutte le transazioni mi disegno il grafo delle precedenze dove i nodi sono le transazioni e gli archi tra essi ci sono se esistono una coppia di transazioni in conflitto, tale che la prima si trova in $T_1$ e la seconda in $T_2$. Il grafo dice velocemente se lo schedule è conflict-serializable, in quanto gli archi indicano chi ha la precedenza. 
>[!Regola]
Una condizione necessaria e sufficiente affinché uno schedule sia conflict-serializable è che il grafo delle precedenze sia aciclico. 

Si capisce che l'esempio visto ha un grafo delle precedenze ciclico. Per trovare uno schedule conflict-equivalent ad un altro posso utilizzare l'algoritmo di ordinamento topologico con complessità polinomiale.

Prendiamo adesso questo esempio:
![[esviewser.jpg|400x400]]
Lo schedule non è conflict-serializable ma equivale allo schedule seriale $T_1,T_2,T_3$, questo anche perché la scrittura effettuata da $T_3$ se ne frega di cosa abbiano fatto prima $T_1,T_2$, ciò viene detto <font color=red>blind write</font>.
Definizione:
> Uno schedule S è view-serializable se è view-equivalent ad uno schedule seriale $S'$, in notazione $S\equiv_V S'$. Due schedule $S,S'$ sono view-equivalent se:
> 1. $\forall$ risorsa $X$, le transazioni che leggono il valore iniziale di $X$ in $S$, leggono tale valore anche in $S'$ e viceversa.
> 2. $\forall$ risorsa $X$, se $T_i$ legge il valore di $X$ scritto da $T_j$ in $S$, allora $T_i$ legge il valore di $X$ scritto da $T_j$ in $S'$ e viceversa.
> 3. $\forall$ risorsa $X$, la transazione (se esiste) che scrive il valore finale di $X$ in $S$, scrive il valore finale di $X$ in $S'$.

Infine abbiamo che: $CS \subset VS\subset S$ dove per CS sta conflict-serializable, per VS sta view-serializable e S sta per serializable. Vediamo un contro esempio che viola la definizione appena data:
![[controesempiovs.jpg|400x400]]
Questo schedule non è view-equivalent a $T_1,T_2,T_3$ come quello di prima e nemmeno a $T_2,T_1,T_3$.
Capire se uno schedule è view-serializable è un problema NP completo, molto pesante infatti come detto i database si limitano a trovare schedule conflict-serializable.

---
# Problema della recuperabilità
L'isolamento garantisce che non ci siano conflitti ma non errori, se ad esempio una transazione fa un'inserimento negativo la transazione salta. 
Supponiamo che ci siano 2 transazioni $T_1$ e $T_2$, che operino entrambe su una risorsa A e che $T_2$ faccia una modifica al valore di A dopo che le abbia fatte $T_1$ e che la commit di $T_2$ avvenga prima di quella di $T_1$. Supponiamo pure che prima della commit di $T_1$ avvenga un errore è possibile fare una roll back? No in quanto c'è stata la commit di $T_2$ che ha fatto quindi modifiche su uno stato inconsistente.
Nasce così il problema della recuperabilità (recoverability): è il problema di garantire che in caso di errori sia sempre possibile ripristinare uno stato consistente.
Cerco perciò ripristinare lo stato consistente che mi comporta meno roll back possibili.

> Condizione sufficiente per recoverability applicabile per conflict-serializable: Ogni qualvolta ho una coppia di transazioni tali che una legge il valore scritto da un altra, la prima che deve fare commit deve essere quella che scrive.

Questo però può non bastare dal punto di vista dell'efficienza. Esempio:
![[recuperabilit.jpg]]
Se la transazione $T_1$ fallisce allora devo fare la roll back di tutte le transazioni in quanto $T_2$ dipende da $T_1$ e $T_3$ dipende da $T_2$. Si genera così il problema delle roll back a cascata. Nei database si cerca di ottenere degli schedule <font color=red>cascadeless</font> per quanto possibile in modo da minimizzare il numero di transazioni da abortire. Per evitare roll back a cascata devo garantire che tutto quello fatto da una transazione $T_i$ si committato prima che la transazione $T_j$ legga il valore modificato da $T_i$. Andiamo perciò a definire una condizione sufficiente per garantire l'assenza di cascate:

> Per ogni coppia di transazioni tale che la seconda legge un valore scritto dalla prima, la commit della prima deve avvenire prima della lettura della seconda.

Questo ovviamente genera un minor grado di libertà nell'interlacciare e generare gli schedule, ma evita errori da gestire.

---

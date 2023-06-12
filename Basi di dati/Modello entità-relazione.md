---
tag: #basi
created: 2022-11-22 15:39:50
updated: 2022-11-22 15:39:50
---
[[Concetti iniziali]]
#basi 
#  Modello ER per la progettazione concettuale
Il modello Entità Relazione (ER) rappresenta un progetto concettuale, utilizzato per rappresentare le informazioni e le loro relazioni. Una volta che conosco le informazioni bisogna rappresentarle in dati che le codificano. Ad esempio, dopo aver effettuato lo studio di fattibilità e l'analisi dei requisiti, andiamo a progettare la richiesta di un committente che vuole gestire forniture per il suo negozio, in particolare:
1. Vuole essere capace di inserire, modificare, rimuovere e ricercare fornitori
2. Gestire i fornitori in base a delle caratteristiche quali ad esempio P.IVA o recapito
3. Vuole essere capace di inserire, modificare, rimuovere e ricercare prodotti
4. Tali prodotto sono identificati da delle caratteristiche quali prezzo o codice
5.  Vuole essere capace di inserire, modificare, rimuovere e ricercare forniture, ossia chi fornisce cosa ed a che prezzo
# Schematizzazione del modello ER
![[esempioER.jpg]]
In figura si è rappresentata la schematizzazione del modello entità relazione, in particolare:
- Un'<font color=red>entità</font> è indicatà da un rettangolo
- Una<font color=red> relazione</font> è indicata da un rombo
- Un <font color=red>attributo</font> è indicato da un pallino

L'allineamento delle informazioni rappresentate rispetto alla realtà si chiama <font color=blue>consistenza/integrità</font>. Ciascuna entità è corredata dai propri attributi e messa in relazione con altre entità se necessario. Un attributo non può essere ricorsivo, ovvero un attributo non può richiamare un'altra entità. 

Plausibilmente un'attributo è identificatore di quell'entità, ad esempio un fornitore è identificato dalla P.IVA. Il meccanismo di identificazione delle varie istanze di un'entità consiste graficamente, nel eseguire un taglio su uno o più attributi. Tale identificatore/i dell'entità è chiamato chiave/i

![[esempiochiaveER.jpg]]
> Dire che un attributo è chiave vuol dire che è identificante, ossia non possono esistere più oggetti di quell'entità che coincidono sulla chiave.

---
## Dettagli sulla relazione e chiave minimale
Una relazione contiene un set di coppie delle entità che va a relazionare. Nell'esempio visto, le coppie saranno del tipo <Fornitore,Prodotto>, inoltre con relazione si rifa alla definizione di relazione matematica, ovvero sottoinsieme di un prodotto cartesiano tra A e B, quindi è un insieme di coppie composta da un elemento di A ed un elemento di B

Abbiamo visto che ci possono essere più attributi chiave di un'entità e non solo uno. Tuttavia gli attributi chiave devono essere presi seguendo un criterio e per capirlo guardiamo due esempi. 
1. L'entità Film ha come attributi titolo e regista. In particolare la chiave è definita dalla coppia titolo e regista, quindi possono esistere film con lo stesso titolo o con lo stesso regista ma non possono esistere film con lo stesso titolo e lo stesso regista. Ad esempio c'è Suspiria di Dario Argento e Suspiria di Luca Guadagnino.
2. L'entità fornitore nell'esempio ha come attributi P.IVA, nome e città. Dire che la chiave di fornitore è la coppia <P.IVA-Nome> è errato, in quanto vuol dire che possono esistere fornitori con la stessa P.IVA o con lo stesso nome ma non possono esistere fornitori con la stessa P.IVA e nome.

Il criterio che bisogna impiegare per ottenere una chiave identificante di un'entità è la minimalità. La definizione di minimale è:
L'insieme A è minimale rispetto alla proprietà P se $\nexists$ A'$\subset$A che soddisfa P 
> La chiave è un insieme di attributi minimale rispetto alla proprietà identificante.

In un'entità ci possono essere più chiavi minimali, che vanno identificate tutte. Andiamo a distinguere perciò chiave primaria da chiave secondaria ecc. Per le relazioni Nel corso tuttavia ci occuperemeo di una sola chiave. 
### Vincoli di cardinalità delle relazioni
Quando si specifica una relazione tra 2 entità si può specificare la cardinalità di ciascun entità alla relazione.
![[cardinalitaRelazione.jpg]]
Nell'immagine sono espresse le cardinalità della relazione fornitura tra fornitore e prodotto, in particolare:
- un fornitore è presente in un numero di coppie fornitura tra 0 e $n$
- ciascuna merce è presente un'unica volta in una coppia <fornitore,merce>

Abbiamo quindi imposto un vincolo sulla cardinalità tra la relazione tra fornitore e merce. I possibili vincoli sono di 4 tipi:
- 1:1. ovvero solo un oggetto dell'insieme A è associato ad un solo elemento dell'insieme B
- 0:n, da 0 fino a qualunque quantità si può associare
- 0:x, dove x è un numero naturale, quindi ad esempio 0:1 indica che da 0 ad 1 oggetto si può associare ad un altro

Distinguiamo così le relazioni in:
- Relazioni molti a molti: dove ambo i lati la cardinalità è 0:n.
- Relazioni uno a molti: dove da un lato c'è 0:n e dall'altro 1:1.
- Relazioni uno a uno: dove ambo i lati la cardinalità è 1:1.

---
# Scelta di rappresentazione dei concetti, chiave esterna e liste
Nel modello ER è importante distinguere i concetti tra entità e relazione. Se i concetti che si hanno sono: fornitore, P.IVA, nome, città e CAP. Come scelgo cosa è un attrittibuto e cosa un'entità? La scelta nasce dalla considerazione della rilevanza nella rappresentazione del concetto. Ad esempio, ci sono ricerche sulla base del CAP? 
Nel fare ricerche il concetto può occorrere più volte? Fatte queste ed altre considerazioni si sceglie come rappresentare i concetti. Vediamo un esempio:
![[attributoErrato.jpg]] La marca di una merce molto spesso è utilizzata a fini di ricerca di essa ed oltre questo ha un'altra proprietà che il nome. Perciò la rappresentazione giusta sarebbe la seguente:
![[rapprcorretta.jpg]]
Per identificare un'entità, una chiave può coinvolgere attributi e relazioni, in questo caso si parla di <font color=blue>chiave esterna</font>. Un caso particolare di chiave esterna è quella che coinvolge solo relazioni. 
> [!regola]
> Il vincolo di cardinalità di una relazione coinvolta in una chiave deve essere 1:1, perchè data la definizione di chiave altri vincoli sono errati.

Da notare che se il vincolo di cardinalità di una relazione è 1:1 non è detto che sia una perciò: 

> [!regola]
> Chiave esterna $\implies$ 1:1 ma 1:1$\centernot\implies$ chiave esterna

Esempio di chiave esterna:
![[chiavemista.jpg]]

Buona norma è utilizzare sostantivi singolari per l'entità e sostantivi per indicare le relazioni. Un attributo ha un valore libero, quindi attributi che si riferiscono a liste o ad entità create sono errati. In particolare se si vuole rappresentare una lista è opportuno utilizzare una relazione per la traduzione del concetto. Ad esempio una squadra di calcio ha una lista di giocatori, quindi la traduzione di ciò sarebbe:
![[tradLista.jpg]]
dove appunto un giocatore appartiene ad una squadra sola ed una ha N giocatori per semplicità ma sarebbe giusto mettere 24 come il numero ufficiale della rosa.

---
# Generalizzazione
Nel caso di studio che esaminiamo si vuole gestire l'attività di una segreteria universitaria, in particolare dall'analisi dei requisiti estrapoliamo come concetti fondamentali: studenti, docenti, corso di laurea, materia ed esame.
Uno studente ed un docente sono entità caratterizzate da attributi in comune quali: codice fiscale, nome e data di nascita. Tuttavia hanno però attributi specifici come la matricola o il dipartimento di appartenteza quindi occore fornire un ulteriore livello d'astrazione. Andiamo così ad introdurre una relazione di generalizzazione:
![[generalizzazione.jpg]]
Le chiavi vengono ereditate ma c'è un'eccezione quando uno o più attributi di una sottoentità sono identificativi. All'interno del corso si utilizzeranno solo le chiavi ereditate. Abbiamo quindi un'entità con sottoentità, ovvero persona è un concetto più astratto rispetto a studente e docente. 

La generalizzazione può essere totale o parziale e esclusiva o inclusiva. Nel nostro caso abbiamo una relazione totale perché tutti i membri dell'entità persona devono fare parte di almeno un sottolivello e l'appartenenza a questo sottolivello è esclusiva. Perciò abbiamo un relazione di generalizzazione totale esclusiva che altro non è che un partizione. Ricordando che:
> Dato un insieme S, una partizione P di S è un insieme di sottoinsiemi di S con le seguenti proprietà: $\forall S_i,S_j\in P$ | $S_i\cap S_j=\oslash$e $\displaystyle\bigcup_{S_i\in P} S_i=S$. Ovvero che ogni sottoinsieme $S_i$ ha elementi che non stanno in un altro sottoinsieme $S_j$ e che l'unione di tutti i sottoinsiemi della partizione P ritorna l'insieme S.

A differenza degli altri tipi di generalizzazione quella totale esclusiva non va scritta.
- Per generalizzazione <font color=orange>esclusiva</font> si intende che le sottoentità sono completamente separate.
- Per generalizzazione <font color=orange>inclusiva</font>  si intende che ci può essere intersezione tra le sottoentità.
- Per generalizzazione <font color=blue>totale</font>  si intede che un membro dell'entità generale deve appartenere ad almeno una delle sottoentità. (Una persona può appartenere a studenti)
- Per generalizzazione <font color=blue>parziale</font>  si intende che un membro dell'entità generale può non appartenere ad alcuna delle sottoentità. (Una persona può non appartenere a studenti)

Non è necessario che le sottoentità abbiano attributi, perché il fatto stesso che noi abbiamo chiamato la sottoentità con un nome diverso è già un attributo in più.
Le relazioni comuni tra sottoentità vanno fatte con l'entità madre, se si fanno relazioni specifiche si può se semanticamente non sono uguali, quindi tutte le caratteristiche comuni vanno astratte all'entità madre. 
La generalizzazione parziale esclusiva a differenza delle altre è rappresentabile tramite due relazioni senza perdere la semantica.

> Un caso particolare di generalizzazione è quella in cui c'è solo una sottoentità. In questo caso si parla di specializzazione.

Se ho una situazione del tipo:
![[ISA.jpg]]
non è errato trasformarla come segue, in quanto la relazione è generale mentre ISA è specifico.
![[tradISA.jpg]]

---
## Caso di studio
Andiamo adesso a sviluppare il modello completo ER per la segreteria universitaria;
![[segretErrata.jpg]]
Sembrerebbe corretto ma in realtà il modello è errato. Un esame è si un concetto che più essere fatto più volte e passato una sola, ma rendendolo relazione i tentativi fatti da uno studente non vengono contati. Risulta quindi più opportuno utilizzare un'entità per rappresentare esame.
![[segreCorrett.jpg]]

---
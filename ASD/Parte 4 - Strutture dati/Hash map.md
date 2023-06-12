#asd
[[Dettagli sulle strutture dati classiche ed alberi]]
# Tabelle accesso diretto
Prima di trattare l'hash map parliamo delle tabelle ad accesso diretto, che sono dizionari basati sulla proprietà d'accesso diretto alle celle di un array, quindi un dizionario memorizzato in un array di m celle. 
A ciascun elemento è associata una chiave intera nell'intervallo \[0, m-1]. L'elemento con chiave k è contenuto in a\[k] e al più si hanno $n\le m$ elementi nel dizionario. Misuriamo il grado di riempimento di una tabella tramite il <font color=green>fattore di carico</font>, ovvero l'occupazione di memoria. 

Siano $n$ il numero effettivo di elementi ed $m$ le celle possibili della tabella, allora il fattore di carico $\alpha$ è pari a $\displaystyle\alpha={n\over m}$.
Ad esempio se n=100 e m=1 milione $\alpha$=0,01% quindi si ha un altissimo spreco di memoria.
Pregi:
- Tutte le operazioni richiedono $O(1)$ 

Difetti: 
- Può esserci grande spreco di memoria e le chiavi sono necessariamente interi compresi tra \[0,m-1]

# Tabelle hash
Trattiamo adesso le tabelle hash, che si basano sulle tabelle ad accesso diretto e differiscono come segue da esse:

- Le chiavi possono avere qualunque valore e non solo valori interi
- Si utilizza una funzione di hash, $h:U→[0,m-1]$ che trasforma chiavi in indici, quindi $U$ dominio delle chiavi che ha come codominio $[0,m-1]$
- Un elemento con chiave k assume posizione v\[h(k)]

Le tabelle hash possono però soffrire di collisioni, ovvero 2 chiavi diverse hanno lo stesso hashcode.

## Funzione perfetta e comportamento buono
Definiamo così una funzione hash perfetta. 

Una funzione hash si dice <font color=green>perfetta</font> se è iniettiva, cioè:

>$\forall u,v$ $\in U: u \ne v \Rightarrow h(u)\ne h(v)$
Deve risultare però che $|U| \le m$ ovvero la cardinalità del dominio delle chiavi sia minore uguale della dimensione della tabella. 

Quindi si dice perfetta una funzione hash se dati $u$ e $v$ elementi diversi, se sottoposti ad hashing, si ha che $h(u)\ne h(v)$.

Si capisce quindi che una funzione hash perfetta è si conveniente ma in rari casi ed, in rari casi è possibile ottenerla. Nella pratica si utilizzano funzioni hash buone, ad esempio $h(k)=ascii(k)$ $mod$ $m$ è una funzione molto buona per chiavi che sono numeri primi, dove l'hashing è pari al codice ascii della chiave per il modulo di m.

Per <font color=green>comportamento buono</font> si intende la riduzione della probabilità di collisioni per massimizzare l'efficienza della tabella, questo si ha ad esempio con funzioni hash che godono di uniformità semplice. Supponiamo di avere $P(k)$, la probabilità che k sia presente nel dizionario e che:

$Q(i)=\displaystyle\large\sum_{k:h(k)=i}P(k)$

sia la probabilità che la cella $i$ sia occupata. Una funzione hash è <font color=green> uniforme semplice</font> se la probabilità che la cella $i$ sia occupata è pari a $Q(i)=$$\displaystyle{1\over m}$.

Se $U$ è pari a l'insieme dei numeri reali compresi tra $[0,1]$ ed ogni chiave ha la stessa possibilità di essere scelta, allora la funzione hash $h(k)=$$\lfloor km\rfloor$ soddisfa la proprietà di uniformità semplice. L'assunzione che ogni chiave ha la stessa probabilità non è sempre valida, perciò dobbiamo trovare una soluzione per risolvere le collisioni. 
Ci sono 2 meccanismi per risolvere le collisioni:
1. Utilizzare spazio aggiuntivo per gestire le collisioni, usando ad esempio liste di collisione.
2. Utilizzare celle libere nella tabella senza usare spazio aggiuntivo. Viene usato l'indirizzamento aperto.

Per le liste di collisione avremo:
- $\theta(1)$ per insert
- $\large T_{avg}=\theta$$\large{(1+{n\over m})}$ per delete e search

Un array estendibile è preferibile in modo da controllare $\large{n\over m}$ adeguatamente.

Per l'indirizzamento aperto supponiamo di voler inserire un elemento con chiave k, ma la sua posizione naturale sia occupata. L'indirizzamento aperto consiste nell'occupare un'altra cella anche se potrebbe spettare di diritto ad un altro elemento. La cella si ottiene scandendo le celle secondo una sequenza di indici. I metodi di scansione sono:
- Scansione lineare: $C(k,i)=$$(h(k)+i)$ $mod$ $m$ per $0\le i\le m$. Funziona ma ha problematica del tipo accumulazione e celle scandite mediamente.
- Hashing doppio: $C(k,i)=$$\lfloor h_1(k)+ih_2(k)\rfloor$ $mod$ $m$ per $0\le i\le m$, $h_1$ e $h_2$ funzioni hash. Questa implementazione riduce l'accumulazione e le celle scandite mediamente. 

Il tempo richiesto in media da un'operazione di ricerca di una chiave, assumendo che le chiavi siano prese con probabilità uniforme da $U$:
![[tempoindi.jpg]]
dove $\large\alpha\ne{n\over m}$ ovvero il fattore di carico, in questo caso avremo costo di delete lineare.

---
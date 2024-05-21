---
tag: #elettronica 
created: 2023-02-17 19:24:51
updated: 2023-02-17 19:24:51
---
#elettronica 
[[Approccio progettuale e MOSFET]]
# Inverter CMOS
Nel caso dell'inverter si va a collegare un primo interruttore tra $V_{DD}$ e $V_{out}$ che sarà chiuso solamente quando l'uscita è 1, ed un secondo interruttore tra $V_{out}$ e GND che sarà chiuso solamente quando l'uscita è 0.
![[inverterNO.jpg|100x500]]
Manca però il necessario segnale di controllo per gli interruttori che sarà anch'esso una tensione e sarà il segnale di ingresso che stabilirà lo stato degli interruttori. Avremo perciò il seguente schema:
![[inverterOK.jpg|500x500]]
Si nota che il simbolo di $V_{DD}$ rappresenta la presenza di un generatore di tensione costante che eroga la tensione $V_{DD}$. Se entrambi gli interruttori sono chiusi si va a creare un cortocircuito. Si nota dalla tabella degli stati che un inverter equivale alla funzione logica più semplice, il NOT.
Ci si aspetta che :
$\begin{gather}
V_{Ing}=V_{DD}\ V_{out}=0V\ T1=OFF\ T2=ON \\
V_{Ing}=0V\ V_{out}=V_{DD}\ T1=ON\ T2=OFF
\end{gather}$
I segnali di controllo sono gli ingressi che il circuito deve processare per svolgere la funzione logica desiderata. Una regola fondamentale è il fatto che:
>[!Regola]
>$\forall\ \text{Tipo1}\ \exists\ \text{Tipo0}$

questo evita la possibilità di cortocircuito e serve a garantire la mutua esclusione. Questa regola afferma che se esiste un percorso attraverso il quale $V_{out}$ può diventare pari a '0', non deve esistere nessun percorso attraverso il quale $V_{out}$ possa assumere anche $V_{DD}$. Per generalizzare queste proprietà nei circuiti CMOS, si fa in modo che il circuito sia composto da 2 sottoreti:
1. La prima prende il nome di <font color=blue>Rete di pull-up</font>, e viene indicata con l'acronimo PUN. Attraverso gli interruttori di questa rete l'uscita può assumere il livello alto '1', da cui nasce "up". Questa rete contiene interruttori di <font color=red>tipo 0</font>.
2. La seconda prende il nome di <font color=green>Rete di pull-down</font>, e viene indicata con l'acronimo PDN. Attraverso gli interruttori di questa rete l'uscita può assumere il livello basso '0', da cui nasce "down". Questa rete contiene interruttori di <font color=red>tipo 1</font>.

![[punpdn.jpg|300x600]]
Più precisamente, per ogni interruttore nella rete PUN deve esistere il suo duale nella rete PDN, in questo modo si riesce a garantire che non siano mai entrambe contemporaneamente aperte o chiuse. Se entrambe le sottoreti fossero aperte, ci si ritrova in uno stato [[Standard logic, process e concurrent statement#^22897a|Z]]. Nei circuiti CMOS il fatto che la PUN contenga interruttori di tipo 0 e la PDN contenga interruttori di tipo 1, è inevitabile data la composizione dei transistor.

---
## Circuiti NAND, AND, NOR e OR
Consideriamo adesso il circuito seguente:
![[circnand.jpg|500x500]]
Per capire la funzione logica andiamo a crearci una tabella degli stati con ogni possibile combinazione degli ingressi.

| Ing1     | Ing2     | Z1  | Z2  | U1  | U2  | $V_{out}$ |
| -------- | -------- | --- | --- | --- | --- | --------- |
| 0V       | 0V       | ON  | ON  | OFF | OFF | $V_{DD}$  |
| 0V       | $V_{DD}$ | ON  | OFF | OFF | ON  | $V_{DD}$  |
| $V_{DD}$ | 0V       | OFF | ON  | ON  | OFF | $V_{DD}$  |
| $V_{DD}$ | $V_{DD}$ | OFF | OFF | ON  | ON  | 0V        |

Si nota che il circuito riproduce il funzionamente della funzione logica NAND.
Se dovessi aggiungere un inverter su $V_{out}$ otterrei la funzione logica AND:
![[circand.jpg|500x500]]
Consideriamo il seguente circuito:
![[circnor.jpg|250x600]]
Creiamo la tabella degli stati per capire il funzionamento:

| Ing1     | Ing2     | Z1  | Z2  | U1  | U2  | $V_{out}$ |
| -------- | -------- | --- | --- | --- | --- | --------- |
| 0V       | 0V       | ON  | ON  | OFF | OFF | $V_{DD}$  |
| 0V       | $V_{DD}$ | ON  | OFF | OFF | ON  | 0V        |
| $V_{DD}$ | 0V       | OFF | ON  | ON  | OFF | 0V        |
| $V_{DD}$ | $V_{DD}$ | OFF | OFF | ON  | ON  | 0V        |

Capiamo quindi che si tratta della funzione NOR. Anche in questo caso basta applicare un inverter su $V_{out}$ per ottenere la funzione OR.
![[circor.jpg|400x500]]
Ciò che si nota è che al contrario di come si pensava all'inizio, i circuiti NAND e NOR di costo uguale, hanno costo più basso di AND e OR anch'essi con costo uguale.

---
# Regole di applicazione sui circuiti
Si consideri un circuito generico CMOS:
![[circgeneric.jpg|300x500]]
È necessario specificare distintamente le regole per la PUN e la PDN.
Regole per la PUN:
1. $\forall AND\in f(I_1,...,I_n)\implies$ collegamento in parallelo. Per ogni operatore AND presente nella PUN, è presente un collegamento in parallelo.
2. $\forall OR\in f(I_1,...,I_n)\implies$ collegamento in serie. Per ogni operatore OR presente nella PUN, è presente un collegamento in serie.

Regole per la PDN:
1. $\forall AND\in f(I_1,...,I_n)\implies$ collegamento serie. Per ogni operatore AND presente nella PDN, è presente un collegamento serie.
2. $\forall OR\in f(I_1,...,I_n)\implies$ collegamento in parallelo. Per ogni operatore OR presente nella PDN, è presente un collegamento in parallelo.

Esiste poi una regola per un circuito generale ed afferma che:
>[!Regola]
>Se la funzione assegnata è negata (NAND, NOR) non devo fare nulla, altrimenti se la funzione assegnata è diretta sull'uscita, bisogna aggiungere un inverter sull'uscita.

^31357b

## Esempio XNOR e XOR
Si supponga di avere la seguente funzione: $f=a\land b+\bar{a}\land\bar{b}$ 
Per costruire il circuito partiamo dalla rete PDN associando quindi ad ogni AND un ramo di interruttori in serie. Ottengo perciò la seguente rete:
![[pdnxnor.jpg|400x500]]
Per quanto riguarda la PUN, segue la regola per cui una OR equivale ad un collegamento in serie, considerando le due operazioni di and come se fossero un unico operando ottenendo perciò 2 porzioni in parallelo messe in serie come segue:
![[punesxnor.jpg|400x500]]
Il circuito che ricavo alla fine è il seguente:
![[escirc.jpg|600x600]]
![[tabescirc.jpg]]
Gli ingressi sono $a$ e $b$ e si fa riferimento alle tensioni per esprimere le combinazioni di valori. Tra la 2° e 3° riga si invertono gli stati per cui il valore non cambierà in quanto a cambiare è solo il percorso. Guardando le tre colonne ($a$,$b$ e $V_out$) si nota che la funzione logica che si esprime è la XNOR. 
Per capire come si ottiene $V_{out}$ si seguono i valori Z-esimi e U-esimi della prima riga, notando che si crea un percorso tra gli interruttori di GND e $V_{out}$.
Quando si sono enunciate le regole per i circuiti si è dette che l'inverter è necessario per funzioni dirette ma la XNOR è una funzione negata, ci troviamo quindi di fronte ad una anomalia. Inoltre eliminando l'inverter finale ottieniamo la funzione logica XOR.
![[circxor.jpg|600x600]]
Tuttavia esiste un altro metodo per rappresentare la XNOR senza l'inverter, quello di rappresentare la funzione $f=a\land\bar{b}+\bar{a}\land b$. Il circuito che si ottiene dopo tutti i passaggi è il seguente:
![[altxor.jpg|600x600]]
Ma questo altro non è che uno XOR! Se tolgo l'inverter come detto, si ottiene una XNOR!
![[altxnor.jpg|700x850]]
In particolare, nel primo caso abbiamo che, $a\oplus b=\overline{a\land b+\bar{a}\land\bar{b}}$ mentre nel secondo caso abbiamo che $\overline{a\oplus b}=\overline{a\land \bar{b}+\bar{a}\land b}$, quindi scegliamo di rappresentare $XOR\equiv\overline{XNOR}$ e $XNOR\equiv\overline{XOR}$ per risparmiare l'inverter all'uscita.
Sostanzialmente a livello di porte stiamo dicendo che sono più semplici le rappresentazioni seguenti:
![[finalxorxnor.jpg|400x400]]

---
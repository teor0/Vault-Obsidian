---
tag: #elettronica 
created: 2023-02-19 12:50:44
updated: 2023-02-19 12:50:44
---
#elettronica 
[[Inverter CMOS e regole di applicazione sui circuiti CMOS]]
[[Esercizi sulle regole di applicazione e capacità]]
# Caratteristiche statistiche e dinamiche
Si consideri l'inverter con le sue proprietà non ideali e schematizzato come segue: 
![[capacita.jpg]]
le caratteristiche che si possono esaminare su qualsiasi circuito ad interruttori si dividono in 2 gruppi:
1. <font color=purple>Caratteristiche statiche</font>, possono essere osservate quando gli ingressi del circuito sono stabili, ovvero quando il loro valore non cambia nel tempo.
2.  <font color=purple>Caratteristiche dinamiche</font>, possono essere osservate durante la commutazione degli ingressi, ovvero cambiano valore. 

## Capacità in situazione statica e dinamica
Supponiamo di essere in una fase di analisi delle caratteristiche statiche di un inverter, in cui I='0'. Essendo gli ingressi stabili, lo sarà anche $V_{out}$, ovvero i segnali del circuito si muovono con frequenza=$0MHz$. Quando le variazioni ai capi di un circuito avvengono con frequenza nulla, la capacità corrisponde ad un circuito aperto, questo perchè ad ogni capacità è associabile ad una impedenza ed in questa situazione è pari a: $\displaystyle\large z_{C_L}={1\over{j\omega C_L}}=\infty$ con $\omega=2\pi f$
Questo implica che nell'analisi statica del circuito $C_L=0$ per cui si è in una situazione ideale e la capacità equivale ad un circuito aperto.
Quando gli ingressi commutano, lo farà anche l'uscita e la frequenza di commutazione dell'uscita determinerà l'impedenza associata alla capacità che sicuramente è $\neq\infty$, quindi la capacità va considerata.

---
# Comportamento statico di un inverter reale
Per semplicità facciamo si che gli interruttori di tipo 0 e 1 abbiano resistenze $R_{ON}$ e $R_{OFF}$ uguali mentre in realtà non è cosi come già visto. Consideriamo adesso la situazione in cui $I=V_{DD}$ e schematizziamo l'inverter reale e quello ideale.
![[staticcirc.jpg]]
Essendoci un generatore di tensione continua nei due circuiti circolerà la corrente, in particolare nel circuito ideale $I_{DD}=0$ mentre nel circuito reale $\displaystyle I'_{DD}={V_{DD}\over R_{ON}+R_{OFF}}$ e siccome $R_{OFF}$ non è $\infty$ si avrà che $I'_{DD}>0$ anche se di poco.
Nel caso di $V_{out}$ per il circuito ideale sarà pari a $0V$ mentre nel circuito ideale $V_{out}=I'_{DD}R_{ON}>0V$. Quindi rispetto alla condizione ideale, la tensione che dovrebbe rappresentare $0V$ non viene raggiunta nominalmente ma si è leggermente sopra.
Consideriamo adesso la situazione in cui $I=0V$ e schematizziamo il circuito reale e quello ideale.
![[staticcirc2.jpg]]
Nel circuito ideale $I_{DD}=0$ mentre nel circuito reale $\displaystyle I'_{DD}={V_{DD}\over R_{ON}+R_{OFF}}>0$. Nel caso ideale il valore di $V_{out}=V_{DD}$ mentre nel caso reale $V_{out}=I'_{DD}R_{OFF}$. Nel caso reale posso anche ottenere $V_{out}$ come la differenza di potenziale ai capi di $R_{ON}$ tenendo in considerazione l'effetto di $V_{DD}$. L'equazione delle maglie è pari a: $-V_{DD}+R_{ON}I'_{DD}+V_{out}=0\ \implies V_{out}=V_{DD}-R_{ON}I'_{DD}$
Questa equazione mi consente di dire che sicuramente $V_{out}<V_{DD}$.
Quindi anche in questa situazione non si riesce a raggiungere il valore di tensione nominale che ci si aspetta nel caso ideale.

--- 
# Dissipazione di potenza
Introduciamo la dissipazione di potenza. La dissipazione di potenza nei circuiti reali è composta da dissipazione di potenza statica e dinamica.
La  dissipazione di potenza statica, si verifica quando gli ingressi del circuito sono stabili e viene calcolata come $P_{Stat}=V_{DD}I'_{DD}$. Nel caso ideale il circuito non dissipa potenza ma nel caso reale, essendo $I'_{DD}>0$ abbiamo che il circuito dissipa staticamente potenza. Solitamente questa potenza è trascurabile rispetto alla potenza dinamica.

---
# Fan-In
Per trattare un'altra caratteristica statica riparliamo del concetto di FAN-IN, il numero massimo di ingressi rappresentabili dalla porta logica. Consideriamo una NAND a 4 ingressi e di non aver limitazioni per il FAN-IN. $f=\overline{a\land b\land c\land d}$
![[nand4fanin.jpg|500x500]]
La tabella degli stati sarà la seguente:
![[tabnand4fanin.jpg|400x400]]
Di queste 16 possibili combinazioni esaminiamo '0000' e '1111'. Nel caso in cui $I=0000$ il circuito utilizzando le resistenze equivalenti sarà:
![[nand4resist.jpg|500x500]]
che può essere semplificato in
![[simplenandrest1.jpg]]
Nel caso in cui si consideri il circuito come ideale $V_{out}=V_{DD}$, mentre nel caso in cui si consideri il circuito reale $\displaystyle V_{out}=V_{DD}-I'_{DD}{R_{ON}\over 4}$. In questo caso il comportamento non è peggiorato rispetto a quello dell'inverter.
Nel caso in cui $I=1111$ il circuito nella versione semplificata è:
![[simplenandrest2.jpg]]
Nel caso ideale $V_{out}=0V$, mentre nel caso reale la resistenza equivalente nella PDN è 4 volte maggiore e questo ha effetto sul valore di $V_{out}$ pari a $V_{out}=4R_{ON}I'_{DD}$ e questo valore è peggiore di quello di un inverter di circa 4 volte!
Perciò all'aumentare degli ingressi non viene peggiorato il comportamento della porta per quanto riguarda il raggiungimento dello stato logico '1' in uscita, ma peggiora il comportamento in termini di tensione in uscita che rappresenta lo stato logico '0'. 
> All'aumentare degli ingressi si crea deterioramento degli stati logici, ovvero le tensioni in uscita non raggiungono i valori nominali che ci si aspetta nel caso ideale.

Si capisce perciò che il fan-in rappresenta il numero massimo di ingressi che una porta logica può processare senza creare deterioramento ed è fissato a 2.

---

---
tag: #elettronica 
created: 2023-02-15 19:59:42
updated: 2023-02-15 19:59:42
---
#elettronica 
[[VHDL]]
# Concetto di driver e tipo standard logic
Fino ad ora si è fatto riferimento ad informazioni di tipo bit o bit_vector, ma questo dal punto di vista elettronico è errato in quanto, nei circuiti si fa riferimento a tensioni con logica positiva. Consideriamo adesso una parte di un circuito logico all'interno del quale passa l'informazione. Tale punto è detto driver e viene rappresentato come segue:
![[driver.jpg]]
Supponiamo di trovarci nella situazione in cui ci siano 2 informazioni differenti collegate:
![[conflittodriver.jpg]]
Si ha un cortocircuito in quanto si sta cercando di collegare 2 valori di tensione diversi. L'informazione intermedia non può essere rappresentata, questo a livello concettuale in VHDL si traduce nel tipo <font color=blue>Standard Logic</font>, che consente di rappresentare i dati mediante valori particolari anche detti non idealità. I segnali di tipo std_logic possono assumere diversi valori:
- 0
- 1
- X: unknown
- H: weak high
- L: weak low
- Z: High impedance, ovvero segnale non collegato ^22897a
- -: don'tcare
- U: uninitialized, non inizializzato presente solo nelle simulazioni

Il valore X è la risposta al problema che si è visto. Un'altra situazione analoga può essere quando ci sono dei rumori all'interno del circuito che vanno a modificare i valori di tensione. Quando si considera un circuito ideale, il valore 1 corrisponde ad 1 Volt, mentre in un circuito reale la tensione non rimane fissa ad 1 Volt e scende al di sotto. Questo viene indicato tramite H e stessa cosa vale, in senso opposto per L.
È possibile individuare una funzione di risoluzione che consente di stabilire il valore di un segnale A in tutte le condizioni di B e C nel momento in cui sono definiti come segnali di tipo std_logic:
![[tabstdlog.jpg]]

Infine per utilizzare il tipo std_logic all'interno di VHDL occorre "importare" la libreria IEEE all'inizio del codice tramite:
```VHDL
library IEEE;
use IEEE.std_logic.1164.all;
```

>Se voglio descrivere più entity all'interno di uno stesso file, occorre importare ogni volta la libreria per ogni entity!

---
# Statement process e test bench
Lo statement process è uno statement concorrente. Il process viene normalmente utilizzato per descrivere parti di codice sequenziali nella quale l'ordine di scrittura abbia importanza. Nelle applicazioni che si studieranno questo statement verrà utilizzato per definire la simulazione dei circuiti logici creati. In VHDL la simulazione dei risultati avviene mediante dei datagrammi di timing, che è possibile generare descrivendo le forme d'onda che si immagina abbiano i segnali ad un determinato istante di tempo. Prendiamo come esempio un full adder con le 3 porte d'ingresso: A,B e Cin, consideriamo i seguenti stati:

$\begin{align}
t=0ns \implies A,B,Cin<=\ '0' \\
t=10ns \implies A<=\ '1' \\
t=20ns \implies B<=\ '1' \\ 
t=30ns \implies Cin<=\ '1' \\
t=50ns \implies A,B,Cin<=\ '0'
\end{align}$

![[diagramsig.jpg]]
![[outsigdiag.jpg]]
A livello di codice in VHDL, le forme d'onda si descrivono tramite un particolare tipo di file che prende il nome test bench. Il test bench non è qualcosa di fisico per cui non ha un'interfaccia con il mondo esterno. La sintassi di VHDL impone di usare le entity per cui quando viene creato un test bench viene utilizzata una entity vuota.

---
# Concurrent statement
Il concurrent statement serva a dichiarare ad alto livello delle condizioni. La condizione è un'espressione logica che ad esempio implementano componenti come il multiplexer.
Abbiamo la condizione <font color=blue>with select</font>:
```VHDL
-- with x select a seconda del valore di x
Y <= A when 0 else
	B when 7-9 else
	C when 1 to 5 else 
	0 when others;
```
e abbiamo anche la condizione <font color=blue> when else</font>:
```VHDL
0 <= I0 when sel='00' else
	I1 when sel='01' else
	I2 when sel='10' else
	I3 when sel='11' else
	X;
```

---

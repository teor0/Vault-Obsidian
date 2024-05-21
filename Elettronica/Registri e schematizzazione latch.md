---
tag: #elettronica 
created: 2023-04-20 12:08:03
updated: 2023-04-20 12:08:03
---
#elettronica 
[[Circuiti sequenziali]]
# Registri
Si consideri ora un Ripple carry adder a 16 bit,
![[rcareal.jpg|650x400]]
non è possibile stabilire in modo deterministico quando la somma assume un valore corretto senza utilizzare circuiti sequenziali, perché il ritardo con cui il circuito sommatore risponde alle sollecitazioni degli ingressi non è costante. L'obiettivo è perciò quello di garantire che gli ingressi A e B arrivino contemporaneamente. È necessario che dopo l'arrivo degli ingressi, si attendi un ritardo prima di leggere il risultato. Tale ritardo, è $\tau_d=\tau_{Max}$ dove $\tau_{Max}$ è detto <font color=red>worst case delay</font> e nel caso del ripple carry adder coincide con $16\times \tau_{FA}$, 17 se nel caso di operandi con segno. 
Se ad esempio temporizzo attraverso flip flop, l'arrivo degli ingressi con un fronte di salita e con un altro fronte di salita, la lettura del risultato, allora tra questi 2 eventi consecutivi deve passare un tempo $\tau_d$.

> Usiamo come detto in precedenza circuiti sequenziali per mascherare variazioni inevitabili, date dai ritardi non nulli. La presenza della temporizzazione limita gli effetti negativi, in termini di dissipazione di potenza legati a queste variazioni non volute.

Gruppi di flip flop vengono indicati come registri, che ereditano la simbologgia degli stessi.
La versione corretta del ripple carry adder sarebbe perciò la seguente:
![[wholecircff.jpg]]
Dove come mostrato in figura un registro equivale ad un insieme di flip flop messi in parallelo, caratterizzati da un clock comune. 

## Setup e Hold
Affinché tutto funzioni correttamente bisogna essere sicuri che nel momento in cui arriva il fronte di clock, l'ingresso $D_i$ di un flip flop si trovi in uno stato assestato, affinché questo sia possibile bisogna garantire che la precedente variazione di $D_i$, sia lontana un certo tempo minimo dal successivo fronte di clock.
Ciò è garantito rispettando due tempi:
1. <font color=orange>Tempo di Setup</font>: minor tempo tra l'ultima variazione dell'ingresso ed il fronte attivo del clock. Rappresenta il tempo in cui preventivamente l'ingresso del flip flop deve diventare stabile.
2. <font color=blue>Tempo Hold</font>: minimo tempo intercorso tra il fronte attivo del clock e la successiva variazione dell'ingresso. 

Normalmente $T_{Setup}>>T_{Hold}$
Per comprendere la necessità di questi tempi utilizziamo il seguente diagramma
![[setupnhold.jpg|400x500]]
in questa situazione, essendo il clock un segnale non ideale con $t_r\neq 0$ (tempo di salita), l'evento a cui fare riferimento è tutto il fronte di salita. Durante questo intervallo di tempo D non è stabile. Si ha infatti ambiguità sul valore da campionare in quanto si identificano diversi valori di D. Non si ha certezza di identificare il valore di tensione corretto che rappresenta il valore logico del segnale. Analogo è il discorso se la variazione di D si ha nel tempo di hold.

>[!regola] Lo stato di indeterminazione in questione è rappresentato in VHDL con 'x' ed affinché non si verifichi è necessario che la cadenza con cui al circuito arrivano fronti di salita attivi dipende da $T=t_{wc}+\tau_{setup}$ cioè, quanto tempo prima del fronte debba essere pronto il dato da campionare. Dove $t_{wc}$ è il tempo del worst case delay. 

Il vincolo è facilmente rispettabile data l'informazione nel data sheet.

## Tipi di registri e metastabilità
È possibile identificare 2 tipi di registri:
1. <font color=orange>PIPO: Parallel In Parallel Out</font>, riceve n bit in parallelo producendo in uscita n valore differenti in parallelo. Tipologia vista nell'esempio del ripple carry adder.
2. <font color=green>SIPO: Serial In Parallel Out</font>, riceve un solo bit in ingresso e l'n-esimo flip flop prende in ingresso l'uscita del $n-1$ esimo flip flop. Di seguito la rappresentazione grafica.

![[regsipo.jpg]]

Inizialmente non si credeva fosse possibile determinare in un circuito digitale, un terzo stato stabile si è capito poi, che non rispettando i vincoli di setup e hold si rischia di entrare nello stato di <font color=red>metastabilità</font>, che non corrisponde né a '0' né a '1' logico ma ad uno stato intermedio.

---
# Definizione circuitale del latch
Si consideri il seguente latch positivo
![[schemalatch.jpg]]
la tabella di verità associata sarà:

| Clk | D   | Q(t)            |
| --- | --- | --------------- |
| 0   | 0   | Q(t-$\Delta t$) |
| 0   | 1   | Q(t-$\Delta t$) |
| 1   | 0   | 0               |
| 1   | 1   | 1               |

Analizziamo il funzionamento nel caso specifico $t=0$, $Clk=0$. Essendo il clock basso, questo forza la prima NAND ad essere 1 e la seconda ad essere 0 per qualsiasi valore di D, quindi Q=0 dove la retroazione delle seconde porte NAND elimina la dipendenza da Q evitando qualsiasi variazione non voluta.
Analizziamo il funzionamento quanto $Clk=1$. In questo caso non è possibile definire il comportamento delle prime 2 porte NAND senza tener conto dell'ingresso D. 
Se D=0, A=0 e B=1 quindi alla fine si arriva ad avere come uscita Q=0.
Se D=1, A=1 e B=0 quindi alla fine si arriva ad avere come uscita Q=1.
Di seguito la visualizzazione dei risultati.
![[latchclk1.jpg]]

>[!important] Un latch viene realizzato con 4 porte NAND ed un inverter per un totale di 10 interruttori/transistor.

---
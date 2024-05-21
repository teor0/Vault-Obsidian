---
tags: 
- elettrotecnica
created: 2024-04-12 10:41:42
updated: 2024-04-12 10:41:42
---
[[Concetti fisici d'interesse, modello circuitale, corrente, potenza ed energia]]
# Convenzioni di utilizzatori
In base al componente che si sta valutando, occorre utilizzare la convenzione giusta per stabilire se assorbe o eroga potenza. Si hanno due possibili convenzioni possibili:
![[convenzioni.jpg]]
Gli elementi si differenziano in:
- Elementi attivi, possono generare energia, assorbire potenza ed anche cederla.
- Elementi passivi, non possono generare energia, solo assorbila o scambiarla.

Elementi passivi sono: resistore, condensatore ed induttore.
Elementi attivi sono: generatore di tensione e generatore di corrente.

---
# Componenti
I componenti, (elementi o blocchi) che utilizzeremo saranno
## Resistore
Che viene schematizzato come ![[resistore.jpg|200x100]] La resistività è proporzionale al tratto del conduttore, quindi se ho $\rho$ resistenza a parità di materiale, più è lunga la resistenza più resiste. A parità di materiale, maggiore è la sezione minore è la resistenza.
La resistenza ha come equazione: $R=\rho{l\over A}$ e si misura in Ohm $\Omega$. La conduttanza è il reciproco della resistenza: $G={1\over R}$ e si misura in Siemens $S$.
La potenza di un resistore è calcolata come $P=VI=RI^2=V^2G={V^2\over R}$.
La <font color=red>relazione costitutiva</font> è la legge di Ohm $V=RI$
>[!regola]
>La resistenza è sempre positiva, al più è pari a zero!

## Condensatore 
Il condensatore è schematizzato con ![[condensatore.jpg|200x150]] Il condensatore accumula energia sotto forma di campo elettrico tramite accumulo di cariche. L'equazione della capacità di un condensatore è $\large{C={Q\over V}={\varepsilon A\over d}}$ e si misura in Farad $F$. La relazione costitutiva per il condensatore si ottiene partendo da $Q=CV$ da cui ${dQ\over dt}={d(CV)\over dt}\implies {dQ\over dt}=C{dV\over dt}\implies i(t)=C{dV\over dt}$
$dV={1\over C}i(t)dt\implies V={1\over C}\displaystyle\int^{t}_{t_0}i(t)dt$
L'energia assorbita è pari a: $E_C={1\over 2}CV^2$.

## Induttore
L'induttore è schematizzato come ![[induttore.jpg|200x150]] L'induttore è il duale del condensatore, accumula energia sotto forma di campo magnetico ovvero sotto forma del campo magnetico. L'induttanza mette in relazione il flusso totale concatenato all'avvolgimento con la corrente: $L=\displaystyle{\phi_B\over i}={N^2\mu A\over d}$ e si misura in Henry $H$. La relazione costitutiva per l'induttore si ottiene partendo da: $\phi_B=L\cdot i(t)$ $\phi_B=L\cdot i(t)\implies v(t)={d\phi_B\over dt}=L{di(t)\over dt}$. L'energia immagazzinata dal induttore è $E={1\over 2}Li^2$, la potenza è pari a $p(t)=v(t)\cdot i(t)=L{di(t)\over dt}i(t)$. La variazione della potenza mi dice come la potenza viene assorbita o erogata.

## Generatore di tensione e di corrente 
Un generatore di tensione è fondamentalmente una pila che viene rappresentata come un cerchio con + e - al suo interno mentre un generatore di corrente si indica con un cerchio con dentro una freccia: ![[generatori.jpg|400x300]] La tensione all'interno di un generatore di corrente ha + sulla punta della freccia e - sulla coda della freccia. I generatori che andremo a considerare sono indipendenti, ovvero erogano sempre la stessa quantità di tensione o corrente prestabilita.
Per il generatore di tensione la potenza si calcola come $P_{V_g}=V_gi=(V_A-V_B)i$.
Per il generatore di corrente la potenza si calcola come $P_{I_g}=i_gV$

---
# Corto circuito e circuito aperto
All'interno di un circuito la corrente passa sempre dal collegamento con differenza di potenziale minore, dunque in un circuito del tipo: ![[cc.jpg|400x200]]
la corrente ignora totalmente la resistenza e si ha quindi un <font color=red>corto circuito</font>. La differenza di potenziale tra i due fili sarà pari a 0. 
Per quanto riguarda il circuito aperto, la corrente non passa dunque $i_{AB}=0$ ![[ca.jpg|400x200]]

## Considerazioni notevoli
>[!important] 
Se il generatore di tensione è "spento" si ha un corto circuito!
Se il generatore di corrente è "spento" si ha un circuito aperto!
Se la resistenza è nulla, la tensione è pari a zero dunque si ha un corto circuito.
Se la resistenza è "infinita" si ha un circuito aperto.

Altre considerazioni importanti sono:
- Prese due resistenze, $R_1\ \text{e}\ R_2$, se $R_2>>R_1$ allora $R_2$ si considera come un circuito aperto e tutta la corrente fluirà lungo $R_1$. 
- Prese due resistenze, $R_1\ \text{e}\ R_2$, se $R_2\simeq 0$ allora $R_2$ si considera come un corto circuito e la corrente fluirà lungo $R_2$.
- La relazione costitutiva del induttore impone che $v(t)=L{di(t)\over dt}$ dunque se la corrente è costante (DC), allora si ha un corto circuito perché $v(t)=L{di(t)\over dt}=L\cdot0=0$.
- La relazione costitutiva del condensatore impone che $i(t)=C{dv(t)\over dt}$ dunque se la tensione è costante, allora $i(t)=C{dv(t)\over dt}=C\cdot0=0$ e perciò si ha un circuito aperto.

---
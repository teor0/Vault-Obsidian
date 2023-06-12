---
tag: #elettronica 
created: 2023-02-27 20:13:20
updated: 2023-02-27 20:13:20
---
#elettronica 
[[Soglia, dissipazione dinamica, tempi di risposta e margini di rumore]]
# Circuiti sequenziali
Prima di analizzare il comportamento di circuiti sequenziali è necessario introdurre un segnale molto nei circuiti digitali, ovvero il segnale di clock. Il segnale di clock, è un segnale periodico nel tempo identificato da un'onda quadra. L'attività del segnale di clock va avanti in modo indefinito nel tempo questo perché, in un sistema digitale esiste un componente (on board) specifico per la generazione di questo segnale. Il clock è descritto da un insieme i caratterestiche:
- Periodo (T): tempo che intercorre tra due eventi dello stesso tipo
- Frequenza (f): dipende dal periodo in particolare $f={1\over T}$

![[clock.jpg]]

La differenza principale tra un circuito combinatorio ed un circuito sequenziale è il che, il circuito sequenziale è in grado rispondere a delle sollecitazioni ricevute in ingresso anche in funzione di ciò che è successo in passato. Per materializzare il "prima" e "dopo", è necessario aver conoscenza sullo scorrere del tempo e ciò avviene tramite il clock. Esistono diversi tipi di circuiti sequenziali caratterizzati dalle operazioni che devono svolgere e sono divisi in due diverse categorie:
1. Di supporto ai circuiti combinatori in modo da trattare correttamente l'informazione sul tempo. Il più elementare dal punto di vista logico di circuito è il latch.
2. Destinati alla memorizzazione di grandi quantità di dati.

I circuiti quali flip-flop, latch, data latch ecc vengono utilizzati per memorizzare localmente (on chip) una quantità limitata di dati, mentre la RAM viene utilizzata off chip per memorizzare grande quantità di dati. I flip flop permettono di accedere tutti i bit in qualsiasi momento mentre la RAM può accedere fino ad una data word (64 bit).

---
## Data latch e flip flop
Il data latch serve a memorizzare in prossimità di un circuito combinatorio un bit di dati, ad esempio un operando del circuito sommatore. Il data latch riceve in ingresso il bit da memorizzare <font color=blue>D</font> ed il segnale di clock <font color=orange>Clk</font>, in uscita produce il segnale <font color=red>Q</font>. Il clock serve a creare una relazione appropriata, tra il dato in ingresso ed il dato in uscita, in particolare viene utilizzato per individuare gli istanti di tempo in cui il bit ricevuto in ingresso può effettivamente essere portato in uscita.
Distinguamo 2 tipi di data latch:
![[latch.jpg]]
Dove il latch positivo, trasferisce il dato in uscita quando Clk=1 mentre il latch negativo trasferisce il dato in uscita quando Clk=0. Gli stati di funzionamento del latch si identificano con latch aperto e latch chiuso. Proprio durante la chiusura del latch che viene attivata la funzione di memorizzazione.

> Quando non si verificano le condizioni richieste D risulta invisibile dall'uscita Q.

Come mostra il seguente diagramma di timing, le variazioni di Q possono essere legate sia al clock che al valore di D.
![[diagtlatch.jpg|650x200]]

Il flip flop consente di discriminare eventi diversi sul segnale di clock, ovvero consente di individuare i fronti sul segnale di clock e quindi specificare eventi molto più particolari. 
![[flipflop.jpg|150x500]]

Anche il flip flop è suddiviso in "positivo" e "negativo", in particolare un flip flop positivo si traduce in uno sensibile a fronti di salita, mentre un flip flop negativo è sensibile a fronti di discesa.

Dato il seguente diagramma di timing ideale, un flip flop positivo, trasferisce il valore in ingresso sull'uscita, solo quando è presente un fronte di salita sul clock.
![[diagtff.jpg|500x250]]
L'andamento del segnale Q viene sincronizzato agli eventi del segnale di clock, questo consente di scandire con precisione quali sono i dati che si vogliono fare arrivare in ingresso ai circuiti. 

>Questa operazione viene detta temporizzazione.

---
## Glitch ed impiego dei circuiti sequenziali
Supponiamo di avere il seguente circuito logico, dove indichiamo con $\tau'$ il ritardo degli inverter e $\tau$ il ritardo del AND, sapendo che $\tau>\tau'$ data la composizione della porta AND. Andiamo perciò ad osservare il comportamento del circuito tenendo conto di tali ritardi.
![[excircseq.jpg]]
![[excircseqdiag.jpg]]
Non tenendo conto dei ritardi ci si aspetta che y=0 ad ogni istante di tempo, in quanto il passaggio di stato $0\rightarrow 1\rightarrow 0$ avviene nello stesso instante e di conseguenza non viene percepito. Il ritardo della AND provoca però la variazione di stato sulla y, questo fenomeno è chiamato <font color=red>glitch/spike</font> ed è una commutazione inaspettata dal punto di vista logico. Per limitare gli effetti del glitch è necessario che la temporizzazione di y, sia fatta in modo da evitare i ritardi delle porte logiche, per fare ciò si sincronizzazno A,B e y ai fronti di salita del clock. 
L'uso dei flip flop, consente di specificare gli istanti di tempo in cui ogni elemento circuitale deve tenere in considerazione gli ingressi ricevuti, mascherando così i glitch.
Andiamo a risolvere il glitch del circuito.
![[glickrisolto.jpg]]
Affinché il circuito funzioni correttamente, tra l'istante di tempo in cui gli ingressi sono validi e l'istante di tempo in cui y è valida, deve passare un tempo pari a $T=\tau +\tau'$ tra un fronte di salita ed un altro, in questo modo sarà possibile mascherare gli eventuali glitch.
![[diagtglitchok.jpg|400x400]]

> Si noti come tra $t_1$ e $t_3$ il valore di y è '0' nonostante il glitch prensente tra $t_2$ e $t_2+\tau$.

L'uso dei circuiti sequenziali assieme a quelli combinatori consentono di ridurre gli effetti legati alle commutazioni dei segnali.

---


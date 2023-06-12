---
tag: #elettronica 
created: 2023-04-21 11:54:11
updated: 2023-04-21 11:54:11
---
#elettronica 
[[Registri e schematizzazione latch]]
# Flip flop master-slave negativo, preset e clear
Un flip flop master-slave viene realizzato collegando in cascata due latch,
![[ffmasterslave.jpg]]
il principio con cui lavora il master-slave è il seguente: si utilizza un primo latch positivo ed un secondo latch negativo, dove mentre il 1° latch è aperto il 2° è chiuso e viceversa.
Osservando il suo funzionamento come macroblocco, corrisponde ad un flip flop sensibile a fronti di discesa. Di conseguenza, un flip flop master-slave composta da latch negativo come master e latch positivo come slave, corrisponderà ad un flip flop sensibile a fronti di salita. 
Il diagramma di timing ideale del master-slave negativo è il seguente:
![[timingffms.jpg]]
Da notare che a $t=0$, $Q=0$ in quanto si vuole sempre avere uno stato iniziale preciso quando si utilizzano circuiti sequenziali. A questo scopo vengono in aiuto dei segnali ausiliari, asincroni e prioritari che consento di forzare l'uscita dei circuiti sequenziali a '0' o '1'.
![[ffprcr.jpg|400x400]]
I due non possono essere contemporaneamente attivi, in quanto porterebbero ad un valore di uscita indeterminato. Per evitare questa situazione, nelle impostazioni vengono descritte delle priorità in modo da non aver problemi anche in caso di conflitto tra due segnali. In particolare:
- Quando $Pr=1$: $Cr=0$, $Q=1$ qualsiasi siano D e Clk.
- Quando $Cr=1$: $Pr=0$, $Q=0$ qualsiasi siano D e Clk.

La cancellazione dell'uscita con $Cr=1$ porta alla dicitura clear attivo alto, come nella schematizzazione precedente.
La cancellazione dell'uscita con $Cr=0$ porta alla dicitura clear attivo basso, con la schematizzazione del clear con un pallino.
![[ffcrneg.jpg|500x400]]
Stesso discorso vale per il preset.
## Costo flip flop master-slave
Nel master-slave negativo, il master ha le prime 2 NAND con 3 ingressi in quanto nel circuito è compresa una doppia retroazione. Imponendo che i latch siano uguali per realizzare un master-slave occorrono 36 interruttori/transistor.
Considerando lo schema logico del master-slave:
- Quando $Clk=0$: master OFF, slave ON
- Quando $Clk=1$: master ON, slave OFF

Sia latch che flip flop possono essere realizzati tramite porte NOR con stesso costo.

---
# Pipeline
Utilizzare circuiti paralleli è il modo più semplice per velocizzare le cose. Facciamo un esempio: 
Dati $n$ utenti che devono realizzare un progetto Vivado ciascuno, se ogni utente è dotato di un PC si ha la situazione più semplice per velocizzare il completamento della task. Questa però ha un certo costo, in quanto ogni utente necessita per l'appunto di un PC.
Una soluzione alternativa può essere quella di dividere il lavoro degli utenti impiegando $n$ PC. Ogni PC ha un tempo max di utilizzo da parte di un singolo utente ed è caratterizzato da un particolare scopo. La somma dei tempi a disposizione è di $y$ minuti. Si consideri un esempio pratico con 3 PC, con 100 minuti max disponibili e 5 utenti: Piero, Mario, Anna, Marco e Luigi.
![[tabpipe.jpg]]
Gli utenti spostano i dati tramite penna USB tra un PC e l'altro. A $t=70$ ogni PC fa riferimento ad un utente diverso ed il sistema sta avendo un parallelismo di 3. Per svolgere il progetto:
- Piero impiega 100 min
- Mario impiega 100+30+10 min
- Anna impiega 100+30+30+20 min

>I tempi in cui i PC lavorano ma non producono alcun risultato utili,  è detto <font color=red>latenza</font> (100 min).
>Il ritmo con cui vengono prodotti i risultati dopo la latenza si chiama <font color=red>throug put</font> (40 min).

Non si raggiunge la prestazione della relazione parallela, ma si garantisce una velocità intermedia che può essere aumentata aumentando il numero di postazioni. Questa modalità di utilizzo delle risorse viene implementata per realizzare circuiti abbastanza veloci ma non eccessivamente costosi. I circuiti <font color=blue>pipeline</font> implementano in elettronica il concetto appena visto, utilizzando dei registri (penna USB) per introdurre degli step di elaborazione intermedi che producono un risultato valido.

## Esempio circuitale
![[pipelinex.jpg]]
Consideriamo il seguente circuito sommatore che riceve in ingresso 3 sequenze di $k$ valore a $n$ bit, quindi A(i) è un numero a $n$ bit.
I primi 3 registri consentono al clock di sincronizzare gli ingressi. Il primo sommatore genera il risultato tra A(i) e B(i) dopo $t=T_s1$. Una volta prodotto il risultato, il secondo sommatore produrrà il suo risultato con ritardo $t=T_s2$.
Se non inserisco il pipeline, la terna di operandi deve avere a disposizione $t=T_s1+T_s2$ per essere processata e solo dopo potrà arrivare un'altra. Essendo il clock ricevuto da tutti i registri, al secondo fronte di clock $t=t_1$ la somma A(0)+B(0)+C(0) viene portata fuori e contemporaneamente entra la terna A(1),B(1),C(1). Questa situazione verrà ripetuta $n$ volte, si avrà perciò la seguente tabella:
![[tabexpipe.jpg]]
Il primo ciclo di clock non produce alcun risultato e sarà pari a $T_{clk}=T_s1+T_s2+T_{reg}$ ed il tempo totale per processare  i$k$ valori delle sequenze in ingresso è $T_{tot}=(k+1)*T_{clk}$.

Il circuito può essere reso più efficiente attraverso il pipeline, inserendo un registro intermedio sul canale di C, in modo da sincronizzarlo con il primo sommatore:
![[realpipeline.jpg]]
così facendo dopo i primi 2 colpi di clock senza risultati validi, si ottiene un risultato ciclicamento dopo un intervallo di tempo pari a $T_{clk}=Max(T_s1+T_{reg},T_s2+T_{reg}$ inferiore al clock precedente per cui il circuito è più efficiente, inoltre il tempo totale per processare i$k$ valori delle sequenze in ingresso è $T_{tot}=(k+2)*T_{clk}$ . Da notare che se non ci fosse il registro intermedio su C, il secondo sommatore darebbe risultati errati SEMPRE.
![[tabrealpipe.jpg]]
> La latenza aumenta con il frazionamento del circuito. Dati $k$ registri la latenza di un circuito è $k-1$

La latenza quindi è formalmente definita come: il numero di cicli di clock che devo aspettare, per avere il primo risultato corretto.
Il throug-put in entrambi gli esempio è pari ad 1, in quanto si produce un risultato per ogni ciclo di clock.

---


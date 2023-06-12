---
tag: #elettronica 
created: 2023-02-17 18:34:56
updated: 2023-02-17 18:34:56
---
#elettronica 
[[Simulazioni, fase di sintesi, lookup table e fase d'implementazione]]
#  Approccio progettuale
Le specifiche di progetto comprendono la funzione logica desiderata e le caratteristiche del circuito. Il progettista può lavorare alla progettazione di un circuito con due approcci:
1. Full custom: Il progettista mette le mani su tutti i livelli circuitali ed a tutti gli elementi di progettazione. È l'approccio più complesso, poiché occorre conoscere la fisica e la matematica dei dispositivi elettronici, usare software di supporto costosi e hardware per la realizzazione. I circuiti sono realizzati in silicio, si parte da silicio puro che poi attraverso processi fisico-chimici verrà modificando diventando un buon conduttore/isolante.
2. Semi custom: Il progettista utilizza una serie di elementi detti standard cells che progettisti a livello full custom hanno realizzato. Anche questo approccio richiede uso di software proprietario e l'acquisto di silicio. Oltre alla progettazione standard cells si può ricorrere alla progettazione basata su array. I chip FPGAs usano una struttura matriciale composta da LOT, basata su array.
   Questa categoria si divide in: 
   - Mask programmable: si acquista un chip FPGA e lo si utilizza per eseguire una certa funzione logica, non può però essere riutilizzato/riprogrammato una volta caratterizzato dalla funzione logica
   - Pre wired: utilizzo di circuiti riprogrammabili una volta tolta la corrente.

I circuiti progettati fino ad ora sono semi custom basati su array.

---
# Mosfet
Il primo passo per entrare nel mondo full custom è quello di individuare a livello circuitale un componente che si presti bene a rappresentare l'informazione digitale, ovvero il bit. Esistono diversi tipi di dispositivi digitali quali:
- Il <font color=orange>diodo</font>: lavora in 2 modalità ON e OFF, dove ON conduce la corrente ed è polarizzato direttamente, OFF non conduce corrente ed è polarizzato inversamente. Questi 2 stati di polarizzazione possono facilemente rappresentare i bit 0 e 1.
- Il <font color=orange>transistor</font>: di ci sono 3 tipi, il transistore a giunzione bipolare (BFT), il transistore ad effetto di campo (FET) ed il transistore ad effetto di campo basato su una giunzione di metallo (MOSFET).

Il <font color=blue>MOSFET</font> può essere utilizzato sia per applicazioni analogiche in cui si comporta come amplificatore di tensione o corrente, sia in applicazioni digitali dove può assumere anche il ruolo di interruttore che lavora a 2 stati, ON e OFF. Per lavorare bene il MOSFET ha bisogno di sfruttare tutte e tre le sue proprietà ovvero, metallo (conduttore), ossido (isolante) e semiconduttore. Graficamente gli interruttori sono schematizzati come segue:
![[interruttori.jpg]]
In particolare :
- Quando un interruttore è OFF si ha: tensione massima e corrente pari a 0.
- Quando un interruttore è ON si ha: tensione pari a 0 e corrente massima.

I circuiti visti fino ad ora sono un gruppo di interruttori collegati opportunamente tra loro.

---
# Famiglia logica
La famiglia logica dipende da come i transistor sono disposti e collegati all'interno delle porte logiche utilizzate. Esistono varie famiglie logiche ognuna con le proprie regole, tra cui:
- <font color=green>Statica CMOS</font>
- <font color=green>Statica NMOS</font>
- <font color=green>Dinamica CMOS</font>
- <font color=green>Dinamica dual-rail</font>


La famiglia logica più utilizzata in commercio è la Statica CMOS, dove CMOS sta per "Complementary Metal Oxide Semiconductor". Complementary indica che all'interno dei circuiti è necessario utilizzare 2 tipologie di interruttori (transistor) che hanno un funzionamento duale tra loro: 
- Tipo 1: segnale di controllo '1'=ON, segnale di controllo '0' =OFF.
- Tipo 0: segnale di controllo '1'=OFF, segnale di controllo '0' =ON.

All'inizio abbiamo scelto di lavorare in logica positiva, ovvero 1 indica la tensione di alimentazione `VDD(Valim)='1'` cosi come `GND(0V)='0'`. All'interno di qualsiasi circuito digitale i primi due elementi circuitali a cui fare riferimento sono la tensione di alimentazione e la messa a terra. L'uscita di un qualsiasi circuito digitale non è altro che il risultato di un collegamento a $V_{DD}$ nel caso in cui l'uscita sia pari a 1 oppure a GND nel caso in cui l'uscita sia pari a 0. 

---
#fondamenti 
[[Prime definizioni - Reti, tipi di commutazione e configurazione dei canali]]
## Modi trasmissivi

I modi trasmissivi dei canali sono di 3 tipi:

- <font color=red> Simplex</font>: un server che comunica al PC
- <font color=red> Half-duplex</font>: la comunicazione può avvenire in due sensi ma ad istanti di tempo diversi
- <font color=red> Full-duplex</font>: la comunicazione può avvenire in entrambi i sensi in contemporanea

---
## Topologia di rete

Prima di parlare di topologia di rete, diamo una prima definizione di rete di telecomunicazione. 
>[!Rete di telecomunicazione]
>Una rete di telecomunicazione è un insieme di nodi e canali che fornisce un collegamento tra 2 o più punti, per permettere la telecomunicazione tra essi.

^22c851

> Si chiama nodo un punto in cui avviene la commutazione

> Si chiama canale un mezzo di trasmissione

La disposizione dei nodi e canali fornisce la <font color=red> topologia</font> di rete, inoltre bisogna distinguere topologia fisica dalla topologia logica, che definisce l'interconnesione tra nodi mediate canali ovvero, come 2 nodi comunicano tra loro.

>Legenda: rettangolo: dispositivo intermedio, cerchio: end-device

Esempio topologia logica rispetto alla topologia fisica di sopra

![[pics/fisica.png]]


![[pics/logica.png]]

---
### Topologia a maglia completamente connessa

![[magliacompleta.png]]

Quanti sono il numero di collegamenti (canali) di una maglia complessa? La sommatoria degenera in $C=\Large{n(n-1)\over2}$ che è nota

- Vantaggio: tolleranza di guasti (molti percorsi alternativi)
- Svantaggio: elevato numero di canali e molto spreco di risorse ma anche controllo complesso.

> È usata quando i nodi sono pochi

---
### Topologia ad albero

![[pics/albero.png]]

Numero di collegamenti: $C=n-1$

- Vantaggio: basso numero di canali
- Svantaggio: vulnerabilità ai guasti

> È usata per ridurre i costi e semplificare la stesura dei canali


---

### Topologia a maglia non completamente connessa

![[maglianoncom.png]]

Numero di collegamenti: $\Large n-1<C<{n(n-1)\over 2}$

- Vantaggio: tolleranza ai guasti e numero di canali selezionabili a piacere tali da disporre di cammini alternativi tra 2 nodi
- Svantaggio: topologia non regolare, commutazione più complessa per il calcolo dell'instradamento

> È la più usata!

---
### Topologia a stella

![[pics/stella.jpg]]

Numero di collegamenti: $C=n$

- Vantaggio: basso numero di canali e commutazione semplice dal punto di vista dei nodi
- Svantaggi: vulnerabilità ai guasti del nodo centrale (attivo o passivo) per attivo si intende che il nodo centrale rigenera il segnale e lo ritrasmette

> È usata per ridurre i costi e semplificare la stesura dei canali
>

Un esempio sono le reti telefoniche tradizionali, reti radio e satellitari.

---
### Topologia ad anello

![[pics/anello.jpg]]

La topologia ad anello può essere unidirezionale o bidirezionale.

Numero di collegamenti: $C=n$

- Vantaggio: commutazione semplice
- Svantaggio: vulnerabilità ai guasti. Nel caso di anello unidirezionale si interrompe la rete, nel caso bidirezionale si riconfigura.

> L'anello bidirezionale è la più semplice topologia che consente un instradamento alternatvio in caso di guasto
>

La topologia ad anello è molto usata in reti locali e metropolitane

---
### Topologia a bus

![[pics/bus.jpg]]

Il bus (broadcast) può essere attivo o passivo. Nel bus attivo, ogni nodo rimanda il segnale al prossimo che lo rigenera lo pulisce e lo ritrasmette

Numero collegamenti: $C=n-1$ (attivo) $C=n$ (passivo)

Molto usato il bus passivo in reti locali e metropolitane

---

### Topologia ibrida o mista

Si mischiano più topologie insieme. Internet ha topologia ibrida ma anche una struttura gerarchica per gestire e fare manutenzione.

In Internet si hanno reti di vario genere, ad esempio:

- LAN (local area network)
- MAN (metropolitan area network)
- WAN (wide area network)

che hanno mezzi trasmissivi e tecnologie diverse. 
Internet è una rete di reti che permette la connessione tra dispositivi terminali che possono essere host o end-system, che eseguono le applicazioni di rete. Abbiamo link di comunicazione quali, fibra, rame ecc. ed infine abbiamo dispositivi di rete che inoltrano pacchetti dati attraverso la rete.

---

#fondamenti 
[[Protocolli ALOHA]]
# Definizione e prestazioni
Il CSMA (carrier sensing multiple access) deriva dal ALOHA con l'aggiunta del feedback che riguarda l'occupazione del canale. Lo strumento che rileva ciò è il carrier sensing, il CSMA ascolta prima di trasmettere. Abbiamo 2 tipi di CSMA:
1. CSMA persistente, che riprova ad ascoltare dopo una probabilità P.
2. CSMA non persistente, che riprova dopo un tempo random.

A causa dei ritardi di propagazione il protocollo, non evita le collisioni. Le collisioni avvengono quando due stazioni accedono al canale in istanti che distano tra loro un tempo inferiore a quello di propagazione tra le 2 stazioni. L'intervallo di vulnerabilità è $\large\tau$, il tempo necessario per garantire che prima di trasmettere non ci siano collisioni è 2$\large \tau$.
Il CSMA persistente possiamo suddividerlo in:
- 1-persistente: la stazione ascolta finché il canale è libero e poi trasmette con probabilità.
- p-persistente: la stazione aspetta finché il canale è libero e quindi trasmette con probabilità p, oppure con probabilità 1-p ritarda la trasmissione di un tempo casuale.
- CSMA/CD: interrompe la trasmissione appena si accorge di una collisione.

---
## Fasi CSMA e performance
1. Rilevazione portante (sensing)
2. se canale idle si trasmette il frame 
3. altrimenti ritrasmette dopo un tempo casuale e goto 1

Per le prestazioni si assuma lo stesso modello dell'ALOHA con: T tempo di trasmissione del pacchetto, $\large\tau$ tempo di propagazione e $\displaystyle\large a={\tau\over T}$. Il throughput per il CSMA è pari a: 
$S= \displaystyle\large {Ge^{-aG}\over G(1+2a)+e^{-aG}}$
dove il numeratore è il traffico utile ed il denominatore è il traffico totale.

Per ALOHA è $\large S=Ge^{-2aG}$, per slotted ALOHA è $\large S=Ge^{-aG}$
2aG è la frazione di traffico inviata in 2$\large\tau$ $\large e^{-aG}$ è la trasmissione di un frame con successo. Con il CSMA/CD si aggiunge la collision detection (CD). Il CSMA/CD continua a rilevare il canale mentre trasmette dopo aver percepito la collisione interrompe la trasmissione in atto del frame. ![[csmacd.png]]
Con:
- $\large\tau$ tempo di propagazione
- $T_1$ tempo di rilevazione collisione
- $T_2$ tempo di permanenza nello stato di collisione

$T_{tot}=2\tau + T_1+T_2$ tempo totale per consentire ad A di percerpire la collisione. Sia $T_2$ trascurabile, allora $\large L_{min}=(2\tau + T_2)R$ con R capacità del canale. $L_{min}$ è la lunchezza minima tale che la collision detection funzioni. Performance del CSMA/CD:
$\displaystyle\large S={Ge^{-aG}\over G(1+2a)+e^{-aG}-G(1-\delta)(1-e^{-aG})}$ 
dove:
- $\large\delta$ tempo per accorgersi della collisione
- $\large (1-\delta)$ tempo rimanente dopo la rilevazione della collisione
- $\large (1-e^{-aG})$ probabilità di collisione
- $\large G(1-\delta)(1-e^{-aG})$ frame che ci risparmiamo di inviare grazie alla rilevazione della collisione

---
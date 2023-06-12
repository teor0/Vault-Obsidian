#fondamenti 
[[Framing e codici controllo e recupero di errori]]
# Protocollo continuos ARQ
Come miglioria rispetto allo [[Diagramma di timing, protocollo stop n wait e calcolo efficienza#^2a22b8|Stop & wait]], l'idea del continuos ARQ è che si possono trasmette n frame senza attendere per ognuno di essi un riscontro.
La logica è quella di tenere il canale più occupato rispetto stop & wait invece di attendere sempre per ogni frame. Si usa una "finestra" per esprimere il numero massimo di frame senza ottenere un riscontro.
Questo protocollo presuppone canali full-duplex.
![[continuosarq.png]]
Sia la finestra w=4, quando arriva 1 supponiamo che parta il riscontro di 0. Arrivato il riscontro passo mandare il frame 4. A secondo dello "scorrimento" della finestra ho più o meno efficienza. Nel caso in cui si riceve un NACK, il protocollo ha due possibili strategie per continuare la trasmissione:
- Go back n
- Selective repeat

## Go back n
![[gobackn.png]]
Nel Go back n la sorgente ha una bufferizzazione mentre la destinazione conserva l'ultimo frame ricevuto correttamente e gli altri frame li scarta. 4 non lo conserva in quanto la sequenza essendo sbagliata necessita di 1, 2 e 3. Questo protocollo lato ricevente non accetta buchi nella sequenza in quanto non si conserva i dati. Il Go back n si usa su canali con alto tasso di errore, l'enumerazione è vitale nel Go back n ma come gestirla? 
Se la window è in trasmissione è w=n e indichiamo con M il numero di bit per numerare (numero di sequenza) i frame si deve verificare che:
$2^M>n$
se w=4 M=3 per soddisfare la disequazione.

### Efficienza Go back n
Assunzioni semplificazione, per costruire un modello di analisi d'efficienza:
1. Trascuriamo il tempo che intercorre tra immissione in linea di un frame e di quello successivo.
2. Scegliamo una lunghezza w tale che appena la sorgente termina d'inviare il suo ultimo frame consentito nella finestra arrivi il riscontro del primo frame trasmesso.
3. Il timeout scelto è uguale al tempo minimo necessario ad ottenere il riscontro del primo pacchetto.

Nessuna ritrasmissione $\Rightarrow t_F$ 
1 $\Rightarrow t_F+1(t_F+t_{out})$
2 $\Rightarrow t_F+2(t_F+t_{out})$
n $\Rightarrow t_F+n(t_F+t_{out})$
$\displaystyle\large E={t_F\over E[t_{tot}]}={t_F\over E[t_F+n_R(t_F+t{out})]}={t_F\over t_F+E[n_R](t_F+t_{out})}$
ricordanci che $E[n_R]={p\over 1-p}$ si ha:
$\displaystyle\large E={t_F\over t_F+{p\over 1-p}(t_F+t_{out})}={1\over 1+{p\over 1-p}(1+{t_{out}\over t_F})}={1-p \over 1+p{t_{out}\over t_F}}$

fissiamo $\large t_{out}=2\tau +\tau_E+ t_R\Rightarrow$ $\displaystyle\large E={1-p\over 1+p({2\tau+2t_E+t_R\over t_F})}={1-p\over 1+p {2\tau\over t_F}}$ se trascuro anche qui $t_E$ e $t_R$

$\displaystyle\large E={1-p\over 1+2ap}$ se il canale è ideale ovvero p=0 allora E=1.

---

## Selective repeat
Complica di più le informazioni al ricevitore. Per i frame fuori sequenza indica al trasmettitore l'ack del frame corrotto.
![[selectiverepeat.png]]
Non perdo la memorizzazione di 2 e 3. Serve quindi un buffer ed un meccanismo di riordinamento dei frame, ideale per errori isolati o canali con alta affidabilità.

---
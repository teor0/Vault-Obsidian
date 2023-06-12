#fondamenti 
[[Comunicazione e protocolli di comunicazione]]
# Definizione e prestazioni
Il protocollo ALOHA è noto per comunicazioni satelittari, ogni utente accede al sistema non appena ha dati da trasmettere una volta condiviso il frame la stazione, si mette in ascolto del ACK, se non lo riceve ritrasmette. Quindi si attende un tempo casuale prima di ritrasmettere.
Per valutare le prestazioni si usa:
- <font color=red> throughput</font>: quantità di dati utili mandati
- <font color=red> ritardo medio per pacchetto</font>

Il protocollo è il più semplice e fa a meno di ogni forma di coordinamento tra le stazioni. Necessita solo del riscontro di ricezione. Regole:
- i pacchetti nuovi sono trasmessi subito
- i pacchetti collisi vengono ritrasmessi dopo un tempo casuale

Casuale perché se è fisso, c'è la possibilità di avere collisioni infinite. Le collisioni hanno una finestra temporale in cui possono avvenire, tale finestra si chiama intervallo di vulnerabilità V. V è pari a 2T dove T è la durata del pacchetto.

Prestazioni:
Consideriamo $\lambda$ come numero medio di arrivi con distribuzione di Poisson. Se moltiplichiamo $\lambda$ per T, otteniamo il numero di pacchetti che inviamo sul canale nell'intervallo T,  tale numero prende il nome di traffico normalizzato G che è pari a G=$\lambda T$. G contiene sia pacchetti trasmessi più volte sia pacchetti trasmessi una sola volta. Quindi durante l'intervallo di vulnerabilità nessuna altra stazione deve trasmettere oltre quella che deve.

Il numero di pacchetti senza ritrasmissioni è $\large S=Ge^{-2G}$ tale valore prende il nome di throughput e $0<S<1$. Prendiamo il valore massimo è <font color=red> $\displaystyle\large S_{max}={1\over 2e}=$ 0,1839 </font>Erlang, quindi il 18,39% di trasmissioni con successo immediato. 

---
## Slotted ALOHA
Per migliorare ALOHA si usano slot di tempo casuale che riducono l'intervallo di vulnerabilità, si passa quindi allo slotted ALOHA. Lo slotted ALOHA, divide il tempo in time slot uguali di lunghezza pari alla durata T di un pacchetto. Dopo una collisione la stazione prova a ritrasmettere un pacchetto dopo un numero di slot scelto uniformemente, tra 0 e $\Large 2^{Min(k,max)}$ dove k è il numero di collisioni già subite dal pacchetto e max è la massima dimensione dell'intervallo.

L'intervallo di vulnerabilità passa da 2T a T e la probabilità di successo passa a $\large S=Ge^{-G}$ con $G_{max}=1$ e $\displaystyle\large S_{max}={1\over e}=0,3679$ Erlang cioè il 36,79% di successo, ma sempre poco. Da qui nasce il CSMA.

---
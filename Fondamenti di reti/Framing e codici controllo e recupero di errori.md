#fondamenti 
[[Livello Data Link nello specifico]]
[[Comunicazione e protocolli di comunicazione]]
# Framing
Quando parliamo di struttura a frame o trame si parla anche di suddivisione di trame in informazioni di controllo ed informazioni utili. L'inizio e la fine di un frame è stabilito da una sequenza di bit. Ma perché dividere il flusso in trame? 
Data la complessità della rete, siamo costretti a mandare i dati suddivisi e non in blocchi enormi. Suddividendo in trame c'è un controllo d'errore sulla singola trama, cosicché se ci sono errori in sequenze di bit, riesco a porre rimedio. Le trame, le posso indirizzare e numerare cosicché posso capire quale trama ritrasmettere o come ricostruire le trame tramite:
- bit speciali (flag)
- violazioni di codice di linea
- temporizzazione (richiede elevata sincronizzazione)
- conteggio dei caratteri o dei bit

Esempio di uso di flag
HDLC (High Data Link Control) usa una sequenza di 8 bit all'inizio ed alla fine di una trama. 
Un altro modo è utilizzare il bit stuffing, ovvero pattern di bit che vengono usati come flag per l'inizio e la fine in modo fittizio. 

È fondamentale rilevare gli errori, i livelli che rilevano o correggono gli errori oltre al livello collegamento sono il livello trasporto ed il livello fisico. La rilevazione del livello di trasporto è più di "alto livello" cioè devo ritrasmettere i pacchetti. In base alla codifica si hanno probabilità d'errore diversi.

---

# Controllo e recupero di errori
Ci sono 2 macrocategorie di codici per rilevare e correggere gli errori, sono i codici FEC e ARQ.

I codici <font color=red> FEC (Forward error correction)</font> sono a correzione di errore, quindi irrobustiscono il segnale. Questi codici fanno parte dei codici per la codifica di canale che serve appunto a mantenere una robustezza elevata attraverso una ridondanza. Se utilizziamo un codice a ripetizione dove ripeto N volte lo stesso bit, ho una capacità di correzzione di $\Large{\lfloor {N\over 2}-1\rfloor}$

I codici <font color=red> ARQ (Automatic Repeat Request) </font>sono interessati a verificare se i bit sono stati manipolati o meno. Questo avviene tramite FCS (Frame Check Sequence), se il ricevitore capisce che non è corretto qualcosa avviene la ritrasmissione.

Un tipo di codice per rilevare gli errori è il codice a parità, dove si somma in modulo 2 i bit consecutivi ed alla fine si aggiunge un bit di parità. Se il numero totale di 1 è pari si ha una parità pari altrimenti dispari. Esistono anche codici di parità a bidimensioni e n-dimensioni. Esempio codice di ripetizione:
![[codripet.png| Frame=101101 Tx=trasmettitore Rx=ricevitore]]
![[coderdecoder.png]]
È come se Tx passa dati ad un coder. Si usa una ricezione a maggioranza, cioè ogni 3 bit vedo quale compare più volte, se l'errore è singolo si riesce a correggere, se è doppio bisogna ritrasmettere. Il decoder è capace solo di rilevare singolo o doppio errore. Se uso un decoder a R5 posso correggere fino a 3 errori e cosi via, solo che più aumenta R più banda si va a togliere. Ad esempio con R5 uso un quinto della banda. 
I codici FEC sono una buona scelta se la distanza alta.
![[codicefec.png| Vt=velocità di trasmissione o data rate Vp=velocità di propagazione, dipende dalle caratteristiche fisico chimiche del mezzo]]
Il tempo di propagazione è dato da: $\Large{\tau_P={d(m)\over V_p(m/s)}=\tau_P(s)}$. Vt dipende dal mezzo e dalla codifica utilizzata. Il tempo di trasmissione è dato da: $\large{\tau_t=frame lenght/V_t}$. Il tempo per mandare il frame da Tx a Rx è dato da $\large T=\tau_t+\tau_P$. Si considera Vp=3x$10^8$m/s ovvero la velocità della luce nel vuoto.

---



---
created: 2022-10-10 10:19:00
---
#elettronica
# Definizioni
Andiamo a trattare l'elettronica in quanto studiamo ciò che ha a che fare con gli elettroni che stanno nei dispositivi fatti in silicio.
Quando parliamo di elettronica digitale, ci riferiamo al trattamento elettronico di segnali digitali binari, cioè segnali che assumono solo due valori. Gli stati di un sistema binario sono rappresentati da due simboli, 1 per alto e 0 per basso. I due stati logici generalmente corrispondono a due tensioni diverse che rappresentano alto e basso.
Per digitale significa che una grandezza può assumere solo un numero discreto di valori all'interno di un range prefissato, finito. Dove discreto si intende che, se prendiamo la misura della temperatura della stanza con un termometro digitale e, la misura è 35°C, mentre magari la misura reale è 35.12°C.
Vantaggi dei sistemi digitali sono: la precisione, la flessibilità e la possibilità di realizzare grandi moli di operazioni algebriche.

---
# Step necessari per iniziare a lavorare con la tensione
Essendo che andremo a lavorare con informazioni rappresentati da tensione dobbiamo compiere degli step prima di lavorare effettivamente.
Il primo step consiste nel campionamento del segnale, che avviene ad intervalli regolari ottenendo appunto i campioni.
![[campionamento.jpg]]
$\Delta t$ è il periodo di campionamento $T_c$, dove il reciproco è la frequenza di campionamento $\displaystyle\large f_c={1\over T_c}$. Se $T_c$ è sufficientemente piccolo, il segnale di partenza può essere ricostruito a partire da quello campionato.
Il secondo step consiste nella quantizzazione
![[quantizzazione.jpg]]
Una volta campionato il segnale è più facile da trasmettere per la facilità di associazione con la differenza di potenziale ovvero la tensione.
Se aumentiamo gli intervalli di quantizzazione abbiamo una migliore definizione ma una quantità di dati maggiore.
![[quantizzazione2.jpg]]
In questo esempio la quantizzazione passa da 1 a 2 bit.

---
## Segnale digitale reale
![[segnalidigitalireali.jpg]]
I segnali digitali reali ovviamente ha un tempo di salita e di scesa non nulli, quando il valore di tensione cambia da alto a basso.

---
# Logica per la rappresentazione della tensione
La logica che è utilizzata per rappresentare la tensione è logica positiva, dove 1 logico corrisponde al valore di tensione più alto mentre lo 0 logico corrisponde al valore di tensione più basso. La logica che si utilizza all'interno del corso è binaria.
Le operazioni logiche elementari sono:
- AND (rappresentata da un punto)
- OR (rappresentata da un più)
- NOT (rappresentata tramite una linea sopra)
- NAND
- XOR
- NOR 
- XNOR

Ma quali sono le più semplici? Possiamo dire che l'ordine di semplicità è:
1. NOT
2. AND OR e XOR
3. NAND NOR e XNOR

Ma vedremo in futuro che non è cosi dal punto di vista elettronico.
![[portelogiche.jpg]]
![[tabelle_verita.jpg]]
Il numero di ingressi in una porta logica è rappresentata dal parametro _Fan-in_ e questo parametro imposta anche il limite che offre la tecnologia. In commercio si ha che le porte logiche hanno _Fan-in_ pari a 2. Si capisce quindi che per realizzare porte logiche con _Fan-in_ maggiore rispetto a quello che la tecnologia fornisce, bisogna utilizzare un insieme di porte logiche dello stesso tipo.
Per complessità di una porta, si intende il numero di transistori per realizzare una porta logica.

Una porta logica è un circuito usato per realizzare in hardware una funzione logica elementare.
Le reti combinatorie sono composte da un insieme di porte logiche collegate tra di loro che consentono di realizzare in hardware una funzione logica complessa.
![[esempioretecom.jpg]]
Dove l'output di questa rete sarà=$A\land B + B\land C + A\land C$.

---

# Multiplexer e demultiplexer
Un multiplexer è un circuito logico che consente di selezionare 1 tra $2^n$ ingressi in base allo stato di $n$ segnali di controllo.
![[multiplexer.jpg]]
Out=$I_j$ se la parola binaria $S_0,S_1,...S_{n-1}$ rappresenta il numero j in binario. Esempio tramite multiplexer 4 a 1: ![[esempiomultiplexer.jpg]]
Quindi abbiamo che $log_2j$ sono i bit per scegliere gli ingressi, se $j\ne 2^n$ allora si hanno $\lceil log_2j \rceil$  bit di selezione. Ad esempio nel multiplexer 5 a 1, ho 5 ingressi e 3 bit di selezione.

Un demultiplexer è un circuito logico che consente di instradare 1 ingresso su una tra $2^n$ uscite in base allo stato di $n$ segnali di controllo, in pratica è duale al multiplexer.

![[demultiplexer.jpg]]

---
# Decoder ed encoder
Un decoder è un circuito logico che riceve $n$ ingressi per produrre $2^n$ uscite corrispondente al numero in ingresso espresso in binario. ![[decoder.jpg]] Quindi se AB è 11 allora l'uscita corrispondente è $O_3$.
![[tabella.jpg]]
Dove:
$O_0=\overline{A} \land \overline{B}$
$O_1=\overline{A}\land B$
$O_2=A\land \overline{B}$
$O_3=A\land B$
Di seguito l'implementazione di un decoder 2 a 4
![[impldecoder.jpg]]

Un encoder è un circuito logico che riceve $2^n$ ingressi per produrre $n$ uscite corrispondenti a $I_j$ in binario, ovvero se ho $I_2$ avrò in uscita 10.
![[encoder.jpg]]

--- 
# Comparatori e sintesi di reti combinatorie
Un comparatore riceve praticamente due segnali A e B e verifica se sono uguali o meno. Quindi fa un confronto bit a bit tra A e B e ritorna 1 se A=B.
![[selettore.jpg]]

Prima di realizzare una rete combinatoria è necessario superare 4 fasi:
1. Stabilire in quali condizioni l'uscita della rete combinatoria deve assumere 1
2. Costruire la tabella di verità
3. Estrarre una formula logica minimizzata
4. Disegnare la rete combinatoria

---

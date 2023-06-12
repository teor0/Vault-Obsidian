---
tag: #basi 
created: 2023-01-09 17:03:10
updated: 2023-01-09 17:03:10
---
#basi 
[[Decomposizione BCNF e suo algoritmo]]
# Ciclo nei grafi delle dipendenze
Se all'interno dei grafi delle dipendenze trovo una struttura simile a:
![[grafdipcic.jpg|800x350]]
non si può decomporre in BCNF tale che si abbia lossless join e che non si perda alcuna dipendenza funzionale!

---
# Terza forma normale
Quando ci si trova davanti ad un ciclo e quindi non si può garantire sia lossless join che il mantenimento delle dipendenze funzionali, si accetta un po' di ridondanza sapendo che oltre un certo livello la ridondanza non si può togliere altrimenti si perdono dipendenze funzionali.

Ciò si può fare attraverso una diversa forma normale detta terza forma normale (3NF). La definizione è la seguente:
> Dato lo schema di relazione R($A_1,...,A_n$) e l'insieme di dipendenze funzionali F, per ipotesi copertura minimale, R è in terza forma normale se $\forall X\rightarrow Y\in F$ in forma canonica vale almeno una delle 2 seguenti proprietà:
> 1. X è una chiave
> 2. Y appartiene ad una chiave (se una dipendenza non soddisfa la BCNF almeno deve avere una parte destra che fa parte di una chiave)

Ad esempio se prendo il ciclo, ![[grafdipcic.jpg|700x300]] le possibili chiavi sono AB e CB. Rispetto alla dipendenza AB$\rightarrow$C la BCNF è soddisfatta, ma rispetto a C$\rightarrow$A la BCNF non è soddisfatta in quanto, C non è chiave e la parte destra ovvero A lo è, quindi se utilizzo la BCNF rischio di perdere la dipendenza funzionale, al contrario utilizzando la 3NF, C$\rightarrow$A è idonea.

Per quanto riguarda la forma canonica, affinché valga la seconda proprietà se ho AB$\rightarrow$CD soddisfa la proprietà se C appartiene a una chiave o se D appartiene ad una chiave. Non è necessario però, che C e D appartengano alla stessa chiave.
La 3NF si usa quindi per garantire poca ridondanza.

>[!regola]
>Se una relazione R è in BCNF, allora è in 3NF. Non è vero il contrario.

Ulteriore regola:
>[!regola]
>Esiste sempre una scomposizione in 3NF senza perdita di informazioni e senza perdita di dipendenze funzionali.

---
# Come scomporre in 3NF
Prendiamo lo schema di relazione R(ABCDEF) ed il seguente grafo:
![[graf3nf.jpg]]
Le dipendenze funzionali sono quindi:
- AB$\rightarrow$C
- CE$\rightarrow$F
- F$\rightarrow$DE
- D$\rightarrow$A
- C$\rightarrow$D
- E$\rightarrow$B

Le possibili chiavi sono keys={F,ED,EC,AE}. Tranne CE$\rightarrow$F e F$\rightarrow$DE le dipendenze funzionali non sono in BCNF.
Riguardo 3NF solo la dipendenza E$\rightarrow$B non soddisfa nessuna delle 2 proprietà. Vediamo quindi come scomporre.
Si prendono tutte le dipendenze funzionali e le accorpo rendendole in forma NON canica. Dopo creo una relazione per ogni dipendenza funzionale e metto tutte le dipendenze funzionali che valgono tra gli attributi. Nel caso d'esempio si avrà:
- $R_1$(ABC){AB$\rightarrow$C, C$\rightarrow$A}
- $R_2$(CEF){CE$\rightarrow$F,F$\rightarrow$EC}
- $R_3$(DEF){F$\rightarrow$DE,DE$\rightarrow$F}
- $R_4$(DA){D$\rightarrow$A}
- $R_5$(CD){C$\rightarrow$D}
- $R_6$(EB){E$\rightarrow$B}

È ovvio che se per ogni dipendenze faccio una relazione con gli attributi di quella dipendenza e si fanno le proiezioni, non si perdono dipendenze funzionali, in quanto una dipendenza sarà rappresentata in 1 degli schemi e la consistenza è forzata attraverso le proiezioni.
Si garantisce sempre che è in 3NF uno schema in quanto almeno uno dipendenza avrà come parte sinistra la chiave dello schema e tutte le dipendenze che si ottengono per proiezioni avranno come parte destra un pezzo della parte sinistra.

>Per garantire che non si perdano informazioni bisogna avere un'ulteriore proprietà, che tra tutti gli schemi di relazione che si ottengono per decomposizione, deve esistere uno schema che contiene una chiave dello schema originale.

Nel caso d'esempio ciò è garantito da $R_3$ ma se non ci fosse $R_3$, dovrei aggiungere uno schema che come attributi ha membri di una chiave ed insieme delle dipendenze funzionali l'insieme vuoto. Questo schema serve per garantire la lossless join, ovvero a ottenere una qualunque istanza originale, attraverso la join delle istanze dei sottoschemi.
## Calcolare una decomposizione minima
All'interno dello scritto è richiesto il calcolo della decomposizione minima ovvero, una decomposizione con il numero minimo di schemi. Per calcolare ciò, si prende la decomposizione ottenuta e si controlla se si può accorpare una coppia di schemi di relazione, senza perdere la 3NF.
In generale per ridurre le dimensioni conviene accorpare i cicli.

---





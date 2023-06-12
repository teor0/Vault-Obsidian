---
tag: #basi 
created: 2023-01-06 17:27:45
updated: 2023-01-06 17:27:45
---
#basi 
[[Linguaggio SQL]]
# A cosa serve e cos'è la dipendenza funzionale
La dipendenza funzionale è un vincolo che serve a garantire la consistenza dei dati. Il vincolo è sul modello relazionale e come la chiave primaria e la chiave esterna, è specificato su uno schema di relazione e dice quali istanze dello schema sono valide.

Prendiamo ad esempio il seguente schema di relazione:
Cliente(<u>CF</u>,Nome,Età,Comune,CAP,Provincia)
se si presenta il caso

| CF  | Nome | Età | Comune  | CAP   | Provincia |
| --- | ---- | --- | ------- | ----- | --------- |
| C1  | A    | 20  | Cosenza | 87100 | CS        |
| C2  | B    | 28  | Crotone | 87100 | KR        |

Si ha un errore in quanto il CAP è unico. 
Se 2 tuple hanno lo stesso valore di CAP allora hanno lo stesso valore di comune. Come imporre ciò? Si utilizza la dipendenza funzionale scrivendo X$\rightarrow$Y dove X,Y sono insiemi d'attributi dello schema di relazione su cui è definita la dipendenza funzionale. Nel caso sopra si ha che {CAP}$\rightarrow${Comune}.
Per leggerezza di notazione il simbolo di insieme non si mette, quindi CAP$\rightarrow$Comune va bene.

Si chiama dipendenza funzionale perché come esplicita la definizione matematica; 
> Una funzione è una relazione che ad ogni elemento del dominio associa 1 ed 1 solo elemento del codominio.

Ad ogni elemento di un insieme ne corrisponde uno ed uno soltanto dell'altro.
Una dipendenza funzionale può portare a sinistra o destra un numero di attributi qualunque.
Ad esempio R(A,B,C,D) con AB$\rightarrow$C, vuol dire che un'istanza r di R è consistente se, per ogni coppie di tuple che hanno gli stessi valori di A e B, queste 2 tuple devono coincidere anche nell'attributo C.

Porre AB$\rightarrow$C è diverso da spezzare la dipendenza in due A$\rightarrow$C, B$\rightarrow$C mentre è possibile spezzare una dipendenza del tipo C$\rightarrow$BD in C$\rightarrow$B, C$\rightarrow$D. 
>Una dipendenza funzionale che nella parte destra hanno un solo attributo si dice che sono in forma canonica.
## Definizione formale
Sia dato uno schema di relazione R($A_1$,...,$A_n$), una dipendenza funzionale su tale schema è un'espressione del tipo: X$\rightarrow$Y, con X,Y$\subseteq {A_1,...A_n}$. Un instanza r di R è consistente rispetto X$\rightarrow$Y, se X={$X_1,...X_n$} e Y={$Y_1,...Y_k$} se: $\forall t_1,t_2 \in r$ si ha che $t_1[X_1]=t_2[X_1]\land...\land t_1[X_n]=t_2[X_n]\implies t_1[Y_1]=t_2[Y_1]\land...\land t_1[Y_k]=t_2[Y_k]$. 
A parole: r è consistente se data una dipendenza funzionale X$\rightarrow$Y con X,Y sottoinsiemi dell'insieme ${A_1,...A_n}$ con $X_1,...X_n$ e $Y_1,...Y_k$ gli attributi in X e Y. Se per ogni coppie di tuple, queste 2 tuple hanno i valori uguali sulla parte sinistra allora devono avere i valori uguali nella parte destra.

Ovviamente X$\rightarrow$X è triviale.

---
# Vincolo di chiave e dipendenza funzionale
La dipendenza funzionale è simile al vincolo di chiave ma è più generale.
Prendiamo il seguente schema: Esame(<u>Matricola,</u>Nome,Data,<u>Materia</u>,Docente,Voto) utilizzando la dipendenza funzionale posso esprimere il fatto che matricola e materia sia una chiave, ovvero: Matricola,Materia$\rightarrow$Nome,Data,Docente,Voto.
Questa dipendenza dice che, se io prendo un'istanza d'esame, questa è consistente se comunque prendo 2 tuple, se riportano stessa matricola e materia, coincidono in tutti gli altri attributi. In pratica la tupla è la stessa.

>Un vincolo di chiave può essere quindi espresso come dipendenza funzionale, in particolare è una dipendenza funzionale dove la parte destra è data da tutti gli attributi che non sono riportati a sinistra.

Dato uno schema di relazione R, io associo un <font color=red>insieme di dipendenze funzionali</font> F. Un'istanza r dello schema è consistente quando è consistente rispetto ad ogni dipendenza di F. In SQL non vi è un meccanismo nativo per definire le dipendenze funzionali, ma si può utilizzare del codice (non tratta nel corso) che fa veriche e anche se non supportate sono facilmente implementabili tramite query.
## Evitare la ridondanza tramite le dipendenze funzionali
Se ci sono dipendenze funzionali dove nella parte sinistra c'è un attributo o un'insieme d'attributi non chiave allora si ha ridondanza, ricordando che essa non è un problema di spazione sprecato, ma di possibilità di commettere errori più facilmente e di non riportare correttamente ciò che si ha nella realtà. Riprendiamo il caso di prima: Esame(<u>Matricola,</u>Nome,Data,<u>Materia</u>,Docente,Voto).
Supponiao di avere F= Matricola,Materia$\rightarrow$Nome,Data,Docente,Voto, Matricola$\rightarrow$Nome e Materia$\rightarrow$Docente. Abbiamo ridondanza in quanto sia Matricola$\rightarrow$Nome e Materia$\rightarrow$Docente sono dipendenze che nella parte sinistra non è una chiave.  

---

# Forma normale di Boyce Codd
>[!regola]
>Dato uno schema di relazione R($A_1,...A_n$) e un'insieme di dipendenze F su R. Si dice che R è in forma normale di Boyce Codd (BCNF) se: $\forall X\rightarrow Y$ non triviali, l'insieme X è una <font color=red>superchiave</font>.

Per superchiave si intende un sovrainsieme di una chiave, ovvero contiene al suo interno una chiave. Perciò una superchiave contiene come suo sottoinsieme una chiave minimale. Da notare che essere superchiave non vuol dire essere chiave candidata.
La superchiave è una certificazione per dire che non contiene ridondanze. Dato lo schema Cliente(<u>CF</u>,Nome,Età,Comune,CAP,Provincia), Comune$\rightarrow$Provincia è indice di ridondanza perché Comune non è superchiave. Una forma normale è uno standard, bisogna ragionare sullo schema, bisogna per ogni parte sinistra vedere se è una superchiave, ossia sapere tutte le possibili chiavi. Le dipendenze funzionali sono utili a capire tutte le possibili chiavi candidate.
## Ragionamento da fare per conoscere le possibili chiavi
Dato lo schema Esame(<u>Matricola,</u>Nome,Data <u>Materia</u>,Docente,Voto) le dipendenze funzionali che ha senso esprimere sono: Matricola$\rightarrow$Nome, Materia$\rightarrow$Docente e Matricola,Materia$\rightarrow$Nome,Docente,Data,Voto.

Il ragionamento da seguire è: quando un insieme identifica in un'istanza valida le tuple dell'istanza dello schema. Questo è vero quando usando i termini usati nella dipendenza funzionale da questo insieme di attributi, dipendono funzionalemente tutti gli altri ossia, data una certa n-upla di valori di X deve esistere un'unica possibile combinazione di valori di Y, che vuol dire che non ci sono tuple distinte che hanno gli stessi valori di X.

Prendiamo R(A,B,C,D,E) con AB$\rightarrow$C, CD$\rightarrow$E e E$\rightarrow$AB. Vediamo se ci sono delle dipendenze funzionali implicate da queste che mi fa capire se da un'insieme di attributi dipende tutto. Per transizione CD$\rightarrow$ABE, quindi C,D è una superchiave. Per verificare che CD è una chiava candidata verifico la minimalità e dato che solo C o solo D non implicano tutti, allora C e D assieme formano una chiava candidata. Prendiamo poi:
- DE$\rightarrow$ABC: DE è superchiave e visto che D sola e E sola non sono chiavi candidate, DE è una chiave candidata.
- ABD$\rightarrow$CE: ABD è una chiave candidata
- ADE$\rightarrow$BC: ADE non è minimale, in quanto DE è minimale.

---

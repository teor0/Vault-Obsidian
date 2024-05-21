---
tags: elettrotecnica, 
created: 2024-04-12 18:50:40
updated: 2024-04-12 18:50:40
---
[[Convenzioni d'uso, componenti, corto circuito e circuito aperto]]
# Definizioni di ramo, nodo, maglia e messa a terra 
>[!definizione]
>Un ramo è un elemento del circuito attivo o passivo.

>[!definizione]
>I collegamenti sono considerati perfetti, senza alcuna di caduta di potenziale o perdita di corrente.

>[!definizione]
>Un nodo è il punto di connessione tra 2 o più rami dove il potenziale è uguale.

>[!definizione]
>Una maglia è un qualunque percorso chiuso in un circuito. La maglia che chiude tutto il circuito è la maglia massima.

>[!definizione]
>Gli anelli sono percorsi chiusi al cui interno non vi sono maglie.

>[!regola]
>Solo i rami che appartengono ad una maglia, ovvero i rami in cui scorre una corrente contribuiscono alla funzionalità del circuito.

Esempio di circuito con una parte da escludere:
![[circesclu.jpg|400x400]]
Perché per disegnare la maglia massima ho 2 passaggi.

Di solito si usa assumere un punto come riferimento per tutti gli altri, per esprimere le differenze di potenziale tra diversi punti del circuito. Al nodo che si sceglie come riferimento viene assegnato un potenziale nullo e tale nodo viene chiamato <font color=red>messa a terra</font> o ground.
Esempio:
![[ground.jpg|300x300]]

---
# Leggi di Kirchhoff
Se si conoscono tutti i potenziali dei nodi rispetto al potenziale del nodo preso come riferimento, allora tutte le grandezze elettriche del circuito possono essere determinate. Lo stesso vale se conosciamo tutte le correnti degli anelli. 
Potenziale dei nodi e correnti di anello sono due insieme di <font color=purple>variabili indipendenti</font>. Dai loro valori, tutti gli altri possono essere determinati.

Le leggi di Kirchhoff delle correnti e delle tensioni sono le leggi fondamentali per l'analisi dei circuiti a partire dalla topologia. Distinguiamo:
- KCL (Kirchhoff Current Law) alla base del metodo dei nodi, per trovare le tensioni dei nodi del circuito.
- KVL (Kirchhoff Voltage Law) alla base del metodo degli anelli, per trovare le correnti di un anello.

Dalla legge di conservazione della carica deriva la <font color=orange>prima legge di Kirchhoff</font> (KCL):
>[!definizione]
>La legge di Kirchhoff delle correnti (KCL) stabilisce che la somma algebrica delle correnti che entrano in un nodo è nulla. $\displaystyle\sum^{n}_{k=0}\pm i_k=0$

Le correnti entranti in un nodo vengono prese positive, mentre le correnti uscenti in un nodo vengono prese negative.
Esempio calcolo KCL ![[kcl.jpg|400x400]]
$i_1-i_2+i_3+i_4-i_5=0$

Dalla legge di conservazione dell'energia deriva la <font color=orange>seconda legge di Kirchhoff</font> (KVL). Più precisamente deriva dall'ipotesi che il campo elettrico sia conservativo e le costanti siano concentrate:
>[!definizione]
>La legge di Kirchhoff delle tensioni (KVL) stabilisce che la somma algebrica delle tensioni lungo un percorso chiuso o maglia è nullo. $\sum^{n}_{k=0}\pm v_k=0$

Esempio calcolo KVL ![[kvl.jpg|700x300]]
$-v_1+v_2+v_3-v_4+v_5=0$ seguendo il verso prescelto di percorrenza di una maglia, una tensione si prende positiva se entra e negativa se esce. 

>[!important] 
In un circuito avente una sola maglia si ha un solo anello dunque in tutti gli elementi del circuito fluisce la stessa corrente.

In particolare quando si ha un circuito del tipo: ![[stessatens.jpg|600x200]]
la differenza di potenziale su tutte le le resistenze sarà pari a $V_g$ perché si hanno 2 nodi.

>[!info] 
>D'ora in avanti si indicherà la tensione con $e$

# Elementi in serie e parallelo
>[!definizione]
Due elementi sono in <font color=blue>serie</font> quando condividono un nodo in maniera esclusiva e nessun altro elemento è connesso al nodo comune. La proprietà è transitiva, se l'elemento A è in serie con B e B è in serie con C allora A è in serie con C. **N.B. Se due elementi sono in serie sono attraversati dalla stessa corrente.**

>[!definizione]
>Due elementi sono in parallelo quando sono connessi alla stessa coppia di nodi. Tutti gli elementi in parallelo vede la stessa differenza di potenziale ai capi.

## Resistenze in serie e parallelo
Due o più resistenze in serie possono essere sostituite da una resistenza equivalente, pari alla somma delle resistenze. $R_eq=\sum^N_iR_i$ Esempio: ![[resserie.jpg|500x300]]
$R_{eq}=R_1+R_2$ La corrente del circuito sarà dunque pari a $i(t)={V\over R_{eq}}={V\over R_1+R_2}$
Dimostrazione:
Uso la KVL dunque $-V_g+V_{R_1}+V_{R_2}=0\implies V_g=V_{R_1}+V_{R_2}=iR_1+iR_2=i(R_1+R_2)\implies i={V_g\over R_1+R_2}$
Quando due o più resistori in serie sono collegati con un generatore di tensione si ha quel che si chiama <font color=red>partitore di tensione</font>. 
![[partitoretensione.jpg|300x500]]
In particolare le tensioni su le resistenze valgono: $\displaystyle v_1=iR_1=v_g{R_1\over R_{eq}}=v_g{R_1\over R_1+R_2}$ $\displaystyle v_2=iR_2=v_g{R_2\over R_{eq}}=v_g{R_1\over R_1+R_2}$
La tensione si ripartisce su i due resistori in maniera linearmente proporzionale al valore della loro resistenza.

Due o più resistenze in parallelo possono essere sostituite da una resistenza equivalente pari al rapporto, prodotto delle resistenze e la loro somma. $R_{eq}={R_1R_2\over R_1+R_2}$. Il valore della resistenza equivalente sarà: ${min(R_1,R_2)\over 2}\le R_{eq}\ge min(R_1,R_2)$
Dimostrazione tramite il seguente circuito ![[partitorecorrente.jpg|300x300]]
Essendo in parallelo le resistenze vedono la stessa differenza di potenziale ed applicando la KCL, $\displaystyle -i+i_1+i_2=0\implies i=i_1+i_2\implies i={V\over R_1}+{V\over R_2}=V{1\over R_1}+{1\over R_2}$ da cui $\displaystyle V={i\over {1\over R_1}+{1\over R_2}}={i\over {R_1+R_2\over R_1R_2}}=i{R_1R_2\over R_1+R_2}=iR_{eq}$ 
Il circuito preso in esame è il <font color=purple>partitore di corrente</font> Dove la corrente sulle resistenze è pari a: $i_1=i{R_2\over R_1+R_2}$ $i_2=i{R_1\over R_1+R_2}$. Dimostrazione: $i=i_1+i_2$ $V_{R_1}=V_{R_2}\implies i_1R_1=i_2R_2\implies i_1R_1=(i-i_1)R_2\implies i_1R_1+i_1R_2=iR_2\implies i_1=i{R_2\over R_1+R_2}$
Stesso discorso per $i_2$.

## Condensatori in serie e parallelo
La capacità di $N$ condensatori in serie è pari alla somma dei reciproci dei condensatori, ovvero al rapporto tra, il prodotto dei condensatori e la loro somma. $\displaystyle {1\over C_{eq}}={1\over C_1}+{1\over C_2}+{1\over C_3}+...+{1\over C_n}\implies C_{eq}={C_1C_2...C_n\over C_1+C_2+...C_n}$ ![[Pictures/condserie.jpg|400x400]] Dimostrazione: $\displaystyle V=v_1+v_2={1\over C_1}\int^{t}_{t_0}i(t)+v_1(t_0)+{1\over C_2}\int^{t}_{t_0}i(t)+v_2(t_0)=({1\over C_1}+{1\over C_2})\int^{t}_{t_0}i(t)+v_1(t_0)+v_2(t_0)$ 
dunque $\displaystyle V={1\over C_{eq}}\int^{t}_{t_0}i(t)+v_1(t_0)+v_2(t_0)$ come volevasi dimostrare.

La capacità di $N$ condensatori in parallelo è pari alla somma delle singole capacità.
![[Pictures/condpar.jpg|600x200]]
$C_{eq}=C_1+C_2+C_3+...+C_n$ 
Dimostrazione: $i=i_1+i_2+i_N$ $\displaystyle i=C_1{dv\over dt}+C_2{dv\over dt}+C_N{dv\over dt}=C_{eq}{dv\over dt}$

## Induttori in serie e parallelo
L'induttanza equivalente di $N$ induttori collegati in serie è pari alla somma delle singole induttanze. ![[indserie.jpg|600x200]] $L_{eq}=L_1+L_2+...+L_N$ 
Dimostrazione: $\displaystyle v=v_1+v_2+...v_N\implies v=L1{di\over dt}+L2{di\over dt}+...+LN{di\over dt}$

L'induttanza equivalente di $N$ induttori collegati in parallelo è pari alla somma dei reciproci delle induttanze, ovvero al rapporto tra, il prodotto delle induttanze e la loro somma. ![[indpar.jpg|400x200]] $\displaystyle {1\over L_{eq}}={1\over L_1}+{1\over L_2}+{1\over L_N}$
Dimostrazione:
$\displaystyle i=i_1+i_2={1\over L_1}\int^{t}_{t_0}v(t)+i_1(t_0)+{1\over L_2}\int^{t}_{t_0}v(t)+i_2(t_0)=({1\over L_1}+{1\over L_2})\int^{t}_{t_0}v(t)+i_1(t_0)+i_2(t_0)$ 

## Generatore in serie e parallelo
Generatori di tensione in serie sono equivalenti ad un generatore che eroga tensione pari alla somma dei singoli generatori. ![[gentenserie.jpg|600x300]]
Generatori di corrente in parallelo sono equivalenti ad un generatore che eroga corrente pari alla somma dei singoli generatori. ![[gencorpar.jpg|400x500]]

>[!regola]
>Due elementi accessibili da una porta sono equivalenti se hanno la stessa caratteristica $i-v\ \forall i,\forall v$ sulla porta. Ciò vale quindi sia per elementi attivi che passivi.

---
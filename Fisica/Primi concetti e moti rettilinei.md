[[Grandezze, vettori e loro operazioni]]
#fisica 
# Introduzione e sistemi di riferimento
La meccanica riguarda lo studio del moto di un corpo: essa spiega la relazione che esiste tra le cause che generano il moto e le caratteristiche di questo e la esprime con leggi quantitative. Se il corpo è esteso, come lo sono tutti i corpi materiali, il moto può risultare notevolmente complicato. Per questa ragione, seguendo un processo molto comune in Fisica, iniziamo lo studio del moto dal più semplice corpo, quello puntiforme, detto punto materiale: si tratta di un corpo privo di dimensioni ovvero che presenti dimensioni trascurabili rispetto a quelle dello spazio in cui può muoversi o degli altri corpi con cui può interagire.

L’analisi completa del moto riguarda sia il collegamento del moto stesso alle interazioni del corpo con i corpi circostanti che la descrizione geometrica dell’evoluzione temporale del fenomeno di movimento. Questa parte della meccanica, descrittiva del moto di un corpo, indipendentemente dalle cause che lo determinano, viene detta cinematica, mentre il perché del moto viene studiato nella dinamica.
Il moto di un punto materiale è determinato se è nota la sua posizione in funzione del tempo in un determinato sistema di riferimento, ossia ad esempio le sue coordinate x(t), y(t), z(t) in un sistema di riferimento cartesiano. Questa scelta, anche se è la più comune, non è unica; in determinate situazioni fisiche possono essere più idonei altri sistemi di riferimento, come quelli basati su coordinate polari.

---
# Traiettoria, quiete e velocità media ed istantanea

>La traiettoria è il luogo dei punti occupati successivamente dal punto in movimento e costituisce una curva continua nello spazio.

Lo studio delle variazioni di posizione lungo la traiettoria nel tempo porterà a definire il concetto di velocità, mentre lo studio delle variazioni della velocità con il tempo introdurrà la grandezza accelerazione. Le grandezze fondamentali in cinematica sono pertanto lo spazio, la velocità, l’accelerazione e il tempo; quest’ultimo molto spesso viene usato come variabile indipendente, in funzione di cui si esprimono le altre grandezze.
La quiete è un particolare tipo di moto in cui le coordinate restano costanti e quindi l'accelerazione è nulla. Si osservi come un punto in quiete in un sistema di riferimento possa apparire in moto rispetto ad un altro, oppure si pensi al volo di un uccello visto da una persona ferma o da un’altra persona in un’auto in movimento.

$\displaystyle v_m={\Delta x \over \Delta t}={x_2 -x_1 \over t_2 -t_1}$

Tale grandezza fornisce una informazione complessiva, ma non dà quasi nessuna indicazione sulle caratteristiche effettive del moto. Per individuare la funzione x(t) e le sue variazioni aumentiamo il numero di misure nell’intervallo di spazio $\Delta$x, cioè suddividiamo l'intervallo $\Delta$x in numerosi piccoli intervalli. Il processo di suddivisione in spazi sempre più piccoli può essere continuato e il limite a tale procedura è posto dalla capacità di apprezzare piccoli intervalli da parte degli strumenti utilizzati per la misura degli intervalli di spazio e di tempo.

In ogni caso se $\Delta$x risulta suddiviso in un numero elevatissimo di intervallini $dx$, ciascuno percorso nel tempo $dt$, si può definire la velocità istantanea, ad un istante t, del punto in movimento come il rapporto $\displaystyle v={dx \over dt}$ calcolato in quel determinato istante. Il metodo descritto consiste nel calcolare il limite $\Delta t \rightarrow 0$ del rapporto incrementale $\displaystyle{x(t+\Delta t)-x(t) \over \Delta t}$. Pertanto la velocità di un punto nel moto rettilineo è data dalla derivata dello spazio rispetto al tempo, quindi la velocità istantanea rappresenta la rapidità di variazione temporale della posizione nell'istante t considerato.

>Il segno della velocità indica il verso del moto sull'asse x.

In generale la velocità può essere espressa come funzione del tempo perciò:

$\displaystyle v={dx \over dt} \Rightarrow v(t)={dx \over dt}$

## Moto rettilineo

Il primo moto che prendiamo in considerazione, sempre iniziando dal caso più semplice, è quello rettilineo. Esso si svolge lungo una retta sulla quale vengono fissati arbitrariamente un’origine e un verso, perciò il moto del punto è descrivibile tramite una sola coordinata x(t). Supponiamo che il punto materiale si trovi nella posizione x al tempo t e nella posizione $x+dx$ al tempo $t+dt$. Dalla velocità istantanea $\displaystyle v={dx \over dt}$ vediamo che lo spostamento infinitesimo $dx$ è dato da $dx=v(t)*dt$ qualunque sia la dipendenza della velocità dal tempo.

Lo spostamento complessivo sulla retta su cui si muove il punto, in un intervallo finito di tempo $\Delta t=t-t_0$ è dato dalla somma di tutti i successivi valori $dx$. Per calcolarne il valore integriamo:

$\displaystyle\Delta x= {\int_{x_0}^x }dx ={\int_{t_0}^t}v(t)dt$

$\displaystyle x-x_0=\int_{t_0}^tv(t)dt$

$\displaystyle x(t)=x_0+\int_{t_0}^tv(t)dt$

Questa è la relazione generale che permette il calcolo dello spazio percorso nel moto rettilineo, qualunque sia il tipo di moto. Il termine $x_0$ rappresenta la posizione iniziale del punto, occupata all'istante $t_0$, pertanto per calcolare x(t), nota v(t) è necessario conoscere la condizione iniziale del moto.

> $\Delta x$ rappresenta lo spostamento complessivo

Ricordando la velocità media ricaviamo la relazione tra velocità media ed istantanea tramite la legge oraria appena trovata:

$x-x_0=\displaystyle\int_{t_0}^tv(t)dt$

$\displaystyle v_m={1\over t-t_0}\int_{t_0}^tv(t)dt$


## Moto rettilileo uniforme

Prendendo la legge oraria trovata in precedenza, consideriamo il caso particolare in cui v=costante. Si ha:

$\displaystyle x=x_0+v\int_{t_0}^tdt=x_0+v(t-t_0)$

$x=x_0+vt$ se $t_0$=0.

In questi due casi trovati la legge oraria è una funzione lineare del tempo, quindi in tempi uguali sono percorsi spazi uguali.

> Qui la velocità media coincide con la velocità istantanea perchè v=costante


## Accelerazione

Abbiamo detto che nel caso più generale di moto rettilineo la velocità è funzione del tempo, v(t). Se in un determinato intervallo di tempo $\Delta t$ essa varia di una quantità $\Delta v$, possiamo definire la grandezza accelerazione media come:

$\displaystyle a_m={\Delta v \over \Delta t}$

Con un procedimento analogo a quello utilizzato per passare dal concetto di velocità media a quello di velocità istantanea definiamo l'accelerazione istantanea, cioè la rapidità di variazione temporale della velocità come:

$\displaystyle a(t)={v(t+\Delta t)-v(t)\over \Delta t}={dv\over dt}={d^2x\over dt^2}$

Se a=0 la velocità è costante, se a>0 la velocità cresce nel tempo mentre se a<0 la velocità decresce.

> È il segno della velocità istantanea a fornire il verso del moto

Possiamo adesso ricavare v(t) tramite integrazione dell'accelerazione:

$dv=a(t)dt$

$\displaystyle\Delta v=\int_{v_0}^vdv=\int_{t_0}^ta(t)dt$

$\displaystyle v-v_0=\int_{t_0}^ta(t)dt$

$\displaystyle v(t)=v_0+\int_{t_0}^ta(t)dt$

In questo caso $v_0$ rappresenta la velocità del punto all'istante iniziale $t_0$. La conoscenza della legge oraria x(t) ci permette di ricavare, derivando, v(t) e a(t).

Supponiamo ora di trovarci in una situazione fisica in cui sia nota la dipendenza dell’accelerazione dalla posizione, cioè la funzione a(x). In tal caso è possibile ricavare il valore della velocità in ogni posizione x, v(x), utilizzando il concetto matematico di funzione di funzione. Infatti se ad un certo istante t il punto occupa una deteminata posizione x, con un valore v della velocità e a dell’accelerazione, queste si possono pensare come funzioni della posizione oltre che del tempo e si può scrivere v(t)=v[x(t)], a(t)=a[x(t)]. Derivando rispetto al tempo si trova:

$\displaystyle a={dv \over dt}={d\over dt}v[x(t)]={dv\over dx}{dx \over dt}$

$\displaystyle a=v{dv\over dx}$

$\displaystyle adx=vdv$

Integrando si trova la dipendenza dell'accelerazione dalla posizione:

$\displaystyle \int_{x_0}^xa(x)dx=\int_{v_0}^vvdv$

$\displaystyle \int_{x_0}^xa(x)dx={1\over 2}v^2-{1\over2}v_0^2$
Esempio calcolo di accelerazione:
$x(t)=ln(t)$ derivando rispetto al tempo si ottiene $\displaystyle v(t)={dx(t)\over dt}={dln(t)\over dt}={1\over t}$ mentre l'accelerazione è pari a $\displaystyle a(t)={dv\over dt}=-{1\over t^2}$.

---
# Moto rettilineo uniformemente accelerato

Il moto rettilineo più generale è vario, intendendo con questo termine che l’accelerazione non è costante, se invece l’accelerazione è costante durante il moto questo si dice uniformemente accelerato e la dipendenza della velocità dal tempo è lineare come si ricava dalla formula della velocità:

$\displaystyle v(t)=v_0+a\int_{t_0}^tdt$

$\displaystyle v(t)=v_0+a(t-t_0)$

Ricaviamo adesso la legge oraria del moto sostituendo la velocità alla legge oraria del moto rettilineo uniforme:

$\displaystyle x(t)=x_0+\int_{t_0}^t[v_0+a(t-t_0)]dt=x_0+\int_{t_0}^tv_0dt+\int_{t_0}^ta(t-t_0)dt$

$\displaystyle x(t)=x_0+v_0(t-t_0)+{1\over 2}a(t-t_0)^2$

Dunque nel moto rettilineo uniformemente accelerato la velocità è una funzione lineare del tempo mentre lo spazio è una funzione quadratica del tempo.

Riprendendo la dipendenza dell'accelerazione dalla posizione, se l'accelerazione è costante abbiamo che:

$\displaystyle v^2=v_0^2+2a(x-x_0)$

---
# Moto verticale di un corpo
Se nel moto uniformemente accelerato considermiamo l'asse delle ordinate e come accelerazione l'accelerazione di gravità $g=-9,81m/s^2$ otteniamo il moto verticale di un corpo. Le formule restano essenzialmente le stesse del moto uniformemente accelerato, solo che in base al sistema di riferimento cambia il segno dell'accelerazione. Se si mantiene un sistema di riferimento cartesiano classico, con l'asse y orientato verso l'alto avremo che:

$\begin{gather}
a=-g \\
v(t)=v_0-gt\\
y(t)=y_0+v_0t-{1\over 2}gt^2
\end{gather}$

In particolare avremo che l'altezza massima si ottiene considerando velocità nulla del corpo.

---

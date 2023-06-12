#fisica 
[[Primi concetti e moti rettilinei]]

# Moto nel piano

Nel caso che il moto sia vincolato a svolgersi su di un piano la traiettoria del punto P in figura è in generale una linea curva.

![[traie.jpg]]

La descrizione del moto diventa subito più complessa e necessita di un numero maggiore di informazioni rispetto al caso del moto rettilineo. Pensando per esempio a come avviene lo spostamento di P ad un certo istante, non basta specificare il valore numerico dello spostamento, ma occorre precisare in quale direzione sta avvenendo il moto e con quale verso ed in generale, questa direzione istantanea cambia continuamente lungo la traiettoria.

Si è visto, che grandezze con caratteristiche direzionali oltre che numeriche si chiamano vettori.

Nel moto su di un piano la posizione del punto viene individuata da due coordinate. Esse possono essere, con riferimento ad un sistema di assi cartesiani ortogonali, x(t) e y(t) oppure in termini di coordinate polari nel piano, r(t) e $\theta(t)$.

Le relazioni che intercorrono tra le coordinate cartesiane e quelle polari sono:

$x=rcos\theta$

$y=rsen\theta$

$r=\sqrt{x^2+y^2}$

$tan(\theta)=\displaystyle {y\over x}$

La posizione del punto P può essere individuata anche tramite il raggio vettore.
$r(t)=OP=x(t)u_x+y(t)u_y$

dove $u_x$ e $u_y$ rappresentano i versori degli assi cartesiani che si considerano fissi nel tempo. Se è nota la dipendenza del tempo di r, cioè la funzione r(t) è individuato il moto del punto P.

La posizione del punto lungo la traiettoria può anche essere data da una coordinata curvilinea s, misurata a partire da un’origine arbitraria. Il valore di s esprime la lunghezza della traiettoria e varia nel tempo durante il moto. $\displaystyle ds\over dt$ indica la variazione temporale della posizione lungo la traiettoria cioè la velocità istantanea del punto, come definita nel moto rettilineo. Se diamo la forma della traiettoria e la velocità con cui viene percorsa abbiamo fornito una descrizione completa del moto. Questa può essere riassunta nella grandezza velocità vettoriale.

![[vel.jpg|300x300]]

Consideriamo due posizioni occupate dal punto P al tempo t ed al tempo t+$\Delta t$.

Esse sono individuate dai vettori $r(t)$ e $r(t+\Delta t)=r(t)+\Delta r$. 
Si costruisce il rapporto incrementale $\displaystyle {r(t+\Delta t)-r(t)\over \Delta t}={\Delta r\over \Delta t}$ e si definisce velocità vettoriale il limite per $\Delta t \rightarrow 0$, $\displaystyle v={dr\over dt}$

La velocità vettoriale è la derivata del raggio vettore rispetto al tempo. Osserviamo che al limite l’incremento $dr$ del raggio vettore, risulta in direzione tangente alla traiettoria nel punto P e in modulo eguale allo spostamento infinitesimo ds lungo la traiettoria, per cui possiamo scrivere:

$\displaystyle dr=dsu_T$

dove $u_T$ è il versore della tangente alla curva, variabile nel tempo man mano che il punto avanza lungo la traiettoria. In sostanza pensiamo il moto come una successione di spostamenti rettilinei infinitesimi con direzione variabile. La direzione istantanea del moto coincide con quella della tangente alla traiettoria nel punto occupato all’istante considerato, passiamo così ad una formula più esplicita:

$\displaystyle v={ds\over dt}u_T=vu_T$

Pertanto la velocità vettoriale v individua in ogni istante con la sua direzione e verso la direzione e il verso del moto e con il suo modulo $\displaystyle v={ds\over dt}$ a velocità istantanea con cui è percorsa la traiettoria.

La traiettoria del moto e il fatto che la velocità si scrive $vu_T$ sono caratteristiche intrinseche, che cioè non dipendono dalla scelta del sistema di riferimento. Si può spostare l’origine O in un’altra posizione, si possono ruotare gli assi, ma la curva, la direzione, il verso, il modulo della velocità restano gli stessi. D’altra parte un vettore si scrive esplicitamente attraverso le sue componenti e queste sì dipendono dal sistema di riferimento. Calcoliamo le componenti della velocità nelle due situazioni più comuni.

## Componenti cartesiane velocità

Poiché $r=xu_x+yu_y$:

$\displaystyle v={dr\over dt}={dx\over dt}u_x+{dy\over dt}u_y=v_xu_x+v_yu_y$

La velocità del punto P, che si muove lungo la traiettoria, ha come componenti cartesiani le velocità $\displaystyle v_x$ e $\displaystyle v_y$ dei due moti rettilinei descritti dai punti proiezione di P sugli assi cartesiani. Quindi:

$\displaystyle v=\sqrt{v_x^2+v_y^2}$

detto $\Phi$ l'angolo tra il vettore v e l'asse x, la tangente è pari a

$\displaystyle tan(\Phi)={v_y\over v_x}$

> Si osservi che se ruotiamo gli assi cambiano $\displaystyle v_x$ e $\displaystyle v_y$

![[velcart.jpg|300x300]]

## Componenti polari velocità

Introduciamo i vettori $u_r$ e $\displaystyle u_\theta$, rispettivamente versore della direzione di r e versore ortogonale alla stessa come in figura:

![[versor.jpg|400x400]]

Il raggio vettore r può essere espresso come $\displaystyle ru_r$ e pertanto:

$\displaystyle v={dr\over dt}={dr\over dt}u_r+r{du_r\over dt}\Rightarrow v={dr\over dt}u_r+r{d\theta \over dt}u_\theta=v_r+v_\theta$

La velocità che, si ricordi, è sempre tangente alla traiettoria si scompone in due componenti: la velocità radiale $v_r$, diretta lungo r e di modulo $\displaystyle dr\over dt$ e la velocità trasversa $\displaystyle v_\theta$, ortogonale a r e di modulo $\displaystyle r{d\theta\over dt}$. 
$\displaystyle v_r$ dipende dalle variazioni del modulo del raggio vettore, $\displaystyle v_\theta$ è collegata alle variazioni di direzione dello stesso. risultato della scomposizione si può anche ottenere considerando che lo spostamento infinitesimo dr ha le componenti dr e $rd\theta$ e dividendo per dt si hanno le componenti della velocità.

Il modulo della velocità è dato da:

$\displaystyle v={ds\over dt}=\sqrt{({dr\over dt})^2+r^2({d\theta\over dt})^2}$

![[velpol.jpg|400x400]]

In definitiva abbiamo mostrato come si determina la velocità se è nota la posizione, in coordinate cartesiane o polari. Analogamente a quanto fatto per il moto rettilineo, ci poniamo il problema inverso e la soluzione si ricava integrando la velocità vettoriale:

$\begin{align}
\displaystyle v &={dr\over dt} \\
dr &=v(t)dt \\
\displaystyle \int_{t_0}^tdr &=\int_{t_0}^tv(t)dt \\
\displaystyle r(t) &=r(t_0)+\int_{t_0}^tv(t)dt
\end{align}$

## Accelerazione nel piano

L’accelerazione nel moto piano deve esprimere le variazioni della velocità sia come modulo che direzione e quindi ci aspettiamo che abbia due componenti, una legata alla variazione del modulo della velocità e la seconda al cambiamento di direzione del moto. Nella figura è mostrata la situazione in modo qualitativo, ma già si capisce che l’accelerazione non è parallela alla velocità ed è diretta verso la concavità della curva che rappresenta la traiettoria.

![[acc.jpg]]

Anche nel moto piano l'accelerazione è ottenibile derivando la velocità rispetto al tempo:

$\displaystyle a={dv\over dt}={d^2r\over dt^t}$

Adesso deriviamo la velocità vettoriale partendo dalla formula trovata:

$\displaystyle a={d\over dt}(vu_T)={dv\over dt}u_T+v{du_T\over dt}={dv\over dt}u_T+v{d\phi\over dt}u_N$

La prima componente, parallela alla velocità, esprime la variazione del modulo della velocità, il secondo termine, dipendente dalla variazione di direzione della velocità, è ortogonale a questa. $u_N$ è un vettore ortogonale a $u_T$ diretto verso la concavità della traiettoria, e $\displaystyle {d\phi\over dt}$ dice quanto rapidamente cambia la direzione di $u_T$ e quindi di $u_N$.

Per esprimere in maniera più significativa la componente normale, ricorriamo alla figura che mostra il moto durante un istante dt.

![[un.jpg|350x350]]

Al limite per $\Delta t\rightarrow 0$ le rette normali alla traiettoria in due punti molto vicini tra loro si incontrano nel punto C, che coincide con il centro della circonferenza tangente alla traiettoria nel punto P e si chiama anche, centro di curvatura della traiettoria nel punto P. L'arco di traiettoria ds è pari a $\displaystyle Rd\phi$ con $R=CP$, raggio di curvatura. Al variare di P lungo la traiettoria variano sia il valore di R che la posizione di C, che può passare da una parte all'altra della curva. Pertanto:

$\displaystyle {d\phi\over dt}={d\phi\over ds}{ds\over dt}={1\over R}v$

e sostituendo nell'espressione dell'accelerazione trovata prima:

$\displaystyle a={dv\over dt}u_T+{v^2\over R}u_N=a_T+a_N$

Le due componenti si chiamano accelerazione tangenziale e centripeta o normale. In un moto curvilineo vario entrambe le componenti sono diverse da zero, se però il moto curvilineo è uniforme è nulla $\displaystyle a_T$. Invece nel moto rettilineo vario è nulla $\displaystyle a_N$e solo nel moto rettilineo uniforme $\displaystyle a_N=a_T=0$.

> In altre parole se $a_T\ne 0$ il moto è sempre vario e con $a_N\ne 0$ è sempre curvilineo

In modulo l'accelerazione è pari a:
$\displaystyle a=\sqrt{a_T^2+a_N^2}=\sqrt{({dv\over dt})^2+{v^4\over R^2}}$

## Componenti cartesiane accelerazione

Le componenti cartesiane dell’accelerazione sono:

$\displaystyle a={dv\over dt}={dv_x\over dt}u_x+{dv_y\over dt}u_y={d^2x\over dt^2}u_x+{d^2y\over dt^2}u_y=a_xu_x+a_yu_y$

![[acce.jpg|400x400]]

Se $\displaystyle\phi$ è l'angolo che $\displaystyle u_T$ forma con $\displaystyle u_x$, si deduce dalla figura che:

$\displaystyle a_x={dv\over dt}cos\phi-{v^2\over R}sen\phi$

$\displaystyle a_y={dv\over dt}sen\phi-{v^2\over R}cos\phi$

---
# Moto armonico semplice

Il moto armonico semplice lungo un asse rettilineo è un moto vario la cui legge oraria è definita dalla relazione:

$x(t)=A sen(\omega t+\phi)$

dove $A,\omega,\phi$ sono grandezze costanti. A è detta ampiezza del moto, $\omega t+\phi$ fase del moto, $\phi$ fase iniziale e $\omega$ pulsazione. Il moto può assumere come valore massimo A e valore minimo -A in quanto, la funzione seno oscilla tra -1 e 1. Il moto armonico, considerando che la funzione seno è periodica con periodo $2\pi$ risulta essere periodico.In effetti il punto descrive oscillazioni di ampiezza A rispetto al centro O, tutte eguali tra loro e caratterizzate dalla durata, detta periodo T del moto armonico.

> Il moto di un punto si dice periodico quando ad intervalli di tempo eguali il punto ripassa nella stessa posizione con la stessa velocità. E questo vale per qualsiasi posizione.


Per determinare il periodo T consideriamo due tempi t' e t con t'-t=T. Per definizione x(t')=x(t) quindi essendo le due fasi nei due istanti differire di $2\pi$, abbiamo che:

$\begin{gather}
\displaystyle \omega t'+\phi=\omega t +\phi+2\pi \\
\omega(t'-t)=2\pi \\
\omega T=2\pi \\
T=\displaystyle {2\pi \over \omega} \\
\displaystyle\omega={2\pi \over T}
\end{gather}$

> Questo fa capire che il moto si ripete più velocemente quando la pulsazione è grande, mentre è lento per valori piccoli.

Si definisce frequenza f del moto il numero di oscillazioni in un secondo:

$\displaystyle f={1 \over T}={\omega \over 2\pi}$

> È molto importante notare che periodo e frequenza sono indipendenti dall'ampiezza del moto.

Fissato il valore della pulsazione abbiamo una classe di moti armonici, caratterizzati dallo stesso periodo, che differiscono tra loro per i diversi valori dell’ampiezza e della fase iniziale.
La velocità del punto si ottiene derivando x(t):

$\displaystyle v(t)=\omega Acos(\omega t+\phi)$

L'accelerazione del punto si ottiene derivando v(t):

$\displaystyle a(t)=-\omega ^2Asen(\omega t+\phi)=-\omega^2x$

La velocità assume il valore massimo nel centro di oscillazione dove vale $\omega A$ e si annulla agli estremi, dove si inverte il senso del moto. L’accelerazione si annulla nel centro di oscillazione e assume il valore massimo in modulo $\omega^2A$ agli estremi, dove si inverte la velocità. Inoltre essa è sempre proporzionale ed opposta allo spostamento dal centro di oscillazione.

![[fase.jpg|450x600]]

A parte il valore dell’ampiezza, le tre funzioni x(t), v(t), a(t) mostrano lo stesso andamento temporale: la forma e il periodo sono eguali, c’è solo uno spostamento di una rispetto all’altra lungo l’asse dei tempi. Quest’ultima caratteristica viene indicata dicendo che le funzioni sono sfasate tra di loro. In particolare la velocità è sfasata di $\displaystyle \pi \over 2$ rispetto allo spostamento, mentre l’accelerazione è sfasata di $\pi$ sempre rispetto allo spostamento.

Importante è calcolare $\phi$:

$\displaystyle tan(\phi)={\omega Asen(\phi) \over \omega Acos(\phi)}={\omega x_0 \over v_0}$

Inserendo l'accelerazione per il moto armonico nella relazione di dipendenza dell'accelerazione dalla posizione si trova, la dipendenza della velocità dalla posizione v(x):

$\displaystyle \int_{x_0}^xa(x)dx=-\omega^2\int_{x_0}^xxdx={1\over 2}\omega^2(x_0^2-x^2)={1\over 2}v^2-{1\over 2}v_0^2$

$\displaystyle v^2=v_0^2+\omega^2(x_0^2-x^2)$

$v^2(x)=\omega^2(A^2-x^2)$

nell'ultimo caso se $x_0=0$ e $v_0=\omega A$.

## Condizione necessaria e sufficiente del moto armonico semplice

La condizione necessaria e sufficiente perché un moto sia armonico è data dall’equazione:

$\displaystyle{{d^2x \over dt^2}+\omega^2x=0}$

detta equazione differenziale del moto armonico. Le funzioni seno e coseno sono tutte e sole le funzioni che soddisfano alla condizione nel campo reale. Quest’ultimo fatto ci porta a osservare esplicitamente che le proprietà generali del moto armonico semplice restano eguali se invece della funzione seno utilizziamo la funzione coseno. Le due funzioni differiscono solo per un termine di sfasamento pari a $\displaystyle {\pi \over 2}$.

---

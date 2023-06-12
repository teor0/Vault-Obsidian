#fisica 
[[Moto in due dimensioni]]
# Moto circolare
Si chiama moto circolare, un moto piano la cui traiettoria è rappresentata da una circonferenza. Considerando che la velocità varia continuamente in direzione, $a_N\ne 0$ sempre.

Nel moto circolare uniforme la velocità è costante in modulo e l’accelerazione tangente è nulla per cui $a=a_N$, se invece il modulo della velocità cambia nel tempo il moto circolare non è uniforme e $a_T\ne 0$, in questo caso la direzione dell’accelerazione non passa per il centro della circonferenza.

Il moto circolare può essere descritto facendo riferimento allo spazio percorso sulla circonferenza s(t) oppure utilizzando l’angolo $\theta (t)$ sotteso dall'arco s(t), con $\displaystyle\theta (t)={s(t)\over R}$.

![[circo.jpg|400x400]]

L'assumere come variabile $\theta (t)$ significa in sostanza porsi in un sistema di coordinate polari di centro in O in cui il moto avviene con r(t)=R=costante e $\theta(t)$ variabile. Anche la rappresentazione in coordinate cartesiane è legata come sappiamo a $\theta(t):x(t)=Rcos\theta(t)$, $y(t)=Rsen\theta(t)$.

## Velocità angolare

Siamo naturalmente interessati alle variazioni dell’angolo nel tempo e pertanto definiamo la velocità angolare come derivata dell'angolo rispetto al tempo:

$\displaystyle \omega={d\theta\over dt}={1\over R}{ds\over dt}={v\over R}$

Risulta che la velocità angolare è proporzionale alla velocità con cui è descritta la circonferenza, se v è variabile lo è anche $\omega$. Nel moto circolare la velocità radiale è identicamente nulla perché il raggio vettore è costante in modulo e la velocità trasversa coincide con la velocità. Da:

$\displaystyle v_\theta=R{d\theta\over dt}$

ritroviamo

$\displaystyle v=R\omega$

Il moto circolare più semplice è quello uniforme dove v e $\omega$ sono costanti e le leggi orarie, con riferimento alle due variabili utilizzate sono:

$\displaystyle s(t)=s_0+vt$

$\displaystyle \theta(t)=\theta_0+\omega t$

> Il moto circolare non uniforme è un moto accelerato con accelerazione costante, ortogonale alla traiettoria

$\displaystyle a=a_N={v^2\over R}=\omega^2R$

Si tratta inoltre di un moto periodico con periodo

$T=\displaystyle{2\pi R\over v}={2\pi\over\omega}$

corrispondente al tempo necessario per compiere un giro completo. I moti proiettati sugli assi cartesiani sono due moti armonici di eguale ampiezza e fase iniziale, sfasati tra loro di $\displaystyle\pi\over 2$, e con periodo coincidente con quello del moto circolare uniforme. Numericamente la velocità angolare è eguale alla pulsazione, anche se il significato fisico delle due grandezze è diverso.

$x=Rcos\theta=Rcos(\omega t+\theta_0)$

$y=Rsen\theta=Rsen(\omega t+\theta_0)$

## Accelerazione angolare

Nel caso del moto circolare non uniforme oltre all’accelerazione centripeta, che è variabile perché la velocità varia anche in modulo, dobbiamo considerare anche l’accelerazione tangenziale $a_T$.

Siccome è variabile anche la velocità angolare definiamo l'accelerazione angolare:

$\displaystyle\alpha={d\omega\over dt}={d^2\theta\over dt^2}={1\over R}{dv\over dt}={a_T\over R}$

Se è nota la legge oraria angolare $\theta(t)$, con le due derivazioni successive determiniamo le variazioni dell’angolo e della velocità angolare. Viceversa nota $\alpha(t)$, possiamo integrare ottenendo:

$\displaystyle\omega(t)=\omega_0+\int_{t_0}^t\alpha(t)dt$

$\displaystyle\theta(t)=\theta_0+\int_{t_0}^t\omega(t)dt$

---
# Moto parabolico

Studiamo adesso il moto di un punto P lanciato dall'origine O con velocità iniziale $\displaystyle v_0$ formante un angolo $\theta$ con l'asse delle ascisse, ovvero un moto parabolico. In particolare vogliamo calcolare la traiettoria, la massima altezza raggiunta e la posizione G in cui il punto ricade sull’asse x ovvero la gittata OG.

Il moto è caratterizzato da un’accelerazione costante $a=g=-gu_y$ e le condizioni iniziali sono r=0 e $\displaystyle v=v_0$ al tempo t=0, istante di lancio. Sostituiamo adesso l'accelerazione costante del moto nella formula della velocità:

$\begin{gather}
\displaystyle v(t)=v_0+\int_{t_0}^tadt \\
\displaystyle v(t)=v_0-gu_y\int_{0}^tdt \\
\displaystyle v(t)=v_0-gtu_y
\end{gather}$

Poichè $\displaystyle  v_0=v_0cos\theta u_x+v_0sen\theta u_y$

$\displaystyle v(t)=v_0cos\theta u_x+(v_0sen\theta -gt)u_y$

Le velocità dei moti proiettati sugli assi sono $\displaystyle v_x=v_0cos\theta$ costante e $\displaystyle v_y=v_0sen\theta -gt$. Quindi le leggi orarie sono:

$\displaystyle x(t)=v_0cos\theta t$

$\displaystyle y(t)=v_0sen\theta t-{1\over 2}gt^2$

perciò, sull’asse x il moto è uniforme, sull’asse y uniformemente accelerato.
La traiettoria viene ricavata eliminando il tempo tra x(t) e y(t):

$\displaystyle t={x\over v_0cos\theta}$

$\displaystyle y(x)=xtan\theta-{g\over 2v_0^2cos^2\theta}x^2$

La direzione del moto, in funzione del tempo o della coordinata x, può essere caratterizzata dall’angolo $\phi$ che il vettore velocità forma con l'asse orizzontale:

$\displaystyle tan\phi={v_y\over v_x}=tan\theta-{g\over v_0cos\theta}t=tan\theta-{g\over v_0^2cos^2\theta}x$
Per calcolare la gittata poniamo y(x)=0 ed ottieniamo 2 soluzioni, x=0 e:

$\displaystyle x_G={2v_0^2cos^2\theta tan\theta\over g}={2v_0^2cos\theta sen\theta\over g}$   $\large x_G=2x_M$

con $x_M$ pari a

$\displaystyle x_M={v_0^2cos\theta sen\theta\over g}$

coordinata del punto di massima altezza. Pertanto l'altezza massima sarà:

$\displaystyle y(x_M)=y_M={v_0^2sen^2\theta\over 2g}$

L’angolo di lancio per cui si ha la gittata massima si ottiene con la condizione:

$\displaystyle{dx_G\over d\theta}=0$ cioè

$\displaystyle {2v_0^2\over g}(-sen^2\theta+cos^2\theta)=0$

Il tempo totale di volo $t_G$ è al tempo impiegato a percorrere OG con velocità costante $\displaystyle v_x=v_0cos\theta$:

$\displaystyle t_G={2x_M\over v_0cos\theta}={2v_0sen\theta\over g}$

---

# Forza centripeta

La risultante delle forze agenti sul punto materiale deve avere una componente ortogonale alla traiettoria, $F_N$, per provocare la variazione di direzione della velocità. La componente tangenziale $F_T$ della forza determina invece la variazione del modulo della velocità.

$F_N$ si chiama forza centripeta ed è sempre diversa da zero in un moto curvilineo. Fare attenzione al fatto che la forza centripeta non è un tipo particolare di forza, come la forza peso ad esempio ma è semplicemente il nome che si dà alla componente ortogonale alla traiettoria della risultante delle forze agenti.

## Forze centripete

Supponiamo che la risultante R delle forze agenti su un punto materiale presenti una componente $F_N$  ortogonale alla traiettoria, che risulta pertanto curvilinea. $F_N$ determina l’accelerazione centripeta secondo la relazione:

$F_N=ma_N=m{v^2 \over r}$

essendo r il raggio di curvatura della traiettoria. In generale R ha anche una componente tangente alla traiettoria, $F_T$ responsabile della variazione del modulo della velocità. Se $F_T=0$ il il moto lungo la traiettoria è uniforme e l’unica accelerazione è $a_N$.

> Forze centripete sono generalmente prodotte da rotaie, pneumatici, fili che collegano il corpo ad un punto fisso ovvero vincoli che consentono di incurvare la traiettoria oppure da azioni a distanza come quelle gravitazionali.

---
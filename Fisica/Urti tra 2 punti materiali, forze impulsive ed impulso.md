#fisica 
[[Centro di massa, teorema del moto del centro di massa quantità di moto e equazione cardinale]]
# Urti
Quando due punti materiali vengono a contatto e interagiscono per un intervallo di tempo trascurabile rispetto al tempo di osservazione del sistema, si parla di urti tra i 2 punti. Il fenomeno è di così breve durata da giustificare l’assunzione che durante l’interazione i punti non si muovano. Nell’urto si possono sviluppare forze molto intense che modificano la quantità di moto di ciascun punto. 

> In assenza di forze esterne o risultate di esse pari a 0, si verifica la conservazione della quantità di moto

Consideriamo 2 masse uguali con velocità uguale ma di verso opposto, con l'avvicinarsi il centro di massa resta invariato ma prima o poi le 2 masse urteranno. Se indichiamo con $v_{i,1}$ e $v_{i,2}$ le velocità nell'istante precedente all'urto dei due punti materiali di masse, $m_1$ e $m_2$, e con $v_{f,1}$ e $v_{f,2}$ le corrispondenti velocità nell'istante successivo all'urto, in assenza di forze esterne la conservazione di P è pari a:

$\displaystyle P_{CM}^i=P_{CM}^f \implies m_1v_{i,1}+m_2v_{i,2}=m_1v_{f,1}+m_2v_{f,2}$


>[!Regola] Se l'energia cinetica dopo l'urto è maggiore di quella iniziale il risultato è insensato al massimo sarà uguale (si conserva) o minore (si dissipa).

---
# Urto completamente anelastico
Un urto si dice completamente anelastico quanto i due punti restano attaccati dopo l'urto formando un unica corpo puntiforme di massa $m_1+m_2$. Se $v_1$ e $v_2$ sono le velocità dei due punti nell'istante prima dell'urto e $v'$ è la velocità comune immediatamente dopo l'urto, tramite l'equazioni della conservazione della quantità di moto si ha:

$m_1v_1+m_2v_2=(m_1+m_2)v'=(m_1+m_2)v_{CM}$

$\displaystyle v_{CM}={m_1v_1+m_2v_2\over m_1+m_2}$

Subito dopo l'urto i punti si muovono con la velocità che aveva il centro di massa un istante prima dell'urto.  Un urto è completamente anelastico se l'energia cinetica finale rispetto a quella iniziale è minore, ovvero dopo l'urto l'energia viene dissipata.

---
# Urto elastico

Si definisce come urto elastico un urto durante il quale si conserva anche l'energia cinetica del sistema. Questo comporta che le forze interne, che si manifestano durante l'urto, siano conservative. I due corpi reali che si urtano subiscono, durante l'urto delle deformazioni elastiche, riprendendo la configurazione iniziale subito dopo l'urto. Nello studio di un urto elastico possiamo utilizzare le equazioni

$P_i=P_f$ e $E_{k,i}=E_{k,f}$

Nel caso unidimensionale abbiamo due equazioni di conservazione e due incognite e possiamo risolvere il problema. Dunque:

$m_1v_{i,1}+m_2v_{i,2}=m_1v_{f,1}+m_2v_{f,2}$

$\displaystyle\large{1\over 2}m_1v_{i,1}^2+{1\over 2} m_2v_{i,2}^2={1\over 2}m_1v_{f,1}^2+{1\over 2}m_2v_{f,2}^2$

Dopo svariati calcoli alla fine si otterrà che:

$\displaystyle v_{f,1}=({1-m_{21}\over 1+m_{21}})v_{i,1}+({2m_{21}\over 1+m_{21}})v_{i,2}$

$\displaystyle v_{f,2}=({2v_{i,1}\over 1+m_{21}})+({2m_{21}-1\over 1+m_{21}})v_{i,2}$

Un urto si dice elastico se l'energia cinetica si conserva!

---
# Forze impulsive e teorema dell'impulso
Quando una massa urta una superficie oppure una massa infinitesimamente più grande, si manifestano quelle che si chiamano forze impulsive. Consideriamo l'istante in cui un oggetto urta una superficie, il corpo si comprimerà per attutire l'urto ovvero la forza inizialmente "non verrà subita", per poi rimbalzare indietro oppure penetrare la superficie, ovvero la forza sarà "subita". Se consideriamo questo comportamento nel tempo della forza otteniamo questo grafico:
![[impulso.jpg|400x400]]

partendo dal secondo principio di Newton, $ma=F$ e considerando la massa con velocità iniziale molto alta, si ha che $\displaystyle m{dv\over dt}=F$. La velocità andrà a variare in un intervallo di tempo come la forza resta costante in tale intervallo perciò riscrivo l'equazione come $\displaystyle m{\Delta v\over \Delta t}=F_{cost}\implies m\Delta v=F_{cost}\Delta t$. Si nota che $m\Delta v$ altro non è che $m(v_f-v_i)=P_f-P_i$ perciò $P_f-P_i=F_{cost}\Delta t$

L’azione di una forza durante un intervallo di tempo provoca una variazione della quantità di moto e ciò viene impulso, $\overrightarrow{J}=F_{cost}\Delta t$. Ciò che si è dimostrato è il teorema del impulso ovvero che $\Delta \overrightarrow{P}=\overrightarrow{J}$. Se la forza non è costante ma varia nel tempo si ha la definizione generale di impulso, $\displaystyle\overrightarrow{J}=\int^{\Delta t}_{0}\overrightarrow{F}(t)dt$


> L'impulso di una forza applicata ad un punto materiale provoca la variazione della sua quantità di moto

Il teorema dell’impulso è utilizzabile per calcolare effettivamente $\Delta P$ solo se si conosce la funzione F(t), in particolare se F è costante come detto. 

---
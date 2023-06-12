[[Sistemi di riferimento inerziali, velocità ed accelerazione relativa]]
#fisica 
# Lavoro

Consideriamo un punto materiale che si muove lungo una generica traiettoria curvilinea e sia F la risultante delle forze agenti sul punto. Si definisce lavoro della forza F, compiuto durante lo spostamento del punto dalla posizione A alla posizione B, la quantità scalare:

$\displaystyle W=\int_A^BFds=\int_A^BFcos\theta ds=\int_A^BF_Tds$

Il lavoro è l'integrale di linea della forza, cioè è dato dalla somma di infiniti contributi infinitesimi $dW=Fds=F_Tds$.  Si osservi che in generale lungo la traiettoria sia F che $\theta$ sono variabili. Si possono presentare 3 casi.

1. F forma con ds un angolo minore di $\displaystyle\pi\over2$, per cui l'accelerazione tangente è concorde con la velocità e la fa aumentare, dW risulta positivo e viene chiamato lavoro motore.
2. F forma con ds un angolo maggiore di $\displaystyle\pi\over 2$, il punto viene frenato e dW risulta negativo (lavoro resistente).
3. Se F è ortogonale alla traiettoria, $\displaystyle\theta={\pi\over 2}$ e il lavoro è nullo, in questo caso F ha azione puramente centripeta e non fa variare il modulo della velocità.

$\displaystyle W=F*x(t)*cos\theta$

Quando F è effettivamente la somma di n forze, per ciascuna si può calcolare il corrispondente lavoro $W_i$ e risulta $W=\displaystyle\sum_iW_i$:

$\displaystyle W=\int_A^BFds=\int_A^B(F_1+...+F_n)ds=\int_A^BF_1ds+...+\int_A^BF_nds=W_1+...+W_n$

> Il lavoro è pari alla somma dei lavori delle singole forze agenti, ciascuno dei quali può essere positivo, negativo o nullo.

Secondo quanto detto sopra il lavoro totale può essere nullo in quanto somma di lavoro motore lungo un arco di traiettoria e di lavoro resistente lungo un successivo arco. Certamente però possiamo affermare che W = 0 quando non agisce nessuna forza oppure agiscono forze la cui risultante o è nulla o è sempre ortogonale alla traiettoria. 
Un esempio di moto con risultante nulla delle forze è il moto rettilineo uniforme in presenza di attrito radente: occorre applicare una forza eguale e contraria alla forza di attrito e quindi fornire un lavoro motore eguale ed opposto al lavoro resistente dell’attrito. Invece un moto con risultante delle forze sempre ortogonale  alla traiettoria (quindi W=0) è il moto curvilineo uniforme: se c’è attrito, oltre alla forza normale deve essere presente una forza tangente, che svolge un lavoro motore, per bilanciare l’effetto dell’attrito.

## Lavoro della forza peso

Calcoliamo il lavoro della forza peso $mg$ per uno spostamento generico dalla posizione A a quella B. L'asse z è orientato dal suolo verso l'alto ed ha quindi verso opposto a g. Riprendendo l'equazione del lavoro:

$W=\displaystyle\int_A^BFds=F\int_A^Bds=mgr_{AB}$

infatti F è costante e l'integrale vale $r_B$-$r_A$=$r_{AB}$.

Poiché il peso ha una sola componente diversa da zero, quella secondo l’asse z che vale $-mg$ e la componente di $r_{AB}$ lungo l'asse z è $z_B-z_A$, il prodotto scalare si scrive semplicemente $(mg)_z(r_{AB})_z=-mg(z_B-z_A)$ e pertanto il lavoro della forza peso vale:

$\displaystyle W=-(mgz_B-mgz_A)=-(E_{p,B}-E_{p,A})=-\Delta E_p$

Con $E_p=mgz$ indichiamo una funzione della coordinata z del punto che ha questa proprietà: il lavoro è eguale all’opposto della variazione di questa funzione durante lo spostamento da A a B e pertanto non dipende dalla particolare traiettoria che collega A e B. La funzione $E_p$ si chiama <font color=red>energia potenziale</font> della forza peso.

> Se il punto B si trova in una posizione più bassa di A il lavoro della forza peso è positivo andando da A a B e $E_p$ diminuisce. Possiamo osservare che questo è lo spostamento naturale di un punto P sottoposto alla sola forza peso. Se il punto B è invece in una posizione più alta di A, $W<0$ e $E_p$ aumenta. 
 
Per fare avvenire questo spostamento bisogna che il punto abbia una sufficiente velocità iniziale così che la diminuzione di energia cinetica eguagli il lavoro oppure bisogna applicare al punto un’altra forza il cui lavoro motore superi in modulo il lavoro resistente della forza peso.

## Lavoro di una forza costante

La trattazione fatta per la forza peso si estende a qualsiasi altra forza costante F. Prendendo come asse z un asse parallelo e discorde a F, il lavoro di F per uno spostamento tra due punti, le cui coordinate z sono $z_A$ e $z_B$, vale

$W=-(F_{Z,B}-F_{Z,A})=-\Delta E_p$

dove ora $E_p=F_Z$. Se invece si scegliesse l'asse z concorde a F, sarebbe sempre $W=-\Delta E_p$, con $E_p=-F_Z$

## Lavoro di una forza elastica

Il lavoro della forza elastica quando si comprime una molla per uno spostamento lungo l'asse x vale

$W=\displaystyle\int_A^B-kxu_xdxu_x=-k\int_A^Bxdx={1\over 2}kx^2_A-{1\over 2}kx_B^2$ con $A=0$ e $B=d$ dove per $d$ si intende la compressione.

La molla compressa ha accumulato $\displaystyle -W=E_p={1\over 2}kx^2$ energia, che è l’ energia potenziale elastica.

Per comprimere la molla il lavoro è negativo, mentre quando si decomprime una molla, il lavoro della forza elastica è positivo ed è pari a $\displaystyle W={1\over 2}kx^2$
> La stessa quantità di lavoro usata per comprimere la molla, è rilasciata quando la molla si decomprime.

## Lavoro di una forza di attrito radente

Ricordando la forza di attrito radente, il vettore $u_v$ è parallelo e concorde allo spostamento $ds$, il lavoro corrispondente si scrive:

$W=\displaystyle\int_A^BF_{ad}ds=\int_A^B-\mu_dNu_vds=-\mu_dN\int_A^Bds$

dove l'integrale scalare $\displaystyle\int_A^Bds$ è la lunghezza del percorso da A e B, misurata lungo A la traiettoria effettiva del punto materiale. Pertanto, a parità dei fattori $\mu_d$ e N abbiamo un lavoro diverso a seconda della forma della traiettoria. Il lavoro della forza di attrito radente dipende dal percorso e non è esprimibile come differenza dei valori di una funzione delle coordinate nei punti *A* e *B*, diversamente da quanto avviene per la forza peso e per la forza elastica. Il risultato resta vero in generale, anche se la reazione normale non è costante.

> Il lavoro della forza di attrito radente è sempre negativo, cioè è
lavoro resistente (si noti che se cambia il verso del moto, cambia anche quello della forza di attrito, sempre opposta alla velocità).

Perché possa verificarsi il moto o deve agire un’altra forza che produca un lavoro motore oppure, in assenza di questa, il punto deve possedere una certa velocità iniziale ovvero una certa energia cinetica $E_{k,A}$. L'energia cinetica diminuisce lungo il percorso ed in B la velocità è minore che in A, in particolare, data $E_{k,A}$ e se N è costante, il punto si ferma dopo una percorso $s_{AB}=\displaystyle {E_{k,A}\over\mu_dN}$

---
# Potenza

La potenza corrisponde al lavoro per unità di tempo:

$\displaystyle P={dW\over dt}=F{dr\over dt}=Fv$

Questa è la potenza istantanea, in generale variabile durante il moto, e caratterizza la rapidità di erogazione del lavoro. La potenza media è il rapporto:

$\displaystyle P_m={W\over t}$

cioè il lavoro totale diviso per il tempo durante cui il lavoro è stato svolto. Tale grandezza risulta particolarmente importante per qualificare le prestazioni di un dispositivo o macchina che fornisce lavoro. A parità di lavoro totale svolto, ha maggiore potenza quella macchina che lo eroga in minore tempo.

---

# Energia cinetica

Riprendiamo la relazione relativa al lavoro infinitesimo associato ad uno spostamento ds:

$\displaystyle dW=F_Tds=ma_Tds=m{dv\over dt}ds=m{ds\over dt}dv=mvdv$

Abbiamo trovato così il legame esplicito tra il lavoro infinitesimo e la variazione infinitesima del modulo della velocità rendendo quantitativa la discussione fatta in precedenza. Per un percorso finito dalla posizione A a quella B abbiamo:

$\displaystyle W=\int_A^Bmvdv={1\over 2}mv_B^2-{1\over 2}mv_A^2=E_{k,B}-E_{k,A}=\Delta E_k$

Il lavoro è eguale alla variazione della quantità $\large {1\over 2}mv^2$ che si chiama energia cinetica del punto materiale. L'equazione nota come teorema dell’energia cinetica, è stata ricavata utilizzando la legge di Newton e pertanto ha validità generale, qualunque sia la forza che agisce.

Se $W>0$, l’energia cinetica finale è maggiore di quella iniziale mentre se $W<0$ l’energia cinetica finale è minore di quella iniziale. Questo è il caso del lavoro delle forze di attrito e pertanto, se agiscono solo tali forze, la velocità diminuisce. Infine, se $W=0$, l’energia cinetica resta costante; ciò si verifica, per esempio, nel moto circolare uniforme: il lavoro della forza centripeta, unica forza agente, è nullo e quindi la velocità rimane costante in modulo.

> Si faccia attenzione al fatto che la nozione di lavoro, e quindi di variazione di energia cinetica, è necessariamente legata a quella di spostamento. Se non c’è spostamento non può esserci lavoro, qualunque sia la forza applicata. Quando si spinge un corpo e questo non si sposta perché è presente un attrito statico, non c’è lavoro né motore né resistente, così come non si compie lavoro quando si spinge con una mano contro un muro.

Tip: calcolare il lavoro totale che svolge il corpo tra A e B per poi eguagliarlo al teorema dell'energia cinetica.
Esempio per un corpo che sale lungo un piano inclinato lungo $d$ con attrito:
$\overline{AB}=d$
Il corpo subisce una forza peso che si divide in componente $x$ e $y$. 

$\begin{gather}
F_a=-\mu gdcos\theta \\
F_{Px}=mgdsen\theta \\
W=F_a+F_{Px}={1\over 2}mv_B^2-{1\over 2}mv_A^2 
\end{gather}$

Infine il lavoro può essere sempre espresso come:
$L=\Delta E_c \lor L=\Delta E_p \lor L=\Delta E_m$

---

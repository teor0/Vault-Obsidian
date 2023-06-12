#fisica 
[[Lavoro, potenza ed energia cinetica]]
# Forze conservative

I tre esempi di calcolo di lavoro precedenti presentano una differenza sostanziale: nei primi due (forza peso e forza elastica) il lavoro viene a dipendere solo dalle coordinate delle posizioni *A* e *B* e non dal particolare percorso che congiunge *A* a *B*, nel terzo (forza di attrito) invece il lavoro dipende dalla traiettoria.

Le forze del primo tipo, quelle per cui il lavoro non dipende dal percorso, si chiamano forze conservative. Per il calcolo del lavoro possiamo utilizzare qualsiasi percorso che colleghi *A* a *B*:

$\displaystyle\int_A^B(F*ds)_I=\int_A^B(F*ds)_{II}=\int_A^BF*ds$

> Il lavoro lungo il percorso I coincide con quello lungo il percorso II o lungo qualsiasi altro

Il lavoro è pertanto esprimibile come differenza dei valori che una funzione delle coordinate assume in *A* e in *B.* Ciò comporta che se si inverte il senso di percorrenza, cioè si va da *B* a *A*, cambia solo il segno del lavoro:

$\displaystyle\int_A^BFds=-\int_A^BFds$

Per un percorso chiuso ABA lungo la traiettoria -II (ovvero la traiettoria II percorsa in senso inverso) si ha

$\displaystyle\int_A^B(F*ds)_I+\int_A^B(F*ds)_{-II}=\int_A^B(F*ds)_I-\int_A^B(F*ds)_{II}=0$

> Capiamo quindi che lungo un percorso chiuso il lavoro è nullo.

Questa proprietà si può assumere come definizione di forza conservativa.

---
# Energia potenziale

La funzione delle coordinate di cui abbiamo parlato finora si chiama energia potenziale e per tutte le forze conservative vale che:

$W=E_{p,A}-E_{p,B}=-\Delta E_p$

Non esiste una formula generale per l'energia potenziale, ma l'espressione esplicita dipende dalla particolare forza conservativa a cui si riferisce. Nei 2 casi discussi della forza peso e forza elastica, si è ottenuto rispettivamente, $E_p=mgz$ e $E_p=\displaystyle {1 \over 2}kx^2$.

Per il calcolo del lavoro vale la formula dell'energia potenziale se, le forze sono conservative altrimenti bisogna usare la definizione, comunque si trovi W, vale sempre la definizione di energia cinetica.

La formula trovata permette il calcolo esplicito dell’espressione dell’energia potenziale e ne precisa il significato fisico, legandolo alla capacità di fornire lavoro. Infatti quando durante il moto l’energia potenziale diminuisce ($\Delta E_p<0$) il lavoro compiuto dalla forza è >0. Al contrario se l'energia potenziale aumenta ($\Delta E_p>0$) il lavoro è negativo e ciò vuol dire che bisogna fornire lavoro esterno, per fare avvenire quel determinato processo.

> Da una forza conservativa non si può ricavare lavoro se il percorso è chiuso ovvero, se il processo è ciclico.

## Forze non conservative e dissipative

Ci sono forze per cui non vale la proprietà di invarianza del lavoro rispetto al percorso e non è quindi possibile espremire il lavoro tramite le differenze dei valori di una funzione delle coordinate. Queste forze non sono conservative e non si può introdurre l'energia potenziale per loro. Un tipo particolare di forze non conservative sono le forze di attrito dette anche, forze dissipative.

---

# Principio di conservazione dell'energia meccanica

Se agiscono solo forze conservative vale sia la definizione di energia cinetica che di energia potenziale ed intuitivamente, essendo il teorema dell'energia cinetica $W=\Delta E_c$,  abbiamo che $\Delta E_c=-\Delta E_p$ ovvero:

$\begin{gather}
W=\Delta E_k=E_{k,B}-E_{k,A} \\
W=-\Delta E_p=E_{p,A}-E_{p,B} \\
E_{k,A}+E_{p,A}=E_{k,B}+E_{p,B}
\end{gather}$

> La somma dell'energia cinetica e potenziale di un punto materiale che si muove sotto l'azione di forze conservative resta costante durante il moto, ossia si conserva

Tale somma si chiama energia meccanica e vale pertanto, in presenza di forze conservative. Il principio di conservazione dell'energia meccanica è quindi:

$E_m=E_k+E_p=costante$

Possiamo perciò dedurre che, il lavoro ottenuto a spese della diminuzione di energia potenziale causa un aumento dell’energia cinetica e viceversa.

> Durante il moto avviene una trasformazione da una forma di energia all’altra, per tramite di lavoro compiuto e assorbito, ma il contenuto energetico totale, dato dall’energia meccanica, non cambia.

Quando agiscono, come avviene in generale, sia forze conservative che non conservative, il lavoro complessivo è dato dalla somma del lavoro delle forze conservative $W_C$ e di quello delle forze non conservative $W_{nc}$:

$W=W_c+W_{nc}=E_{k,B}-E_{k,A}$

## Lavoro delle forze non conservative

In presenza di forze non conservative l’energia meccanica non resta costante e la sua variazione è eguale al lavoro delle forze non conservative.

$\displaystyle E_{p,A}-E_{p,B}+W_{nc}=E_{k,B}-E_{k,A}\Rightarrow W_{nc}=(E_{k,B}+E_{p,B})-(E_{k,A}+E_{p,A})=E_{m,B}-E_{m,A}$

In qualunque processo meccanico si osserva sperimentalmente che è sempre presente una forza di attrito che si oppone al moto. Se tutte le altre forze sono conservative, $W_{nc}=W_{diss}<0$ e quindi l'energia meccanica diminuisce durante il processo.

A questa situazione si può porre rimedio con l’intervento di altre forze non conservative e l’energia meccanica del punto può essere mantenuta costante o anche aumentare. Se però si considera un sistema più vasto, costituito dal punto e dal meccanismo che ha fornito il lavoro non conservativo, si trova sempre che l’energia meccanica complessiva non si conserva, ma diminuisce a causa di effetti dissipativi.

---
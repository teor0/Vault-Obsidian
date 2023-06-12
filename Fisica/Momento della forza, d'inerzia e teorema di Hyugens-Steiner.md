#fisica 
[[Urti tra 2 punti materiali, forze impulsive ed impulso]]
# Momento della forza
Supponiamo di avere una massa vincolata ad un vettore $\overrightarrow{r}$ che subisce una forza $\overrightarrow{F}$. 
![[momento.jpg|400x400]]
Traslando $\overrightarrow{r}$ su m ed utilizzando le componenti di $\overrightarrow{F}$ definiamo $\overrightarrow{\tau}=\overrightarrow{r}\times\overrightarrow{F}$ il prodotto che tenderà a ruotare la massa m come momento. Perciò il momento della forza è definito come: $\displaystyle\overrightarrow{\tau}=\overrightarrow{r}\times\overrightarrow{F}$ in modulo $\displaystyle\overrightarrow{\tau}=|rF|$.

Unità di misura del momento della forza è Nm, ovvero il Joule.
Facendo un analogia con il 2° principio di Newton, la forza $F=ma$ fa traslare il corpo mentre il momento lo fa ruotare. Quanto più $\alpha \simeq 0$ allora il momento sarà minimo, mentre quanto pi+ $\alpha\simeq 1$ allora il momento sarà massimo. Quando ad un punto sono applicate più forze con risultante R uguale alla sommatoria di tale forze, si ha:

$\overrightarrow{\tau}=\overrightarrow{r}\times\overrightarrow{R}$

il momento complessivo è uguale al momento della forza risultante.

> Pertanto un sistema di forze applicate nello stesso punto può sempre essere sostituito, nel calcolo dell’accelerazione, del lavoro e del momento complessivi, dalla forza risultante. Tale proprietà non può evidentemente essere utilizzata se le forze sono applicate in punti diversi.

---
# Momento d'inerzia
Supponiamo di porre la massa su una circonferenza, ![[mominerzia.jpg|400x400]] se $\overrightarrow{r}$ è fisso allora ottengo una rotazione se $\overrightarrow{r}$ e $\overrightarrow{F}$ sono perpendicolari per tutto il moto partendo da $ma_T=F$ e $\displaystyle l=\theta r\implies {dl\over dt}=r{d\theta\over dt}$ si nota che $\displaystyle{dl\over dt}=vt$ e $\displaystyle{d\theta\over dt}=\omega$, ma se derivo una velocità ottengo l'accelerazione perciò $\displaystyle {d^2l\over dt^2}=r{d^2\theta\over dt^2}\implies a_T=r\alpha$. A questo punto l'equazione diventa $mr\overrightarrow{\alpha}=\overrightarrow{F}$ e se moltiplichiamo entrambi i membri per $\overrightarrow{r}$ si ottiene $\overrightarrow{r}\times mr\overrightarrow{\alpha}=\overrightarrow{r}\times\overrightarrow{F}$. Se si calcola il modulo si ottiene $|\overrightarrow{r}\times |mr\overrightarrow{\alpha}||=|\overrightarrow{r}\times\overrightarrow{F}|\implies mr^2\alpha sen(\theta)=rFsen\theta$ che con $\theta=90\implies mr^2\alpha=rF$. Come visto prima però $\displaystyle\tau=rF\implies \tau=mr^2\alpha$, da questa equazione molto simile al secondo principio di Newton si può ottenere l'accelerazione $\displaystyle\overrightarrow{\alpha}={\tau\over mr^2}$ ma soprattutto l'equazione $I=mr^2$ che altro non è che il momento d'inerzia. 
La componente perpendicolare è quella che interessa il moto.

> Tale momento svolge il ruolo della massa nella traslazione per la rotazione. La difficoltà di mettere in rotazione un corpo è il momento d'inerzia.

La relazione tra i momenti può essere scritta come: $I\overrightarrow{\alpha}=\overrightarrow{\tau}$ 
Se agiscono 2 o più momenti per stabilire come ruota il corpo occorre calcolare il momento totale dato dalla somma dei momenti agenti sul corpo. Per la regola della mano destra se il vettore è uscente la rotazione è antioraria, se invece è entrante è oraria.
Il braccio è il vettore che collega il polo al punto d'applicazione della forza.

Molto importante per la rotazione è la scelta del polo, che indipendentemente dalla scelta deve risultare giusto, inoltre una scelta giusta comporta a facilitazioni nei calcoli. 

> Se la massa del corpo rigido è distribuita in modo omogeneo, ad esempio una sfera, è più facile far ruotare il corpo rispetto ad un corpo che ha la massa distribuita tutta in una dimensione rispetto al centro di massa.

---
# Teorema di Huygens-Steiner
Se si sceglie un altro asse per il quale vengono meno le condizioni di simmetria  il calcolo diventa complicato. Il teorema di Huygens-Steiner semplifica enormemente il problema.

> Il momento d’inerzia di un corpo rispetto ad un generico punto si può trovare come la somma tra il momento d'inerzia, calcolato nel asse passante per il centro di massa, più la massa del corpo per la distanza tra il polo ed il centro di massa al quadrato. 

$\displaystyle I=I_{CM}+md^2$
![[corporigidohs.jpg|400x400]]
L'asse è uscente dal foglio ed il corpo ruota rispetto al centro di massa. Scelto il punto O, l'asse passante per O ha momento pari a $\displaystyle I=I_{CM}+m{\overline{CMO}}^2$

---




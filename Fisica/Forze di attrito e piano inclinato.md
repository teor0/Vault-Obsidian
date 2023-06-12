#fisica 
[[Azione dinamica delle forze, risultante, equilibrio statico e reazione vincolare]]
# Coefficiente di attrito statico e dinamico
Applichiamo ad un corpo appoggiato su un tavolo, con il piano di appoggio orizzontale, una forza F tale da presentare una componente $F_1$ normale al piano di appoggio e una $F_2$ parallela al piano stesso. Si osserva sperimentalmente che il corpo non entra in movimento, per effetto della componente $F_2$ della forza applicata, fino a che il modulo di $F_2$ non superi il valore $\mu_sN$ dove $\mu_s$ è il coefficiente di attrito statico ed N, è il modulo della componente normale al piano di appoggio della reazione vincolare.

> La condizione perchè il corpo possa essere messo in movimento per effetto della forza applicata è quindi data da $F_2>\mu_sN$

Supponiamo che la forza F formi un angolo $\theta$ con il piano di appoggio. Pertanto $F_1=Fsen\theta$ e $F_2=Fcos\theta$. La reazione R del piano in condizioni di equilibrio statico del corpo è tale che:

$R+P+F=0$

![[reazione.jpg | 400x500]]

Proiettiamo la formula secondo le due direzioni ortogonali tra loro, quella normale al piano di appoggio assunta positiva verso l’alto e quella parallela al piano stesso (positiva nel verso di $F_2)$. Chiamiamo N e $F_{as}$ le corrispondenti componenti di R.

L'equazione fornisce:

$N+P+F_1=0\Rightarrow N=P-F_1=P-Fsen\theta$

$F_{as}+F_2=0\Rightarrow F_{as}=-F_2=-Fcos\theta$

La condizione di appoggio del corpo è data da N>0 cioè $P>Fsen\theta$, se questa è soddisfatta la componente parallela al piano di appoggio della reazione vincolare controbilancia, quando il corpo è in quiete, la componente orizzontale della forza applicata. Dovendo essere, $F_2\le\mu_sN$, la condizione di quiete si scrive:

$\displaystyle {Fcos\theta\le\mu_s(P-Fsen\theta)\Rightarrow F\le{\mu_smg\over cos\theta+\mu_ssen\theta}}$

In particolare se:

$\theta=0$, $F_1=0$, $F_2=F$, $N=P=mg$ e $F_{as}=-F_2=-F$ allora la condizione di quiete si scrive

$F\le\mu_sN=\mu_smg$

> Riassumendo, a causa della forza che preme il corpo contro il piano, si sviluppa una forza di attrito statico $F_{as}$ che è capace di equilibrare la forza orizzontale applicata $F_2$

Quando $F_2$ supera $\mu_sN$ il corpo entra in movimento lungo il piano e si osserva che si oppone al moto la forza di attrito radente dinamico $\large F_{ad}=\mu_dNu_v$ dove $\mu_d$ rappresenta il coefficiente di attrito dinamico che risulta sempre minore di $\mu_s$. L'equazione del moto è pertanto:

$Fcos\theta-\mu_dN=ma$

La componente normale della reazione N è sempre data da $P-Fsen\theta$ in quanto ortogonalmente al piano non c’è moto, non c’è accelerazione e la risultante delle forze è nulla. La forza di attrito dinamico non dipende dalla velocità del corpo rispetto al piano di appoggio ed ha verso contrario alla direzione del moto e quindi al versore della velocità. Vettorialmente:

$\displaystyle F_{ad}=-\mu_dNu_v$

## Forze di coesione

Le forze di attrito radente hanno origine dalle forze di coesione tra due materiali.

> Il valore del coefficiente di attrito dipende dallo stato delle superficie a contatto e dalla loro composizione chimica. Una eccessiva levigatura fa aumentare la coesione e quindi l’attrito. Se le superficie vengono invece bagnate, la forza di attrito diminuisce notevolmente.

Si consideri però che le forze di attrito radente sono sempre presenti, per quanto si possa tentare di ridurle. Quindi se vogliamo realizzare un moto uniforme dobbiamo applicare una forza eguale e contraria alla forza di attrito in modo che la risultante sia nulla. È questa la condizione pratica che deve essere realizzata in ogni moto uniforme al fine di ottenere una situazione di equilibrio dinamico. Soltanto per esaminare casi limite semplificati porremo eguale a zero la forza di attrito, diremo allora che la superficie di scorrimento è liscia.

---
# Piano inclinato

Consideriamo un corpo, assimilabile ad un punto materiale di massa m, che possa muoversi sotto l’azione del suo peso e di eventuali altre forze, compresa la forza di attrito radente, su una superficie piana inclinata di un angolo $\theta$ rispetto ad un piano orizzontale. Se agisce solo la forza peso P, in assenza perciò di attrito tra corpo e piano inclinato, si ha secondo la legge di Newton:

$P+N=ma$

dove N è la reazione vincolare del piano di appoggio che ha un’unica componente normale al piano stesso. Scomponendo lungo le direzioni ortogonale e parallela al piano inclinato si ottiene:

$mgcos\theta-N=0$

$mgsen\theta=ma$

dato che il corpo è vincolato a muoversi lungo il piano inclinato. Dalla prima condizione si calcola il valore della reazione vincolare, $N=mgcos\theta$, dalla seconda il valore dell'accelerazione, $a=gsen\theta<g$, quindi il corpo scende cono moto uniformemente accelerato con un'accelerazione minore di quella di gravità.

Se esiste un attrito radente tra il piano inclinato e il corpo, il moto lungo il piano non può iniziare solamente se

$\displaystyle mg sen\theta\le\mu_sN=\mu_smgcos\theta$

la componente normale di R vale ancora $N=mgcos\theta$ però c'è ora anche una componente parallela al piano inclinato che vale, in equilibrio statico, $-mgsen\theta$. Pertanto la condizione per l'equilibrio statico è

$tan\theta\le\mu_s$:condizione equilibrio statico in caso di attrito radente

Per avere moto occorre aumentare l’angolo di inclinazione $\theta$ in modo da non soddisfare la condizione suddetta, vale allora l'equazione:

$mgsen\theta-\mu_dmgcos\theta=ma$

$\displaystyle a=(sen\theta-\mu_dcos\theta)g$

Dovendo essere il termine tra parentesi positivo, si ha che per il coefficiente di attrito dinamico è $\mu_d<tan\theta$. In particolare, se $\mu_d=tan\theta\Rightarrow a=0$ il moto è uniforme e si tratta di un esempio di equilibrio dinamico.

> Riassumendo, se il corpo è fermo sul piano inclinato rimane fermo per tutti gli angoli di inclinazione compresi tra $0$  e $\theta_s$ tale che: $tan\theta=\mu_s$.

## Casi di moto

- Per $\theta>\theta_s$ il corpo non può restare fermo e scende lungo il piano inclinato. Però, una volta che il corpo si è messo in movimento, poiché la forza di coesione in queste condizioni è minore di quella in quiete, si può avere moto anche per angoli minori di $\theta_s$ precisamente compresi tra $\theta_s$ e $\theta_d<\theta_s$ tale che $\large tan(\theta_d)=\mu_d$.
- Se invece il corpo all’istante iniziale sta scendendo lungo il piano con velocità $\large v_0$, esso si ferma se $\large mgsen\theta<\mu_dmgcos\theta$ cioè se $tan\theta<\mu_d$.
- Si muove di moto uniformemente accelerato se $\large tan\theta>\mu_d$ e prosegue con velocità $\large v_0$ se $tan\theta=\mu_d$. L’unica differenza rispetto alla partenza da fermo è che si può avere moto anche se $tan\theta<\mu_d$ proprio perché c’è una velocità iniziale.

---

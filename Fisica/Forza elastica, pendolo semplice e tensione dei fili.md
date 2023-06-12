#fisica 
[[Forze di attrito e piano inclinato]]
# Forza elastica

Si definisce forza elastica una forza di direzione costante, con verso rivolto sempre ad un punto O, chiamato centro, e con modulo proporzionale alla distanza da O. Se assumiamo come asse x la direzione della forza e come origine il centro, possiamo scrivere:

$F=-kxu_x$

dove k è una costante positiva detta costante elastica, e $u_x$ è il verso dell'asse x.

Il moto risultante per effetto di una forza elastica è rettilineo, qualora la velocità iniziale sia nulla o diretta come $u_x$. L'accelerazione vale:

$\displaystyle a={F\over m}=-{k\over m}x=-\omega^2x$

e quindi il moto è armonico semplice con pulsazione $\large\omega$ e periodo T determinati dal rapporto tra la costante elastica e la massa del punto materiale a cui è applicata la forza elastica:

- $\displaystyle \omega=\sqrt{k\over m}$
- $\displaystyle T={2\pi\over\omega}=2\pi\sqrt{m\over k}$

Una forza elastica viene praticamente applicata tramite una molla, questa presenta in genere una lunghezza a riposo, cioè quando non si trova in condizioni di compressione o di estensione, di valore finito $\large l_0$. Se la molla viene estesa assume una lunghezza $\large l>l_0$, essa sviluppa una forza F che tende a riportarla alla condizione di riposo.

$F=-k(l-l_0)=-kx$

dove x>0 rappresenta la deformazione. Se invece la molla viene compressa alla lunghezza $\large l<l_0$, la forza ha la stessa espressione, con x<0. In ogni caso possiamo scrivere la forza, come già detto.

Il modulo di questa forza di richiamo è proporzionale alla deformazione fino a che non si supera il limite di elasticità della molla. Se vogliamo mantenere la molla deformata con una determinata lunghezza l dobbiamo applicare alla molla una forza eguale ed opposta alla forza esercitata dalla molla.

![[molla.jpg| 350x450]]

esempio estensione

Discutiamo tale situazione di equilibrio con la molla deformata $(l-l_0=x>0)$ osservando la figura sotto in cui la molla estesa è fissata nell’estremo Q di una parete.

![[molla2.jpg| 300x300]]

I punti P e Q sono fermi e pertanto le forze applicate a ciascun punto devono essere eguali ed opposte. Nel punto P la forza elastica $F_2$ dovuta alla deformazione della molla (in modulo kx) viene bilanciata da una forza esterna $F_1=-F_2$. Nel punto Q la situazione è analoga, solo che la forza elastica $F_3$ è bilanciata dalla reazione vincolare, che si sviluppa nel punto di aggancio, $F_4=-F_3$. Considerando che la molla, nel suo insieme, è ferma, deve essere nulla la risultante delle forze applicate alla molla, deve cioè essere $F_1=-F_4$ da cui segue $F_2=-F_3$.

> Da questo risultato deduciamo che se abbiamo una molla libera ad entrambi gli estremi e vogliamo deformarla di una quantità x, dobbiamo applicare ai due estremi due forze eguali e contrarie di modulo kx
>

Supponiamo ora di avere la molla bloccata nell’estremo Q, deformata di $x_0$, e che in P sia fissato alla molla un punto materiale di massa m (la massa della molla è trascurabile rispetto a m). Se all’istante t=0 il punto viene lasciato libero con velocità nulla, esso si muove di moto armonico per effetto della forza elastica agente su di esso.

$\displaystyle m{d^2x\over dt^2}=-kx$

---
# Pendolo semplice

Il pendolo semplice è costituito da un punto materiale appeso tramite un filo inestensibile e di massa trascurabile. La posizione di equilibrio statico è quella verticale, con il punto fermo ed il filo teso. La forza esercitata dal filo vale in modulo:

$T_F=mg$

Se spostiamo il punto dalla verticale esso inizia ad oscillare attorno a questa, lungo un arco di circonferenza di raggio L, pari alla lunghezza del filo, in un piano verticale. Vogliamo studiare, in assenza di attrito, questo moto oscillatorio.

Le forze agenti sul punto P sono il peso mg e la tensione del filo $T_F$ per cui il moto è regolato da $mg+T_F=ma$.

Consideriamo le componenti lungo la traiettoria, orientata come in figura, e ortogonalmente alla traiettoria (verso positivo da P a O).

![[pendolo.jpg| 600x500]]

$R_T=-mgsen\theta=ma_T$

$R_N=T_F-mgcos\theta=ma_N$

Il segno negativo della componente lungo la traiettoria è dovuto al fatto che la forza ha segno opposto rispetto a quello della coordinata s sulla traiettoria. Infatti per s<0, posizioni sull’arco di circonferenza a sinistra della verticale, la forza è diretta secondo il verso assunto positivo, mentre per s>0, a forza è diretta secondo il verso negativo (e il risultato non dipende dalla scelta del verso di s). Fisicamente $R_T$ è una forza di richiamo che tende a riportare il punto sulla verticale, anche se non è di direzione costante come nel caso delle forze elastiche.

Riagganciandoci all'accelerazione angolare:

$\displaystyle a_T=L{d^2\theta\over dt^2}\Rightarrow {d^2\theta\over dt^2}=-{g\over L}sen\theta$

$\displaystyle a_N={v^2\over L}\Rightarrow m{v^2\over L}=T_F-mgcos\theta$

La prima è l’equazione differenziale del moto del pendolo, la cui soluzione ci fornisce la legge oraria del moto $\theta(t)$ però per $\theta$ qualunque, la soluzione è analiticamente complicata. Consideriamo allora piccoli valori di $\theta$ ed una volta analizzata la serie per sen$\theta$, abbiamo che per piccole oscillazioni l'equazione differenziale diventa:

$\displaystyle {d^2\theta\over dt^2}+{g\over L}\theta=0$

e coincide con quella del [[Moto in due dimensioni#Moto armonico semplice|moto armonico semplice]] posto $\displaystyle \omega^2={g\over L}$. In conclusione il moto del pendolo è oscillatorio armonico quando l’ampiezza delle oscillazioni è piccola così che $sen\theta\cong\theta$. La legge oraria del moto è:

$\displaystyle\theta=\theta_0sen(\omega t+\phi)$

l’ampiezza $\theta_0$ dell’oscillazione e la fase iniziale $\phi$ dipendono dalle condizioni iniziali del moto. Il periodo del moto T è dato da:

$T=\displaystyle {2\pi\over\omega}=2\pi\sqrt{L\over g}$

ed è indipendente dall'ampiezza. La legge oraria dello spostamento lungo l’arco di circonferenza è dato da:

$s=L\theta=L\theta_0sen(\omega t+\phi)$

mentre la velocità angolare e la velocità lineare hanno le espressioni

$\displaystyle {d\theta\over dt}=\omega\theta_0cos(\omega t+\phi)$

$\displaystyle v={ds\over dt}=L{d\theta\over dt}=L\omega\theta_0cos(\omega t+ \phi)$

La velocità è massima quando il punto passa per la verticale cioè $\theta=0$, e nulla agli estremi delle oscillazioni dove il verso del moto si inverte.

Quando l’ampiezza delle oscillazioni non è piccola il moto è ancora periodico, ma non armonico, e il periodo T' dipende dall'ampiezza. Risolto il problema del moto, e quindi note $\theta(t)$ e v(t), possiamo ritornare all’equazione del moto proiettata sulla normale alla traiettoria e calcolare la tensione del filo che sostiene il punto:

$T_F=\displaystyle m[gcos\theta(t)+{v^2(t)\over L}]$

La tensione è massima nella posizione verticale, dove sia $cos\theta(t)$ che v(t) assumono i valori massimi, ed è minima nei punti di inversione.

> Queste conclusioni valgono qualunque sia il valore dell’ampiezza

---
# Tensione dei fili
Nel pendolo semplice, il filo di sostegno serve per applicare una certa forza al punto in movimento: il filo risulta teso e la forza, con direzione lungo il filo teso, che questo esercita sul punto viene chiamata tensione del filo. Il filo può essere fissato in un estremo ad un punto fisso e nell’altro ad un punto materiale oppure può collegare due punti materiali. Supporremo sempre che il filo sia inestensibile, cioè che la sua lunghezza sia costante, e di massa trascurabile rispetto alle altre masse.

Per chiarire il concetto di tensione consideriamo un filo teso in quiete e prendiamo in esame un elemento infinitesimo di esso. Tale elemento è tirato dalle due parti restanti di filo e l’equilibrio statico richiede che le due forze, agenti sull’elemento di filo, siano eguali in modulo e direzione e di verso opposto (caso a). Ciò vale per qualunque elemento di filo e il valore della tensione è lo stesso ovunque, in particolare ad un estremo T=-F (caso b). Per il filo AB nel suo insieme si ha la situazione c della figura e deve essere in modulo $F_A=F_B=T$ per tendere il filo si applicano le forze F e -F e la tensione, in modulo, è uguale al modulo di F.

![[filo.jpg| 450x400]]

Consideriamo adesso un filo teso in movimento. L’ipotesi che il filo sia inestensibile comporta che tutti i punti del filo, compresi gli estremi, abbiano la stessa accelerazione, pertanto due corpi in movimento collegati da un filo teso devono avere la stessa accelerazione.

![[collegati.jpg| 750x150]]

L’ipotesi che il filo abbia massa trascurabile fa sì che il prodotto ma risulti nullo per il filo di conseguenza il valore della tensione durante il moto è lo stesso in qualunque punto del filo, come nel caso statico. Lo stesso ovviamente succede se il moto è uniforme. Riassumendo, il filo teso esercita agli estremi la tensione T, il cui valore dipende dalle forze applicate, e che deve essere pensata come la reazione del filo alla forza che lo tende.

> Per un filo reale la tensione non può superare un valore massimo $T_{max}$, oltre il quale il filo si spezza. $T_{max}$ dipende dalla sostanza con cui è fatto il filo e dalle dimensioni geometriche. Se ad un estremo è collegato un punto materiale, la tensione T va inserita nella legge di Newton come le altre forze agenti sul corpo.

## Caso carrucola

Non è necessario che il filo sia completamente rettilineo, esso può scorrere attorno ad un perno o essere parzialmente avvolto attorno ad un disco mobile (carrucola), allo scopo di cambiare la direzione della forza.

![[carrucola.jpg| 200x900]]

Con riferimento alla figura sopra, un tratto di filo curvo è sottoposto alle due tensioni $T_1$ e $T_2$ e alla forza F reazione del perno, ortogonale al perno se questo è liscio.

In questa situazione le due tensioni, che per simmetria formano lo stesso angolo con la tangente alla circonferenza, hanno componenti tangenti eguali ed opposte per soddisfare alla relazione:

$F_T=ma_T=0$. $T_1$ e $T_2$ sono dunque eguali in modulo ed eguali sono le componenti normali la cui somma vale $F_N$. Ortogonalmente alla traiettoria si ha quindi $F_N-F=ma_N=0$ ovvero in modulo la reazione normale è eguale alla risultante delle tensioni.

## Caso bacchette solide

Oltre ai fili rettilinei si possono utilizzare, per lo stesso scopo, bacchette solide con queste differenze:

- Mentre il filo funziona in trazione, la bacchetta può funzionare in trazione ed in compressione. Per esempio, con un filo si può solo tirare un corpo mentre con una bacchetta si può anche spingerlo
- Un filo può esercitare solo forze che hanno la direzione del filo stesso, cioè non può sopportare una sollecitazione ortogonale, una bacchetta non presenta questa limitazione.

Un modo semplice per mettere in evidenza la tensione di un filo e misurarne il valore consiste nel tagliare il filo e inserire una molla di costante elastica nota k. Quando si tende il filo ai capi della molla sono applicate le forze T e -T e si misura la deformazione x. In modulo è T=kx.

## Fili inestensibili con massa non trascurabile

Quando si rilascia l’ipotesi di trascurabilità della massa, la tensione non può più essere la stessa lungo il filo. Preso un piccolo tratto di filo in movimento, abbiamo $T_1+T_2=ma\ne 0$, per cui $T_1\ne T_2$.

Riprendendo in esame il caso in cui due corpi siano collegati da un filo supponendo che il filo abbia massa $m_F$. Le forze applicate ai corpi e al filo sono rappresentate in figura e le equazioni del moto sono:

![[massa_non_trascurabile.jpg| 650x200]]

$F-T_P=m_Pa$

$T_P-T_Q=m_Fa$

$T_Q=m_Qa$

e hanno soluzione

$a=\displaystyle {F\over m_P+m_F+m_Q}$

$T_P=\displaystyle {m_F+m_Q\over m_P+m_F+m_Q}F$

$T_Q=\displaystyle {m_Q\over m_P+m_F+m_Q}F$

Vediamo che la tensione varia lungo il filo, dal valore $T_Q$ al valore $T_P>T_Q$. Se la massa è egualmente distribuita lungo il filo, cioè se la massa per unità di lunghezza è costante la tensione varia linearmente da $T_Q$ a $T_P$: detta d la lunghezza del filo e x la distanza del generico punto del filo dall'estremo Q, si ha:

$T(x)=\displaystyle T_Q+{m_FF\over m_P+m_F+m_Q}{x\over d}$

e si verifica subito $T(d)=T_P$.


---


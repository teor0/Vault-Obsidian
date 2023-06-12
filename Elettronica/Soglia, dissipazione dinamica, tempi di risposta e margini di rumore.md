---
tag: #elettronica 
created: 2023-02-21 11:11:00
updated: 2023-02-21 11:11:00
---
#elettronica 
[[Caratteristiche dei circuiti ad interruttore]]
# Valore di soglia degli interruttori
Abbiamo parlato di come nel mondo reale un circuito non ha una tensione fissa sempre pari a $0V$ o $V_{DD}$, ma ha valori che oscillano continuamente. Nella realtà un interruttore è un elemento a soglia, ovvero un interruttore si chiude se l'ingresso supera un certo valore di riferimento. Il valore di soglia è definito dalla tecnologia che si decide di usare, ad esempio un interrutore di tipo 1 ha soglia pari a: $V_{Th}=0,5V$. Un valore sufficiente a tollerare dei rumori all'interno del circuito. 
Il valore di soglia è cruciale in quanto se troppo basso, si rischia attraverso la dissipazione di potenza di superarlo e quindi di avere un comportamento opposto a quello desiderato, oppure se troppo basso, sempre attraverso la dissipazione il valore della tensione potrebbe essere non abbastanza alto da rappresentare lo stato logico '1', ma finire per rappresentare lo stato logico '0'.
La soglia è la prima caratteristica dinamica che osserviamo.
Facciamo riferimento ancora una volta all'inverter, considerando l'ingresso I che varia nel tempo per studiare dinamicamente il circuito:
![[invsignid.jpg]]
Quello rappresentato però è il diagramma ideale nel tempo, mentre quello reale presenta tempi di salita e discesa:
![[invsignreal.jpg]]
Dove il tempo di salita è l'intervallo temporale dove il segnale assume il 10% di $V_{DD}$ ed assume il 90% di $V_{DD}$, mentre il tempo di discesa è l'intervallo temporale dove il segnale si trova al 90% di $V_{DD}$ e 10% di $V_{DD}$ entrambi diversi da 0.
Come detto gli interruttori sono aperti o chiusi in base al valore di soglia $V_{Th}$, in particolare:
- Tipo 0: ON se $I\le V_{Th}$, OFF se $I> V_{Th}$.
- Tipo 1: ON se $I\ge V_{Th}$, OFF se $I<V_{Th}$.

Sempre per semplicità si presuppone che le $V_{Th}$ siano uguali per tipo 0 e 1. Si crea una indecisione, in quanto quanto $I=V_{Th}$ entrambi gli interruttori sono chiusi. Questo porta a lavorare con un circuito equivalente a:
![[intnogood.jpg]]
>La mutua esclusione non è rispettata!

Nella realtà esistono due tensione di soglia, che amplificano il problema in quanto portano ad individuare un intervallo di valori dove le reti PUN e PDN sono entrambe chiuse. Questo comporta al fatto che nel circuito la corrente $I(t)\ne 0$ sempre, e questo valore può essere anche piuttosto significativo tanto al più da portare a dissipazione di potenza dinamica. La dissipazione di potenza dinamica è pari a $P=I(t)V_{DD}$ e prende il nome di potenza di corto circuito. Tale potenza è una caratteristica dinamica in quanto si osserva durante la variazione degli ingressi. Riferendoci al diagramma reale visto in precedenza, quando il segnale è costante il circuito dissipa potenza statica mentre quando il segnale commuta il circuito dissipa potenza dinamica. La potenza di corto circuito è un contributo della dissipazione dinamica ma ne esiste un altro.

---
## Dissipazione in commutazione completa
Supponiamo che I abbia la seguente variazione che viene detta <font color=red>commutazione completa</font>, in quanto da uno stato si passa ad un altro e si ritorna allo stato originale.
![[commcomp.jpg]]
Nell'istante $t_1,\ I=V_{DD}$ per cui gli interruttori saranno nello stato OFF (tipo 0), ON (tipo 1). Per semplicità consideriamo la $R_{OFF}$ come un circuito aperto essende molto alta come resistenza. La tensione corrispondente all'uscita del circuito sarà data dalla differenza di potenziale ai capi di $C_L$ che essendo scarica è pari a 0 ovvero, $0V$.
![[state1.jpg|375x550]]
Nell'istante $t_2$, il circuito equivale a ![[state2.jpg|375x550]] la capacità $C_L$ tende a caricarsi tramite $V_DD$ fino ad arrivare al valore $V_{out}=V_{DD}$. Una parte di energia è accumulata in $C_L$ ma una parte è dissipata per mezzo di $R_{ON}$, tale energià è pari a: $E_C=E_{ACC}+E_{DISS}$. La dissipazione di calore per effetto Joule avviene in quanto gli interruttori non sono ideali.
Per valutare l'energia messa in gioco, devo considerare la potenza istantanea $p(t)=i(t)v(t)$ tra 0 e $\infty$ ovvero: $\displaystyle E_C=\int^{\infty}_{0}i(t)v(t)dt=\int^{\infty}_{0}i(t)V_{DD}dt=V_{DD}\int^{\infty}_{0}i(t)dt$

La corrente $i(t)$ è la stessa corrente che passa nel condensatore che è pari a $\displaystyle i_C(t)=C_LdV_C(t)=C_L{dV_{out}(t)\over dt}$ dove $dV_C(t)$ è la derivata della tensione ai capi della capacità. Si ottiene perciò:
$\displaystyle E_C=V_{DD}\int^{\infty}_{0}C_L{dV_{out}(t)\over dt}dt=V_{DD}C_L\int^{\infty}_{0}dV_{out}(t)$
per continuare effettuo un cambio di variabile dove per $t=0, V_{out}=0V$ e per $t=\infty, V_{out}=V_{DD}$ ottenendo infine
$\displaystyle E_C=V_{DD}C_L\int^{V_{DD}}_{0V}dV_{out}(t)$ $=\displaystyle V_{DD}C_L[V_{out}]_0^{V_{DD}}=C_LV_{DD}^2$

Di questa $\alpha C_LV_{DD}^2$ viene dissipata mentre $(1-\alpha)C_LV_{DD}^2$ viene accumulata.

Nell'istante $t_3$ la capacità inizia a scaricarsi e l'energia accumulata precedentemente è dissipata da $R_{ON}$. Questo ci consente di dire che in una commutazione completa tutta l'energia messa in gioco dal generatore è dissipata, ovvero $E_{Tdiss}=C_LV_{DD}^2$. Da qui otteniamo la potenza dissipata totale dividendo per il tempo di osservazione totale T, quindi $\displaystyle P_{diss}={E_{Tdiss}\over T}$.

In un circuito reale si verificano tante commutazioni complete che spesso si ripetono con una certa periodicità. Scrivendo $\displaystyle P_{diss}=E_{Tdiss}f$ si va a valutare come il ripetersi di commutazioni complete influenzano la dissipazione di potenza. Questo contributo di potenza viene chiamato <font color=orange> potenza di switching</font> e come visto è pari a $\displaystyle P_T=C_LV_{DD}^2f$.
All'aumentare della frequenza di funzionamento dei circuiti, la dissipazione di potenza aumenta linearmente, questo è in contrasto con l'avere dispositivi con batteria duratura ma allo stesso tempo con frequenza di funzionamento elevata. Inoltre aumentare la frequenza aumenta implicitamente la potenza di corto circuito. Si ha dipendenza quadratica dalla tensione di alimentazione e che negli ultimi anni è passata da 5V a 0,9V e questo valore di tensione rappresenta il riferimento con cui stabilire i valori logici. Lavorando a soglie non si possono utilizzare valori molto piccoli di tensione in quanto risulta difficile ottenere il corretto funzionamento del circuito, abbiamo quindi una limitazione fisica. 
Per quanto riguarda la capacità all'aumentare del numero di porte logiche che dovranno processare il segnale aumenta il contributo capacitativo, quindi ogni carico corrisponde ad un certo contributo capacitativo.
Ad esempio in questo circuito
![[contrdiss.jpg|400x400]]
complessivamente sul inverter si ha un effetto capacitativo pari a $C_L=C_{L1}+C_{L2}+C_{L3}$
Più un circuito ha un carico elevato, più dissipa potenza, per cui il fan-out è limitato per limitare la potenza dissipata.

---
## Tempi di carica e scarica e tempi di risposta
È possibile definire i tempi di carica e scarica della capacità come:
$\begin{gather}
t_{carica}=ln(2\tau_{carica})=0,69R_{ON}C_L
t_{scarica}=ln(2\tau_{scarica})
\end{gather}$
Facendo riferimento all'inverter di seguito, identifichiamo i tempi di risposta.
![[timerisp.jpg|600x600]]
Il tempo che intercorre dal momento in cui l'ingresso durante un fronte di discesa raggiunge $V_{DD}/2$ e l'uscita raggiunge salendo  $V_{DD}/2$, prende il nome di tempo di propagazione basso alto $t_{pLH}$, ovvero il tempo che l'uscita richiede per commutare dallo stato logico 0 allo stato logico 1 rispetto alla commutazione dell'ingresso. Il tempo necessario all'uscita per commutare dallo stato logico alto allo stato logico basso prende il nome di tempo di propagazione alto basso $t_{pHL}$, ovver il tempo che l'uscita richiede per commutare dallo stato logico 1 allo stato logico 0 rispetto alla commutazione dell'ingresso.
Questi tempi possono essere chiamati anche tempi di commutazione o ritardi. In generale questi 2 tempi sono diversi tra loro.

---
# Margini di rumore
Prima di passare all'ultima caratteristica dinamica, ricapitoliamo le caratteristiche esaminate nate dagli interruttori non ideali:

| Statica                         | Dinamica                                              |
| ------------------------------- | ----------------------------------------------------- |
| FAN-IN                          | FAN-OUT                                               |
| Dissipazione di potenza statica | Dissipazione di potenza di corto circuito e switching |
| -                               | Ritardo                                               |

La caratteristica più critica in quanto se non rispettata i circuiti non funzionano bene. Nell'analisi delle caratteristiche è stato preso un inverter ed esaminato individualmente, collegando in uscita la capacità che tiene conto del collegamento sul noto out. Per analizzare i margini di rumore, è necessario analizzare il comportamento di una porta logica che riceve in ingresso l'uscita di un'altra porta logica. La situazione più semplice si ha con 2 inverter collegati in cascata:
![[marginirum.jpg]]
Il primo inverter è detto pilota o driver mentre il secondo è detto di carico o load. Affinché tutto funzioni correttamente è necessario che l'inverter di carico sia in grado di valutare correttamente l'uscita del driver. Si supponga che $I1=0V$, per garantire il giusto funzionamento bisogna conoscere:
- il minimo valore di tensione raggiungibile in uscita dal driver con in ingresso lo '0' logico, tale per cui O1 assume un valore rappresentativo del '1' logico. Questo è anche detto $V_{OH}$ e abbiamo che U1=OFF e Z1=ON.
- il minimo valore di tensione raggiungibile in ingresso interpretato dal load come '1' logico, in questo caso si parla di $V_{IH}$ dove U2=ON e Z2=OFF.

Per effetto della presenza di rumore queste tensioni O1 e I2 non assumono un valore unico, andiamo cosi ad individuare i due valori descritti.
>Con $V_{OH}<V_{IH}$ il circuito non può funzionare in quanto $V_{OH}$ è più piccolo del minimo valore di tensione che l'inverter di carico riconosce come '1' logico, mentre con $V_{OH}\ge V_{IH}$ il circuito sicuramente funzionerà.

Il margine di rumore che il circuito sopporta è $NMH=V_{OH}-V_{IH}$ e prende il nome di <font color=red>margine di rumore alto</font>. Questo parametro indica la robustezza del circuito rispetto al rumore. Sia $V_{OH}$ che $V_{IH}$ sono presenti nel datasheet delle componenti logiche, per cui basta rispettare i vincoli. Analogamente supponiamo che $I1=V_{DD}$ quindi identifichiamo:
- $V_{OL}$ come la tensione massima raggiungibile dall'uscita del driver tale per cui il valore assunto è interpretato dal load come '0' logico.
- $V_{IL}$ come il valore massimo di tensione in ingresso che l'inverter di carico riconosce come '0' logico.

Se $V_{OL}\le V_{IL}$ tutto funziona correttamente. Il <font color=red>margine di rumore basso</font> è identificato come $NML=V_{IL}-V_{OL}$. I circuiti CMOS hanno intrinsecamente margini di rumore alti, sostanzialmente sia NML che NMH sono pari a $V_{Th}$ che si aggira intorno a $2^5 Ohm$.

---


#fisica 
[[Moto circolare e parabolico e forza centripeta]]
# Dinamica e prima legge di Newton
All’inizio ci siamo proposti di studiare il moto indipendentemente dalle cause che lo determinano. Il perché avviene il moto, quali sono le cause fisiche per cui un corpo entra in movimento e descrive un certo tipo di moto invece che un altro, la formulazione quantitativa della legge del moto per un punto materiale e le sue più importanti conseguenze sono spiegate dalla dinamica del punto.
Un’osservazione fondamentale è che la variazione dello stato di moto di un punto è determinata dall’interazione del punto con l’ambiente circostante, espressa dal concetto della forza. La prima prova è contenuta nel principio d'inerzia o prima legge di Newton

> Un corpo non soggetto a forze non subisce cambiamenti di velocità, ovvero resta in uno stato di quiete se era in quiete (v=0), oppure si muove di moto rettilineo uniforme (v costante non nulla).

In altre parole, l’assenza di forza non implica che non ci sia moto, bensì comporta che la velocità non vari. Dato che il principio d’inerzia richiede, in caso di moto, che questo sia rettilineo uniforme, un moto accelerato segnala la presenza di una forza agente. Un esempio è costituito dal moto circolare uniforme, nel quale la velocità rimane costante in modulo, ma varia in direzione a ciascun istante per effetto dell’accelerazione centripeta, e quindi di una forza. Se improvvisamente si annullasse tale forza il punto cesserebbe il moto circolare uniforme e inizierebbe un moto rettilineo uniforme con direzione secondo la tangente alla circonferenza nella posizione dove è cessata l’azione della forza.

---
# Concetto di forza

> La forza dunque è la grandezza che esprime e misura l'interazione tra sistemi fisici.

Intuitivamente possiamo affermare che alla forza è associata la nozione di intensità e di direzionalità. L’effetto di una forza cambia con la direzione, come viene evidenziato in figura:

![[forza.jpg|400x500]]

- a) si ha in generale un moto
- b) non si ha moto, ma solamente una deformazione del corpo e del supporto
- c) non si manifesta alcun moto, quest'ultimo caso introduce la nozione di eguaglianza di due forze e di equilibrio.

Sperimentalmente, si osserva che in uno stesso luogo tutti i corpi, qualunque sia la massa inerziale, assumono se lasciati liberi la stessa accelerazione detta gravità,  diretta verticalmente verso il suolo il cui modulo, che varia leggermente da posto a posto sulla terra, vale in media $9,8\displaystyle {m\over s^2}$.  Tale accelerazione è conseguenza della forza di attrazione terrestre, cioè dell’interazione gravitazionale tra la terra e il corpo.

Partendo dalla seconda legge di Newton, se agisce solo la forza peso P, abbiamo che:

$P=ma$

ma visto che a=g,

$P=mg$

All'interno del corso andremo a considerare l'attrito viscoso dell'aria pari a 0 in modo da semplificare le cose. Si tratta di una forza costante e in assenza di altre forze il moto ha una componente uniformemente accelerata nella direzione parallela a g. Se invece agiscono anche altre forze in generale si ha $a\ne g$, in particolare un corpo che cade nell’aria presenta un’accelerazione minore di quella di gravità a causa dell’attrito con l’aria.

Un corpo di massa m, poggiato su un pavimento, esercita una forza sul pavimento e risente di una reazione N che in modulo vale $mg$. È questa reazione applicata per esempio al nostro corpo che ci dà la sensazione di peso.

Consideriamo ora il corpo posato su una piattaforma che può muoversi verticalmente con una accelerazione a. Finché il corpo resta sulla piattaforma la sua accelerazione è $a$ e la seconda legge di Newton si scrive:

$\displaystyle N+P=ma\Rightarrow N+mg=ma$

in quanto al corpo sono applicate sia la forza peso che la reazione dovuta al contatto con la piattaforma, tale reazione è incognita. Solo se  $a=0$ sarebbe in modulo $N=P=mg$. Risolvendo troviamo:

$N=m(a-g)$

Abbiamo 4 casi da esaminare, come asse di riferimento prendiamo l'asse z verticale orientato verso l'alto per cui $g=-gu_z$:

1. $a$ discorde a g, piattaforma che accelera verso l'alto:
$\displaystyle N=m[au_z-(-gu_z)]=m(a+g)u_z\Rightarrow N>mg$
2. $a$ concorde a g, ma minore in modulo:
$\displaystyle N=m[-au_z-(-gu_z)]=m(g-a)u_z\Rightarrow N<mg$
3. $a=g\Rightarrow N=0$:
non c'è reazione e non c'è sensazione di peso (ciò si realizzerebbe con la piattaforma in caduta libera)
4. $a$ concorde a g ma maggiore in modulo:
si ha il distacco del corpo dalla piattaforma, infatti la soluzione darebbe N discorde all’asse z, la reazione dovrebbe attirare il corpo verso la piattaforma, il che è privo di senso.

Si noti che i casi 2, 3, 4 non richiedono necessariamente un moto della piattaforma verso il basso: questa potrebbe salire, ma frenando.

---

# Seconda legge di Newton

$F=ma$

L'interazione del punto con l'ambiente circostante, espressa tramite la forza F, determina l'accelerazione del punto ovvero la variazione della sua velocità nel tempo, m rappresenta la massa inerziale del punto.

Il termine massa inerziale è legato al fatto che la massa esprime l’inerzia del punto, cioè la sua resistenza a variare il proprio stato di moto, ossia a modificare la velocità. Fissata una determinata forza F, l’effetto dinamico è tanto maggiore quanto minore è la massa del punto. Per un punto materiale che si muove con una determinata accelerazione a, la forza necessaria a mantenere tale moto è tanto maggiore quanto maggiore è il valore di m, essendo F direttamente proporzionale a m.

Si giustifica così anche il nome punto materiale: per descrivere il comportamento dinamico del punto occorre conoscere la sua massa, si può cioè semplificare al massimo concependo un corpo privo di struttura, ma non si può rinunciare alla massa che è un concetto dinamico fondamentale per qualsiasi corpo.

In assenza di interazione con l’esterno la forza è nulla e quindi a=0 e v=costante. La legge di Newton ha come caso particolare, il principio d'inerzia. La legge può essere espressa anche come:

$\displaystyle F=m{dv\over dt}=m{d^2r\over dt^2}$

---
# Terza legge di Newton

La seconda legge è la legge dinamica in base alla quale spieghiamo perché un moto avviene con certe caratteristiche. Newton scoprì anche una proprietà generale delle forze, che si può enunciare in questa forma:

> Se un corpo A esercita una forza $F_{A,B}$ su un corpo B, il corpo B reagisce esercitando una forza $F_{B,A}$ sul corpo A. Le due forze hanno la stessa direzione e modulo ma verso opposto


Inoltre esse hanno la stessa retta d'azione, come mostrato in figura nei due casi di forze attrattive e repulsive:

![[forze.jpg|400x400]]

Tale legge è detta terza legge di Newton oppure principio di azione e reazione. Il fatto che non esista una forza isolata, ma che le forze vadano considerate sempre in coppie, secondo il principio di azione e reazione, chiarisce che l’interazione tra due corpi è sempre un’azione mutua.

---

---
tag: #fisica 
created: 2023-05-15 19:39:28
updated: 2023-05-15 19:39:28
---
#fisica 
[[Momento della forza, d'inerzia e teorema di Hyugens-Steiner]]
# Momento angolare
Si definisce momento angolare, il momento del vettore quantità di moto:

$\overrightarrow{L}=\overrightarrow{r}\times m\overrightarrow{v}$
![[momento_angolare.jpg|400x400]]
Nella figura O è il polo rispetto a cui è calcolato L. Importante è calcolare l'angolo tra $\overrightarrow{r}$ e $\overrightarrow{v}$.

> Più il moto si discosta dal moto curvilineo, più il momento angolare è nullo.

In modulo il momento angolare vale al massimo $|L|=rmv$, nel caso del momento la direzione e verso non sono immediate come nel caso della forza. Se il momento è uscente l'accelerazione angolare è antioraria, se è entrante l'accelerazione è oraria. Riprendendo la prima equazione cardinale dei sistemi di punti, $\displaystyle{d\overrightarrow{P}\over dt}=\overrightarrow{F}$ se si effettua un prodotto vettoriale per $\overrightarrow{r}$ si ottiene: $\displaystyle\overrightarrow{r}\times{d\overrightarrow{P}\over dt}=\overrightarrow{r}\times\overrightarrow{F}$.
Ricordando che $\overrightarrow{r}\times\overrightarrow{F}=\overrightarrow{\tau}$ e data la definizione di quantità di moto, si ha anche che $\overrightarrow{L}=\overrightarrow{r}\times\overrightarrow{P}$. 

Derivando entrambi i membri si ottiene $\displaystyle{d\overrightarrow{L}\over dt}={d(\overrightarrow{r}\times\overrightarrow{P})\over dt}={d\overrightarrow{r}\over dt}\times\overrightarrow{P}+\overrightarrow{r}\times{d\overrightarrow{P}\over dt}=\overrightarrow{v}\times\overrightarrow{P}+\overrightarrow{r}\times{d\overrightarrow{P}\over dt}$ ma essendo $\overrightarrow{P}=m\overrightarrow{v}$, $\overrightarrow{v}\times\overrightarrow{P}=0$ in quanto la velocità è parallela a se stessa, si ottiene che $\displaystyle{d\overrightarrow{L}\over dt}=\overrightarrow{r}\times{d\overrightarrow{P}\over dt}=\overrightarrow{\tau}$.

Infine mettendo in relazione $\displaystyle{d\overrightarrow{L}\over dt}=\overrightarrow{\tau}$ e $I\overrightarrow{\alpha}=\overrightarrow{\tau}$, si ottiene che $\displaystyle{d\overrightarrow{L}\over dt}=I\overrightarrow{\alpha}$.

$\displaystyle {dL\over dt}=I\alpha$ se $\alpha=costante$, $dL=I\alpha dt\implies \int^{L(t)}_{0}dL=I\int^{t}_{0}\alpha dt\implies L(t)=I\alpha t=I\omega(t)$

Ricavate queste equazioni, la scelta di quale utilizzare è cruciale. Ad esempio supponiamo di avere una sfera, che ruota intorno ad un asse uscente dal foglio. La relazione $L=rmv$ non si può applicare in quanto il corpo non è puntiforme ma rigido. Tutti i punti del corpo possiedono però un'accelerazione angolare uguale quindi si può utilizzare l'equazione $L(t)=I\alpha t=I\omega(t)$ per calcolare il momento angolare complessivo del corpo.

## Teorema del momento angolare
Supponiamo di calcolare il momento in due istanti di tempo diversi e di ottenere che: $\overrightarrow{L_i}=\overrightarrow{L_f}$.
Il momento angolare di un punto materiale rimane costante nel tempo, perciò si conserva.

---


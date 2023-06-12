[[Forze conservative e non, energia potenziale ed energia meccanica]]
#fisica 
# Centro di massa

Si definisce centro di massa di un sistema di punti materiali il punto geometrico la cui posizione è individuata, nel sistema di riferimento considerato, dal raggio vettore:

$\displaystyle r_{CM}={\sum_i m_i r_i\over\sum_i m_i}={m_1r_1+m_2r_2+...+m_nr_n\over m_1+m_2+...+m_n}$

le componenti di $r_{CM}$, ovvero le coordinate del centro di massa di un sistema di coordinate cartesiane con l'origine in O, sono:

$\displaystyle x_{CM}={\sum_im_ix_i\over\sum_im_i}$

$\displaystyle y_{CM}={\sum_im_iy_i\over\sum_im_i}$

$\displaystyle z_{CM}={\sum_im_iz_i\over\sum_im_i}$

Si noti che la posizione del centro di massa rispetto agli n punti materiali non dipende dal sistema di riferimento, mentre le sue coordinate invece variano a seconda del sistema prescelto.

![[centro.jpg || 500x550]]

Piuttosto che trovare tutte le coordinate del centro di massa separatamente, utilizziamo il raggio vettore e la sua scomposizione ovvero ad esempio
$\displaystyle r_{CM}={m_1 r_1 + m_2 r_2\over m_1+m_2}={m_1(x_1\hat{i}+y_1\hat{j}+z_1\hat{k})+m_2(x_2\hat{i}+y_2\hat{j}+z_3\hat{k})\over m_1+m_2}$

Se gli *n* punti sono in movimento, di norma la posizione del centro di massa varia. Sulla base della definizione calcoliamo la velocità del centro di massa:

$\displaystyle v_{CM}={dr_{CM}\over dt}={\sum_im_iv_i\over \sum_im_i}={P\over m}$

con P quantità di moto totale del sistema e m la massa totale del sistema. Ricaviamo poi l'accelerazione:

$\displaystyle a_{CM}={dv_{CM}\over dt}={\sum_im_ia_i\over\sum_i m_i}={\sum_im_ia_i\over m}$

Se il sistema di riferimento è inerziale:

$m_ia_i=F_i=F_i^{(E)}+F_i^{(I)}\Rightarrow \displaystyle ma_{CM}=\sum_im_ia_i=\sum_i(F_i^{(E)}+F_i^{(I)})=R^{(E)}+R^{(I)}=R^{(E)}$

## Teorema del moto del centro di massa

Dato che la risultante delle forze interne è pari a 0, l'equazione:

$R^{(E)}=ma_{CM}$

esprime il teorema del moto del centro di massa. Il centro di massa si muove come un punto materiale in cui sia concentrata tutta la massa del sistema ed a cui sia applicata la risultante delle forze esterne. Utilizzando l'equazione delle velocità nell'equazione appena trovata si ha:

$\displaystyle R^{(E)}=ma_{CM}=m{dv_{CM}\over dt}={d\over dt}(mv_{CM})={dP\over dt}$

> La risultante delle forze esterne è uguale alla derivata rispetto al tempo della quantità di moto totale del sistema. Il moto del centro di massa è determinato dunque solo dalle forze esterne. L'azione delle forze interne non può modificare lo stato di moto del centro di massa, invece il moto di ciascun punto dipende dall'azione delle forze esterne ed interne agenti su di esso

Il fatto che ad un certo istante $v_{CM}$ abbia un determinato valore significa che il sistema in media si sta spostando in quella data direzione, anche se nessuna delle singole $v_i$ coincide con $v_{CM}$.

---

# Quantità di moto

Si definisce quantità di moto di un punto materiale il vettore:

$P=mv$

se la massa è costante si può scrivere

$F=\Large{dp\over dt}$

In realtà questa relazione è la forma più generale della legge di Newton, utilizzabile anche se la massa non è costante. Essa va intesa in questo senso: lo stato dinamico del punto è individuato dalla quantità di moto, in cui compaiono la massa e la velocità. L'azione di una forza determina la variazione nel tempo della quantità di moto ovvero di qualcuna o di tutte queste quantità: massa, direzione, verso, modulo della velocità. Un punto materiale in senso stretto, cioè privo di struttura, ha massa costante, qualunque sia la sua velocità.

## Conservazione della quantità di moto

Se il sistema di punti considerato è isolato, cioè non soggeto a forze esterne, oppure l'azione delle forze esterne ha risultante nulla, si ha:

$a_{CM}=0$

$v_{CM}=costante$

$P=costante$

> Quando la risultante delle forze esterne è nulla, la quantità di moto totale del sistema rimane costante nel tempo ed il centro di massa si muove di moto rettilineo uniforme o resta in quiete.

Tale risultato esprime il principio di conservazione della quantità di moto per un sistema di punti materiali.

> In assenza di forza applicata la quantità di moto di un punto materiale rimane costante ovvero si conserva.

Si tratta evidentemente di un’altra formulazione del principio di inerzia.

---
# Equazione dei sistemi di particelle
La quantità di moto del centro di massa è data da: $\displaystyle\overrightarrow{P}_{CM}(t)=\sum^n_{i=1}\overrightarrow{P}_i(t)$ che è detta anche equazione dei sistemi di particelle tale equazione scritta anche come $\displaystyle{d \overrightarrow{P}_{CM}\over dt}=\overrightarrow{F}_{Tot}$ vale se la forza totale è 0 ovvero se $\overrightarrow{P}_{CM}=costante$.

---
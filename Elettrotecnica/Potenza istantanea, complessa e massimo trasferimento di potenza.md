---
tags: elettrotecnica, 
created: 2024-05-17 16:24:14
updated: 2024-05-17 16:24:14
---
[[Sinusoidi e fasori]]
# Potenza istantanea
La potenza è definita come $p(t)=v(t)i(t)$. Quando attacco un carico ad una porta AB, $p(t)=v_{AB}(t)i_{AB}(t)$. L'energia è data a $E=\int \Delta P$ in un'ora di tempo $E(t)={1\over 3600}\int p(t)={1\over 3600}\int v(t)i(t)={1\over 3600}\int v_{AB}(t)i_{AB}(t)$
$v_{AB}=V_mcos(\omega t+\theta_v)$ e $i_{AB}=i_mcos(\omega t+\theta_i)$ hanno uno sfasamento in regime sinusoidale.
La potenza istantanea in regime sinusoidale è pari a: $p(t)=[V_mcos(\omega t+\theta_v)][I_mcos(\omega t+\theta_i)]={1\over 2}V_mI_mcos(\theta_v-\theta_i)+{1\over2}V_mI_mcos(2\omega t+\theta_v+\theta_i)$ 
si nota che 
$\displaystyle p(t)\geq 0\ se\begin{cases} v(t)i(t)\ge 0\\
v(t)i(t)\leq 0
\end{cases}$
$\displaystyle p(t)< 0\ se\begin{cases} v(t)>0,i(t)< 0\\
v(t)<0, i(t)> 0
\end{cases}$
Lo sfasamento tra tensione e corrente determina il segno di $p(t)$.

## Fattore di potenza
Prese due sinusoidi generiche sia $\alpha=(\omega t+\theta_v)$ $\beta=(\omega t+\theta_i)$ allora $V_{AB}=V_mcos\alpha$ $I_{AB}=I_mcos\beta$ se moltiplico $V_{AB}I_{AM}$ ottengo $p(t)=V_{AB}(t)I_{AB}(t)=V_mI_mcos\alpha cos\beta$ dato che $cos\alpha cos\beta={cos(\alpha+\beta)+cos(\alpha-\beta)\over 2}$ $\displaystyle p(t)=V_mI_m{cos(\alpha+\beta)+cos(\alpha-\beta)\over 2}={V_mI_m\over 2}(cos(\omega t+\theta_v-\omega t-\theta_i)+cos(\omega t+\theta_v+\omega t+\theta_i))$
$=\displaystyle {V_mI_m\over 2}cos(\theta_v-\theta_i)+{V_mI_m\over 2}cos(2\omega t+\theta_v+\theta_i)$
In particolare: $cos(\theta_v-\theta_i)=cos\phi$ è detto <font color=orange>fattore di potenza</font>. 
- Per la resistenza $\theta_v=\theta_i$
- Per il condensatore $\theta_v-\theta_i=-{\pi\over2}$
- Per l'induttore $\theta_v-\theta_i={\pi\over 2}$

Per gli elementi passivi L,C e R, $cos\phi$ è compreso tra 0 e 1. Per gli elementi attivi $cos\phi<0$ quindi potenze negative possibili. 
## Potenza attiva, potenza apparente e potenza reattiva
Se calcolo l'energia tra $t_0$ e $T$ dove $T$ è molto più grande del periodo allora $\displaystyle E(t_0,T)=\int^{T}_{t_0}p(\tau)d\tau$ la potenza media è pari $\displaystyle\lim_{T\rightarrow\inf}{E(t_0,T)\over T-t_0}$ ma essendo $T>>t_0$, $t_0=0\implies\displaystyle\lim_{T\rightarrow\inf}{E(0,T)\over T}$ dunque $\displaystyle p_{media}={1\over T}\int^{T}_{0}{V_mI_m\over 2}cos(\theta_v-\theta_i)dt+{1\over T}\int^{T}_{0}{V_mI_m\over 2}cos(2\omega t+\theta_v+\theta_i)dt=$
il primo integrale non dipende dal tempo, mentre il secondo dipende da $t$ ed è sinusoidale dunque $p_{media}\displaystyle ={1\over T}{V_mI_m\over 2}cos\phi T={V_mI_m\over 2}cos\phi$ detta <font color=green>potenza media o potenza attiva</font>. In particolare $\displaystyle{V_mI_m\over 2}$ è la <font color=orange>potenza apparente</font> mentre la potenza attiva è $\displaystyle P={V_mI_m\over 2}cos\phi$. 
Quando potenza apparente pari a potenza attiva allora $cos\phi=1$ e vale solo per il resistore. Quando sia potenza apparente che potenza attiva sono pari a 0 allora si ha un conduttore o induttore.

Riscrivendo $\theta_v+\theta_i=\theta_v+2\theta_i-\theta_i$ dunque $\displaystyle p(t)={V_mI_m\over 2}cos\phi+{V_mI_m\over 2}(2\omega t+\theta_v-\theta_i+2\theta_i)$ sia $\alpha=2\omega t+2\theta_i$ sia $\phi=\beta=\theta_v-\theta_i$ attraverso prostaferesi $cos(\alpha+\beta)=cos\alpha cos\beta-sen\alpha sen\beta$ dunque $\displaystyle p(t)={V_mI_m\over 2}cos\phi+{V_mI_m\over 2}(cos\alpha cos\beta-sen\alpha sen\beta)={V_mI_m\over 2}cos\phi+{V_mI_m\over 2}(cos\alpha cos\phi-sen\alpha sen\phi)=$
$\displaystyle={V_mI_m\over 2}cos\phi+{V_mI_m\over 2}cos\alpha+{V_mI_m\over 2}cos\phi-{V_mI_m\over 2}sen\phi sen\alpha$
In particolare $\displaystyle{V_mI_m\over 2}sen\phi$ viene detta <font color=orange>potenza reattiva</font>.
- Per la resistenza: potenza attiva=potenza apparente, potenza reattiva=0
- Per il condensatore: potenza attiva=0, potenza reattiva=-potenza apparente
- Per l'induttore: potenza attiva=0, potenza reattiva=potenza apparente

Ricordando che $Z=R+jX$ dove $R\ne 0$ se c'è un resistore mentre $jX\ne 0$ se c'è un condensatore o induttore.

---
# Potenza complessa e triangolo delle potenze
Introduciamo $\overline{S}=\overline{P}+j\overline{Q}$ dove $\overline{S}$ è la <font color=green>potenza complessa</font> $\overline{P}$ è la potenza attiva e $\overline{Q}$ è la potenza reattiva mentre $|\overline{S}|$ è la potenza apparente.
$\overline{S}=\overline{P}+j\overline{Q}={1\over 2}\overline{V}\overline{I}^*$ dove $\overline{I}^*=I_me^{-j\theta_i}$ $\overline{V}=V_me^{j\theta_v}$ 
Dimostrazione.
$\displaystyle\overline{S}=\overline{P}+j\overline{Q}={1\over 2}\overline{V}\overline{I}^*={1\over 2}V_me^{j\theta_v}I_m^{-j\theta_i}={1\over 2}V_mI_me^{j\theta_v-\theta_i}={1\over 2}V_mI_m[cos\phi+jsen\phi]=$
$\displaystyle={1\over 2}V_mI_mcos\phi+j{1\over 2}V_mI_msen\phi=\overline{P}+j\overline{Q}$
Un altro modo per esprimere la potenza complessa è:
$\overline{S}=|\overline{S}|e^{j\phi}=|\overline{S}|e^{j(\theta_v-\theta_i)}$ $|\overline{S}|=\sqrt{P^2+Q^2}$ $\displaystyle cos\phi={P\over |\overline{S}|}={Re\{\overline{S}\}\over |\overline{S}|}$ $\phi=\arctan({Q\over P})$
La forma polare è pari a:
$\overline{S}={1\over 2}\overline{V}\overline{I}^*=|\overline{S}|e^{j(\theta_v-\theta_i)}=|\overline{S}|=e^{j\phi}$
Se trattiamo condensatore, induttore e resistenza come se fossero tutte resistenze attraverso l'impedenza si ottiene: $\displaystyle\overline{V}=Z\overline{I}$ $\overline{S}={1\over 2}\overline{V}\overline{I}^*={1\over 2}Z\overline{I}\overline{I}^*={1\over 2}Z|\overline{I}|^2$
$\displaystyle{\overline{V}\over Z}=\overline{V}\overline{Y}=\overline{I}\implies \overline{S}={1\over 2}\overline{V}{\overline{V}^*\over Z^*}={1\over 2}{|\overline{V}|^2\over Z^*}={1\over 2}|\overline{V}|^2Y^*$
La potenza complessa e le impedenze degli elementi passivi, condividono il vettore sul piano di Gauss (Parte reale, parte immaginaria). 
![[triangolopotenze.jpg|500x200]]
Calcolata la potenza di ogni elemento del circuito possiamo porle su un grafico e notare come, data la natura vettoriale della potenza complessa, il vettore delle potenze assorbite è uguale e contrario a quello delle potenze generate. Il termine triangolo deriva dal fatto che ognuna delle potenze delle componenti passive è parallela a un’asse e la loro somma genera un vettore che forma un triangolo con l’asse reale.


---
# Massimo trasferimento di potenza e conservazione potenza complessa
Come per la potenza complessa in regime stazionario, la potenza complessa si conserva, quindi anche la potenza attiva e reattiva.
>[!attention] 
>Non vale dunque per la potenza apparente.

$\displaystyle\sum \overline{S}_n=0$, $\displaystyle\sum \overline{P}_n=0$, $\displaystyle\sum \overline{Q}_n=0$ mentre $\displaystyle\sum |S_n|\ne0$

Partendo da un circuito nel dominio del tempo a regime sinusoidale e passando al circuito nel dominio dei fasori, il grafo rimane inalterato. Inoltre le stesse KCL e KVL che scriviamo per le grandezze nel tempo, valgono per i rispettivi fasori ed anche la matrice di incidenza è la stessa per il circuito nel tempo e per quello nel dominio dei fasori. 
Se prendiamo inoltre un circuito "coniugato" nel dominio dei fasori, tutte le grandezze di questo circuito saranno le complesse coniugate delle grandezze dell'altro. Per questo circuito, la matrice di incidenza e il grafo saranno uguali al circuito originale nel dominio del tempo e a quello corrispondente nel dominio dei fasori dunque, i vettori delle tensioni e dei fasori delle tensioni di questi 3 circuiti saranno ortogonali a tutti i vettori delle correnti e dei fasori delle correnti dei 3 circuiti. Perciò il prodotto tra le tensioni e le correnti dei fasori è pari a 0 ed anche il prodotto tra le tensioni e le correnti coniugate è pari a 0 dunque: $\displaystyle\overline{V_R}\overline{I}^*_R=0\implies\sum{1\over 2}\overline{V_i}\overline{I}_i^*={1\over 2}\sum\overline{V_i}\overline{I}_i^*=\sum\overline{S}_i=0$

Preso un generico circuito in regime sinusoidale, ![[matrasf.jpg|400x200]] dove:
- $\overline{V_g}=V_me^{j\theta}$
- $Z_g=R_g+jX_g$
- $Z_L=R_L+jX_L$
- $P_{R_L}={1\over 2}Z_L|\overline{I}|^2$

essendo maglia singola la corrente è pari a $\displaystyle\overline{I}={\overline{V_g}\over R_g+jX_g+R_L+jX_L}={\overline{V_g}\over R_g+R_L+j(X_g+X_L)}$ dunque
$\displaystyle P_{R_L}={1\over 2}(R_L+jX_L){|\overline{V_g}|^2\over (R_g+R_L)^2+[j(X_g+X_L)]^2}$
per calcolare il massimo trasferimento di potenza devo fare le derivate parziali di $P_{R_L}$. La prima derivata è:
$\displaystyle{\partial P_{R_L}\over\partial X_L}=0\implies {1\over2}|\overline{V_g}|^2{-2(X_g+X_L)R_L\over[(R_g+R_L)^2+(X_g+X_L)^2]^2}=0$
Un caso banale in cui il numeratore è pari a 0 è quando $\overline{V_g}^2=0$ oppure quando $R_L=0$ altrimenti per essere pari a 0 occorre che: 
$-2(X_g+X_L)=0\implies X_L=-X_g$
La seconda derivata è:
$\displaystyle{\partial P_{R_L}\over\partial R_L}=0\implies {1\over2}|\overline{V_g}|^2{(R_g+R_L)^2+(X_g+X_L)^2-R_L[2(R_g+R_L)]\over[(R_g+R_L)^2+(X_g+X_L)^2]^2}=0$
Un caso banale in cui il numeratore è pari a 0 è quando $\overline{V_g}^2=0$ altrimenti per essere pari a 0 occorre che: $(R_g+R_L)^2+(X_g+X_L)^2-R_L[2(R_g+R_L)]=0\implies$ 
$R_g^2+R_L^2+2R_gR_L+(X_g+X_L)^2-2R_gR_L-2R_L^2=0\implies R_g^2-R_L^2+(X_g+X_L)^2=0$
Sostituendo il risultato ottenuto nella prima derivata parziale, $R_g^2-R_L^2=0\implies R_L=\pm R_g$ ovvero $R_L=R_g$. Dunque per avere massimo trasferimento di potenza occorre che $R_L=R_g$ e $X_L=-X_g$ perciò che l'impedenza sarà $Z_L=R_L+jX_L=R_g-jX_g=Z_g^*$.

---
# Rifasamento
Preso un generatore reale di tensione attaccato ad una porta A-B ed un carico collegato a tale porta. La potenza complessa del generatore è pari a $\overline{S_{V_{g1}}}$ con fase $\phi_1$ mentre la potenza complessa del carico è $\overline{S_{V_{g2}}}$ con fase $\phi_2$ dove $\phi_2<\phi_1$. Per attuare il rifasamento attacco in parallelo un condensatore al carico alla porta A-B. In modo che $\overline{S_{V_{g1}}}+\overline{S_{C}}=\overline{S_{V_{g2}}}$

---


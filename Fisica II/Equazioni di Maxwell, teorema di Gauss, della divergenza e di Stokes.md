---
tags: elettromagnetismo 
created: 2024-02-10 18:37:48
updated: 2024-02-10 18:37:48
---
[[Induzione e forza magnetica, legge di Biot-Savart e legge di Ampere]]
# Equazioni e loro caratteristiche
Nell'elettrostatica e nella magnetostatica, si considerano grandezze che non variano nel tempo ovvero: $\displaystyle{\sigma\over\sigma t}=0$. In contesti dinamici le grandezze sono gestite dalle equazioni di Maxwell tratte da esperimenti empirici. Le equazioni di Maxwell hanno come obiettivo quello di introdurre il concetto di campo elettromagnetico. Vediamo le equazioni in forma differenziale nel dominio del tempo: $$\begin{gathered}
\nabla\times\underline{e}=-{\sigma\underline{b}\over\sigma t}\\
\nabla\times\underline{h}={\sigma\underline{d}\over\sigma t}+\underline{J}\\
\nabla\cdot\underline{d}=\rho\\
\nabla\cdot\underline{b}=0
\end{gathered}$$

## Caratteristiche 
1. Sono equazioni che tengono in considerazione sia le variazioni spaziali che temporali ad esempio il campo $\underline{e}(x,y,z,t)$ dipende da quattro variabili.
2. Le grandezze coinvolte sono di 3 gruppi:
   - Sorgenti: densità di corrente $\underline{J}$ e densità di carica $\rho$
   - Campi: campo elettronico $\underline{e}$ e campo magnetico $\underline{h}$
   - Induzioni: induzione magnetica $\underline{b}$ ed induzione elettrica $\underline{d}$

Nel caso delle staticità ovvero con $\displaystyle{\sigma\over\sigma t}=0$ allora le equazioni diventano:
$$\begin{gathered}
\nabla\times\underline{e}=0\\
\nabla\times\underline{h}=\underline{J}\\
\end{gathered}$$
dunque non c'è variazione spaziale di campo elettrico allora non c'è campo elettrico, mentre si può avere un campo magnetico in condizioni statiche solo se c'è corrente. In assenza di corrente posso avere un campo magnetico variabile se sono in condizioni dinamica. 

Ne deriva che in condizioni dinamiche se si ha un campo magnetico allora si ha un campo elettrico e viceversa.

>[!info] 
>$\nabla\cdot\underline{A}$ permette di valutare quanto diverge in una zona. Un valore alto indica divergenza brusca mentre un valore basso indica un parallelismo fra le linee di flusso.
>$\nabla\times\underline{A}$ permette di valutare quanto è inteso un campo magnetico in quanto ad una certa distanza le onde di un campo tendono ad appiattirsi.

---
# Teorema di Gauss 
Dato un volume $V$ delimitato dalla superficie $S$ e normale $\hat{u}$: $$\iiint_V \nabla\cdot\underline{A}dV=\large\unicode{x222F}_S\underline{A}\circ\hat{u}\ dS$$
da ciò si dimostra che la terza equazione di Maxwell sarà $$\iiint_V \nabla\circ\underline{d}\ dV=\iiint_V\rho\ dV$$
dove $$\begin{gathered}
\iiint_V\rho dV=Q \\
\iiint_V\nabla\circ\underline{d}\ dV=\large{\unicode{x222F}}_S\ \underline{d}\circ\hat{u}\ dS
\end{gathered}$$
abbiamo proprio la legge di Gauss $Q=\large{\unicode{x222F}}_S\ \underline{d}\circ\hat{u}\ dS$. Se considero il teorema per $\nabla\cdot\underline{b}=0$ si ha che: $$\begin{gathered}
\iiint_V \nabla\cdot\underline{b}dV=0\\
\large{\unicode{x222F}}_S\ \underline{b}\circ\hat{u}\ dS=0
\end{gathered}$$
Dunque in natura non esistono cariche isolate ma dipoli magnetici e poiché $\nabla\cdot\underline{b}=0$ allora $\underline{b}$ è solenoidale.

---
# Teorema della divergenza
Avendo un campo e la sua divergenza, l'integrale di volume della divergenza è pari all'integrale di superficie orientata del campo, cioè: $$\iint_V\nabla\cdot AdV=\large\unicode{x222F}_S\ A\cdot\hat{u} dS$$

---
# Teorema di Stokes e legge di Faraday
Data una superficie aperta $S$ chiusa da un contorno $C$ allora: $$\iint_S(\nabla\times A)\circ\hat{u}\ dS=\oint_C\underline{A}\circ d\underline{l}$$
di conseguenza se applico l'equazione a $\nabla\times\underline{h}$: $$\iint_S(\nabla\times \underline{h})\circ\hat{u}\ dS=\iint_S{\sigma\underline{d}\over\sigma t}\circ\underline{u}\ dS+\iint_S \underline{J}\circ\hat{u}\ dS$$
da qui si ottiene dunque la seconda equazione di Maxwell: $$\oint_C\underline{h}\circ\hat{u}\ dS={\sigma\over\sigma t}\iint_S\underline{d}\circ\underline{u}\ dS+I$$
In condizione statiche l'integrale di superficie dell'induzione elettrica è pari a 0 e conferma perciò l'equazione di Maxwell.
Se applico l'equazione a $\nabla\times\underline{e}$: $$\iint_S(\nabla\times \underline{e})\cdot\hat{u}\ dS=\iint_S -{\sigma\underline{b}\over\sigma t}\circ\underline{u}\ dS$$ essendo $\displaystyle\iint_S(\nabla\times \underline{e})\cdot\hat{u}\ dS=\oint_C \underline{e}\circ d\underline{l}$ allora $$\displaystyle\oint_S\underline{e}\circ d\underline{l}=-{\sigma\over\sigma t}\iint_S \underline{b}\circ\hat{u}\ dS$$
Se la divergenza è zero il campo è solenoidale, cioè le linee di campo si chiudono su loro stesse, mentre se il rotore è zero, il campo è irrotazionale.
In particolare attraverso la prima equazione di Maxwell ottengo la legge di Faraday $$f_{em}=-{\sigma\over\sigma t}\phi_b$$
che permette di calcolare la forza elettromotrice attraverso il flusso dell'induzione magnetica variabile nel tempo. 
La forza di Lorentz è la somma tra forza elettrica e forza elettromotrice: $$\underline{F}=\underline{F}_e+\underline{F}_{em}$$

---
# Condensatori
Si ha il condensatore semplice con un solo dielettrico:
![[condesatore.jpg]]
i condensatori in parallelo:
![[condpar.jpg]]
dove la tensione viene applicata allo stesso modo ad entrambi i condensatori ed infine i condensatori in serie: ![[condserie.jpg]]

---

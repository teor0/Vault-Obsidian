---
tags:
  - elettromagnetismo
created: 2024-02-09 16:05:11
updated: 2024-02-09 16:05:11
---
[[Legge di Kirchhoff, dipolo elettrico, corrente, legge di Ohm]]
# Resistenza e potenza dissipata
L'equazione della resistenza è pari a: $$R={V\over I} \text{in generale}\ \large R={-\int_l \underline{E}\circ d\underline{l}\over \iint_S \underline{J}\circ \hat{u}\ dS}$$
Consideriamo un mezzo semiconduttore. Sulle sue cariche agiscono le seguenti forze:
$$\begin{gather}
\underline{F}_e=q_e\underline{E}=\rho_{Ve}\Delta V\cdot\underline{E}\\
\underline{F}_h=q_h\underline{E}=\rho_{Vh}\Delta V\cdot\underline{E}
\end{gather}$$
per spostare una carica di un tratto $\Delta l$ si ha un lavoro $\Delta W$ tale che $\Delta W=\underline{F}_e+\underline{\Delta l}_e+\underline{F}_h+\underline{\Delta l}_h$. Poiché la potenza dissipata è il lavoro compiuto nell'unità di tempo, allora: $$\Delta P={\Delta W\over \Delta t}=\underline{F}_e+{\underline{\Delta l}_e\over \Delta t}+\underline{F}_h+{\underline{\Delta l}_h\over\Delta t}\ \text{siano:}\ \underline{u}_e={\underline{\Delta l}_e\over \Delta t}\ \text{e}\ \underline{u}_h={\underline{\Delta l}_h\over \Delta t}$$
$$\Delta P=\underline{F}_e\circ\underline{u}_e+\underline{F}_h\circ\underline{u}_h=\rho_{Ve}\Delta V\cdot\underline{E}\circ\underline{u}_e+\rho_{Vh}\Delta V\cdot\underline{E}\circ\underline{u}_h=$$
$$=(\rho_{Ve}\cdot\underline{E}\circ\underline{u}_e+\rho_{Vh}\cdot\underline{E}\circ\underline{u}_h)\cdot\Delta V=\underline{E}\circ\underline{J}\cdot\Delta V$$
Per calcolare la potenza totale dissipata in un volume, si utilizza la seguente equazione:
$$P=\iiint \Delta P=\iiint_V \underline{E}\circ\underline{J}dV=\iiint_V \sigma\underline{E}\cdot\underline{E}dV=\iiint_V \sigma |\underline{E}|^2dV$$
in particolare l'integrale che permette di calcolare la potenza totale dissipata è la legge di Joule: $$P=\iiint_V \sigma |\underline{E}|^2dV$$

---
# Capacità di un condensatore
Il condensatore è formato da 2 conduttori separati da un dielettrico. Questi conduttori sono collegati ad un generatore di tensione. Sul primo condensatore si accumula una carica di polarità opposta a quella del secondo. Il campo elettrico che si genera è di verso opposto alla tensione, è nullo ed ha un certo valore nel dielettrico. La capacità vale $C={Q\over V}$ e si misura in Farad. Se l'induzione elettrica è $D=\varepsilon\cdot\underline{E}$, la carica per la legge di Gauss è pari a: $$\large Q={\unicode{x222F}}_{S}\ \underline{D}\ \circ\ \hat{u}\ dS=\unicode{x222F}_S\ \varepsilon\underline{E}\circ\hat{u}dS$$
La tensione è $V=V_1-V_2=\int^{1}_{2}-\underline{E}\circ d\underline{l}$, di conseguenza ne deriva che $$\displaystyle\large {C={\unicode{x222F}_{S}\ \varepsilon\underline{E}\circ\hat{u}dS\over -\int^{1}_{2}\underline{E}\circ d\underline{l}}}$$
ne deriva che la capacità di un condensatore non dipende dal campo ma solo dalle caratteristiche geometriche del condensatore.

---
# Energia potenziale elettrostatica
Il generatore collegato ad un'armatura consuma energia per caricare il condensatore. Se il dielettrico e l'armatura sono ideali, non vi è dissipazione di energia vi è accumulo di energia, in particolare <font color=blue>energia potenziale elettrostatica</font>. Sapendo che $dW_e=dq\cdot V$ e che $V={Q\over C}$ allora: $$W_e=\int^{Q}_{0}{q\over C}dq={1\over C}\int^{Q}_{0}qdq={1\over C}{q^2\over 2}|^Q_0={Q^2\over 2C}={C^2V^2\over 2C}={CV^2\over 2}$$

---
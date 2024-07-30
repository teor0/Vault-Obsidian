---
tags: elettromagnetismo 
created: 2024-02-09 09:45:56
updated: 2024-02-09 09:45:56
---
[[Forza elettrica, legge di Gauss e potenziale elettrico]]
# Legge di Kirchhoff e dipolo elettrico
La caduta potenziale netta in un circuito chiuso, ovvero dove $P_1= P_2$ è pari a zero. Matematicamente:
$$\oint_C=\underline{E}\cdot d\underline{l}=0$$
questa legge prende il nome di legge di Kirchhoff, ed è conseguenza della natura conservativa dell'energia elettrica.

Il dipolo elettrico è composto da due cariche di segno opposto poste ad una distanza $\underline{d}$. Si considera un punto P identificato da un vettore $\underline{R}>>\underline{d}$. Il potenziale in P sarà data da: $$V(\underline{R})=\sum^{2}_{i=1}{q\over 4\pi\varepsilon |R-R_i|}={q\over 4\pi\varepsilon}({1\over R_1}-{1\over R_2})$$
![[dipolo.jpg|500x400]]
Se parametrizzo $R_2\simeq R_1+dcos\theta$, ottengo che: $$\begin{eqnarray}
R_2-R_1\simeq dcos\theta \\
R_1\cdot R_2=R^2
\end{eqnarray}$$
perciò il potenziale in un punto a causa del dipolo è:
$$V\simeq {q\over 4\pi\varepsilon}\cdot{dcos\theta\over R^2}$$
Se ribalto il vettore $\underline{d}$ su $\underline{R}$ ottengo: $qdcos\theta=q\underline{d}\circ \hat{i}_R$, che è il <font color=orange>momento di dipolo elettrico</font> che viene indicato con $\underline{P}$. Si deriva che il potenziale considerando un dipolo è pari a : $$V= {\underline{P}\cdot \hat{i}_R\over 4\pi\varepsilon R^2}$$

---
# Corrente
Si consideri un cilindro elettricamente carico con una densità di carica volumetrica con sezione omogenea $\Delta S$. Al suo interno le cariche si muovono con una velocità media $\underline{u}$, nell'intervallo di tempo $\Delta t$, le cariche si spostano di un tratto $\Delta l$ tale che $\Delta l=u\cdot\Delta t$. Si vuole calcolare la carica infinitesima $\Delta q$ che attraversa la sezione $\Delta S$ nel tempo $\Delta t$
Sapendo che $\Delta q=\rho_V\Delta V$ e che $\Delta V=\Delta l\cdot\Delta S$ allora $\Delta q=\rho_V\cdot u \Delta t\cdot\Delta S$
![[cilicorr.jpg]]

Definiamo corrente come la quantità di carica $\Delta q$ che passa in un intervallo $\Delta t$: $$\Delta i={\Delta q\over \Delta t}=\rho_V u\Delta S=J\Delta S$$ Nel caso generale $\underline{J}=\rho_V\cdot \underline{u}$ è un vettore, dunque la corrente è data da: $$\underline{I}=\iint_S \underline{J}\circ \hat{u}\ dS$$ In presenza di un campo indotto, gli elettroni liberi si muoveranno con velocità media $\underline{u}_e$ detta <font color=orange>velocità di deriva elettronica</font> e dà origine ad una corrente detta di <font color=red>conduzione</font>. Inoltre $\underline{u}_e=-\mu_e\cdot\underline{E}$, dove $\mu_e$ è la <font color=blue>mobilità elettronica</font>.

## Semiconduttori
I semiconduttori hanno elettroni liberi e lacune, ovvero protoni che hanno segno positivo. Queste lacune hanno una velocità data dalla mobilità di lacuna. Si dicono lacune perché prima in quella posizione c'era un elettrone che lascia un vuoto e perciò dato il numero non elevato di elettroni si crea una lacuna. La velocità di lacuna è data da: $$\underline{u}_h=\mu_h\underline{E}$$
La densità di corrente è data da: $$\begin{split}
\underline{J}=\underline{J}_e+\underline{J}_h=\rho_{Ve}\cdot\underline{u}_e+\rho_{Vh}\cdot\underline{u}_h=-\rho_{Ve}\cdot\mu_e\underline{E}+\rho_{Vh}\cdot\mu_h\underline{E}\\
=\underline{E}(-\rho_{Ve}\cdot\mu_e+\rho_{Vh}\cdot\mu_h)=(N_e\cdot e\mu_e+N_h\cdot e\mu_h)=\sigma\underline{E}
\end{split}$$

Perciò $\large\sigma=e(N_e\cdot\mu_e+N_h\cdot\mu_h)$, dove $N_e\ \text{e}\ N_h$ sono rispettivamente numero di elettroni e numero di lacune questo per i semiconduttori. Per i conduttori $\large\sigma=(N_e\cdot e\mu_e)$

---
# Legge di Ohm 
La legge di Ohm afferma che $V=RI$ .

---

---
tags: elettromagnetismo
created: 2024-02-10 11:28:53
updated: 2024-02-10 11:28:53
---
[[Resistenza, potenza dissipata, legge di Joule, condensatore e energia potenziale elettrostatica]]
# Induzione magnetica e forza magnetica
Rispetto all'elettrostatica, la carica si muove di velocità $\underline{V}$. Se è presente un campo elettrico allora una particella q subisce una forza elettrica $\underline{F}_e=q\cdot\underline{E}$ mentre se è presente un'induzione magnetica $\underline{B}$ allora essa è soggetta ad una forza magnetica $\underline{F}_m=q\underline{V}\times\underline{B}$. Inoltre data la permeabilità magnetica $\mu$ ad un campo magnetico $\underline{H}$, l'induzione magnetica è data da: $$\underline{B}=\mu\underline{H}$$
Le differenze fra forza elettrica e magnetica:
1. La forza elettrica è parallela al campo elettrico, mentre la forza magnetica è perpendicolare all'induzione magnetica.
2. La forza elettrica agisce su cariche stazionarie o in moto mentre la forza magnetica solo su cariche in moto.
3. La forza elettrica dissipa energia mentre la forza magnetica non compie lavoro, infatti $dW=\underline{F}_m\circ d\underline{l}=\underline{F}_m\circ \underline{V}dt$, poiché $\displaystyle{\underline{V}={d\underline{l}\over dt}}$ ma poiché la forza magnetica è perpendicolare al vettore velocità allora il prodotto vettoriale è pari a 0 e dunque il lavoro è pari a 0.

![[conduttore.jpg]]
Si consideri un conduttore con corrente costante immerso in un campo magnetico con induzione magnetica $\underline{B}$. Isolando una parte infinitesima di forma cilindrica di area A e lunghezza $dl$, assumiamo una densità di carica $\rho_{Ve}=-N_ee$. Sia $dQ$ la carica infinitesima data da $dQ=\rho_{Ve}\cdot dV=-N_e\cdot e\cdot A\cdot dl$ e sia la forza magnetica esercitata $d\underline{F}_m=dQ\cdot\underline{V}\times\underline{B}=-N_e\cdot eA\cdot dl\cdot\underline{V}\times\underline{B}$. Essendo il vettore velocità e la lunghezza opposti, si ha che $dl\underline{V}=-d\underline{l}V$ ed essendo $I=N_e\cdot eAV$ la forza magnetica è pari a: $$\displaystyle\underline{F}_m=\int_C Id\underline{l}\times\underline{B}=I\int_C d\underline{l}\times\underline{B}$$
Consideriamo un contorno chiuso per il conduttore, allora la forza magnetica è pari a: $$\underline{F}_m=\oint_C Id\underline{l}\times\underline{B}=I\oint_C d\underline{l}\times\underline{B}$$
se $\underline{B}$ è costante allora la forza magnetica è nulla. Si conclude che se si va ad immergere un circuito chiuso attraversato da corrente, in un campo con induzione magnetica $\underline{B}$, la forza magnetica totale è zero. Tale circuito si chiama <font color=blue>spira</font>, nel caso di un filo attraversato da una corrente e immerso in un campo di induzione magnetica $\underline{B}$ allora $$\displaystyle\underline{F}_m=I\int^{b}_{a}d\underline{l}\times\underline{B}=I\cdot\underline{l}\times\underline{B}$$
Si capisce perciò che la forza magnetica non dipende dal percorso ma solo dalla lunghezza.

---
# Legge di Biot-Savart
Questa legge viene usata per calcolare il campo magnetico in presenza di corrente. Consideriamo una sezione di un cavo elettrico, dove passa una corrente $I$ costante e $d\underline{l}$ la direzione del elemento di corrente. Si vuole calcolare il campo magnetico $\underline{H}$ in un punto P generico, a distanza $\underline{R}$. Il campo $d\underline{H}$ prodotto da $I$ è dato da: $\displaystyle d\underline{H}={I\over 4\pi}\cdot {d\underline{l}\times\hat{i}_R\over R^2}$. Il campo magnetico $\underline{H}$ è ortogonale a $d\underline{l}$ e $\hat{i}_R$, perciò è ortogonale al piano che contiene sia il vettore $d\underline{l}$ che $\underline{R}$ perciò esce dal piano. La legge di Biot-Savart in generale è: $$\underline{H}={I\over 4\pi}\int_l{d\underline{l}\times\hat{i}_R\over R^2} dz$$
ricordando che $Id\underline{l}=\underline{J}dV=J_SdS$ allora su un volume:$$\underline{H}={1\over 4\pi}\iiint_V{\underline{J}\times\hat{i}_R\over R^2}dV$$ mentre su una superficie: $$\underline{H}={1\over 4\pi}\iint_S{J_S\times\hat{i}_R\over R^2}dS$$

---
# Legge di Ampere
Dato un conduttore cilindrico lungo l'asse $z$ di lunghezza $l$ e diametro trascurabile. Si considera un punto P posto a distanza $r$ sull'asse x e si vuole calcolare il campo nel punto P. 
![[ampere.jpg|350x450]]
Considerando un tratto $d\underline{l}=\hat{z}dz$ e considerando la legge di Biot-Savart, il prodotto vettoriale $d\underline{l}\times\hat{i}_r=(\hat{z}\times\hat{i}_r)dz=\hat{\phi}sin\theta dz$ per cui si ottiene $$\large\underline{H}={1\over 4\pi}\int^{l\over 2}_{-{l\over 2}}{\hat{\phi}sen\theta\over R^2}dz=\hat{\phi}{I\over 4\pi}\int^{l\over 2}_{-{l\over 2}}{sen\theta\over R^2}dz$$
Esprimendo tutto in funzione di $\theta$ si ha che: $$\begin{align}
r=Rsen\theta\implies \displaystyle{R={r\over sen\theta}} \\
r=-ztan\theta
z=-{r\over tan\theta}\implies dz={r\over sen^2\theta}d\theta
\end{align}$$
dunque dopo tutti i passaggi e considerando $l>>r$ si ottiene $$\underline{H}=\hat{\phi}{I\over 2\pi r}$$
In definitive si ottiene la legge di Ampere $$I=\oint_C\underline{H}d\underline{l}$$
La corrente è pari alla circuitazione del campo magnetico sul conduttore. La legge di Ampere è duale alla legge di Biot-Savart.

---
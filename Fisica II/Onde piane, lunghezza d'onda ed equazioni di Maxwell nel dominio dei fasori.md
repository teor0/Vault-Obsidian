---
tags: elettromagnetismo
created: 2024-02-12 15:44:56
updated: 2024-02-12 15:44:56
---
[[Equazioni di Maxwell, teorema di Gauss, della divergenza e di Stokes]]
# Onde
I parametri da cui dipendono le variabili delle equazioni di Maxwell $x,y,z,t$ dove:
- $x,y,z$ regolano la propagazione.
- $t$ indica la dipendenza dal tempo e descrive dunque una dinamicità del sistema.

In natura siamo in presenza di segnali ondosi di natura periodica, ovvero onde. In particolare il periodo e la velocità di un'onda sono direttamente proporzionali fra loro, cioè maggiore è la frequenza maggiore è la velocità di un'onda. Un'onda elettromagnetica è generata da un campo elettrico ed uno magnetico. Un segnale in forma generica è dato da $u(z,t)=Acos(\omega t-kz)$ dove $t$ è il tempo e $z$ è una semplificazione che modella lo spazio. La rappresentazione secondo coordinate temporali è la seguente:
![[onde.jpg|300x400]]
In particolare si può vedere l'equazione in forma generica come $u(z,t)=Acos(\omega t-\alpha)$ una funzione periodica sia spazialmente che temporalmente, dove $\alpha$ è la fase ovvero dallo sfasamento della curva coseno. La periodicità dello spazio è la lunghezza d'onda $\lambda$. Assumendo che il segnale non si deformi, se considero $t=t_0+\Delta t$ la lunghezza d'onda rimane la stessa. 
Se traccio una parallela a $z$ riesco a calcolare la velocità di propagazione del segnale. Se prendo $u(z,t)=Acos(\omega t_0-kz)=(kz-\omega t_0)$ e poiché $cos(\alpha)=cos(-\alpha)$ in quanto funzione dispari, posso scrivere la costante di propagazione come: $\large k={2\pi\over\lambda}$. Se considero un istante diverso allora  la forma d'onda si trasla lungo l'asse z lasciando immutata la sua forma: ![[lungonda.jpg|400x300]]
Presi due punti $P_1,P_2$ tale che $u(P_1)=u(P_2)$ dunque che $Acos(\omega t_0-kz_0)=Acos(\omega t_0+\omega\Delta t-kz_0-k\Delta z)$ da cui posso ottenere che $$cos(\omega t_0-kz_0)=cos(\omega t_0+\omega\Delta t-kz_0-k\Delta z)\implies\omega t_0-kz_0=\omega t_0+\omega\Delta t-kz_0-k\Delta z$$ $$\implies\omega\Delta t-k\Delta z=0\implies {\Delta z\over\Delta t}={\omega\over k}$$ Che altro non è che l'equazione della velocità di propagazione: $\displaystyle V_p={\Delta z\over\Delta t}={\omega\over k}$ e se $\displaystyle\omega={2\pi\over T}$, $\displaystyle k={2\pi\over\lambda}$ allora $$V_p={\lambda\over T}=\lambda f$$
Si capisce perciò che lunghezza d'onda e frequenza sono inversamente proporzionali. 
Fissata la frequenza, $\lambda$ dipende dal mezzo di propagazione. Nel vuoto la velocità di propagazione è data da: $\displaystyle V_p={1\over\sqrt{\varepsilon\mu}}={C\over\sqrt{\varepsilon_r}}$

## Penetrazione e Banda
La profondità di penetrazione di un'onda in un mezzo è $\displaystyle\delta={1\over\alpha}$ dove $\alpha$ è il coefficiente di attivazione e varia da materiale a materiale.
Alla dipendenza spaziale è associato il fenomeno di propagazione, ossia il trasferimento d'informazioni sotto forma di onde elettromagnetiche. Un segnale monocromatico è un segnale con una sola frequenza ossia una sola onda:
![[ondamono.jpg|400x400]]
applicando la trasformata di Fourier ![[monofour.jpg|400x400]] posso solo trasferire alla frequenza $\omega_0$. Per trasferire informazioni ho bisogno di una banda, ovvero $B=N\Delta f$ dove $N$ consente di associare $N$ informazioni. Nella propagazione si usano i numeri complessi in particolare, il modulo esprime l'intensità del campo mentre la fase esprime la posizione.

---
# Equazione di Maxwell nel dominio dei fasori
Ricordando che il fasore è dato da $u(z)=Ae^{-jkz}$. Per risolvere l'equazioni di Maxwell posso lavorare nel dominio del tempo, nel dominio dei fasori, ovvero $u(z,t)=R_e{u(z)e^{j\omega t}}$ ed anche il dominio della frequenza per passare da $u(z)\rightarrow\tilde{u}(z,\omega)$ dove la scelta dipende dal contesto applicativo. L'idea è di partire dalle equazioni di Maxwell nel dominio del tempo, assumere una dipendenza dallo spazio e passare al dominio dei fasori. Nel dominio dei fasori le equazioni diventano: $$\begin{gathered}
\nabla\times\underline{E}=-J\omega\underline{B}\\
\nabla\times\underline{H}=J\omega\underline{D}+\underline{J}\\
\nabla\cdot\underline{D}=\rho\\
\nabla\cdot\underline{B}=0
\end{gathered}$$

---
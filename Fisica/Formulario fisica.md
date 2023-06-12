![[archiassociati.jpg|200x200]]


| km/h$\rightarrow$m/s                                    | m/s$\rightarrow$km/h                                    | rad$\rightarrow$ gradi                   | gradi$\rightarrow$rad                     | cal$\rightarrow$J | Conversione Pressione | 
| ------------------------------------------------------- | ------------------------------------------------------- | ---------------------------------------- | ----------------------------------------- | ----------------- | --------------------- |
| $\displaystyle {km\over h}\xrightarrow{/3,6}{m\over s}$ | $\displaystyle {m\over s}\xrightarrow{*3,6}{km\over h}$ | $\displaystyle rad\times {180\over \Pi}$ | $\displaystyle gradi\times{\Pi\over 180}$ | $1cal=4,186J$     | $\begin{gather}1atm=1,01\times 10^5\\ 1bar=10^5Pa \\ P={F\over S}\end{gather}$                      |


| Prodotto scalare                                                                | Prodotto vettoriale | 
| ------------------------------------------------------------------------------- | --- |
| $\begin{multline}A*B=A*B*cos(\theta )\\ =A_x*B_x+A_y*B_y+A_z*B_z\end{multline}$ | $A\times B=A*B*sen(\theta)=\begin{bmatrix}i\ j\ k\\ A_x A_y A_z \\ B_x B_y B_z \end{bmatrix}=\begin{align}\hat{i}[Ay*B_z-(A_z*B_y)]\\ -\hat{j}[Ax*B_z-(A_z*B_x)]+\\ \hat{k}[Ax*B_y-(A_y*B_x)] \end{align}$    |


### Moto armonico

| Legge oraria               | Velocità                          | Accelerazione                                     | Pulsazione                   | Periodo |
| -------------------------- | --------------------------------- | ------------------------------------------------- | ---------------------------- | ------- |
| $x(t)=Asen(\omega t+\phi)$ | $v(t)=\omega Acos(\omega t+\phi)$ | $a(t)=-\omega^2Asen(\omega t+\phi)$ | $\large\omega={2\pi\over T}$ | $\large\displaystyle T={2\pi\over\omega}$        |


### Moto circolare uniforme
| Accelerazione centripeta                       | Velocità angolare                      | Legge oraria angolo           | Legge oraria  | Periodo                                                   | Frequenza |
| ---------------------------------------------- | -------------------------------------- | ----------------------------- | ------------- | --------------------------------------------------------- | --------- |
| $\displaystyle\large a={v^2\over r}=\omega^2r$ | $\large\displaystyle\large\omega={v\over r}$ | $\large\theta(t)=\theta_0+\omega t$ | $\large s(t)=s_0+vt$ | $\displaystyle\large T={2\pi\over\omega}={2\pi R\over v}$ | $\displaystyle\large f={1\over T}$          |

### Moto parabolico

| Accelerazione | Velocità | Legge oraria |
| ------------- | -------- | ------------ |
| $\large\begin{align}a_x=0 \\ a_y= -g\end{align}$ |$\large\begin{align}v_x(t)=v_0cos(\theta)\\ v_y(t)=v_0sen(\theta)-gt\end{align}$  | $\large\begin{align}x(t)=x_0+v_xt\\ y(t)=y_0+v_yt-{1\over 2}gt^2\end{align}$              |


![[piano inclinato.jpg|300x200]]
$\begin{gather}L={h\over sen\theta} \\ h=L sen\theta \end{gather}$

| Quantità di moto | Impulso                                                  | Attrito                      | Forza Centripeta                        | Forza elastica    | 
| ---------------- | -------------------------------------------------------- | ---------------------------- | --------------------------------------- | --- |
| $P=mv$           | $\overrightarrow{J}=F_{cost}\Delta t=\Delta P=m\Delta v$ | $\displaystyle F_{ad}=\mu N$ | $\displaystyle F_N=ma_N=m{v^2 \over r}$ | $\large F=-k\Delta x$    |



| Lavoro                                                                                  | Espressioni lavoro                           | Potenza | Potenza media           |
| --------------------------------------------------------------------------------------- | -------------------------------------------- | ------- | ----------------------- |
| $\large \overrightarrow{L}=\overrightarrow{F}\times \overrightarrow{d}=F*d*cos(\theta)$ | $L=\Delta E_c$ $L=\Delta E_p$ $L=\Delta E_m$ | $P=Fv$  | $\large P_m={L\over t}$ |

| Energia cinetica                   | Energia potenziale gravitazionale | Energia potenziale elastica        | Energia meccanica | Conservazione energia meccanica |
| ---------------------------------- | --------------------------------- | ---------------------------------- | ----------------- | ------------------------------- |
| $\displaystyle E_c={1\over 2}mv^2$ | $\displaystyle E_p=mgh$           | $\displaystyle E_e={1\over 2}kx^2$ | $E_m=E_c+E_p$     | $E_c^i+E_p^i=E_c^f+E_p^f$                                |

## Pendolo 
| Periodo |
| ------- |
| $\displaystyle T=2\pi{\sqrt{l\over k}}={2\pi\over \omega}$        |

| Raggio vettore                                                                                                                                     | Velocità | Accelerazione |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------- |
| $\displaystyle r_{CM}={m_1(x_1\hat{i}+y_1\hat{j}+z_1\hat{k})+m_2(x_2\hat{i}+y_2\hat{j}+z_3\hat{k})\over m_1+m_2}$ | $\displaystyle v_{CM}={\sum_im_iv_i\over \sum_im_i}={P\over m}$ | $\displaystyle a_{CM}={\sum_im_ia_i\over\sum_i m_i}$               |


| Urto elastico velocità                                                                                                                                                                                                          | Urto elastico energia |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
|$\begin{align}\displaystyle v_{f,2}=({2v_{i,1}\over 1+m_{21}})+({2m_{21}-1\over 1+m_{21}})v_{i,2} \\ \displaystyle v_{f,1}=({1-m_{21}\over 1+m_{21}})v_{i,1}+({2m_{21}\over 1+m_{21}})v_{i,2}\\ m_{21}={m2\over m1}\end{align}$ | $E_c^i=E_c^f$         |

| Momento della forza                                                | Momento d'inerzia                                                                   | Hyugens-Steiner  | Momento Angolare | 
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------- | ---------------- | ---------------- |
| $\overrightarrow{\tau}=\overrightarrow{r}\times\overrightarrow{F}$ | $\begin{align}I=mr^2 \\ I\overrightarrow{\alpha}=\overrightarrow{\tau} \end{align}$ | $I=I_{CM}+m*d^2$ | $\begin{align} \overrightarrow{L}=\overrightarrow{r}\times m\overrightarrow{v} \\ \overrightarrow{L}=\overrightarrow{r}\times\overrightarrow{P} \\ L(t)=I\alpha t=I\omega(t)  \end{align}$               |

| Calore, calore latente e           | Principio termodinamica     | Eq. gas  | Lavoro termodinamico | Relazione Mayer e libertà |
| --------------------------------- | --------------------------- | -------- | -------------------- | --------------- |
| $\begin{gather} Q=C\Delta T=cM\Delta T \\ Q_L=Lm \\ \eta={L_{TOT}\over Q_{ASS}}\end{gather}$ | $\Delta U=Q-L=nc_v\Delta T$ | $PV=nRT$ | $L=P*V$              |   $\begin{gather}c_p-c_v=R \\ c_v={1\over 2}fR \\ mono=3\\ bi=5 \\ tri=7 \end{gather}$              |

| Tr. adiabatica                                                                                                                              | Tr. isocora | Tr. isobara | Tr. isoterma |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ----------- | ------------ |
| $\begin{gather}PV^\gamma=cost \\ TV^{\gamma-1}=cost \\ \gamma={c_p\over c_v} \\ L=P_iV_i^{-\gamma}({V_f^{-\gamma+1}-V_i^{-\gamma+1}\over -\gamma+1})\end{gather}$ | $\begin{gather}V=cost \\ L=P\Delta V=0 \\ \Delta U=Q \\ Q=nc_v\Delta T\end{gather}$ | $\begin{gather} nRT_f=nRT_i=P_iV_i \\ P_fV_f=P_iV_i=PV \\ L=P_iV_iln({V_f\over V_i}) \\ Q=n\Delta T(c_v+R) \end{gather}$            |  $\begin{gather} T=cost \\ \Delta U=nc_v\Delta T=0 \\ \Delta U=Q-L=0 \\ Q=L\end{gather}$            |


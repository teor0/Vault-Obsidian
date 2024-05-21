---
tags: elettromagnetismo
created: 2024-02-07 12:16:32
updated: 2024-02-07 12:16:32
---
[[Caratteristiche elettromagnetiche, densità di carica, forza e campo elettrico]]
# Forza elettrica
Se prendiamo in considerazione 2 cariche disposte come segue,
![[forzele.jpg|200x300]]
possiamo definire la forza elettrica come: <font color=orange>$$F_E= {\hat{i}_{R_{12}} \cdot {q_1q_2\over 4\pi \varepsilon_0 R_{12}^2}}$$</font>
Si nota una similitude con l'equazione della forza gravitazionale: $F_G=-{\hat{i}_R \cdot {Gm_1m_2\over R^2}}$. Inoltre non vi è solo questa similitudine ma anche le seguenti:

- Nella forza elettrica le cariche hanno un segno mentre nella forza gravitazionale, le masse no.
- Entrambe dipendono da una costante, gravitazionale o dielettrica
- La forza elettrica può essere sia repulsiva che attrattiva, la forza gravitazionale è solo attrattiva.
- Le due equazioni si somigliano: $$\begin{align}
F_G=-{\hat{i}_R \cdot {Gm_1m_2\over R^2}} \\
F_E= {\hat{i}_R \cdot {q_1q_2\over 4\pi \varepsilon_0 R^2}}
\end{align}$$

---
# Induzione elettrica e legge di Gauss 
Un mezzo può essere:
- <font color=green>Lineare</font>, se si comporta linearmente.
- <font color=blue>Continuo</font>, se preso un campo elettrico e lo perturbo la reazione del mezzo non viene stravolta.
- <font color=purple>Omogeneo</font>, se fatta una traslazione nello spazio o nel tempo di un campo elettrico, il mezzo risponde con una traslazione dello spazio e nel tempo.
- <font color=orange>Isotropo</font>, se la risposta del materiale è invariante rispetto ad una rotazione.

L'induzione elettrica è il vettore che descrive la reazione del mezzo all'introduzione di una carica in un mezzo e dunque descrive la reazione alla distorsione. $$\underline{D}=\varepsilon\cdot\underline{E}$$
Ipotizziamo di avere una carica immersa in un mezzo e che essa generi un campo elettrico, allora l'induzione sarà pari a: $\underline{D}=\varepsilon\cdot\underline{E}$, ma la generica espressione del campo elettrico è data da: $\large\underline{E}=\hat{i}_R{q\over 4\pi\varepsilon R^2}$, perciò l'equazione dell'induzione passa a: $\large\underline{D}=\hat{i}_R{q\over 4\pi R^2}$. Se isolo la carica e ne calcolo il modulo ottengo che: $q=|\underline{D}|\cdot4\pi R^2$. Generalizzando l'equazione su una superficie ottengo la legge di Gauss: $$\large Q={\huge\unicode{x222F}}_{S}\ \underline{D}\ \circ\ \hat{u}\ dS$$
La carica totale lungo una superficie chiusa è data dall'integrale di flusso, dell'induzione elettrica per il versore normale. 
Una carica puntuale genera un'induzione elettrica che è costante per tutte le circonferenze di raggio costante. Se però si considera una distribuzione di carica non costante e dunque, non discreta ma continua, bisogna ricorrere a tale integrale. Esempio:
![[esgauss.jpg]]

---
# Potenziale elettrico
Si prenda in esame il seguente campo elettrico uniforme persistente, generato in precedenza da delle cariche:
![[potel.jpg]]
Il campo è d'equazione: $\underline{E}=-\hat{y}E_y$. Si immerge un'ulteriore carica q nel campo, essa subirà una forza elettrica $\underline{F}=q\cdot\underline{E}=-\hat{y}q\cdot E_y$ mostrando che la forza elettrica ha lo stesso verso del campo. Se si sposta la carica lungo l'asse y con una velocità che è costante, allora la forza totale agente sulla carica deve annullarsi secondo i principi della meccanica. 
Di conseguenza: $$\underline{F_{ext}}+\underline{F}=0\implies \underline{F_{ext}}=-\underline{F}=\hat{y}q\cdot E_y$$

Per conoscere l'energia necessaria a spostare la carica di una lunghezza $d\underline{l}=\hat{y}dy$, sarà necessario un lavoro $dW=\underline{F_{ext}}d\underline{l}=qE_ydy$.

## Potenziale elettrico differenziale o tensione
L'energia potenziale elettrica infinitesima per unità di carica è data da: $$dV={dW\over q}=E_ydy=-\underline{E}\circ d\underline{l}$$
L'equazione prende anche il nome di differenza di potenziale in un punto. Dati due punti $P_1\ \text{e}\ P_2$ la differenza di potenziale è pari a: $$V_{21}=V_2-V_1=\int^{P_2}_{P_1}-\underline{E}\circ d\underline{l}$$
Per il principio di conservazione dell'energia essendo la forza elettrica conservativa, il lavoro o meglio la differenza di potenziale è indipendente dal cammino.

Data una carica puntuale ed un punto P individuato da coordinate polari, si vuole calcolare il potenziale nel punto P a distanza R.
![[potelpolari.jpg]]
Per definizione la tensione in un punto è calcolata tramite l'integrale fra R e $\infty$ dove la tensione all'infinito tende a 0 per definizione, dunque: $$V=-\int^{R}_{\infty}\underline{E}\circ d\underline{l}$$

posto $d\underline{l}=\hat{i}_RdR$ allora $$V=-\int^{R}_{\infty}\hat{i}_R\cdot({q\over 4\pi\varepsilon R^2})\cdot\hat{i}_RdR=-{q\over 4\pi\varepsilon}\int^R_{\infty}{dR\over R^2}={q\over 4\pi\varepsilon}\cdot{1\over R}\large\vert^R_\infty={q\over 4\pi\varepsilon R}$$
In sostanza in punto P si hanno campo elettrico e potenziale elettrico pari a: $$\begin{align}
\underline{E}=\hat{i}_R\cdot{q\over 4\pi\varepsilon R^2} \\
V={q\over 4\pi\varepsilon R}
\end{align}$$
Il campo è un vettore mentre il potenziale è uno scalare. Il potenziale è inversamente proporzionale alla distanza mentre il campo al quadrato della distanza.
Se la carica dovesse essere posta in un punto diverso dall'origine l'equazione del potenziale sarà: $$V(\underline{R})={q\over 4\pi\varepsilon |R-R_1|}$$
mentre se si vuole calcolare il potenziale in un punto P dato da $n$ cariche, l'equazione sarà:
$$V(\underline{R})=\sum^{n}_{i=1}{q\over 4\pi\varepsilon |R-R_i|}$$


---
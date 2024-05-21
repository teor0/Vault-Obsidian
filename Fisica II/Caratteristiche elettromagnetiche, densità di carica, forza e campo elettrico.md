---
created: 2023-11-17 15:50:02
updated: 2023-11-17 15:50:02
tag: elettromagnetismo
---
#elettromagnetismo 
# Caratteristiche elettromagnetiche, cariche e forza elettrica
La conducibilità rappresenta essenzialmente la possibilità che ci siano degli elettroni liberi nel mezzo per effetto del quale si produce la corrente. Il vuoto è un mezzo ideale, che spesso verrà considerato all'interno degli esercizi. Dividiamo in 2 categorie i materiali :
- Dielettrici volgarmente detti isolanti, che non fanno passare la corrente appunto.
- Conduttori, materiali che permettono il passaggio di elettroni al loro interno. 

Le caratteristiche elettromagnetiche dei materiali che ci interessano sono essenzialmente 3:
1. $\large\varepsilon$ <font color=orange>costante dielettrica</font> espressa dall'equazione: $\large{\varepsilon=\varepsilon_r\cdot\varepsilon_0}$ con $\large{\varepsilon_0}$=$8.854\times10^{-12}$ e $\large{\varepsilon_r}$ costante dielettrica relativa, che per il vuoto vale 1.
2. $\large\mu$ <font color=purple>permeabilità magnetica</font> espressa dall'equazione: $\large{\mu=\mu_r\cdot\mu_0}$ con $\large{\mu_0}$=$4\pi\times10^{-12}$ e $\large{\mu_r}$ permeabilità magnetica relativa, che per il vuoto vale 1.
3. $\large\sigma$ <font color=blue>conducibilità</font> che misura la capacità degli elettroni di muoversi se viene applicato un campo.

> Un materiale non magnetico ha $\mu_r=1$.

L'elettrone è la carica negativa presente in natura, mentre le lacune, cariche positive sono generate dallo spostamento spaziale di un elettrone. Le cariche si indicano con $q$ ed hanno come unità di misura Coulomb. La carica è la sorgente del campo elettromagnetico, in particolare una sorgente immerso in mezzi differenti genera campi differenti. Un campo esercita una forza in fisica, in particolare la forza è maggiore più vicino alla sorgente e minore se la distanza dalla sorgente aumenta.
Prese 2 cariche nel vuoto, $q_1\ \text{e}\ q_2$ per effetto della carica sorgente $q_1$, la carica $q_2$ risente della forza elettrica: $\displaystyle\Large\underline{F}_e=\hat{i}_R{q_1\cdot q_2\over 4\pi\varepsilon_0R^2}$ dove il segno è dato dalle cariche.
![[cariche.jpg|100x200]]

Nel vuoto la forza elettrica è massima perché la forza dipende sia dalla distanza sia da $\varepsilon$.
Preso un materiale in equilibrio elettrico se inserisco una carica avviene una distorsione degli atomi che prende il nome di <font color=red>polarizzazione elettrica</font>. La misura di polarizzazione di un materiale è $\large{\varepsilon=\varepsilon_r\cdot\varepsilon_0}$ ovvero la costante dielettrica.

---
# Densità di carica e campo elettrico
Dal punto di vista microscopico le cariche sono distribuite in modo discreto, ma volendo sapere la distribuzione media di carica si usa un approccio macroscopico. Definiamo così la <font color=red>densità di carica</font>: sia $\Delta V$ un volume infinitesimo, $Delta S$ una superficie infinitesima e $\Delta l$ una lunghezza infinitesima su cui sono distribuite in modo uniforme una carica infinitesima $\Delta Q$, allora definiamo le seguenti densità di carica:
- $\displaystyle\large\rho_l=\lim_{\Delta l\rightarrow0}{\Delta Q\over\Delta l}={dQ\over dl}$
- $\displaystyle\large\rho_S=\lim_{\Delta S\rightarrow0}{\Delta Q\over\Delta S}={dQ\over dS}$
- $\displaystyle\large\rho_V=\lim_{\Delta V\rightarrow0}{\Delta Q\over\Delta V}={dQ\over dV}$

La carica totale lineare, su una superficie e su un volume è data rispettivamente da:
- $\displaystyle\large{Q=\int_{l}\rho_l dl}$
- $\displaystyle\large{Q=\iint_{S}\rho_S dS}$
- $\displaystyle\large{Q=\iiint_{V}\rho_V dV}$

Presa una carica positiva definiamo il <font color=orange>campo elettrico</font> prodotto:
$\displaystyle\large\underline{E}=\hat{i}_R{q\over 4\pi\varepsilon R^2}$
ovvero la legge di Coulomb.
Su tutti i punti a distanza R dalla carica il valore del campo elettrico è costante. Se dovessi spostarmi ad una distanza $R_1>R$ il campo perderebbe di forza rispetto al quadrato di $R_1$, in particolare il campo sarebbe dato dall'equazione: $\displaystyle\large\underline{E}(R_1)=\hat{i}_R{q\over 4\pi\varepsilon_0R_1^2}$
![[campele.jpg|100x300]]
Supponiamo di avere una carica identificata dal vettore posizione $\underline{R}_1$
![[campoelees.jpg|300x400]]
si supponga di volere calcolare il campo elettrico a cui è soggetto il punto $P(x,y,z)$ identificato dal vettore posizione $\underline{R}$. Il campo è dato da: $\displaystyle\large\underline{E}=\hat{i}_{R-R_1}{q_1\over 4\pi\varepsilon_0|\underline{R}-\underline{R}_1|^2}$ con $\displaystyle\large\hat{i}_{R-R_1}={\underline{R}-\underline{R}_1\over|\underline{R}-\underline{R}_1|}$.

Supponiamo di avere $n$ cariche identificate ognuna da un vettore posizione, perciò $q_1,q_2,...,q_n$ e $\underline{R}_1,\underline{R}_2,...,\underline{R}_n$, il campo elettrico totale usando il principio di sovrapposizione che vale nel vuoto sarà:
$\displaystyle\large\underline{E}=\sum^{n}_{i=1}\underline{E}_i=\sum^{n}_{i=1}{\underline{R}-\underline{R}_i\over|\underline{R}-\underline{R}_i|}{q_i\over4\pi\varepsilon_0|\underline{R}-\underline{R}_i|^2}={1\over 4\pi\varepsilon_0|\underline{R}-\underline{R}_1|^2}\sum^{n}_{i=1}{q_i(\underline{R}-\underline{R}_i)\over|\underline{R}-\underline{R}_i|}$

## importate proprietà
Se la carica è posta nel origine il grafico sarà del tipo ![[campimpl.jpg|200x300]] questo perché nel origine il campo implode quindi è come se non fosse definito. Se due cariche sono poste simmetricamente i campi si vanno ad annullare in un punto come la figura seguente illustra: ![[campnull.jpg|300x300]].

---
---
tags: elettrotecnica, 
created: 2024-04-18 18:25:14
updated: 2024-04-18 18:25:14
---
[[Topologia dei circuiti]]
# Incongruenze dei mezzi ideali
Presi due generatori: ![[genideali.jpg|200x400]]
- Se $v_1(t)\neq v_2(t)$ il nodo A e B avrebbero contemporaneamente due differenze di potenziale diversa.
- Se $v_1(t)=v_2(t)$ non si potrebbe calcolare la corrente perché ci sarebbero infinite soluzioni.

Essendo i generatori ideali, possono erogare una potenza infinita. Occorre introdurre un modello più accurato combinando più elementi ideali per evitare incongruenze e limitazioni. Andiamo quindi ad utilizzare i generatori reali.

## Generatori reali

>[!definizione]
>Un generatore reale è formato da un generatore ideale e una resistenza. Nel caso del generatore di tensione, la resistenza è in serie, mentre per il generatore di corrente la resistenza è in parallelo.

![[genreali.jpg|600x300]]
Riprendiamo adesso il circuito con due generatori di tensione in parallelo, ma consideriamoli reali adesso. ![[circreale.jpg|400x400]]
Sapendo che $e_D=0,e_B=v_1,e_C=v_2$, calcoliamo la tensione al nodo A tramite KCL:
$\displaystyle i_{R_1} + i_{R_2}=0\implies {e_A-e_B\over R_1}+{e_A-e_C\over R_2}=0\implies e_A({1\over R_1}+{1\over R_2})={v_1\over R_1}+{v_2\over R_2}\implies$ 
$\displaystyle \implies e_A=({v_1\over R_1}+{v_2\over R_2}){R_1R_2\over R_1+R_2}$. Dunque il potenziale è calcolabile!

## Potenza con generatori reali
Quanto vale la potenza in presenza di generatori reali? Riprendiamo i circuiti usati per definire i generatori reali e calcoliamo la potenza sulla resistenza che non fa parte del generatore reale, ovvero la resistenza di carico $R_L$. ![[genreali.jpg|400x300]]
- Per il generatore reale di tensione: $P_{R_L}=V_{R_L}I_{R_L}$ con $V_{R_L}={V_gR_L\over R_L+R_g}$ essendo un partitore di tensione il circuito. Perciò $\displaystyle P_{R_L}={V_gR_L\over R_L+R_g}{V_g\over R_g+R_L}=V_g^2{R_L\over (R_g+R_L)^2}$
- Per il generatore reale di corrente: $P_{R_L}=V_{R_L}I_{R_L}$ con $I_{R_L}={I_gR_g\over R_L+R_g}$ essendo un partitore di corrente il circuito. Perciò $\displaystyle P_{R_L}={R_LI_gR_g\over R_L+R_g}{I_gR_g\over R_L+R_g}=I_g^2R_g^2{R_L\over (R_L+R_g)^2}$

Quando le due resistenze dei generatori sono uguali allora eguagliando le potenze dei generatori reali si ha che: $V_g^2{R_L\over (R_g+R_L)^2}=I_g^2R_g^2{R_L\over (R_L+R_g)^2}\implies V_g^2=I_g^2R_g^2\implies V_g=I_gR_g$
Dunque a parità di resistenze i generatori reali si possono scambiare!

## Corrente massima e tensione massima
La massima corrente che si può fornire è detta <font color=red>corrente di cortocircuito</font>, la massima tensione è detta invece <font color=red>tensione di circuito aperto</font>. 
Preso il seguente circuito ![[correntemax.jpg|600x200]] la corrente massima è calcolata tramite KVL come: $-V_g+i_{AB}R_g+i_{AB}R_L=0\implies -V_g+i_{AB}(R_g+R_L)=0\implies i_{AB}={V_g\over R_g+R_L}$ dunque per avere corrente massima occorre che $R_L=0\implies i_{AB}={V_g\over R_g}=i_{CC}$
Per la tensione massima invece, se $R_L=\infty\implies i_{AB}={V_{AB}\over\infty}=0$ dunque tramite KVL: $-V_g+i_{AB}R_g+V_{AB}=0\implies V_g=V_{AB}=V_{CA}$

---
# Teorema massimo trasferimento di potenza e rendimento
La massima corrente per il generatore reale è la corrente di cortocircuito, $\displaystyle i_{CC}={V_g \over R_g}$ a cui corrisponde una potenza erogata sulla resistenza di carico pari a 0. $\displaystyle P=V_g{V_g\over R_g}-R_g({V_g\over R_g})^2=0$
La potenza massima sulla resistenza di carico è pari a $\displaystyle P={V_g^2\over 4R_g}$, perciò per $R_g=0$ la potenza cresce indefinitamente al crescere di $i$.

In presenza di trasferimento massimo della potenza, il rendimento è del 50% ovvero il 50% della potenza viene dissipato in calore. Formalmente definiamo <font color=orange>rendimento</font>, il rapporto tra la potenza assorbita dal carico e la potenza erogata dal generatore reale.
$\displaystyle \eta={P_{R_L}\over P_{V_g}}={V_{R_L}i\over V_gi}={(V_g-V_{R_g})i\over V_gi}$
Calcolo rendimento: $\displaystyle\eta=1-{V_{R_g}i\over V_gi}=1-{R_L{V_g^2\over (R_L+R_g)^2}\over{V_g^2\over R_L+R_g}}=1-{R_L\over R_L+R_g}$

---
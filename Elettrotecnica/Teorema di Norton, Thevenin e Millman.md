---
tags: elettrotecnica, 
created: 2024-04-24 15:21:15
updated: 2024-04-24 15:21:15
---
[[Linearità]] 
# Teorema di Norton
>[!definizione]
>Il teorema di Norton afferma che, un circuito lineare o una porzione di circuito accessibile da due terminali A e B, può essere sostituito con un circuito equivalente formato da un generatore di corrente $I_N$ in parallelo ad un resistore $R_N$.

In particolare, la corrente $I_N$ è la corrente di corto circuito tra i terminali A e B, mentre $R_N$ è la resistenza equivalente vista ai loro capi quando i generatori indipendenti sono spenti.
Si passa da ![[circuthnor.jpg|500x300]]
a ![[circnorton.jpg|500x200]]
## Dimostrazione
1. I parametri del teorema non dipendono dal resto del circuito ma solo dalla porzione da sostituire.
2. Il resto del circuito può essere rappresentato nel caso più generale da un generatore di tensione che imprime esattamente la tensione di porta.

![[dimnorton.jpg|600x400]]
Applicando il principio di sovrapposizione degli effetti al circuito lineare, si ottiene $i_{AB}=\sum_i a_iV_i+\sum_j b_jI_j+ cv=i_{AB}^{int}+i_{AB}^{ext}$
con $V_i$ e $I_j$ i generatori indipendenti di tensione e corrente interni al circuito. L'effetto dei generatori indipendenti interni alla rete coincide con la corrente di corto circuito a meno del verso. $i_{AB}^{int}=\sum_i a_iV_i+\sum_j b_jI_j=i_{AB}|_{V=0}=-i_{CC}$
dunque $i_{AB}^{int}=\sum_i a_iV_i+\sum_j b_jI_j=i_{AB}=-i_{N}$
L'effetto dei generatori esterni alla rete coincide con la corrente generata dal generatore di tensione $i_{AB}^{ext}=cv=i_{AB}|_{V_i=0,I_j=0}$
Il parametro $c$ si ottiene calcolando la conduttanza vista tra i due terminali, quando i generatori indipendenti sono spenti e pertanto coincide con l'inverso della resistenza di Norton $\displaystyle c={i_{AB}\over v}|_{V_i=0,I_j=0}={1\over R_N}$
Il circuito lineare con due terminali risulta equivalente al bipolo di Norton in quanto presentano la stessa relazione corrente-tensione.
$\displaystyle i_{AB}=i_{AB}^{int}+i_{AB}^{ext}=-I_N+{v_{AB}\over R_N}$
![[circnorton.jpg|500x200]]
Se eseguo una KCL su A con il nodo B a terra ottengo infatti: $\displaystyle -I_N+{V_{AB}\over R_N}-i_{AB}=0\implies i_{AB}=-I_N+{V_{AB}\over R_N}$

---
# Teorema di Thevenin
>[!definizione]
>Il teorema di Thevenin afferma che, un circuito lineare o una porzione di circuito accessibile da due terminali A e B, può essere sostituito con un circuito equivalente formato da un generatore di tensione $V_{Th}$ in serie ad un resistore $R_{Th}$.

In particolare, la tension $V_{Th}$ è la corrente di corto circuito tra i terminali A e B, mentre $R_N$ è la resistenza equivalente vista ai loro capi quando i generatori indipendenti sono spenti.
Si passa da ![[circuthnor.jpg|500x300]]
a ![[circthev.jpg|500x300]]

## Dimostrazione
1. I parametri del teorema non dipendono dal resto del circuito ma solo dalla porzione da sostituire.
2. Il resto del circuito può essere rappresentato nel caso più generale da un generatore di corrente che imprime esattamente la corrente di porta.

![[circthevdim.jpg|400x500]]
Applicando il principio di sovrapposizione degli effetti al circuito lineare, si ottiene $V_{AB}=\sum_i A_iV_i+\sum_j B_jI_j+ Ci=V_{AB}^{int}+V_{AB}^{ext}$
$V_i$ e $I_j$ sono generatori di tensione e corrente interni. Se spengo il generatore di corrente esterno ottengo che $V_{AB}=\sum_i A_iV_i+\sum_j B_jI_j=V_{AB}|_{i=0}=V_{AB}^{vuoto}\implies V_{AB}^{int}=V_{Th}$
L'effetto dei generatori esterni alla rete coincide con la tensione generata dal generatore di corrente: $V_{AB}^{ext}=Ci=V_{AB}|_{V_i=0,I_j=0}$ ma il parametro C, che è un resistenza si ottiene tramite $C={V_{AB}\over i}$ e la prima espressione implica lo spegnimento di tutti i generatori interni che è la definizione di resistenza di Thevenin $R_{Th}=C$
Dunque $V_{AB}=V_{AB}^{int}+V_{AB}^{ext}=V_{Th}+R_{Th}i$ la prova di ciò, si ottiene anche tramite KVL: $V_{R_{Th}}=-iR_{Th}$ $V_{R_{Th}}+V_{AB}-V_{Th}=0\implies V_{AB}=V_{Th}+R_{Th}i$ 

---
# Relazione tra Thevenin e Norton
- I circuiti di Thevenin e Norton rappresentano rispettivamente un generatore reale di tensione e generatore reale di corrente. 
- $R_{Th}=R_{N}$.
- È possibile sostituire un circuito equivalente di Thevenin con uno di Norton e viceversa.
- Siccome Thevenin e Norton valgono per qualsiasi carico possiamo dire che godono di equivalenza esterna alla porta tra di loro.

La conversione tra generatori di Norton e Thevenin:
![[sostgennor.jpg|400x600]]
![[sostthev.jpg|400x600]]

In particolare per la conversione del generatore reale di tensione a circuito di Norton si ha che: $I_{CC}=I_N={V_g\over R_g}$
mentre per la conversione del generatore reale di corrente a circuito di Thevenin si ha: $V_{CA}=V_{Th}=I_gR_g$

---
## Potenza su Thevenin e Norton
La massima potenza erogabile dal circuito alla porta A-B è $P_{Max}={V_{Th}I_N\over 4}$ quando la porta è chiusa da una resistenza $R_{AB}=R_{Th}=R_N$ $V_AB={V_{Th}\over 2}$ $I_{AB}={I_N\over 2}$ $P_{AB}=V_{AB}I_{AB}={V_{Th}I_N\over 4}$

---
# Teorema di Millman
Il teorema di Millman afferma che:
>[!definizione]
>La tensione $V_0$ ai capi di un parallelo di:
>- Generatori di tensione $V_{Ai}$ con in serie resistenza $R_{Ai}$
>- Generatori di corrente $I_{Bj}$ con eventuali resistenze in serie $R_{Bj}$
>- Resistenze $R_{Ck}$
>è pari a $\displaystyle V_0=R_0I_0={\sum_i{V_{Ai}\over R_{Ai}}+\sum_j I_{Bj}\over \sum_i{1\over R_{Ai}}+\sum_k{1\over R_{Ck}}}={\sum_i{V_{Ai}G_{Ai}}+\sum_j I_{Bj}\over \sum_i G_{Ai}+\sum_k G_{Ck}}$

>[!regola]
>Le resistenze in serie ai generatori di corrente vengono ignorate

## Dimostrazione
Per dimostrare Millman si può usare il bilancio della corrente ad uno dei due nodi:
![[dim1mill.jpg|650x150]]
$V_{AB}=e_A-e_B=e_A=V_0=I_0R_0$ tramite KCL ottengo: $\displaystyle {e_A-V_{A1}\over R_{A1}}+{e_A-V_{AN}\over R_{AN}}-I_{B1}-I_{BM}+{e_A\over R_{C1}}+{e_A\over R_{CK}}+{e_A\over R_{C_{N_R}}}=0$
$\displaystyle e_A(\sum^{N}_{i=1}{1\over R_{Ai}}+\sum^{N_R}_{K=1}{1\over R_{CK}})=\sum^{N}_{i=1}{V_{Ai}\over R_{Ai}}+\sum^{M}_{j=1}I_{Bj}\implies V_0=I_0R_0=e_A={\sum^{N}_{i=1}{V_{Ai}\over R_{Ai}}+\sum^{M}_{j=1}I_{Bj}\over \sum^{N}_{i=1}{1\over R_{Ai}}+\sum^{N_R}_{K=1}{1\over R_{CK}}}$ come volevasi dimostrare.
Altrimenti si può usare l'equivalenza tra generatore reale di tensione e generatore reale di corrente.
1. Trasformo i generatori reali di tensione in generatori reali di corrente.
2. Elimino le resistenze $R_{Bj}$ in serie ai generatori di corrente $I_{Bj}$.
 
Ottengo dunque il seguente circuito: ![[dim2mill.jpg|400x150]] $\displaystyle V_0=I_0R_0={\sum^{N}_{i=1}{V_{Ai}\over R_{Ai}}+\sum^{M}_{j=1}I_{Bj}\over \sum^{N}_{i=1}{1\over R_{Ai}}+\sum^{N_R}_{K=1}{1\over R_{CK}}}$

---
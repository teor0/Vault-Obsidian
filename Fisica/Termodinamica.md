---
tag: #fisica 
created: 2023-05-17 11:26:01
updated: 2023-05-17 11:26:01
---
#fisica 
[[Momento angolare e teorema del momento angolare]]
# Definizioni di base
Il calore si trasferisce da un corpo più caldo ad uno più freddo. Generalmente all'aumentare del calore aumenta pure la temperatura. La temperatura verrà espressa in Kelvin ($K$) e la relazione tra Kelvin e gradi Celsius è $0°C=273,15K\implies T_C=T-273,15$. Prendiamo adesso un tipico grafico calore-temperatura:
![[grafterm.jpg|500x400]]
Come detto al crescere del calore, cresce la temperatura e la retta. La pendenza della retta rappresenta la capacità termica $C$, la cui unità di misura è $\displaystyle {J\over kg*K}$

>Un corpo assorbe calore e modifica la propria temperatura a seconda della capacità termica.

Il calore perciò può essere formulato come $Q=C\Delta T$. Esiste poi il calore specifico, che indica per unità di massa la capacità termica e viene indicato con $c$.
Nasce così una seconda equazione per definire il calore: $Q=cm\Delta T$, da cui si ricava che $C=cm$ e $\displaystyle c={C\over m}$.

>Una caloria è la quantità di calore che serve per far salire di 1° la temperatura di un litro d'acqua. La relazione tra caloria e calore è: $1\ cal=4,186\ J$. 

Il calore specifico si misura in $\displaystyle{J\over kg*K}$, $\displaystyle{kcal\over kg*K}$ oppure $\displaystyle{cal\over g*K}$.

>Una mole è il numero di atomi contenuti in 12g dell'isotopo del carbonio avente numero di massa 12.

Il numero di atomi o molecole in una mole è pari al numero di Avogadro: $N_A=6,02\times 10^{23}$. Per questo se si ha un gas monoatomico, esso ha $6,02\times 10^{23}$.

>Il calore latente è la quantità di calore per effettuare un passaggio di stato, e viene espresso come: $Q_L=Lm$ dove $L$ è il calore latente della particolare trasformazione che si vuole effettuare ad esempio fusione e m è la massa da trasformare.

Se si fa un passaggio di stato, il calore latente è lo stesso cambiato di segno, perciò per solidificare l'acqua occorre lo stesso calore latente per la fusione. Per sapere ad esempio quanto ghiaccio si riesce a sciogliere si può usare la seguente equazione:
$C_{H_2O}m_{H_2O}(T_z-T_{H_2O})-C_gm_g(T_z-T_g)-L_fm_x=0\implies$ 
$\displaystyle m_x={C_{H_2O}m_{H_2O}(T_z-T_{H_2O})-C_gm_g(T_z-T_g)\over L_f}$

In un sistema isolato il calore ceduto e calore assorbito saranno uguali perciò vale l'equazione: $Q_{ced}+Q_{ass}=0\implies Q_{ced}=-Q_{ass}$

>Un gas perfetto è un sistema di punti materiali che non si urtano ma urtano con le pareti del recipiente che lo contiene. 

Un gas perfetto possiede: pressione, volume e temperatura. Esistono 4 trasformazioni fondamentali del gas in un sistema isolato:
1. Isobara: pressione costante
2. Isocora: volume costante
3. Isoterma: temperatura costante
4. Adiabatica: calore pari a 0

>[!regola]
> Il Primo principio della termodinamica afferma che: La somma di tutte le energie interne delle molecole del gas è pari al calore scambiato dal sistema meno il lavoro termodinamico. $\Delta U=Q-L$

Il lavoro termodinamico corrisponde al lavoro meccanimo. Il lavoro nel caso più semplice è dato da $L=F*S$, moltiplicando e dividendo per un'area: $\displaystyle L={F\over S^2}*S*S^2$, ma la pressione è data da $\displaystyle {F\over S^2}$ mentre $V=S^3$ perciò si ottiene che $L=P*V$.
Se il volume varia nel tempo $L=P*\Delta V=P*(V_f-V_i)$, in particolare calcoliamo il valore di infinite molecole come $dL=P*dV$.

Per tutte le trasformazioni vale la seguente equazione: $\Delta U=n*c_v*\Delta T$ dove $n$ è il numero di moli e $c_v$ è il calore specifico molare a volume costante del gas. Il calore specifico molare a volume costante di un gas è dato da $c_v={1\over 2}fR$ con R costante di Rydberg, pari a $8,31$ e $f$ grado di libertà. Un atomo ha grado di libertà pari a 3, due atomi legati fra loro hanno grado di libertà $f=5$.

>[!regola]
> La legge dei gas perfetti afferma che: PV=nRT.

La relazione di Mayer afferma che $c_p-c_v=R$, ovvero che la differenza tra calore specifico molare a pressione costante e calore specifico molare a volume costante è pari alla costante di Rydberg.

Per le trasformazioni adiabatiche valgono le seguenti equazioni: $\displaystyle PV^\gamma=cost$ con $\displaystyle\gamma={c_p\over c_v}$. Ma costante vuol dire che $P_iV_i^\gamma=P_fV_f^\gamma$. L'altra equazione è $TV^{\gamma-1}=cost$ ma anche in questo caso costante equivale a dire $T_iV_i^{\gamma-1}=T_fV_f^{\gamma-1}$. Calcoliamo il lavoro, ricordando che $Q=0$ perciò $\Delta U=-L$ o meglio $\displaystyle L=\int^{V_f}_{V_i} PdV$. Utilizzando $P_iV_i^{\gamma}=P_fV_f^{\gamma}=PV^{\gamma}$ sostituendo a P nell'integrale $\displaystyle {P_iV_i^{\gamma}\over V^{\gamma}}$ si ottiene $\displaystyle L=\int^{V_f}_{V_i}{P_iV_i^{\gamma}\over V^{\gamma}}dV=P_iV_i^{\gamma}\int^{V_f}_{V_i}{dV\over V^{\gamma}}=P_iV_i^{\gamma}\int^{V_f}_{V_i}V^{-\gamma}dV=$
$\displaystyle\large {=P_iV_i^{\gamma}({V^{-\gamma+1}\over -\gamma+1})|^{V_f}_{V_i}}=P_iV_i^{\gamma}({V_f^{-\gamma+1}-V_i^{-\gamma+1}\over -\gamma+1})\implies$
$\displaystyle L=P_iV_i^{-\gamma}({V_f^{-\gamma+1}-V_i^{-\gamma+1}\over -\gamma+1})$.

Per la trasformazione isocora, valgono le seguenti equazioni: $V=cost\implies L=P\Delta V=0\implies \Delta U=Q\implies Q=nc_v\Delta T$.

Per la trasformazione isoterma, valgono le seguenti equazioni: $T=cost\implies \Delta U=nc_v\Delta T=0\implies\Delta U=Q-L=0\implies Q=L$.

Prima di passare alla trasformazione isobara, scriviamo la legge dei gas perfetti per gli stati iniziali: $P_iV_i=nRT_i$ e $P_fV_f=nRT_f$ ma $T_i=T_f$ quindi $nRT_f=nRT_i=P_iV_i$ perciò $P_fV_f=P_iV_i=PV$. Calcoliamo così il lavoro come $\displaystyle L=\int^{V_f}_{V_i}PdV=\int^{P_i}_{V_i}{dV\over V}=P_iV_i\int^{V_f}_{V_i}{dV\over V}=P_iV_i({ln V|}^{V_f}_{V_i})=P_iV_i(ln V_f-ln V_i)=P_iV_iln({V_f\over V_i})$
Per la trasformazione isobara, valgono le seguenti equazioni: $\displaystyle P=cost\implies L=\int^{V_f}_{V_i}PdV=P\int^{V_f}_{V_i}dV=P(V_f-V_i)$ esplicitando il volume con la legge dei gas perfetti $\displaystyle V_i={nRT_i\over P}$ e $\displaystyle V_f={nRT_f\over P}$ si ha che 

$Q=\Delta U+L=nc_v\Delta T+P\Delta V=nc_v\Delta T+P(V_f-V_i)$
$\displaystyle =nc_v\Delta T+P({nRT_f-nRT_i\over P})=nc_v\Delta T+nRT_f-nRT_i$
$=nc_v\Delta T+nR\Delta T=n\Delta T(c_v+R)\implies Q=n\Delta T(c_v+R)$.

---

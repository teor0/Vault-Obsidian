---
tags: automatica
created: 2024-02-26 11:34:02
updated: 2024-02-26 11:34:02
---
# Definizione di automatica 
Partiamo con il dare la definizione di automatica. 
>[!definizione] 
>L'automatica è una disciplina appartenente all'area dell'ingegneria dell'informazione che si occupa delle modalità attraverso le quali un dato fenomeno (un processo fisico o biologico) evolve nel tempo, perseguendo un dato obiettivo senza intervento del fattore umano.

Il modello di afflusso-deflusso è il primo fenomeno che analizziamo. La figura descrive il modello ![[affldefl.jpg]]
È un processo fisico dove un bacino che si riempie e si svuota d'acqua, tramite dighe, fiumi ecc. L'obiettivo è far sì che il serbatoio non vada a tracimare, causando inondazioni. Dunque la quantità che va monitorata è il livello di acqua corrente. Lo scopo dell'automatica è quello di sostituire il "controllore", una persona, con un sistema automatizzato. 
Formalizzazione dell'obiettivo:
> Per quanto riguarda l'altezza indicata con $h(t)$, si costruisce un intervallo di sicurezza tale che $h_{min}(t)<h(t)<h_{max}(t)$. Dove $h_{min}$ e $h_{max}$ vanno ad indicare i livelli estremi, in modo tale che il serbatoio non deve né riempirsi né svuotarsi troppo.

Esempio di algoritmo: 
``` 
0. SARACINESCA := OFF
1. IF((SARACINESCA==OFF) AND (h(t)>=hmax))
		THEN SARACINESCA:=ON
2. IF((SARACINESCA==ON) AND (h(t)<=hmin))
	THEN SARACINESCA:=OFF
3. GO TO 1
```
Descrivere il modello afflusso-deflusso consiste nel descrivere il <font color=blue>controllo a catena chiusa</font> (feedback/retroazione). Se considero il sistema come una serie di blocchi si ha: ![[catenachiusa.jpg]]
Più in generale: ![[gencatenachiusa.jpg]]

---
# Sistema dinamico
Un sistema dinamico è una rappresentazione astratta di una relazione fisica di causa-effetto. Gli ingressi sono le cause, mentre le uscite sono l'effetto. Un segnale è la rappresentazione formale nel tempo di una grandezza fisica. Definiamo adesso nel esempio del modello afflusso-deflusso alcuni segnali: 
- Afflusso: segnale analogico, identificato con $q_i(t)$ è una funzione sul dominio dei tempi che restituisce un numero reale di unità di misura. Lega dunque il tempo ad una quantità dotata di una certa unità di misura dunque: $q_i: T\rightarrow R$
- Saracinesca: segnale digitale/logico, identificata con $s(t)$ è una funzione del tipo: $S: T\rightarrow {ON,OFF}$
- Altezza: segnale analogico, identificata con $h(t)$ misurata in metri, è del tipo: $h: T\rightarrow R$

Il dominio individua il tipo di sistema tra:
1. Sistema dinamico a tempo continuo, $T=R$ analizzo con "continuità" un dato fenomeno.
2. Sistema dinamico a tempo discreto, $T=Z$ analizzo un dato fenomeno co una "logica di campionamento".

Esempio:
![[leggebil.jpg]]
Ipotizziamo che la saracinesca sia aperta (stato ON), e poniamo che la sezione del serbatoio sia costante pari a S e la sezione del rubinetto di uscita sia sempre costante pari a $S_0$. Poi poniamo che: 
- Causa (ingresso) $\rightarrow$ afflusso
- Effetto (uscita) $\rightarrow$ deflusso

Enunciamo adesso la legge di bilancio: se l'acqua è un fluido ideale vale che la relazione afflusso-deflusso="variazione di volume di acqua nel serbatoio nell'unità di tempo" da cui, formalmente, si ha che se $v(t)=s\cdot h(t)\implies q_i(t)-q_o(t)={d\over dt}v(t) \implies q_i(t)-q_o(t)={d\over dt}(s\cdot h(t))\implies q_i(t)-q_o(t)=s{dh\over dt}$
Per determinare l'uscita la sola conoscenza dell'ingresso non è sufficiente, bisogna conoscere l'altezza.

---
# Principio energetico o legge di Bermulli
$s{dh\over dt}=q_i(t)-q_o(t)$ anche se sembra un'equazione differenziale, non presenta l'altezza al netto dell'ingresso. Dunque tramite il principio energetico la trasformo in equazione differenziale che mi permette di trovare l'altezza. Ipotizziamo che il moto di deflusso sia laminare, ovvero senza turbolenze. Il principio energetico che si utilizza è il seguente: Lavoro delle forze di pressione atmosferica + energia cinetica del fluido + energia gravitazionale (Archimede) = costante dunque: $P+{1\over 2}p\cdot V^2+pgh=costante$.
Applicando il principio al flusso in ingresso = flusso in uscita otteniamo che: $$P_1+{1\over 2}p\cdot V_1^2+pgh(t)=P_2+{1\over 2}\cdot V_2^2+pg\cdot 0\implies pgh(t)={1\over 2}p\cdot V_2^2$$ Ponendo $V_1<<V_2$ ottengo $V_1=0$ e apportando altre approssimazioni si avrà in fine che: $$\displaystyle{V_2^2(t)\over 2}=gh(t)$$
Deflusso e velocità sono legate dalla relazione $q_o(t)=S_o\cdot V_2(t)=S_o\sqrt{2gh(t)}$ per cui otteniamo che $q_o(t)=S_o\sqrt{2gh(t)}$ e possiamo scrivere che: $$\begin{align}
s{dh\over dt}=q_i(t)-S_o\sqrt{2gh(t)} \\
q_o(t)=S_o\sqrt{2gh(t)}
\end{align}$$
Per ottenere il deflusso occorre risolvere l'equazione differenziale calcolando l'altezza e poi data l'altezza calcolare il deflusso.

>[!definizione] 
>Lo stato del sistema è una variabile intermedia necessaria per ottenere l'uscita noto l'ingresso. È necessario conoscere lo stato iniziale affinché dato ad esempio, la legge precedente si possa integrare per ottenere l'altezza. Dunque bisogna conoscere $h(t_0)=h_0$

Perciò "l'algoritmo" sarà:
1. Conoscere $q_i(t)$ per $t\ge t_0$
2. Integrare l'equazione differenziale dell'altezza a partire da $h(t_0)=h_0$ e quindi determinare $h(t)$ per $t\ge t_0$
3. Calcolare $q_o(t)=S_o\sqrt{2gh(t)}$ per $t\ge t_0$

---

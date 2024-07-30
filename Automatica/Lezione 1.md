---
tags:
  - automatica
created: 18-06-2024
---
# Sistema dinamico
Un sistema dinamico è la rappresentazione (astratta) di un dato fenomeno caratterizzato dalla presenza di segnali che variano nel tempo e che interagiscono reciprocamente. Dal punto di vista fisico: un sistema dinamico è una rappresentazione astratta di una relazione fisica di causa-effetto. Gli ingressi sono le cause, mentre le uscite sono l'effetto. Un segnale è la rappresentazione formale nel tempo di una grandezza fisica.
L'obiettivo sarà passare dalla narrazione del fenomeno alle equazioni che descrivono il sistema dinamico.
Ad esempio il fenomeno dell'emigrazione di una popolazione di individui contiene due segnali:
1. Italiani residenti in italia
2. Italiani residenti all'estero

Ogni anno una frazione di residenti in italia si trasferisce all'estero. Lo stato del sistema è la collezioni di variabili che descrive il fenomeno in maniera definitiva. Il dominio individua il tipo di sistema tra:
1. Sistema dinamico a tempo continuo, $T=R$ analizzo con "continuità" un dato fenomeno.
2. Sistema dinamico a tempo discreto, $T=Z$ analizzo un dato fenomeno co una "logica di campionamento".

Assieme alle variabili dipendenti possono essere presenti le variabili indipendenti. Dato sempre lo stesso contesto, il modello può essere rappresentato tramite nodi ed archi, dove i nodi sono le variabili dipendenti o di stato: ![[sisisolato.png|500x200]]
Il sistema d'esempio è un sistema isolato che rappresenta gli italiani residenti in Italia e gli italiani residenti al estero. Una variabile indipendente del sistema è il fenomeno dell'immigrazione. Le variabili indipendenti si rappresentano con un quadrato numerato. Siano:
- $\alpha_{12}$ è la percentuale di cittadini che vanno al estero
- $\alpha_{21}$ è la percentuale di cittadini che tornano in Italia
- $\beta_{11}$ è il coefficiente di amplificazione.

La rappresentazione del sistema è la seguente: ![[esempiovariabili.png|400x400]] descriviamo il sistema a tempo discreto:
- $x_1(k)$: italiani in Italia.
- $x_2(k)$: italiani all'estero.
- $u_1(k)$: immigrati di anno in anno.
- $\alpha_{12}$: frazione di italiani che emigra (da un anno al successivo).
- $\alpha_{21}$: frazione di emigrati che ritorna in Italia (da un anno al successivo).
- $\beta_{11}$: posto per il momento a 1.

$$
\begin{align}
x_1(k+1)-x_1(k)=-\alpha_{12}x_1(k)+\alpha_{21}x_2(k)+u_{1(k)}\\
x_2(k+1)-x_2(k)=\alpha_{12}x_1(k)-\alpha_{21}x_2(k)
\end{align}
$$
I segni sono dati da gli archi e dal loro segno, segno meno uscenti segno più entranti. $u_1(k)$ influenza sia $x_1(k)\text{ che} x_2(k)$ nel corso del tempo. In maniera compatta: 
$$
\begin{align}
x_1(k+1)=x_1(k)-\alpha_{12}x_1(k)+\alpha_{21}x_2(k)+u_{1(k)}\\
x_2(k+1)=x_2(k)+\alpha_{12}x_1(k)-\alpha_{21}x_2(k)
\end{align}
\implies
\begin{aligned}
x_1(k+1)=(1-\alpha_{12})x_1(k)+\alpha_{21}x_2(k)+u_{1(k)} \\
x_2(k+1)=(1-\alpha_{21})x_2(k)+\alpha_{12}x_1(k)
\end{aligned}
$$ 
da notare come i secondi membri del sistema sono combinazioni lineari.
Ricordando la definizione di stato si ha che: $$
\begin{bmatrix}
x_1(k)\\
x_2(k)
\end{bmatrix}\in N^2$$
vettore che appartiene a $N^2$ perché sono numeri finiti. Vado quindi a realizzare una mappa lineare o applicazione lineare. Una mappa lineare è rappresentata univocamente da una matrice.
Separando le variabili indipendenti da quelle dipendenti si ottengono si nota che si hanno 2 variabili quindi 2 colonne e 2 equazioni quindi 2 righe. La matrice che ne esce è la seguente:
$$
\begin{bmatrix}
(1-\alpha_{21}) & \alpha_{21} \\ \alpha_{12} & (1-\alpha_{21})
\end{bmatrix}
\begin{bmatrix}
x_1(k) \\ x_2(k)
\end{bmatrix}
$$
per quanto riguarda $u_1(k)$ nella prima equazione ha coefficiente 1 mentre nella seconda equazione non compare dunque ha coefficiente 0. Il sistema può essere quindi riscritto in forma matriciale come:
$$
\begin{bmatrix}
x_1(k+1) \\ x_2(k+1)
\end{bmatrix}=
\begin{bmatrix}
(1-\alpha_{21}) & \alpha_{21} \\ \alpha_{12} & (1-\alpha_{21})
\end{bmatrix}
\begin{bmatrix}
x_1(k) \\ x_2(k)
\end{bmatrix}
+
\begin{bmatrix}
1 \\ 0
\end{bmatrix}
u_1(k)
$$
dove $\begin{bmatrix}
(1-\alpha_{21}) & \alpha_{21} \\ \alpha_{12} & (1-\alpha_{21})
\end{bmatrix}=A \text{ e }\begin{bmatrix}
1 \\ 0
\end{bmatrix}=B$ 
Riscrivendo tutto si ha che: $x(k+1)=Ax(k)+Bu(k)$ ovvero <font color="#ff0000">l'equazione di stato</font>. Se il legame è lineare al interno del modello di decisione, genera questa rappresentazione dove A in genere è una matrice quadra, mentre B è una matrice rettangolare. Sono presenti anche le variabili osservabili che altro non sono che le misure, perché nei sistemi complessi gli stati non sono direttamente accessibili.
Supponendo di misurare istante per istante i cittadini italiani e gli immigrati, rappresento le variabili osservabili con $y$.





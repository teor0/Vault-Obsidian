---
tags:
  - elettrotecnica
created: 2024-04-09 16:32:27
updated: 2024-04-09 16:32:27
---
 # Concetti fisici d'interesse per l'elettrotecnica
 I fenomeni elettromagnetici sono descritti dalle equazioni di Maxwell, che legano tra loro le varie grandezze fisiche vettoriali e le proprietà dei materiali. Le grandezze fisiche utilizzate dalle equazioni sono:
 - $\underline{E}$ campo elettrico
 - $\underline{D}$ induzione elettrica
 - $\underline{H}$ campo magnetico
 - $\underline{B}$ induzione magnetica
 - $\underline{J}$ densità di corrente

mentre le proprietà dei materiali che interessano Maxwell sono: 
- $\varepsilon$ permettività dielettrica
- $\mu$ permeabilità magnetica
- $\sigma$ conducibilità elettrica
- $\rho$ densità spaziale di carica

Le equazioni di Maxwell possono essere espressa in forma integrale o in forma differenziale ed ognuna di esse esprime una legge. In particolare in forma integrale le equazioni sono le seguenti:
$$\begin{gather}
\oint \underline{E}\cdot d\underline{A}={Q\over\varepsilon_0} \\
\oint \underline{B}\cdot d\underline{A}=0 \\
\oint \underline{E}\cdot d\underline{l}=-{d\Phi_B\over dt} \\
\oint \underline{B}\cdot d\underline{l}=\mu_0(i_C+\varepsilon_0{d\Phi_E\over dt})
\end{gather}$$
nella forma differenziale invece 
$$\begin{gather}
\nabla\times \underline{E}=-{\partial B\over \partial t} \\
\nabla\times \underline{H}= J+{\partial D\over\partial t}\\
\nabla\cdot \underline{D}=\rho_{lib} \\
\nabla\cdot B=0
\end{gather}$$

La prima equazione è la legge di Gauss per il campo elettrico, la seconda equazione è la legge di Gauss per il campo magnetico, la terza equazione è la legge di Faraday sull'induzione elettromagnetica e la quarta equazione è la legge di Ampere con l'aggiunta della corrente di spostamento. 
La soluzione completa di un problema elettromagnetico richiederebbe la soluzione delle equazioni di Maxwell in un istante di tempo in tutto il volume di spazio di interesse. Nasce così il modello circuitale un modello che descrive con un elevata approssimazione il funzionamento di un circuito.

---
# Modello circuitale
L'approccio circuitale coniuga due processi fondamentali: 
1. La modellazione fisica di dispositivi elementari che compiono una determinata azione tramite opportune grandezze descrittive.
2. Lo studio delle relazioni che si instaurano tra le grandezze descrittive dei singoli componenti dovute alle connessioni dei componenti, ovvero le relazioni topologiche.


>[!definizione]
>Un circuito è composto da una serie di componenti (anche detti elementi, blocchi, dispositivi o bipoli) collegati tra loro attraverso dei collegamenti (morsetti, fili o conduttori). 

I circuiti che si tratteranno saranno considerati come circuiti ideali, ovvero senza perdite. 

>[!definizione]
>Un componente è un elemento circuitale caratterizzato da un particolare insieme di morsetti, e da un opportuno insieme di equazioni fra le variabili di interfaccia o relazioni costitutive, dipendenti da un numero finito di costanti numeriche.

>[!definizione]
Un collegamento è una linea orientata o non orientata che collega tra loro i morsetti dei componenti. Un collegamento impone omogeneità e continuità delle relazioni costitutive.

L'insieme dei collegamenti di un circuito è descritto da un grafo, che può essere orientato o non orientato.

>[!definizione]
>Le variabili d'interfaccia sono grandezze fisiche sottoposte sia alle equazioni di vincolo generate dai collegamenti, che alle equazioni dei componenti. Nel nostro caso le variabili d'interfaccia sono funzioni analogiche del tempo che riproducono l'andamento di grandezze nel mondo fisico.

Si tratterà la dipendenza delle variabili a tempo continuo.

>[!definizione]
>Una relazione costitutiva è il comportamento rispetto a tensione e corrente che un componente assume.

## Classi di circuiti 
I circuiti si differenziano in: 
- <font color=blue> circuiti a costanti concentrate</font> dove tutte le tensioni e le correnti sono funzioni solamente del tempo.
- <font color=blue> circuiti a costanti distribuite</font> dove tutte le tensioni e le correnti sono funzioni del tempo e dello spazio.

Si tratteranno solo i circuiti a costanti concentrate, ma per farlo occorre imporre delle limitazioni e delle ipotesi. Si impongono limitazioni su:
- frequenze di lavoro ovvero i campi variano lentamente e ciò implica che la corrente di spostamento sia nulla e dunque che non si generano onde elettromagnetiche.
- natura dei componenti

Si ipotizza che:
- le dimensioni geometriche della struttura sede del fenomeno elettromagnetico siano sufficientemente piccole da essere trascurabili per consentire un approccio topologico.
- la velocità di propagazione del fenomeno elettromagnetico può considerarsi infinita in modo da Individuare le regioni tipiche dove è presente solo un fenomeno.
- il tempo di trasmissione del fenomeno elettromagnetico all'interno della struttura è nullo per cui le grandezze dipendono solo dal tempo, ossia circuiti a costanti concentrate.

Da notare che se la lunghezza d'onda è molto più grande della dimensione del componente non si ha variazione nello spazio del campo elettrico. Piccola dimostrazione: Ipotizziamo di avere 2 porte il cui potenziale è pari a $V=5 V$, poste a $d=2 km$ di distanza. Ipotizziamo adesso che la corrente abbia una frequenza di 50 Hz, dunque la lunghezza d'onda sarà pari a $\lambda={c\over f}={300\cdot10^8\over 50}=6\cdot10^5 km$ dunque $\lambda>>d$

---
# Corrente, tensione, potenza ed energia
La corrente elettrica è la velocità di variazione nel tempo della carica. Anche se è una grandezza scalare, andremo ad indicare il verso di percorrenza all'interno dei circuiti generalmente dal + della tensione al -. La corrente si differenzia in: 
- <font color=blue>Corrente continua</font> DC (direct current). Essendo costante la corrente si ha che $q=\int_0^t i(t)dt=i(t)\int_0^t dt=i(t)t$
- <font color=purple>Corrente alternata</font> AC (alternate current) 

Le cariche che fluiscono hanno energia potenziale che si trasformerà in lavoro.

La tensione detta anche differenza di potenziale, è il lavoro necessario che il campo elettrico deve compiere per spostare, la carica unitaria dal punto A al punto B. La caduta di tensione tra A e B è equivalente ad un aumento di tensione tra B e A $V_{AB}=-V_{BA}$ ![[tensione.jpg|250x250]]
La potenza è la variazione di energia nel tempo o anche, la velocità di assorbimento/emissione di energia nel tempo. In un sistema isolato si ha che $\sum_i^n P_i=0$ La potenza è definita come $P={dW\over dt}={dW\over dq}\cdot{dq\over dt}=v\cdot i$

L'energia assorbita/erogata in un intervallo di tempo si calcola $W=\int_0^tPdt=\int_0^tvidt$

Le tensioni variano ai capi dei componenti, mentre le correnti variano al presentarsi di più componenti in un circuito.

---
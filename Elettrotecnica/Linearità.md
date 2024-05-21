---
tags: elettrotecnica, 
created: 2024-04-20 11:18:54
updated: 2024-04-20 11:18:54
---
[[Incongruenze mezzi ideali, generatori reali, corrente e potenza massima e rendimento]]
# Linearità, tempo invarianza, memoria e casualità

Un sistema è lineare se gode contemporaneamente di omogeneità ed additività.
- Omogeneità: se l'ingresso $x(t)$ viene moltiplicato per un fattore costante, l'uscita $y(t)$ risulta moltiplicata per lo stesso fattore. $L(x(t))=y(t); L(kx(t))=ky(t)$
- Additività: la risposta alle somme di più ingressi è pari alla somma delle risposte agli ingressi applicati separatamente. $L(x_1(t))=y_1(t); L(x_2(t))=y_2(t); L(\alpha x_1(t)+\beta x_2(t))=\alpha y_1(t)+\beta y_2(t)$

Un sistema lineare è descritto da un sistema di equazione differenziali lineari. Un circuito costituito da elementi lineari e generatori indipendenti è lineare perché le loro relazioni costitutive sono operatori lineari.

>[!definizione]
Un sistema è tempo invariante quando la relazione causa-effetto non varia nel tempo. $L(x(t))=y(t); L(x(t-t_0))=y(t-t_0)$

>[!definizione]
>Un sistema è con memoria quando l'uscita ad un generico istante $t$ dipende non solo dall'ingresso all'istante $t$ ma anche ad istanti precedenti o successivi. $y(t)=arctan(x(t))$ senza memoria
>$y(t)=x(-t)$ con memoria

>[!definizione]
>Un sistema con memoria è causale quando l'uscita dipende solo dall'ingresso a quell'istante di tempo o ad istanti precedenti. 
>$y(t)=x(-t)$ non causale
>$\displaystyle y(t)=\int^{t}_{-\infty}x(\tau)d\tau$ causale

La resistenza è lineare senza memoria. Il condensatore come l'induttore ha memoria. La potenza non è lineare!

---
# Sovrapposizione degli effetti, equazione di porta e teorema di sostituzione
>[!definizione]
>Il principio di sovrapposizione degli effetti, afferma che l'effetto dovuto all'azione di più cause concomitanti, è pari alla somma degli effetti che si ottengono quando ciascuna causa agisce da sola. 

Il principio vale per i sistemi lineari, dunque non può essere applicata al calcolo della potenza su un elemento. Per applicare il principio di sovrapposizione degli effetti occorre:
1. Spegnere tutti i generatori tranne uno, sostituendo generatore di tensione con cortocircuiti e generatori di correnti con circuiti aperti.
2. Calcolare il valore dell'uscita dovuto all'unico generatore rimasto.
3. Ripetere per tutti i generatori.
4. Sommare i valori delle uscite.

Definiamo ora l'equazione di porta, utile per dimostrare i teoremi delle reti.
>[!definizione]
>Consideriamo una parte di circuito accessibile da una porta composta dai terminali A-B. La tensione $V_{AB}(t)$ e la corrente $i_{AB}(t)$ sono vincolati a soddisfare una relazione del tipo $f(V_{AB}(t),i_{AB}(t))=\text{effetto dei generatori}$

Per circuiti resistivi lineari abbiamo 2 casi:
1. Assenza di generatori: $\alpha V_{AB}(t)+\beta i_{AB}(t)=0\implies V_{AB}=R_{AB}i_{AB}; i_{AB}=G_{AB}V_{AB}$
2. Presenza di generatori: $\alpha V_{AB}(t)+\beta i_{AB}(t)=\gamma\in R$

L'equazione di porta individua una curva nel piano tensione-corrente che è il luogo di punti dove giacciono tutti valori che possono essere assunti dalle grandezze e per circuiti resistivi lineari, questa curva è una retta detta <font color=red>retta di carico</font>.
$\displaystyle\alpha V_{AB}(t)+\beta i_{AB}(t)=\gamma \implies \alpha V_{AB}(t)=-{\beta\over\alpha} i_{AB}(t)+{\gamma\over\alpha}$
![[rettacarico.jpg]]

Infine abbiamo il <font color=purple>teorema di sostituzione</font>, che afferma che:
>[!definizione]
>Una parte di circuito accessibile da una porta composta dai terminali A-B, può essere sostituita da un generatore di tensione che assicura la tensione di porta o da un generatore di corrente che imprime la corrente di porta, senza alterare le grandezze elettriche nella parte del circuito esterna alla porta.

Il seguente circuito ![[sostporta.jpg|800x150]] si sostituisce con ad esempio un generatore reale di corrente ![[sostituzione.jpg|500x300]] Facile dimostrazione del problema: 
Le grandezze di porta $V_{AB}(t), i_{AB}(t)$ sono vincolate dall'equazione di porta. Se fisso il valore di una delle due grandezze alla porta, automaticamente l'altra è vincolata!

---

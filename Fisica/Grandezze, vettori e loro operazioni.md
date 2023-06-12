---
tags: #fisica 
---
#fisica
# Le grandezze fisiche e l'analisi dimensionale
All'interno del corso verranno utilizzate diverse grandezze fisiche, ma che cosa sono e cose le rende tali, per esempio, cos'è il tempo? Il tempo è quella grandezza fisica che si misura con l'orologio. L'insieme delle operazioni che si fanno per associare un numero ad una grandezza fisica viene chiamato misurazione. Essa rende possibile e non ambiguo ogni giudizio di uguaglianze o disuguaglianza fra due grandezze della stessa specie.
I procedimenti che si utilizzano nella misurazione devono garantire che il numero, la misura della grandezza, sia stato ottenuto in modo non ambiguo e riproducibile, inoltre devono garantire la sua invariabilità nel tempo, cioè a prescindere dalle condizioni ambientali e dal trascorrere del tempo la misura resta uguale. Le grandezze fisiche sono di 2 tipi:
1. Fondamentali
2. Derivate

Le 7 grandezze fondamentali del sistema internazionale sono:
![[tab.jpg|300x300]]
Alcune definizioni:

- Metro: è la distanza percorsa dalla luce nel vuoto in un intervallo temporale di $\large1\over299792458$ secondi
- Secondo: è l'intervallo di tempo corrispondente a 9192631770 periodi della radiazione emessa nella transizione tra 2 particolari livelli di Cesio 123

Tutte le altre grandezze possono essere espresse tramite una relazione funzionale con le grandezze fondamentali e risultano quindi derivate. Ovviamente per esprimere grandi quantità si utilizza la notazione scientifica:
![[tab2.jpg|500x700]]
A ogni grandezza misurata o calcolata si associa una dimensione. In meccanica le grandezze quali: massa, lunghezza e tempo servono come dimensioni fondamentali, cioè ogni grandezza fisica può essere espressa tramite equazioni dimensionali di esse. Ogni equazione deve possedere coerenza dimensionale vale a dire che i membri dell'equazione devono avere la stessa dimensione. Perciò si parla di analisi dimensionale, che può essere talvolta di aiuto per evitare di fare errori durante i calcoli. Alcune grandezze non hanno dimensione, ad esempio i gradi sessagesimali o i radianti. Anche alcune funzioni non hanno dimensioni( esponenziali, logaritmiche e trigonometriche). Le grandezze fisiche omogenee possono essere sommate, mentre le grandezze fisiche non omogenee no. Vediamo due esempi:

1. Il volume V è espresso tramite $m^3$ quindi ha dimensione $[L^3]$.
2. Un angolo $\alpha$ di una circonferenza è dato da, s l'arco creato ed il raggio r. $\alpha=\large{s\over r}$ ovvero $[L]\over[L]$= $[L^0]$.

# Vettori e versori

Le grandezze fisiche fondamentali sono anche dette grandezze scalari, perché espresse solamente tramite valore numerico con segno. Le grandezze fisiche derivate come velocità e forza vanno espresse anche come direzione e verso. Queste grandezze vengono dette grandezze vettoriali.

Le 3 caratteristiche delle grandezze vettoriali e quindi dei vettori sono:

- Modulo: che indica l'intensità ossia il valore numerico.
- Direzione: che indica la retta di appartenenza.
- Verso: dove punta il vettore lungo la direzione.

![[dir.jpg]]

Il punto di partenza specifica il punto di applicazione del vettore, una volta specificato il punto di applicazione resta individuata un'unica freccia ed il vettore corrispondente è detto vettore applicato. Un vettore viene identificato da una lettera con una freccia sopra ed il suo modulo viene espresso tramite valore assoluto. Esempio: |$\overrightarrow{a}$|=3.

Due vettori si dicono uguali quando hanno stesso modulo, verso e direzione. Due vettori si dicono opposti quando hanno stesso modulo e direzione ma verso opposto.
![[vettuop.jpg|400x600]]
## Operazioni tra vettori

La somma tra due vettori A e B si effettua mettendo la coda di un vettore sulla testa dell'altro in base a come si è scritta. Il vettore risultato della somma prende il nome di risultante ed ha la coda sulla coda del primo vettore e testa sulla testa del secondo vettore. La somma gode di proprietà associativa e commuttativa.

![[sum.jpg]]

Un altro metodo è quello del parallelogramma visualizzato come segue:

![[para.jpg]]

La differenza tra due vettori si effettua tramite la somma di un vettore A con l'opposto del vettore B. La coda del risultante parte dalla testa di B e termina in A, anche per la differenza esiste il metodo del parallelogramma.

![[dif.jpg]]

Si può moltiplicare o dividere il modulo di un vettore per un numero ma in particolare si può avere un prodotto scalare ed un prodotto vettoriale.

Per prodotto scalare si intende, il prodotto tra 2 vettori U e V che si ottiene moltiplicando il modulo del primo per la proiezione del secondo sul primo.
![[scal.jpg]]

La formula generale è $\overrightarrow{u}*\overrightarrow{v}=|\overrightarrow{u}|*|\overrightarrow{v}|*cos(\theta)$ quindi si verificano 3 casi particolari:

- se i vettori sono paralleli e di verso concorde il prodotto scalare è massimo ed è uguale al prodotto tra i moduli di u e v.
- se i vettori sono paralleli e di verso opposto il prodotto scalare è minimo ed è uguale al prodotto tra i moduli di u e v con il segno meno.
- se i vettori sono perpendicolari il risultato è nullo.

![[casi.jpg]]

Dati due vettori u e v si definisce il prodotto vettoriale $\overrightarrow{u}$x$\overrightarrow{v}$ il vettore ad essi perpendicolare, il cui modulo è dato dall'area del parallelogramma costruito su u e v il cui verso è dato dalla regola della mano destra. Esempio visivo:

![[vett.jpg]]

 Il modulo del vettore risultante è dato da $|\overrightarrow{u}$x$\overrightarrow{v}|$=$|\overrightarrow{u}|*|\overrightarrow{v}|*sen(\theta)$.

Un vettore può essere scomposto nelle sue componenti, che siano tridimensionali o bidimensionali tramite il piano cartesiano.

![[comp.jpg]]

In formule per 3 dimensioni:

- $v_x=|v|*sen\theta * cos\varphi$
- $v_y=|v|*sen\theta * sen\varphi$
- $v_z=|v|*cos\theta$

In formule per 2 dimensioni:

- $v_x=|v|*cos\theta$
- $v_y=|v|*sen\theta$
- $\displaystyle tan(\theta)={{v_y}\over{v_x}}$

![[FPics/esempio.jpg]]

---
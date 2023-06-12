[[Forza elastica, pendolo semplice e tensione dei fili]]
#fisica 
# Sistemi di riferimento

È provato sperimentalmente che le leggi fisiche non dipendono dalla scelta del sistema di riferimento. Fissato un sistema di riferimento e stabilita una certa proprietà, questa resta vera anche se cambiamo l'origine e l'orientazione degli assi. Ovvero se ci riferiamo ad un altro sistema ottenuto dal primo con un traslazione (spostamento dell'origine, conservando la stessa direzione degli assi) o con una rotazione (stesso origine, ma cambio della direzione degli assi) o con una operazione combinata.

![[FPics/Sistemi di riferimento e velocità ed accelerazion/unknown.jpg]]

Nella figura riportata è rappresentato un punto P in movimento su una traiettoria generica. Il suo moto è osservato da un sistema di riferimento con origine O, che chiamiamo sistema fisso e da un sistema di riferimento con origine O', che chiamiamo sistema mobile. La relazione tra le posizioni del punto P, misurate rispetto ai 2 sistemi di riferimento è la seguente:

$\large r=OO'+r'$

## Velocità relativa

La velocità dell'origine O' del sistema di riferimento mobile misurata da un osservatore nel sistema fisso è data da:

$\large v_{O'}={dOO'\over dt}={dx_{O'}\over dt}u_x+{dy_{O'}\over dt}u_y+{dz_{O'}\over dt}u_z$

calcolando bene le derivate alla fine si ottiene che:

$\displaystyle\large v=v_{O'}+v'+\omega\times r'$

## Accelerazione relativa

Consideriamo ora la relazione tra le accelerazioni del punto P misurate ai 2 sistemi di riferiemento. Pertanto abbiamo che l'accelerazione dell'origine del sistema mobile O' rispetto ad O è data da:

$\displaystyle a_{O'}={dv_{O'}\over dt}$

derivando per bene si ottiene:

$\displaystyle a={dv\over dt}={dv_{O'}\over dt}+{dv'\over dt}+{d\omega\over dt}\times r'+\omega\times {dr'\over dt}$

Calcolando bene la derivata di $\displaystyle {dv'\over dt}$ otteniamo infine:

$\displaystyle a=a'+a_{O'}+\omega\times(\omega\times r')+{d\omega\over dt}\times r'+2\omega\times v'$

---
# Sistemi di riferimento inerziali

Definiamo come sistema di riferimento inerziale un sistema in cui valga la legge d'inerzia, cioè un punto non soggetto a forze rimane in stato di quiete o di moto rettilineo uniforme. È evidente che la definizione di sistema di riferimento inerziale ha significato solo se siamo in grado di verificare che sul punto non agiscano forze. Perciò è ragionevole supporre che ciò si verifichi se, il punto è sufficientemente lontano da ogni altro corpo in modo da poter trascurare ogni interazione oppure, se la risultante delle forze agenti sul corpo sia nulla.

In un sistema di riferimento inerziale, la legge di Newton ha l'espressione più semplice. Consideriamo ora un altro sistema di riferimento che si muove di moto rettilineo traslatorio uniforme, rispetto ad un certo sistema inerziale. Pertanto si ha:

$v_{O'}=costante$    $a_{O'}=0$  $\omega=0$

Attraverso l'accelerazione relativa ottieniamo $\large a=a'$, quindi le accelerazioni di un punto misurate nei 2 sistemi di riferimento sono uguali. Se a=0 anche a'=0 e quindi pure il secondo sistema è inerziale.

> Definito un sistema di riferimento inerziale, tutti gli altri sistemi in moto rettilineo uniforme rispetto ad esso sono anch'essi inerziali

## Forze d'inerzia e sistemi di riferimento non inerziali

Se il moto del secondo sistema è accelerato rispetto al sistema inerziale, sia perché $a_{O'}\ne 0$ oppure $\omega\ne 0$ o per entrambe, si nota che la legge di Newton non è più valida. Infatti se F=ma nel sistema inerziale, nell'altro sistema in moto accelerato non può essere $F=ma'$ dato che $a'\ne a$.

Se tuttavia moltiplichiamo i termini dell'accelerazione relativa per la massa del punto e teniamo conto che $F=ma$ abbiamo che:

$F-ma_t-ma_c=ma'$

dove $a_t$ è l'accelerazione di trascinamento e $a_c$ è l'accelerazione di Coriolis. La formula rappresenta una forma modificata dalla legge di Newton: in un sistema non inerziale il prodotto della massa del punto materiale per l’accelerazione misurata in quel sistema è eguale alla forza vera agente sul punto più le forze apparenti. Queste ultime, che sono sempre proporzionali alla massa del punto e vengono chiamate forze d'inerzia.

> È chiaro che le forze apparenti non derivano dalle interazioni fondamentali e non esistono in un sistema di riferimento inerziale.

In un sistema accelerato dove F=0 non comporta che $a'=0$ e quindi un moto rettilineo uniforme. Questo risultato giustifica il nome di sistema di riferimento non inerziale per un sistema accelerato.

>Una forza apparente è sempre contraria al verso del moto.

---
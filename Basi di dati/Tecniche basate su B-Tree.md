---
tag: #basi 
created: 2023-01-11 18:37:41
updated: 2023-01-11 18:37:41
---
#basi 
[[Tecniche di hashing dinamico e difetti dell'hashing]]
# Differenze tra tecniche basate su B-Tree e tecniche basate su hashing
Un B-Tree è una struttura ad albero che generalizza l'albero di ricerca, perché pensato per lavorare in memoria secondaria per essere durabile. Quindi sia il B-Tree che i dati vengono mantenuti in memoria secondaria. A differenza dell'hashing che è una tecnica di <font color=orange>indicizzazione procedurale</font>, in quanto basta memorizzarsi una procedura per indicizzare i dati la tecnica basata su B-Tree è una tecnica <font color=orange>tabellare</font> cioè l'indice verso i dati è come una tabella, quindi come le tabelle sono rappresentate in memoria secondaria anche l'indice B-Tree è rappresentato in memoria secondaria. Come tale si crea il problema di organizzarlo in maniera propria. I B-Tree che studiamo sono sistemi di indicizzazione che generalizzano gli alberi e sono adatti a gestire il bilanciamento in memoria secondaria. Anche se nel caso peggiore hanno prestazioni logaritmiche rispetto al numero di pagine, nella pratica le strutture B-Tree sono costanti.

Nella gran parte dei casi l'albero è fatto in modo che solo l'ultimo livello stia in memoria secondaria e la maggior parte di esso è in memoria principale. Con questa tecnica presa una chiave, si accede prima ad una pagina dell'indice e poi alla pagine dov'è la tupla, qui l'area dati e l'area indice sono separate quindi posso ordinare le tuple come voglio e costruire alberi sopra. In un B-Tree ogni nodo è una pagina ed ogni pagina punta a tuple in modo ordinato. Ogni nodo ha la forma seguente:
![[struttpagbtree.jpg]]
La parte superiore contiene i valori della chiave di ricerca, la parte inferiore contiene il puntatore all'area dati che contiene la tupla con chiave espressa nella chiave superiore. Le barrette laterali contengono puntatori a nodi figli, a sinistra c'è un sottoalbero con chiavi di valore minore mentre a destra c'è un sottoalbero con chiavi di valore maggiore. Non tutte le caselle sono riempite. I nodi foglia non hanno figli come in un tipico albero, quindi le loro barre laterali punteranno al nulla. Quest'albero è detto n-ario, cioè ogni nodo può avere più figli. 

>Date x chiavi si avranno x+1 figli.

Da notare che per dei nodi non terminali un sottoalbero è figlio destro di un nodo e figlio sinistro di un altro. Un B-Tree di grado 4 ha nodi che contengono 3 chiavi. Il grado di un B-Tree è dato dal numero di figli che si possono avere oppure il numero massimo di figli in un nodo. Il grado di un B-Tree si sceglie a priori e dipende da quanto è grande la chiave e quanto è grande la pagina. Solitamente i puntatori sono da 32/64 bit. le chiavi sono grandi rispetto l'attributo al quale creo il B-Tree. Ogni nodo, che corrisponde ad una pagina determina la dimensione totale che le chiavi ed i puntatori devono avere. Ad esempio se la pagina è 4KB, bisogna determinare il grado del B-Tree sulla base di quante chiavi e puntatori si possono mettere per arrivare a 4KB.
Nota la dimensione della pagina e la dimensione dei puntatori che dipendono dal sistema, presa una chiave di ricerca si può stabilire il numero di caselle massime per pagina. Questo numero è il grado.

La ricerca avviene come in un albero normale, accedendo ad ogni passo ad un nodo del livello corrente. Un B-Tree è messo di default sulla chiave primaria perchè coinvolta con i vincoli di chiavi esterne. Il costo d'accesso di un B-Tree nel caso peggiore è pari all'altezza del B-Tree. Il B-Tree ha garantito un bilanciamento molto forte ossia, tutte le foglie stanno alla stessa altezza, questo fa si che l'altezza diventi logaritmica rispetto al grado del B-Tree ed essendo di solito la base del logaritmo molto larga questo fa si che i B-Tree abbiano un altezza molto bassa.

Nel B-Tree bisogna stare attenti ad avere nodi sufficientemente pieni, evitando quindi una struttura sparsa che ha prestazioni scadenti.

---
## Proprietà di un B-Tree di grado m
- Ogni nodo ha la struttura [[struttpagbtree.jpg|descritta in precedenza]] dove i nodi $K_1,...K_m$ sono ordinati ed il sottoalbero puntato da $p_i$, contiene chiavi di $K_i+1$ se $i\gt 1$ e minori di $K_i$ se $i\lt m$
- Se un nodo ha x chiavi e non è foglia allora ha x+1 figli.
- Se un nodo ha x figli ha x-1 chiavi
- Tutte le foglie sono alla stessa altezza
- Ogni nodo non radice possiede almeno $\lceil{m\over2}\rceil -1$ chiavi, ossia 50%. Questa proprietà è una proprietà minima, nella pratica si raggiunge una percentuale di riempimento anche del 80%.

>Un B-Tree è molto efficiente se garantisce le proprietà elencate.

---
# Inserimento e rimozione in un B-Tree
Vediamo adesso la logica dietro l'inserimento in un B-Tree.
![[insbtree.jpg]]
Quando voglio inserire 30, il nodo risulta pieno perciò si spezza la radice e si creano nodi pieni secondo la proprietà di riempimento ossia $\lceil{m\over2}\rceil -1$. Ogni inserimento quindi si fa nell'ultimo livello, l'albero perciò cresce verso l'alto non verso il basso come accadeva per gli alberi binari. Ogni volta che si deve inserire un valore bisogna scandire dalla radice alla foglia, quindi si fanno $h$ accessi con $h$ altezza del B-Tree. Nel caso peggiore si deve splittare una foglia quindi il costo è di $h$ letture e $2h+1$ scritture. Il numero di nodi foglia, in B-Tree di grado m è dato da: $\displaystyle 1+m+m^2+m^3+...+m^{h-2}+m^{h-1}={m^{h-1}-1\over{m-1}}$ se B-Tree è pieno, dove $m-1$ sono i nodi prima dell'ultimo livello e,  $m^{h-1}$ è il numero di nodi all'ultimo livello. Di queste $2h+1$ scritture in memoria secondaria ne faccio solo 2 e delle $h$ letture ne faccio solo 1.

>Se il grado è 100, i nodi all'ultimo livello sono 100 volte di più di quelli di tutto il resto dell'albero. 

La rimozione deve sempre garantire le proprietà. Nel rimuovere un nodo possiamo ricondurci al caso in cui il nodo sia nella foglia spostando, il nodo alla foglia più a destra del sottoalbero sinistro. ![[rimbtree.jpg]] supponiamo di trovarci in questa situazione e di voler rimuovere 20. Adesso il nodo che lo conteneva è sceso sotto la soglia di riempimento minimo, a questo punto prendo tutti i valori dell'insieme non riempito al minimo, in questo caso solo 10, il valore del nodo padre, 30 in questo caso e i valori del sottoalbero destro/sinistro, 40, 50 e 60 in questo caso. Faccio così una rotazione a seconda del caso e verifico che la condizione di riempimento minimo sia mantenuta. Supponiamo poi di voler rimuovere il valore 30, fatte tutte le operazioni necessari si avrà come situazione finale la seguente:
![[finerimbtree.jpg]]
Il costo della rimozione di una foglia con un albero con altezza $h$ è definito in 2 casi:
1. La chiave da eliminare non rende necessario né una rotazione né un accorpamento quindi il costo è dato da $h$ letture, in quanto scendo fino alle foglie per trovare la chiave da eliminare ed 1 scrittura, che sarebbe la cancellazione.
2. Il caso peggiore è quando dal figlio della radice in giù, è richiesto un accorpamento ed una volta ritornati al figlio della radice bisogna fare una rotazione. Il tutto costa $2h-1$ letture e $h-1$ scritture.

---
# Dimostrare altezza logaritmica
Supponiamo di avere un B-Tree di grado m ed altezza h. Se ho riempimento massimo, ovvero tutti i nodi hanno m figli, l'albero è composto da: $P_{max}=\displaystyle 1+m+m^2+m^3+...+m^{h-2}+m^{h-1}={m^{h-1}-1\over{m-1}}$

Il numero massimo di tuple che posso indicizzare è dato da: $N_{max}=(m-1)\times\ P_{max}=m^h-1$.

Se ho riempimento minimo invece, l'albero è composto da: $\displaystyle P_{min}=1+2+2\lceil{m\over2}\rceil+2{\lceil{m\over2}\rceil}^2+...+2{\lceil{m\over2}\rceil}^{h-2}=$
$\displaystyle 1+2(1+\lceil{m\over2}\rceil+{\lceil{m\over2}\rceil}^2+...+{\lceil{m\over2}\rceil}^{h-2})$=
$\displaystyle\large 1+2({{\lceil{m\over2}\rceil}^{h-1}-1\over  {\lceil{m\over2}\rceil}-1})$

Il numero minimo di tuple che posso indicizzare è dato da: $\displaystyle N_{min}=1+(P_{min}-1)(\lceil{m\over2}\rceil-1)=1+2{\lceil{m\over2}\rceil}^{h-1}-2=2{\lceil{m\over2}\rceil}^{h-1}-1$

Il riempimento massimo ci da un lower bound per h, quello minimo ci da un upper bound, quindi avremo che: $N\le m^h-1\implies h\ge log_m(N+1)$ e $\displaystyle {N\ge 2{\lceil{m\over2}\rceil}^{h-1}-1\implies h-1\le log_{\lceil{m\over2}\rceil}({N+1\over 2})\implies h\le 1+log_{\lceil{m\over2}\rceil}({N+1\over 2})}$

$m\over 2$ è sempre un numero abbastanza grande tale che anche nel caso peggiore l'altezza del B-Tree è piccola perché la base del logaritmo è sempre un numero grande!

---

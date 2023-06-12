---
tag: #basi 
created: 2023-01-10 17:52:10
updated: 2023-01-10 17:52:10
---
#basi 
[[Sistemi di indicizzazione e tecniche di hashing statico]]
# Tecniche di hashing dinamico
Nell'hashing statico l'area primaria non cambia, cioè le pagine allocate per le tuple restano le stesse. Riempire l'area primaria rende inefficiente l'hashing, portando ad avere un'area secondaria più grande e quindi una gestione quasi seriale. Se si hanno tante pagine vuote si ha uno spreco di tempo in quanto le tuple non essendo ammassate, fanno perdere tempo nell'iterazione.

> Questo accade quando si fa una ricerca non sulla chiave K ma su un altro attributo.

Nelle tecniche di hashing dinamico il numero di pagine M è variabile a differenze delle tecniche di hashing statico. Questo porta molti vantaggi ed aumento dell'efficienza.

---
# Hashing virtuale
La prima tecnica che studieremo è l'hashing virtuale, una tecnica teorica utile a capire quelle utilizzate. Ogni volta che si ha un trabocco si allarga l'area primaria. In corrispondenza al vettore delle pagine creo un vettore di bit B, che valgono 0-1 a seconda che esista almeno un tupla nella pagina. A questo punto utilizzo la funzione di hashing $H_0(K)=K\ mod\ M$. Ad ogni trabocco raddoppio le pagine, utilizzo una nuova funzione di hashing del tipo $H_1(K)=K\ mod\ 2M$ e ridistribuisco le tuple all'interno della pagina traboccata, sperando che le tuple finiscano in pagine diversa da quella traboccata.

Il valore restituito dal resto è tra 0 e 2M-1. Se io ho $i$ trabocchi avrò $2^i\times M$ pagine e funzione  $H_i(K)=K\ mod\ 2^iM$.

Il vettore di bit serve per le ricerche. Supponiamo di cercare la tupla 10, seguendo  $H_1(K)=K\ mod\ 2M$, si trova la pagina 4. Nella pagina 4 la tupla 10, non c'è anche perché il bit della pagina 4 è pari a 0 questo vuol dire che la tupla 10 o non esiste, oppure è stata inserita prima del raddoppio. Uso quindi la funzione di hashing precedente  $H_0(K)=K\ mod\ M$ e trovo bit pari a 1 e controllo se c'è il 10. Quindi per le ricerche si parte dall'ultima funzione hash usata, andando a ritroso fino alla funzione hash $i$ oppure fino alla funzion $H_0(K)$ per verificare la presenza della tupla.

Il vettore di bit può essere rappresentato in memoria principale con un numero intero. Presa ad esempio la pagina 420, verifico che B(420) è pari a 1 in RAM e se si accedo al disco. Essendo operazioni in RAM il loro costo è pari a 0, quindi il costo della ricerca è pari ad 1 accesso solo sul disco. Il costo dell'inserimento quando non c'è un trabocco costa 2 accessi, uno per trovare la posizione ed 1 per scrivere la tupla, con trabocco si allocano pagine nuove e si ristribuisce la pagina quindi faccio 3 accessi al disco.

>Legge che regola il funzionamento dei moduli:
>$K\ mod\ 2M= \begin{cases} 
K\ mod\ M=0, \\
(K\ mod\ M)+M
\end{cases}$

>[!regola]
>Le funzioni di ricerca ed inserimento devono essere accoppiate altrimenti non funziona l'hashing virtuale!

Se dovessi invece aumentare non a $2\times M$, ma a M+1 dovrei ridistribuire tutte le pagine e non solo quella dove accade il trabocco, inoltre la ricerca sarebbe peggiore. Il raddoppiare le pagine è il motivo per cui si chiama hashing virtuale, in quanto il raddoppio non è sostenibile, infatti 20 trabocchi portano ad avere $2^{20}$ pagine sparsissime e questo non va bene. Una soluzione a ciò è l'hashing lineare che ha crescita lineare e non esponenziale.

---
# Tecnica di hashing lineare a crescita lineare
L'idea è di tenere traccia dell'indice $p$ della pagina non ancora ridistribuita più a sinistra. 
Supponiamo di essere nella situazione seguente: ![[esHashvirt.jpg]] e di voler inserire la tupla 11. 
Data la funzione $H_0(K)=K\ mod\ M$ ho che il è pari a 2, ma la pagina 2 è piena quindi si verifica il primo trabocco. La pagina non è puntata da $p$ quindi creo una lista di trabocco dove metto la tupla traboccata, dopodiché aggiorno la funzione di hash a $H_1(K)=K\ mod\ 2M$ ed aggiungo una pagina. Infine prendo la pagina puntata da $p$ la ridistribuisco secondo la nuova funzione di hash ed aumento il valore di $p$. Nel caso in cui la pagina che trabocca è puntata da $p$ aggiungo subito una pagina e ridistribuisco la pagina che trabocca secondo la funzione hash $H_1(K)$ ed aumento il valore di $p$.

>Il resto può avere o il valore di prima oppure il valore di prima più M. Cosa succede se la pagina di reindirizzamento non esiste? Non può succedere, perché ridistribuiamo la pagina più a sinistra puntata da $p$ e questa pagina restituisce l'indirizzo vecchio oppure, quello della pagina appena creata e non può dare altri valori, perché è una proprietà dell'algebra modulare. 

Quando si cerca un valore si usa la funzione attuale assieme al valore $p+M-1$ da confrontare con il resto dato dalla funzione di hashing. Supponiamo di cercare la tupla 4, il risultato della funzione hash è 4 (in quanto 4 mod 6 fa 4), ma la pagina 4 non esiste e questo significa che non è stata ancora ridistribuita la pagina corrispondente alla pagina 4. Passo quindi alla funzione hash precedente.
Quando accede un trabocco su una pagina non puntata da $p$, se la pagina puntata da $p$ ha una lista di trabocco allora nella ridistribuzione anch'essa verrà contata.
Perciò le liste di trabocco hanno vita breve, in particolare se avvengono molti trabocchi le liste di trabocco verranno cancellate dopo poco tempo e se non ci sono molti trabocchi, allora le prestazioni non calano. 

>Quando $p$=M, la struttura si resetta quindi M=2M, $p$=0 e si passa a $H_0(K)=K\ mod\ M$. Ogni M trabocchi raddoppio l'argomento per questo si ha crescita lineare e non esponenziale.

---
# Hashing estendibile
Questa tecnica non usa l'algebra modulare, prende la chiave K ed usa la codifica binaria. Quindi distribuisce la tuple sulla base della codifica binaria della loro chiave. Per chiave non si intende la chiave primaria ma la chiave di ricerca. Ogni pagina è associata ad un numero $p'$ che è pari al numero di trabocchi che ne ha determinato l'esistenza,tramite $p$ tengono traccia del numero di trabocchi totali.
All'inizio ho una pagina ed un vettore chiamato indice. L'indice dice dove sono le tuple che hanno la caratteristica della celletta, ossia di avere gli ultimi $x$ bit pari a quelli specificati. All'inizio $x=0$, perciò tutte le tuple finiscono nella prima pagina.

Supponendo di avere pagine che con dimensione pari a 2 tuple, dopo aver memorizzato la tupla 1 e 2, quando arriva la tupla 3 avviene un trabocco ed aggiorno $p$. A questo punto spezzo in due la prima pagina per ottenerne 2. Le pagine avranno come valore di $p'$, il valore non più 0 ma quello precedente aumentato di 1. Infine raddoppio l'indice per distinguere le tuple dove la chiave termina con bit 0 e dove termina con bit 1.
Dopo tutto questo, ridistribuisco le tuple della pagina che ha traboccato assieme alla tupla che ha generato il trabocco, secondo l'indice quindi ultimo bit 0 ed ultimo bit 1.
Supponiamo di trovarci nella seguente situazione: ![[eshashest.jpg]] e di voler aggiungere la tupla 5. In questo caso si crea un trabocco, perciò andrò a spezzare a metà la pagina traboccata aggiornerò il loro $p'$ e raddoppierò l'indice. In sostanza passerò a questa situazione: ![[finehashest.jpg]]

Per essere precisi $p$ indica il numero di volte che si raddoppia l'area indice. 
>La tecnica in risposta ad ogni trabocco, spezza la pagina traboccata, se raddoppio la pagina che ha traboccato vuol dire che il numero di pagine complessivo è aumentato di 1. L'area indice la raddoppio quando $p'=p$.

La tecnica si predispone bene anche per la contrazione delle pagine. L'area indice è facile da rappresentare inoltre questa tecnica si predispone bene anche a ridurre le pagine. Per rappresentare efficientemene l'area indice si può usare un albero. 

---
# Difetti hashing
Nei database l'hashing non è efficace perché non supporta ricerche basate su chiavi diverse da quelle usate nel'hashing stesso oppure le ricerche per range in quanto le tuple sono distrubuite casualmente.
L'hashing è una <font color=red>tecnica di indicizzazione di tipo primario</font>, cioè oltre a tenere traccia di dove si trovano le tuple anche il dove collocarle, ciò limita il come tenere le pagine ordinate rispetto una caratteristica che viene chiamata <font color=red>partizionamento orizzontale</font>.

---
---
tag: #basi 
created: 2023-01-10 16:31:23
updated: 2023-01-10 16:31:23
---
#basi 
[[Ciclo dei grafi delle dipendenze e terza forma normale]]
# Sistemi di indicizzazione
Dove vanno a finire le tuple? Di solito i DBMS hanno un architettura di tipo client-server, dove c'è un server a cui arrivano richieste da diversi utenti, ovvero statement in SQL. Il server si appoggia ad una collezione di dati, che sono rappresentati nel DBMS secondo una rappresentazione proprietaria, di solito si usa una codifica binaria proprietaria rispetto a stringhe. La differenza nei DBMS sta nel come si appoggiano allo stato fisico, infatti la gestione dei file non è effettuata dal file system perché è necessario l'accesso concorrente. Le tuple devono essere contenute in dati durabili e le strutture dati "classiche" studiate nel corso di ASD non sono idonee. 
La testina del hard disk non preleva solo 64 bit (grandezza del bus indirizzi) quando gira, ma preleva un microsettore che è maggiore di 64 bit ad esempio 1KB. Passiamo a ragionare per blocchi di tuple, quindi prelevare una tupla o le sue 10 vicine ha lo stesso costo.

Solitamente i dati di una tabella vengono rappresentati in forma paginata e la tabella è trattata come una serie di pagine dati. 
>Per valutare l'efficienza di rappresentazione dei dati, devo contare il numero di pagine da accedere per trovare una tupla, trascurando la scansione della pagina in quanto essendo il tempo di accesso gargantuesco. Questo è dovuto al fatto che un hard disk lavora nell'ordine di grandezza dei MHz.

Ipotizziamo di inserire tuple in modo seriale, supponiamo di tenere un puntatore all'ultima pagina, quindi se è vuota inserisco la tupla, se piena ne creo una nuova. L'operazione d'inserimento ha costo $\theta(1)$, la ricerca ha costo $\theta(N)$ con $N$ numero di pagine ma il costo reale della ricerca è N+N$\times$T, dove N$\times$T è il costo in RAM dello scandire N pagine con T tuple. Questo sistema fu il primo utilizzato ma ormai è inefficiente, in quanto veniva usato sui nastri magnetici. Memorizzare i dati in maniera sequenziale, significa ordinare le tuple tramite un attributo quindi comporta tempi lineari.
In sostanza avremo che:

| Tipologia   | Costo inserimento | Costo ricerca |
| ----------- | ----------------- | ------------- |
| Seriale     | $\theta(1)$       | $\theta(N)$   |
| Sequenziale | $\theta(N)$       | $\theta(N)$   |

Si cerca quindi di evitare strutture dati che si basano su politiche di rappresentazione seriale o sequenziale.

---
# Tabella hash e tecniche di hashing statico
La prima tecnica che vediamo è l'hashing lineare dove il vettore che rappresenta la tabella, non contiene celle con tuple ma pagine. Ogni volta che arriva una tupla la prima cosa che faccio è trasformarla in una chiave di ricerca K, la funzione hash che si usa normalmente è $H(K)=K\ mod\ M$ con M numero di pagine. Se K=6 H(K)=6 mod 4=2 quindi la tupla con chiave 6 andrà a finire nella pagina 2.

Quando cerco una tupla devo usare una serie di attributi per calcolare la chiave K. Le collisioni dato che ogni elemento è una pagina, non sono difficili da gestire, se la pagina si riempie però devo fare qualcosa. 
>Nella tabella hash vanno tuple intere non spezzate. 

Supponiamo che ogni pagina abbia dimensione 2, se la pagina è piena assegno un puntatore in cui metto i trabocchi della pagina che ha anch'esso dimensione 2. Nel caso migliore inserimento e ricerca hanno costo costante, nel caso peggiore il costo è lineare rispetto al numero di pagine N. 

| Caso  | Costo inserimento | Costo ricerca |
| ----------- | ----------------- | ------------- |
| Migliore     | $\theta(1)$       | $\theta(1)$   |
| Peggiore | $\theta(N)$       | $\theta(N)$   |
### Migliorie

Utilizzare pagine di trabocco singole può portare a frammentazione, si crea quindi un unica lista di trabocco e non una lista per pagina. dove il tutto viene gestito tramite puntatori.

L'hashing lineare ad indirizzamento aperto evita l'uso dei puntatori e fa la stessa cosa. Invece di allocare una tupla secondo $H(K)=K\ mod\ M$ quando devo allocare l'i-esimo trabocco, uso $H(K)=K+i\ mod\ M$. 
Devo tenere traccia dei valori di $i$ da qualche parte per ricomporre i trabocchi, rendendo il tutto più leggero tuttavia si ha il problema <font color=red>dell'agglomerazione primaria</font>: mano a mano che ci sono trabocchi, alcune pagine vengono ignorate affinché la probabilità di trabocco resti pari tra tutte le pagine ma questo tende a creare alla fine dei trabocchi a catena. Per evitare questo problema, il valore $i$ è casuale. Un altro difetto della tecnica è che devo sapere a priori M. 

>Queste tecniche prendono il nome di hashing statico, perché la dimensione dell'area primaria non varia nel tempo, cioé M è sempre fisso e determinato a priori.

---






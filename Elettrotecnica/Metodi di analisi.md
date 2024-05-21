---
tags: elettrotecnica, 
created: 2024-04-27 18:07:20
updated: 2024-04-27 18:07:20
---
[[Teorema di Norton, Thevenin e Millman]]]
# Metodi di analisi
Dato un circuito di $R$ rami e $N$ nodi, il suo comportamento è completamente determinato quando si conoscono tutte le $2R$ grandezze elettriche. Se considerassimo tutte le incognite contemporaneamente si arriverebbe a sistemi di equazioni troppo complicati. Per le reti senza memoria ovvero rapporto tra tensione e corrente costante, 
si usano sistemi risolutivi algebrici per semplificare e risolvere i circuiti, o al massimo per trovare il minimo numero di equazioni necessarie per la soluzione.
Invece in presenza di elementi con memoria le relazioni tra tensione e corrente sono 
differenziali e spesso richiedono strumenti matematici come la trasformata di Laplace per la risoluzione. In caso di sistemi a regime sinusoidale possono essere ricondotti a sistemi  
algebrici con coefficienti complessi sfruttando il metodo dei fasori.

Preso un generico circuito si individuano $R$ equazioni dalle leggi di Kirchhoff e $R$ equazioni dalle relazioni topologiche. Nasce poi il problema di assicurarsi l'indipendenza lineare delle equazioni. Dalle leggi di Kirchhoff si nota che le equazioni sono linearmente dipendenti, si ricerca perciò un insieme minimo di tensioni o correnti indipendenti da cui ricavare le altre. Per determinare gli insiemi minimi di tensioni e correnti linearmente indipendenti, si sfruttano proprietà topologiche che non dipendono dalla natura degli elementi sui rami. Ciò è facilmente esprimibile tramite un grafo.

Nel grafo di circuito si individuano: 
- Maglia: percorso chiuso di rami tale che non percorre mai due volte lo stesso ramo.
- Anello: maglia che non contiene altre maglie al suo interno.
- Taglio: una superficie finita chiusa che taglia un insieme di rami (una sola volta ogni ramo).

## Metodo dei nodi
Dato un circuito, cerchiamo un insieme di KCL indipendenti scrivendo le KCL di tutti i nodi riportandole nella matrice d'incidenza $\hat{A}$. La matrice d'incidenza è legata al vettore $\overrightarrow{i}$ dall'equazione $\hat{A}\overrightarrow{i}=\overrightarrow{0}$. Si nota che la sommatoria di tutte le KCL è pari a 0, dunque non sono indipendenti. Preso un nodo qualsiasi come riferimento ottengo invece un insieme indipendente di N-1 KCL. Inoltre è un insieme complete dato che, una generica KCL associata ad una superficie chiusa $\sigma$ è data dalla somma delle KCL dei nodi contenuti in $\sigma$.
"L'algoritmo" per il metodo dei nodi è dunque il seguente:
- Scrivo le KCL dei nodi escluso il riferimento
- Le KCL sono somme di correnti, le trasformo in equazioni nei potenziali nodali incogniti attraverso le relazioni constitutive dei rami
- Per rami resistivi si avrà che la corrente $i_{jk}$ che va dal nodo $j$ al nodo $k$ verrà scritta come $i_{jk}=G_{jk}(e_j-e_k)$ dove $e_j,e_k$ sono i potenziali dei nodi $j,k$ mentre $G_{jk}$ è il rispettivo valore di conduttanza del ramo $jk$.
- Per i rami in cui sono presenti generatori sfrutto l'equazioni di vincolo dei generatori

Se scriviamo in forma matriciale il vettore delle tensioni di ramo $\overrightarrow{v}$ come una matrice $\hat{B}$ per il vettore dei potenziali nodali $\overrightarrow{e}$, $\overrightarrow{v}$ =$\hat{B}$$\overrightarrow{e}$. Si vede facilmente che $\hat{B}$ è la trasposta di $\hat{A}$.

I vantaggi del metodo dei nodi sono:
1. Applicabile a qualsiasi tipo di circuito
2. Le KCL sono semplicemente le equazioni di bilancio dei nodi quindi di immediata individuazione.
3. Le tensioni dei rami si esprimono come differenze tra i potenziali dei rispettivi nodi per cui non serve scrivere le KVL per mettere in relazione le tensioni tra loro.
4. Le relazioni costitutive sono sostituite direttamente nel sistema di equazioni delle KCL, riducendo la dimensione del sistema risolutivo.

## Metodo degli anelli
Dato un circuito, cerchiamo un insieme di KVL indipendenti scrivendo le KVL di tutti gli anelli riportandole nella matrice d'incidenza $\hat{L}$. La matrice d'incidenza è legata al vettore $\overrightarrow{v}$ dall'equazione $\hat{L}\overrightarrow{v}=\overrightarrow{0}$. 
Si nota che la sommatoria di tutte le KVL è pari a 0, dunque non sono indipendenti. La KVL di una maglia può essere scritta come combinazione delle KVL degli anelli.
In forma matriciale il vettore delle correnti di ramo come una matrice $\hat{M}$ per il vettore della corrente di anello $\overrightarrow{i_L}$ si nota che $\hat{M}=\hat{L}^T$. Quindi si ottengono $R-N+1$ KVL degli anelli indipendenti. "L'algoritmo" è il seguente:
- Scrivo le KVL degli anelli
- Scrivo le cadute di potenziali come corrente di ramo per resistenza dove suddetta corrente è combinazione delle correnti di anello.
- Risolvo il sistema i generatori di tensione sono noti.

In conclusione i vantaggi del metodo degli anelli sono:
1. Gli anelli sono univocamente identificati rendendo immediata la scrittura delle KVL indipendenti
2. Le correnti dei rami si esprimono tramite le correnti di anello per cui non serve scrivere le KCL per mettere in relazione le correnti tra loro.
3. Posso scrivere le tensioni dei rami resistivi direttamente tramite le correnti di anello per ottenere un sistema di $R-N+1$ correnti indipendenti.
4. La presenza di generatori di corrente riduce il numero di correnti incognite e semplificando il sistema risolutivo.

---
# Teorema di Tellegen
Il teorema di Tellegen è importante perché, dimostra la conservazione della potenza istantanea a partire solo dalle proprietà topologiche e permette di effettuare analisi di sensibilità degli elementi circuitali tramite il concetto di potenze virtuali di due circuiti.

Il bilancio energetico ovvero la conservazione della potenza istantanea può essere scritto come: $\displaystyle\sum^{R}_{k=1}p_k(t)=\sum^{R}_{k=1}v_k(t)i_k(t)=0$ ovvero come il prodotto scalare del vettore delle tensioni di ramo e del vettore delle correnti di ramo: $\displaystyle\sum^{R}_{k=1}v_k(t)i_k(t)=0=\overrightarrow{V}\cdot\overrightarrow{I}=\overrightarrow{V}^T\cdot\overrightarrow{I}$
ricordando che $\overrightarrow{V}=\hat{B}\overrightarrow{e}=\hat{A}^T\overrightarrow{e}$ $\hat{A}\overrightarrow{I}=\overrightarrow{0}$ dunque
$\displaystyle\sum^{R}_{k=1}v_k(t)i_k(t)=\overrightarrow{V}^T\cdot\overrightarrow{I}=(\hat{A}^T\overrightarrow{e})^T\overrightarrow{I}=\overrightarrow{e}^T\hat{A}\overrightarrow{I}=\overrightarrow{e}^T\overrightarrow{0}=0$

Il bilancio energetico è assicurato dalle proprietà topologiche espresse dalla matrice di incidenza. Non si fa nessuna ipotesi sulla natura dei componenti. Inoltre dato che la matrice di incidenza contiene solo le informazioni sulle connessioni tra rami e nodi, se la topologia è la stessa, la matrice d'incidenza è la medesima e questo permette di verificare l'analisi di sensibilità degli elementi circuitali. Consideriamo due circuiti aventi la stessa tipologia e quindi la stessa matrice d'incidenza $\hat{A}$. Il generico prodotto $v_{k,a}(t)i_{k,b}(t)$ o $v_{k,b}(t)i_{k,a}(t)$ di una corrente di ramo per la tensione delle stesso ramo appartenente però ad un circuito associato è detta potenza virtuale. Separatamente varranno le relazioni $\overrightarrow{V}_a^T\overrightarrow{I}_b=\overrightarrow{e}_a^T\hat{A}\overrightarrow{I}_b=0$ e $\overrightarrow{V}_b^T\overrightarrow{I}_a=\overrightarrow{e}_b^T\hat{A}\overrightarrow{I}_a=0$ ovvero anche la potenza virtuale si conserva.

---
#asd
[[Hash map]]
# Albero binario di ricerca

L'albero binario di ricerca è un albero dove ogni nodo può avere al massimo 2 figli e la disposizione dei nodi è in modo ordinato e favorisce la ricerca. Per ricercare un elemento si usa una strategia simile alla ricerca binaria. Diamone 2 definizioni:

1. Sia A un albero binario, i cui valori appartengono ad un dominio ordinato D. A è un albero binario di ricerca se e solo se: <font color=red>per tutti i nodi di A, tutti i valori che appaiono nel sottoalbero sinistro del nodo n sono minori del contenuto del nodo n ed tutti i valori che appaiono nel sottoalbero destro del nodo n sono maggiori del contenuto del nodo n </font>
2. Sia A un albero binario, i cui valori appartengono ad un dominio ordinato D. A è un albero binario di ricerca se e solo se: <font color=red> tutti i valori che appaiono nel sottoalbero sinistro di A sono minori del valore contenuto nella radice, tutti i valori che appaiono nel sottoalbero destro sono maggiori del valore contenuto nella radice. I sottoalberi sinistro e destro di A sono alberi binari di ricerca</font>.

Esempi di alberi binari di ricerca e non:

![[abr.jpg]]

A non è un ABR, B è un ABR e C l'albero vuoto è un ABR perchè soddisfa le 2 definizioni.

Piccolo appunto:
$\gamma=\forall n\in S\Rightarrow\phi(n)$ allora se $S=\oslash\Rightarrow\gamma$ è vera. Quindi se per ogni n di un insieme di valori una condizione logica è valida allora se l'insieme è l'insieme vuoto la condizione è valida ugualmente.

I metodi per la ricerca di un nodo e dell'inserimento di un nodo, hanno complessità $T(n)\in\theta(h)$ dove h è l'altezza dell'albero, quindi l'altezza per la complessità è cruciale. Bisogna quindi tenere l'altezza dell'albero il più bassa possibile. Gli alberi completi sono la scelta migliore per tenere un'altezza bassa, perciò avere alberi binari di ricerca completi è l'ideale, ma spostare i nodi e cambiare strutture è molto costo e complesso. Infatti toccare ogni nodo andrebbe a portare la complessità a $\theta(n)$, non usiamo perciò l'altezza più bassa ma una sufficientemente bassa.

---

# Alberi AVL

Abbiamo parlato di alberi binari di ricerca e del fatto di dover tenere un'altezza sufficientemente bassa. Andiamo perciò ora a parlare di alberi AVL. Negli alberi AVL, si utilizza un concetto nuovo, il concetto del fattore di bilanciamento in un nodo n.

Il fattore di bilanciamento è uguale all'altezza del sottoalbero sinistro di n meno l'altezza del sottoalbero destro di n in valore assoluto, se il valore del fattore è ≤ 1 allora il nodo è bilanciato, se ogni nodo è bilanciato l'albero è bilanciato. Esempio:

![[avl.jpg]]

Calcoliamo i fattori di bilanciamento dei nodi:

- h($v_0$)=3-2=1
- h($v_1$)=2-0=2
- h($v_2$)=0-1=1
- h($v_3$)=0-1=1
- h($v_4$)=0
- h($v_5$)=0

Quest'albero perciò non è bilanciato.

Adesso occupiamoci di dimostrare come l'altezza rispetto al numero di nodi sia sufficientemente bassa. Per un albero bilanciato nel caso peggiore ha un numero minimo di nodi per essere bilanciato pari a Nmin(h). Nmin(1)=1, Nmin(h)=Nmin(h-1)+Nmin(h-2)+1, dove il +1 indica la radice.

Questa equazione ricorda quella di fibonacci. In questo caso Nmin è il numero minimo di nodi dell'albero dato da radice ed un sottoalbero di altezza h-1 ed uno alto h-2. Nmin(h)=$\phi^h\le n$ dove $\phi$ è la costante di fibonacci. Nmax(h) invece è $2^h-1$ con $n\le 2^h-1$. Mettendo insieme le 2 disequazioni, si ottiene $\phi^h\le n\le 2^h-1$. Se si estrae il log si ottiene, $log_2n\le h\le log_\phi n$. Quindi avremo l'altezza è pari a $O(logn)$, dove la base non si sa ma è comunque una quantità inferiore.

---

## Tecniche di rotazione

Sono tecniche per ripristinare il bilanciamento mantenendo l'ordine di ricerca, se lo sbilanciamento è al più 1. Le operazioni di inserimento e rimozione operano un nodo alla volta, perciò non si hanno problemi con lo sbilanciamento perchè al più avrò -2 o 2 come fattore.
Vediamo un esempio:
![[rota.jpg]]
Questa è una rotazione di base, si nota che:

- prima $T_1$ era minore di u ed adesso pure
- prima $T_3$ era maggiore di v adesso pure
- prima $T_2$ era minore di v e maggiore di u ed adesso pure
- u era minore di v prima ed adesso pure

Perciò in una rotazione di base si DEVE mantenerare la gerarchia. Esistono 4 tipi di rotazione:

1. sinistra-sinistra: T è il sottoalbero sinistro del figlio sinistro di v
2. destra-destra: T è il sottoalbero destro del figlio destro di v
3. sinistra-destra: T è il sottoalbero destro del figlio sinistro di v
4. destra-sinistra: T è il sottoalbero sinistro del figlio destro di v

Con l'inserimento l'altezza rimane uguale assieme al fattore di bilanciamento. Vediamo i passi per l'inserimento:

``` 
insert(elem e, key k)
1) crea un nodo u con elem=e e key=k
2) inserisco come in un albero binario di ricerca
3) ricalcola i fattori di bilanciamento dei nodi, nel cammino dalla radice al nodo u e mi fermo appena un nodo v ha un fattore pari a + o - 2
4) eseguo una rotazione adeguata su v
```

Nel caso della delete:

``` 
delete(elem e)
1) elimino come in un albero binario di ricerca
2) ricalcola i fattori di bilanciamento dei nodi, nel cammino dalla radice al padre del nodo eliminato
3) ripercorro dal basso verso l'alto e mi fermo sul primo nodo che ha fattore pari a + o - 2.
4) ribilancio abbassando però l'altezza di 1. Questo porta a ricalcolare i fattori di bilanciamento e risalire.
```

Potrebbero essere necessarie al più $O(logn)$ rotazioni per sistemare il bilanciamento. Per la delete non è necessario calcolare sempre l'altezza, ma basta mantenere il fattore di bilanciamento, facendo ciò propago verso l'alto la variazione d'altezza rispetto all'operazione che si effettua.

Tutte le operazioni hanno costo $O(logn)$ poichè l'altezza dell'albero è $O(logn)$ e ciascuna rotazione richiede tempo costante.

In sostanza mantenere il bilanciamento è cruciale per ottenere prestazioni buone.

---
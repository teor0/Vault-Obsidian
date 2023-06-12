#asd 
[[Algoritmo di Floyd]]
# Problema di edit distance
Vediamo adesso un'altra applicazione della programmazione dinamica però sulle stringhe. Il problema è: abbiamo 2 stringhe ABBA e ACA. Quanto 2 stringhe tra di loro sono distanti?

In altre parole sarebbe l'autocorrezione di una tastiera di uno smartphone. Si vuole modellare la distanza tra 2 parole in termini del numero di correzioni da apportare alla prima parola per trasformarla nella seconda. È il cosiddetto problema di edit distance. Fissato un insieme di operazioni che si potrebbero applicare alla stringa, in questo caso: inserimento, cancellazione e modifica di un carattere in una posizione.
C'è anche lo swap tra 2 caratteri, che può variare in swap adiacenti, la tipologia principale di errori di battitura. 
Vogliamo portare abba → aca  come fare? mod('c',1), del(2) per ottenere aca da abba. In generale è sempre possibile trasformare una stringa S1 in una stringa S2, e si hanno varie modalità per trasformarla. 

Definiamo la distanza di edit: una sequenza di edit $\large\sigma$ è una sequenza di operazioni di modifica ed il costo di $\large\sigma$ è la sua lunghezza. Date 2 stringhe S1 e S2 $\sigma$ applicata a S1 produce la stringa S2=$\large\sigma$(S1) applicando a S1 le operazioni in ordine se $\large\sigma$=\[$op_1,...op_k$] allora $\large\sigma$(S1)=$op_k$(...($op_1$(S1))).

Date due stringhe S1 e S2 la distanza di edit da S1 a S2 è uguale al costo della sequenza di edit $\large\sigma$ tale che $\large\sigma$(S1)=S2 e $\nexists$ una sequenza di edit $\large\sigma '$ tale che: $\large\sigma '$(S1)=(S2) e costo($\large\sigma '$)<costo($\large\sigma$). 

>Esiste sempre la distanza di edit tra 2 stringhe di lunghezza finita.

La sequenza di edit di costo più piccolo è quella vuota di costo 0. Esiste almeno una sequenza di edit che ritorna S2 da S1, ovvero delete di tutti i caratteri fino alla stringa vuota e poi insert, tale sequenza ha costo pari alla lunghezza della prima stringa più quella della seconda. Il costo $\sigma$ corrisponde ad associare ad ogni operazione un costo unitario. Questa assunzione in alcuni contesti potrebbe non essere ragionevole. 
Una strategia triviale ma inefficiente è calcolare tutte le sequenze di edit perché vogliamo essere efficienti rispetto la lunghezza delle stringhe. 

È inutile provare sequenze di edit con costo maggiore di len(S1)+len(S2) perché abbiamo già una sequenza di edit di questo costo perché prendere una maggiore?
Detto ciò il numero di sequenze di edit che abbiano un costo più basso è esponenziale con base alta quindi un algoritmo risulta impraticabile.

---
## Algoritmo per il calcolo di edit distance
L'algoritmo di programmazione dinamica è applicabile solo su le 3 operazioni disponibili (ins, del e mod) e si basa sulla strategia di utilizzare la dimensione del problema. I sottoproblemi sono sempre di calcolo di edit distance ma fra prefisso(S1,i) e prefisso(S2,j). 

Quindi il problema è caratterizzato dalla coppia i,j dove il caso banale è i=0, j=0 quindi edit("","")=0, edit distance di una stringa vuota che è pari a 0. 

L'assunzione importante che si fa, è che in qualche modo calcolo la distanza tra il prefisso i-esimo e j-esimo utilizzando l'informazione solo sulle distanze tra i prefissi di ordine inferiore rispetto a (i,j). Mi concentro quindi sulle sequenze di edit che mi consentono di rendere uguali 2 stringhe rendendo prima uguali i prefissi di ordine inferiori di queste 2 stringhe. Esempio:

abda→aca
scelgo i prefissi abd e ac e faccio del('b'), mod('d','c'). Fare al contrario è errato in quanto il prefisso abc non è uguale al prefisso ac. Bisogna quindi fare attenzione perché la strategia potrebbe non portarmi alla risoluzione in quanto trascura alcune sequenze di edit. La caratteristica delle sequenze di edit per rendere uguali i prefissi è di applicare le operazioni in ordine crescente di posizione. L'insieme di operazioni di ins, del e mod sono invertibili, se inserisco lo swapAd senza restrizioni questo non vale più. Bisogna considerare solo per i prefissi, tanto per ogni sequenza di edit che non procede per prefissi, c'è una equivalente con le stesse operazioni che procede in ordine in posizione. Ci ricaviamo un'equazione di ricorrenza per passare da distanze di edit dei prefissi a quella dei prefissi di ordine maggiore. Il costo di
edit(0,0) è 0 in quanto da stringa vuota a stringa vuota non servono operazioni. Anche edit(0,j) e edit(i,0) sono sempre stringhe vuote. Ho un solo modo per trasformare S1 in S2 con il numero minimo di operazioni, ed è fare j inserimenti. Nel caso in cui devo trasformare S2 in S1 faccio i del, ricordando che assumiamo costi unitari per j e i. 
Prendiamo adesso questa matrice:
![[string.png]]
I valore nelle celle sono le distanze di edit per risolvere i problemi. Bisogna calcolare il generico edit(i,j) avendo calcolato prima tutti i prefissi di ordine minore (i',j') dove abbiamo i'$\le$i, j'$\le$j e che almeno uno dei due indici sia strettamente minore quindi: i'<i o j'<j. Ci sono 3 modi per calcolare edit(i,j):
- edit(i-1, j-1)+(S1[i]\==S2[j])?0:1 quindi ho reso le stringhe fino al penultimo carattere uguali. Se l'ultimo carattere i e j sono uguali allora non faccio operazioni altrimenti effettuo una sostituzione.
- edit(i,j-1)+add perchè manca l'ultimo carattere i di S2 da S1
- edit(i-1,j)+del cancello l'ultimo carattere i di S1

Di questi 3 modi ne vogliamo quello di costo minore, ovvero edit(i-1, j-1)+(S1[i]\==S2[j])?0:1 dove al minimo faccio 1 operazione mentre, negli altri casi ne faccio 2. La matrice verrà riempita per diagonali, colonne o righe. 
![[stringmat.png]]
A questo punto per calcolare il costo della edit distance calcoliamo percorriamo gli archi e facciamo un cammino.
![[finalmat.png]]
Abbiamo quindi che l'edit distance costa 3 nei due cammini esaminati in figura, ricordando che lungo le righe si hanno inserimenti e lungo la diagonale sostituzioni.

---

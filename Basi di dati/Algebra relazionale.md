---
tag: #basi 
created: 2022-12-05 17:26:43
updated: 2022-12-05 17:26:43
---
#basi 
[[Dettagli su i vincoli e generalizzazioni nel modello relazionale]]
# Definizioni, regole e semantica
Quali sono le operazioni per estrarre informazioni da un database? Supponiamo di avere un database popolato da:
Fornitore

| P.IVA | Nome | Città |
| ----- | ---- | ----- |
| F1    | A    | CS    |
| F2    | B    | RC    | 

Merce

| Codice | Nome | Marca    |
| ------ | ---- | -------- |
| M1     | X    | $\alpha$ |
| M2     | Y    | $\beta$  |

>Le tabelle popolate si chiamano istanze della relazione.
> Per <font color=red>arità</font> di una tabella si intende il numero di colonne.
> Per <font color=red>cardinalità</font> di una tabella si indica il numero di tuple\righe

L'algebra relazionale consente di manipolare tuple attraverso operatori e all'interno di è possibile utilizzare gli operatori classici dell'insiemistica, quali: $\bigcup$ (unione), $\bigcap$ (intersezione), $\times$ (prodotto cartesiano) e $\setminus$ (differenza).
>[!Regola]
>Per utilizzare un operatore di unione o intersezione, in generale di una comparazione i 2 operandi devono contenere tuple con la stessa arità e necessitano di attributi comparabili.

Un operatore si dice <font color=red> rientrante</font>, quando applicato ad un dominio restituisce elementi di quel dominio, indi per cui si possono innestare gli operatori.
>Ogni operatore dell'algebra relazionale è rientrante!

Da notare che il risultato di un'operazione ha la stessa struttura della tabella di partenza.
All'interno di un database le istruzioni non vengono interpretate nell'ordine in cui sono scritte, quindi non c'è nessun problema di complessità o di efficienza, ma esiste solo il problema della correttezza dell'interrogazione che si vuole fare. 

L'operatore di unione, restituisce una tabella con all'inteno tuple di un'altra tabella compatibile, quindi il risultato avrà come detto la stessa struttura della tabella di partenza. Ad esempio Fornitore $\bigcup$ Merce non si può fare in quanto le colonne hanno attributi diversi, ma Fornitore $\bigcup$ Fornitore ritorna una tabella con la struttura di Fornitore con tutte le tuple di entrambe le tabelle. Ovviamente l'intersezione torna l'intersezione tra due tabelle compatibili e la differenza torna la differenza tra due tabelle compatibili.
L'operatore del prodotto cartesiano, restituisce tutti i possibili accoppiamenti tra due tabelle e restituisce una tabella che è l'unione delle due.


| P.IVA | Nome | Città | Codice | Nome | Marca    |
| ----- | ---- | ----- | ------ | ---- | -------- |
| F1    | A    | CS    | M1     | X    | $\alpha$ |
| F2    | B    | RC    | M2     | Y    | $\beta$  |

Il risultato è dato dalla lista degli attributi della prima tabella concatenato con la lista degli attributi della seconda. Le tuple sono la concatenazione tra tutte le tuple e la cardinalità è $n\times m$ con $n$ cardinalità della prima tabella e $m$ cardinalità della seconda.

Per compattezza ed ambiguità indichiamo in una tabella le colonne con gli attributi tramite \$n. Tuttavia se provo a fare $Fornitore\bigcap Merce$ è scorretto anche se l'arità delle tabelle è uguale. È scorretto in quanto il nome degli attributi è diverso, quindi si necessità di un meccanismo di ridenominazione. Per rinominare una colonna si utilizza l'operatore $\large\rho$, esempio:
$\large\rho_{\$2\rightarrow 'nome'}[\Pi_{\$2}(Fornitore)]\bigcap\rho_{\$2\rightarrow 'nome'}[\Pi_{\$2}(Merce)]$

---

# Operatori dell'algebra relazionale

Il primo operatore è l'operatore di <font color=green> selezione </font> che si indica con $\sigma$. È un operatore monodico, quindi prende come argomento solo una relazione. Come pedice del operatore occorre indicare la condizione che si vuole rispettare, ad esempio:
$\displaystyle\large\sigma_{Città='CS'}$ (Fornitore) 

| P.IVA | Nome | Città |
| ----- | ---- | ----- |
| F1    | A    | CS    |

che equivale in un linguaggio di programmazione a 
```
for(tupla in Fornitore)
	if(tupla.città equals CS)
		return tupla
```
La condizione ovviamente può essere una formula di algebra booleana più complicata del tipo: $(Città='CS')\lor(P.IVA\ne 'F1'\land Nome\ne 'C')$ 

L'operatore<font color=red> proiezione</font> $\Pi$ restringe le colonne di una relazione, ovvero applica un filtro su di loro. Anche questo operatore è monodico ed ha come pedice la colonna da visualizzare oppure una lista d'attributi separatati da una virgola. Esempio:
$\large\Pi_{Nome}$(Fornitore)

| Nome |
| ---- |
| A    |
| B    |
| C     |

Si chiama proiezione in quanto proiettare una tabella significa restingerla. Da notare che la proiezione modifica sia l'arità che la cardinalità, mentre la selezione modifica solo la cardinalità. La proiezione ha complessità $\theta(n^2)$

L'operazione di <font color=blue> join</font> serve ad attuare un prolungamento fra tuple, cioè serve a unire/concatenare tuple di due relazioni secondo il criterio indicato come pedice. L'arità della relazione risultato è uguale a $n+m$ ed equivale ad un prodotto cartesiano con selezione applicata. L'operatore join si dice derivato e si indica come $\bowtie$.

Join e selezione traducono in realtà $\exists$, mentre $\setminus$ traduce $\forall$.

## Diverse join ed operazione di divisione
La <font color=red>join naturale</font> consiste in fare una join sugli attributti omonimi oppure sulle chiavi esterne. Esempio: $Fornitore\bowtie Fornitura$. 
Quando in una join vengono scritte solo condizioni di uguaglianza si chiama <font color=blue>equi join</font>, quando viene scritta una condizione qualunque si chiama <font color=blue>$\theta$ join</font>.
C'è poi la <font color=blue>left outer join</font> ⟕che restituisce anche un prolungamento con null. Il concetto di <font color=blue>right outer join</font> ⟖è analogo. C'è poi la <font color=blue>full outer join</font> ⟗ dove tuple di A che non hanno una tupla di B corrispondente vengono prolungate con NULL e tuple di B che non hanno una tupla di A corrispondente vengono anch'esse prolungate con NULL. Infine c'è la <font color=blue>semi join</font> $\bowtie$ senza l'ultima stanghetta verticale, corrisponde a proiettare sugli attributi di A.

L'operatore di divisione % corrisponde a calcolare tutti, ma è specifico per solo alcuni che non verranno tratti nel corso.

---



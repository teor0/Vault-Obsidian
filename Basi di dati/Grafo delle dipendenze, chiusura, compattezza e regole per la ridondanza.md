---
tag: #base
created: 2023-01-06 19:26:26
updated: 2023-01-06 19:26:26
---
#basi 
[[Dipendenza funzionale e forma normale di Boyce Codd]]
# Grafo delle dipendenze e chiusura
Per velocizzare il procedimento di "calcolo" delle chiavi si utilizza il grafo delle dipendenze.
![[grafodip.jpg]]
Si tratta di un <font color=red>ipergrafo</font> perché, per percorre gli archi devo trovarmi su tutti i nodi d'ingresso, ovvero per arrivare su C devo trovarmi su A e B.
Qui bisogna scoprire quali attributi sono raggiungibili. Grazie alle dipendenze funzionali riesco a garantire consistenza se le impongo, se non imposte riesco a trovare tutte le chiavi candidate dove scelgo una primaria e le altre UNIQUE. Dato l'insieme AE, l'insieme di attributi che sono funzionalmente dipendenti da AE si chiama <font color=red>chiusura</font>. Nel grafo corrisponde all'insieme di nodi raggiungibili da AE, nell'esempio la chiusura è $(AE)^+=AEBC$.

Calcolare la chiusura aiuta a capire se è una superchiave. Nel grafo corrisponde a fare un percorso. Meccanicamente si passa da considerare insiemi di attributi con 1 attributi, poi 2, poi 3, fino a n-1 dove n è il numero di attributi. 
>Devo trovare insiemi di chiavi minimali!

---
# Compattezza nelle dipendenze funzionali e regole per evitare ridondanza
Riprendendo lo schema Esame(<u>Matricola,</u>Nome,Data,<u>Materia</u>,Docente,Voto) con le dipendenze Matricola$\rightarrow$Nome, Materia$\rightarrow$Docente e Matricola,Materia$\rightarrow$nome,docente,data,voto possiamo riscrivere in maniera compatta il tutto come: Matricola$\rightarrow$Nome, Materia$\rightarrow$Docente e Matricola,Materia$\rightarrow$data,voto.

Per evitare ridondanza ogni volta che appare un'implicazione già fatta la devo togliere. Esempio: X$\rightarrow$Y, Y$\rightarrow$Z, X$\rightarrow$Z ho che l'ultima dipendenza è ridondante.
Altro esempio: A$\rightarrow$B, B$\rightarrow$C, AC$\rightarrow$D in questo caso due tuple con stesso valore di A hanno stesso valore di C, quindi la terza dipendenza diventa A$\rightarrow$D.

---
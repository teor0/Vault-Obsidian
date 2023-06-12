---
tag: #basi
created: 2022-11-26 17:58:43
updated: 2022-11-26 17:58:43
---
#basi 
[[Modello entità-relazione]]

# RDBMS - Relational DataBase Management System
Una volta fatto il progetto concettuale i dati andranno a finire nel sistema per la gestione di database relazionali. In questa fase vogliamo capire qual è la struttura logica più opportuna per le tabelle.
Tutte le informazioni saranno codificate in un record cioè una riga o più formalmente tupla. Si può utilizzare una tabella singola per rappresentare tutto oppure più tabelle a seconda dello spazio di manovra che si vuole avere. 

>[!Regola]
>Nella progettazione logica non si discute l'implementazione della tabella!

Riprendiamo l'esempio di fornitore
![[esempioRDBMS.jpg]]

| P.IVA | nomeF | Città | Codice | nomeM | Marca    |
| ----- | ----- | ----- | ------ | ----- | -------- |
| F1    | N1    | C1    | M1     | NM1   | $\alpha$ |
| F1    | N1    | C1    | M2     | NM2   | $\beta$  |
| F2    | N2    | C2    | M1     | NM1   | $\alpha$ |

Lo schema di tabella indica il suo scheletro ovvero il suo nome e l'elenco degli attributi e visivamente è l'intestazione della tabella. L'istanza è una tabella vera e propria. La progettazione definisce gli schemi adeguati e valuta se la scelta è opportuna o meno. Nei database si può inserire $null$ per indicare che quella cella è vuota. Lo schema non rappresenta le chiavi e non rispetta il concetto di relazione facendo rappresentare la stessa coppia! Bisogna quindi definire un meccanismo d'identificazione per la tabella stessa, che serve ad evitare l'inserimento di informazioni scorrette. Tale meccanismo è detto <font color=orange>vincolo di chiave</font> come per il modello ER.

> Per ogni tabella bisogna esprimere un vincolo di chiave minimale suggerito dal modello ER. Tale vincolo è espresso sottolineando gli attributi chiave

Nel caso specifico della tabella sopra, scegliere P.IVA e codice come vincoli non risolve le problematiche dove ad esempio lo stesso fornitore fornisce più merci o la stessa merce è fornita da più fornitori. Per questo la soluzione più oppurtuna è:

Fornitore

| **P.IVA** | nomeF | Città | 
| ----- | ----- | ----- | 
| F1    | N1    | C1    |
| F1    | N1    | C1    |
| F2    | N2    | C2    | 

Merce

| **Codice** | Nome | Marca    |
| ------ | ---- | -------- |
| M1     | NM1  | $\alpha$ |
| M2     | NM2  | $\beta$  |

Fornitura

| **Fornitore** | **Merce** | Prezzo |
| --------- | ----- | ------ |
| F1        | M1    | 10€    |
| F2        | M2    | 15€    |
| F2        | M1    | 10€    | 

Fornitore(<u>P.IVA</u>: varchar, Nome: varchar, città:char(15))
Normalmente  devono essere espressi i tipi degli attributi e la loro lunghezza se finita, in questo caso varchar fa le veci di stringa alfanumerica e char rappresenta una stringa di caratteri e basta, ma all'interno del corso non sarà necessario esprimere la tipologia degli attributi. Una possibile lineaguida è quindi quella di utilizzare una tabella per ogni entità e relazione ma ci sono casi e casi.

>[!Regola]
>Tutte le tabelle devono avere una chiave primaria!

---
# Traduzione opportuna delle relazioni e chiave esterna
![[modelloFornitoreCompleto.jpg]]
Riprendendo il modello ER completo andiamo ad esprimere i vincoli di chiave delle tabelle:
- Fornitore(<u>P.IVA</u>, Nome, Città)
- Merce(<u>Codice</u>, Nome)
- Marca(<u>Nome</u>, Sede)
- Fornitura(<u>Fornitore, Merce</u>, Prezzo)
- Produzione(<u>Merce</u>, Marca)

Per la tabella produzione la chiave è solo merce perché il vincolo nel modello ER è 1:1 e specifica ancora meglio l'insieme delle coppie <merce,marca> in quanto rende la chiave minimale rispetto alla chiave <u>Merce,Marca</u>. Per rappresentare bene il modello ER e garantire il vincolo 1:1 tra Merce e Marca dobbiamo inserire una colonna Marca nella tabella Merce. 
In sostanza per le relazioni, se c'è un vincolo 1:1 non si crea una tabella che rappresenta la relazione ma si mette un riferimento nella tabella che codifica l'entità, facendo così <font color=red>l'accorpamento</font> dei due concetti.

Gli attributi possono contenere valori nulli a patto che questo si espicitato scrivendo NULL sopra l'attributo, cioè: Merce(<u>Codice</u>, Nome, $\overset{NULL}{Marca}$ ).
Tuttavia per il vincolo 0:1, utilizzare tabelle dove ci sono attributi che possono essere nulli può essere problematico per la gestione della struttura dati dove le righe sono di dimensione diverse ed in casi particolari potrei avere colonne vuote ed inutili. 
> Non è in generale opportuno creare tabelle con molti valori NULL, perchè creano problemi di gestione di memoria.

Questi schemi sono corretti a meno di un aspetto, il riferimento. Ad esempio per Merce, utilizzo solo il riferimento alla chiave Codice, in particolare ogni volta che voglio indicare che i valori di 1 o più attributi sono presi da un'altra tabella, utilizzerò il <font color=red>vincolo di chiave esterna</font>, che non ha niente a che vedere con la chiave esterna del modello ER, un esempio per la tabella Fornitura è:
Fornitura\[Fornitore\]$⊑_{FK}$Fornitore\[P.IVA\]
Fornitura\[Merce\]$⊑_{FK}$Fornitore\[Codice\]


Mentre la chiave primaria impone che il valore debba essere sempre specificato, la chiave esterna nel dire che un valore prende valori da un altro, non impone che debba essere specificato e qualora non è specificato allora il vincolo di contenimento non vale più. In sostanza se ho un vincolo 1:1 è bene accorpare l'entità nello schema: 
Merce(<u>Codice</u>, Nome, Marca)
Merce\[Marca\]$⊑_{FK}$Marca\[Nome\]

---








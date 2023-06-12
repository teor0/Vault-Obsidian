---
tag: #basi 
created: 2022-12-13 10:59:36
updated: 2022-12-13 10:59:36
---
#basi 
[[Algebra relazionale]]
# Base del linguaggio
Il linguaggio SQL, Structured Query Language, è un linguaggio di interrogazione strutturato in quanto le espressioni che vengono utilizzate per scrivere le interrogazioni hanno una struttura. Il linguaggio è standard per i DBMS relazionali e si suddivide in due parti:
1. Una parte DDL, Data Definition Language: serie di costrutti per creare e definire tabelle
2. Una parte DML, Data Manipulate Language: serie di comandi utili per la gestione di tabelle già definite ed estrazioni di informazioni su tuple

Per la parte DDL, abbiamo innanzitutto il costrutto <font color=blue>CREATE</font> che crea una tabella o un nuovo database ed ha la seguente sintassi: 
``` SQL
CREATE database nomedatabase
USE nomedatabase
CREATE table Fornitore AS
(PIVA char(20) primary key,
 Nome varchar(40) unique,
 Citta varchar(20) NOT NULL
);
```

>La chiave e tutti i vincoli di unicità per leggibilità è meglio scriverli al termine della creazione.

``` SQL
CREATE table Merce AS
(Codice number(10),
 Nome varchar(40),
 Marca varchar(20),
 primary key Codice
);

CREATE table Fornitura AS
(Fornitore char(20),
 Merce number(10),
 Prezzo number(4,2),
 foreign key Fornitore references Fornitore(PIVA),
 foreign key Merce references Merce(Codice),
 primary key (Fornitore,Merce)
);
Il 4,2 di prezzo serve ad indicare che è un double.
```

Poi ci sono tutti i comandi che si possono fare sulla tabella quali:
- <font color=orange>DROP table</font>: cancella la tabella.
- <font color=orange>ALTER table</font>: modifica la tabella.
- <font color=orange>INSERT into</font>: inserisce una tupla.
- <font color=orange>DELETE</font>: cancella una tupla.
- <font color=orange>UPDATE</font>: modifica una tupla.

Per motivi di efficienza in SQL se non viene specificato, il risultato può contenere duplicati a differenza dell'algebra relazionale che li elimina. Una tabella SQL non è una relazione ma un multi-insieme di tuple, ovvero un oggetto può non appartenere o appartenere x volte ad un multi-insieme.
SQL non è veramente rientrante come l'algebra rispetto il concetto di tabella, in SQL il rientrante si riferisce al concetto di multi-insieme. Quando si fa una query SQL si potrebbe ottenere un qualcosa che non è un insieme di tuple, in quanto potrebbe contenere duplicati.

Al momento della creazione di una tabella si può usare un vincolo di CHECK affinché valga una proprietà per quell'attributo.

---
## Select, from, as, where e distinct
Vi sono poi i costrutti della parte DML di SQL, primo tra tutti <font color=red>SELECT</font> che serve a restituire un output e riceve attributi come argomenti non tabelle. Segue poi il costrutto <font color=red>FROM</font> che serve a prelevare i dati e come argomento può avere una lista di tabelle. Esempi:
```SQL
SELECT PIVA, Nome
FROM Fornitore;

SELECT Nome
FROM Merce;

SELECT *
FROM Fornitore;
```

La prima query equivale in algebra relazionale a $\Pi_{\$1,\$2}(Fornitore)$, mentre la terza query equivale a $\Pi_{\$1,\$2,\$3}(Fornitore)$ ovvero si estrae tutto.
> SELECT è l'unico costrutto che deve essere presente in una query!

Il costrutto <font color=red>AS</font> serve per ridenominare un attributo. Esempio:
```SQL
SELECT Nome AS NomeF
FROM Fornitore;
```
In particolare la query sopra, estra e crea una tabella NomeF con all'interno tutti i nomi della tabella Fornitore. Quindi in sostanza attraverso SELECT e FROM siamo in grado di esprimere la proiezione.
Il costrutto <font color=red>WHERE</font> viene sfruttato come clausola per la selezione. Esempi:
```SQL
SELECT Nome 
FROM Fornitore
WHERE Citta='CS';

SELECT M.Nome AS NomeM
FROM Merce as M
WHERE M.Marca='Barilla'
```
>Il secondo esempio ci fa capire inoltre che si possono specificare gli attributi di una tabella come in Java.

Se voglio eliminare i duplicati all'interno di una query devo utilizzare <font color=red>DISTINCT</font>,
```SQL
SELECT DISTINCT Nome, Citta
FROM Fornitore
WHERE Citta='CS';
```

Come tradurre, coppie di nomi di fornitori della stessa città in SQL? In algebra relazionale la query è: 
$\displaystyle\large\Pi_{\$2,\$5}(Fornitore \bowtie_{\$1\neq\$1\land \$3=\$3}Fornitore)$
ma come si sa la join si può tradurre in un prodotto cartesiano a cui si applica la selezione perciò, $\displaystyle\large\Pi_{\$2,\$5}[\sigma_{\$1\neq\$4\land\$3=\$6}(Fornitore\times Fornitore)]$ ritorna esattamente il risultato e si può tradurre facilmente in SQL come:
```SQL
SELECT F1.Nome, F2.Nome
FROM Fornitore AS F1, Fornitore AS F2
WHERE F1.PIVA!=F2.PIVA AND F1.citta=F2.citta;
```

Ulteriore esempio: coppie nome fornitore, nome merce tale che il fornitore fornisce la merce. In algebra corrisponde a: 
$\displaystyle\large\Pi_{\$2,\$8}[(Fornitore\bowtie_{\$1=\$1} Fornitura)\bowtie_{\$5=\$1}Merce]$ che tradotta con il prod. cartesiano è
$\displaystyle\large\Pi_{\$2,\$8}[\sigma_{\$1=\$4\land\$5=\$7}(Fornitore\times Fornitura\times Merce)]$ in SQL si traduce in
```SQL
SELECT F.Nome, M.Nome
FROM Fornitore F, Fornitura X, Merce M
WHERE F.PIVA=X.Fornitore AND M.Codice=x.Merce;
```
All'interno della FROM quindi non è necessario scrivere AS per ridenominare una tabella. 
SQL presenta il costrutto INNER JOIN che traduce la join di algebra relazionale, ma rende le query molto lunghe ed illeggibile, quindi all'esame NON si utilizza.
La priorità tra i vari costrutti è:
1. FROM
2. WHERE
3. SELECT

---
## Except, Union, Intersect e viste
Come ci sono all'interno dell'algebra relazionale, anche in SQL vi sono gli operandi di sottrazione, unione ed intersezione. Supponiamo di voler tradurre: $\Pi_{\$1}(Fornitore)\setminus\Pi_{\$1}(Fornitura)$ in SQL avremo
```SQL
SELECT PIVA
FROM Fornitore
	EXCEPT
SELECT Fornitore
FROM Fornitura;
```
Perciò il costrutto <font color=red>EXCEPT</font> necessita di 2 SELECT, come d'altrocanto anche <font color=red>UNION</font> e <font color=red>INTERSECT</font> anche se quest'ultimo non è implementato commercialmente.
Le viste sono molto utili per realizzare risultati intermedi. Se ad esempio voglio i fornitori che forniscono esattemente una merce, le viste sono molto comode che realizzare i risultati intermedi di almeno 1 merce fornita ed almeno 2. Per creare una vista si utilizza <font color=red>CREATE VIEW</font>. Esempio di fornitore che fornisce esattamente una merce:
```SQL
CREATE VIEW Almeno1(Fornitore) AS
(SELECT Fornitore
 FROM Fornitura);

CREATE VIEW Almeno2(Fornitore) AS
(SELECT X1.Fornitore
 FROM Fornitura X1, Fornitura X2
 WHERE X1.Fornitore=X2.Fornitore AND X1.Merce!=X2.Merce);

SELECT *
FROM Almeno1;
	EXCEPT
SELECT *
FROM Almeno2;
```
quindi CREATE VIEW NomeVista (Attributi che compongono la vista).

---
## Exists, not exists, in, not in
<font color=red>EXISTS</font> prende come argomento una query e restituisce true quando la query restituisce almeno una riga. La query all'interno della WHERE viene valutata ogni volta per ogni riga.
Esempio nomi fornitore che forniscono almeno una merce e nomi fornitori che non forniscono alcuna merce:
```SQL
SELECT F.Nome
FROM Fornitore F
WHERE EXISTS(SELECT *
			  FROM Fornitura X
			  WHERE X.Fornitore=F.PIVA);

SELECT F.Nome
FROM Fornitore F
WHERE NOT EXISTS(SELECT *
			  FROM Fornitura X
			  WHERE X.Fornitore=F.PIVA);
```
> EXISTS ha solo 1 argomento che è sempre SELECT.

<font color=red>IN</font> serve a stabilire se un valore di un attributo o una combinazione di valore di più attributi, fa parte della tabella riportata a destra. Esempio: 
```SQL
SELECT F.Nome
FROM Fornitore F
WHERE F.PIVA IN (SELECT Fornitore
			  FROM Fornitura);
```
<font color=red>NOT IN</font> serve a stabilire se un valore di un attributo o una combinazione di valore di più attributi, non fa parte della tabella riportata a destra. 
Esempio fornitori che non forniscono merci:
```SQL
SELECT F.Nome
FROM Fornitore F
WHERE F.PIVA NOT IN (SELECT Fornitore
				 FROM Fornitura);
```

Coppie nome fornitore, nome merce tale che le corrispondenti coppie (P.IVA,Codice) appartengono a fornitura:
```SQL
SELECT F.Nome, M.Nome
FROM Fornitore F, Merce M
WHERE (F.PIVA, M.Codice) IN (SELECT Fornitore, Merce
					    FROM Fornitura);
```
Gli attributi della SELECT su fornitura potrebbero essere sbagliati e necessitare di ridenominazione a seconda del DBMS che si utilizza. La query sopra calcola il prodotto cartesiano Fornitore $\times$ Merce e ogni riga prosegue se la coppia P.IVA, Codice è presente nella SELECT.

SQL è un linguaggio che consente di esprimere le query in forma dichiarativa, per dichiarativo si intende un liguaggio che consente di esprimere un risultato dichiarandone la proprietà, questo fa si che la query in SQL è facilmente comprensibile. L'algebra relazionale è invece intrinsecamente procedurale.

---

# Costrutti di aggregazione
I costrutti di aggregazione sono dei possibili calcoli che ad esempio calcolano il valore massimo da un insieme di tuple. Le aggregazioni si riferiscono a fare operazioni di valori che stanno su più righe della tabella attraverso operatori quali SUM, COUNT, MIN, MAX, AVG ecc. Utilizziamo come riferimento il seguente schema relazionale:
Cliente(<u>CF</u>,  Nome, Città, Eta)

| Codice | Nome | Città | Età |
| ------ | ---- | ----- | --- |
| C1     | N1   | CS    | 10  |
| C2     | N2   | RC    | 30  |
| C3     | N3   | RM    | 26  |

Fare
```SQL
SELECT Max(Eta) AS EtaMax
FROM Cliente;
```
Ritorna una tabella con numero di righe diverso da quello di cliente. Ogni qualvolta si usa un operatore di aggregazione la SELECT si rimanda, si esegue la FROM e quindi vengono importate le righe di cliente e vengono filtrate dalla WHERE e prese tutte le righe si valuta l'aggregato e poi si valuta la SELECT. Vale l'ordine di priorità come detto.

<font color=red>COUNT</font> è l'operazione di conteggio che ritorna il numero di volte che l'attributo è specificato, ovvero in cui non è NULL. Distinguiamo 3 casi:
```SQL
SELECT COUNT(CF) AS Numero Clienti
FROM Cliente;

SELECT COUNT(*)
FROM Cliente;
```
La prima query ritorna il numero di tuple contenenti CF in Cliente ovvero il numero di clienti. La seconda query ritorna il numero di righe. Per calcolare il numero di volte distinte si utilizza COUNT DISTINCT. Fare SELECT COUNT di una chiave è uguale a SELECT COUNT(\*).

Contare ad esempio il numero di clienti per ogni città non è possibile che debba fare 100 query. In aiuto viene il costrutto <font color=red>GROUP BY</font>. Esempio:
```SQL
SELECT citta, Count(*)
FROM Cliente
WHERE Nome!='Pasquale'
GROUP BY citta;
```
GROUP BY fa una partizione della tabella iniziale. Quello che sta in GROUP BY non deve stare per forza nella SELECT, è errato invece mettere attributi che non stanno in GROUP BY. 
C'è poi il costrutto HAVING che può ricevere un aggregato qualunque, e considera una condizione sulla tabella raggruppata da GROUP BY.

---

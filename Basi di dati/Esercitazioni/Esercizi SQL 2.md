Dato lo schema:
P(<u>CodP,</u>NomeP,Taglia,Colore,Magazzino)
F(<u>CodF</u>,NomeF,NSoci,Sede)
FP(<u>CodF,CodP,</u>,Qta)
1. Trovare il codice dei prodotti rossi forniti da più di un fornitore
```SQL
SELECT P.CodP
FROM P, FP
WHERE P.Colore="Rosso" AND P.CodP=FP.CodP
GROUP BY P.CodP
HAVING COUNT(*)>1;
```
Dato lo schema:
Studente(<u>Matricola</u>,Nome,Citta)
Corso(<u>Codice</u>,Nome,Docente)
Docente(<u>Matricola</u>,Nome)
Esame(<u>Corso,Studente</u>,Data,Voto)
1. Per ogni studente visualizzare matricola e il voto massimo,minimo e medio conseguito negli esami.
```SQL
SELECT E.Studente, MAX(E.Voto), MIN(E.Voto), AVG(E.Voto)
FROM Esame E
GROUP BY E.Studente;
```
2. Per ogni studente visualizzare matricola, il nome e il voto massimo,minimo e medio conseguito negli esami.
```SQL
SELECT S.Matricola, S.Nome, MAX(E.Voto), MIN(E.Voto), AVG(E.Voto)
FROM Esame E, Studente S
WHERE E.Studente=S.Matricola
GROUP BY S.Matricola, S.Nome;
```
3. Per ogni studente con una media di voti superiore al 28, visualizzare matricola, nome e il voto massimo,minimo e medio conseguito negli esami.
```SQL
SELECT S.Matricola, S.Nome, MAX(E.Voto), MIN(E.Voto), AVG(E.Voto)
FROM Studente S, Esame E
WHERE E.Studente=S.Matricola
GROUP BY S.Matricola, S.Nome
HAVING AVG(E.Voto)>28;
```
4. Per ogni studente con una media di voti superiore a 28, che ha sostenuto esami in almeno 10 date diverse, visualizzare matricola, nome e il voto massimo,minimo e medio conseguito negli esami.
```SQL
CREATE VIEW Al10(Matricola) AS
SELECT S.Matricola AS Matricola
FROM Studente S,Esame E
WHERE S.Matricola=E.Studente
HAVING COUNT(DISTINCT E.Data)>=10;

SELECT S.Matricola, S.Nome, MAX(E.Voto), MIN(E.Voto), AVG(E.Voto)
FROM Studente S, Esame E
WHERE S.Matricola=E.Studente AND S.Matricola IN (SELECT Matricola
									    FROM Al10)
GROUP BY S.Matricola, S.Nome
HAVING AVG(E.Voto)>28;

oppure 

SELECT S.Matricola, S.Nome, MAX(E.Voto), MIN(E.Voto), AVG(E.Voto)
FROM Studente S, Esame E
WHERE E.Studente=S.Matricola
GROUP BY S.Matricola, S.Nome
HAVING AVG(E.Voto)>28 AND COUNT(DISTINCT E.Data)>=10;
```
Dato lo schema:
Persona(<u>CF</u>,Nome,DataNascita)
LezionePrivata(<u>CF,Data,Ora</u>,Istruttore)
Istruttore(<u>Codice</u>,Nome)
1. Per ogni persona visualizzare il codice fiscale ed il numero di lezioni frequentate
```SQL
SELECT L.CF, COUNT(*) AS NumLez
FROM LezionePrivata L
GROUP BY L.CF;
```
2. Per ogni persona visualizzare il codice fiscale, il nome ed il numero di lezioni frequentate
```SQL
SELECT P.CF, P.Nome, COUNT(*) AS NumLez
FROM LezionePrivata L, Persona P
WHERE P.CF=L.CF
GROUP BY P.CF, P.Nome;
```
3. Per ogni persona visualizzare il codice fiscale, il nome, il numero di lezioni frequentate ed il numero di istruttori diversi con cui ha fatto lezione
```SQL
SELECT P.CF,P.Nome, COUNT(*) AS NumLez, COUNT(DISTINCT L.Istruttore) AS NumIst
FROM LezionePrivata L, Persona P
WHERE P.CF=L.CF
GROUP BY P.CF, P.Nome;
```
4. Per ogni persona che ha frequentato almeno 5 lezioni,visualizzare il codice fiscale, il nome, il numero di lezioni frequentate ed il numero di istruttori diversi con cui ha fatto lezione
```SQL 
SELECT P.CF,P.Nome, COUNT(*) AS NumLez, COUNT(DISTINCT L.Istruttore) AS NumIst
FROM LezionePrivata L, Persona P
WHERE P.CF=L.CF
GROUP BY P.CF, P.nome
HAVING COUNT(*)>=5;
```
5. Per ogni persona nata dopo il 1970 che ha frequentato almeno 5 lezioni,visualizzare il codice fiscale, il nome, il numero di lezioni frequentate ed il numero di istruttori diversi con cui ha fatto lezione
```SQL
SELECT P.CF,P.Nome, COUNT(*) AS NumLez, COUNT(DISTINCT L.Istruttore) AS NumIst
FROM LezionePrivata L, Persona P
WHERE P.CF=L.CF AND YEAR(P.DataNascita)>1970
GROUP BY P.CF, P.nome
HAVING COUNT(*)>=5;
```
6. Per ogni persona visualizzare il codice fiscale, il nome, le date in cui ha frequentato almeno una lezione ed il numero di lezioni frequentate in ciascuna di tale date.
```SQL
SELECT P.CF,P.Nome,L.Data,COUNT(*)
FROM LezionePrivata L, Persona P
WHERE L.CF=P.CF
GROUP BY P.CF, P.Nome, L.Data;
```
Dato lo schema:
Corso(<u>Codice</u>,Nome,Anno,Semestre)
Orario(<u>Corso,Giorno,OraInizio</u>,OraFine,Aula)
1. Trovare il codice del corso, nome corso e numero totale di ore di lezione settimanali per i corsi del terzo anno, per cui il numero complessivo di ore di lezione settimanali è superiore a 10 e le lezioni sono in più di tre giorni diversi della settimana.
```SQL
SELECT C.Codice, C.Nome, SUM(O.OraFine-O.OraInizio) 
FROM Orario O, Corso C
WHERE C.Anno="Terzo" AND O.Corso=C.Codice
GROUP BY C.Codice, C.Nome
HAVING COUNT(DISTINCT O.Giorno)>3 AND SUM(O.OraFine-O.OraInizio)>10;
```
Dato lo schema:
Orchestra(<u>Codice</u>,Nome,Direttore,NumEl)
Concerti(<u>Codice</u>,Data,Orchestra,Sale,Prezzo)
Sale(<u>Codice</u>,Nome,Citta,Capienza)
1. Trovare il codice ed il nome delle orchestre con più di 30 elementi che hanno tenuto concerti sia a Torino che a Milano ma non hanno mai tenuto concerti a Bologna.
```SQL
SELECT O.codice, O.Nome
FROM Orchestra O, 
WHERE O.NumEl>30 AND 
	 O.Codice IN (SELECT C.Orchestra
			    FROM Concerti C, Sale S
			    WHERE C.Sale=S.Codice AND S.Citta="Torino")
		 AND IN (SELECT C.Orchestra
			    FROM Concerti C, Sale S
			    WHERE C.Sale=S.Codice AND S.Citta="Milano")
	  AND NOT IN(SELECT C.Orchestra
			    FROM Concerti C, Sale S
			    WHERE C.Sale=S.Codice AND S.Citta="Bologna");
```
Dato lo schema:
Aerei(<u>Matricola</u>, Modello, NumPosti)
Orario(<u>Sigla</u>,CittaPartenza,CittaArrivo,OraPart,OraArr)
Voli(<u>Orario,Aereo,Data</u>,PostiPren)
1. Trovare le tratte, città di partenza, città di arrivo che non sono state mai effettuate con un aereo Boing-747.
```SQL
SELECT DISTINCT O.CittaPartenza, O.CittaArrivo
FROM Orario O
WHERE (O.CittaPartenza,O.CittaArrivo) NOT IN 
				 (SELECT O1.CittaPartenza, O1.CittaArrivo
				  FROM Orario O1,Voli V1, Aerei A1
				  WHERE O1.Sigla=V1.Orario AND V1.Aereo=A1.Matricola AND A1.Modello="Boing-747");

oppure

SELECT DISTINCT O.CittaPartenza, O.CittaArrivo
FROM Orario O1
WHERE NOT EXISTS (SELECT *
			   FROM Orario O2,Voli V, Aerei A
			   WHERE O2.Sigla=V.Orario AND A.Matricola=V.Aereo 
			   AND A.Modello="Boing-747" AND O1.CittaPartenza=O2.CittaPartenza 
			   AND O1.CittaArrivo=O2.CittaArrivo);

```

---
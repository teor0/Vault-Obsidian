![[sql310323.jpg]]
Query 1)
```SQL
CREATE VIEW EventiSi(Evento,Sede) AS
SELECT E.codice AS Evento, E.sede AS Sede
FROM Evento E, Biglietto B1, Biglietto B2
WHERE E.tipologia="Concerto" AND B1.evento=E.codice AND B2.evento=E.codice AND B1.costo="57€" AND B2.costo="58€" AND B1.partecipante!=B2.partecipante;


SELECT S.codice
FROM Sede S, EventiSi E1, EventiSi E2
WHERE E1.Evento!=E2.Evento AND E1.Sede=S.codice AND E2.Sede=S.codice AND S.citta="Ravenna";
```
Query 2)
```SQL
SELECT P1.codicefiscale, P2.codicefiscale
FROM Partecipante P1, Partecipante P2
WHERE P1.codicefiscale!=P2.codicefiscale AND P1.citta="Roma" AND P2.citta="Roma" AND
	NOT EXISTS (SELECT *
			  FROM Biglietto B, Evento E
			  WHERE E.anno=2021 AND B.evento=E.codice 
				  AND B.partecipante=P1.codicefiscale 
				  AND E.codice NOT IN (SELECT E2.codice
								   FROM Biglietto B2, Evento E2
								   WHERE E2.anno=2021 AND B2.evento=E2.codice
									   AND B2.partecipante=P2.codicefiscale))
	AND NOT EXISTS (SELECT *
			  FROM Biglietto B, Evento E
			  WHERE E.anno=2021 AND B.evento=E.codice 
				  AND B.partecipante=P2.codicefiscale 
				  AND E.codice NOT IN (SELECT E2.codice
								   FROM Biglietto B2, Evento E2
								   WHERE E2.anno=2021 AND B2.evento=E2.codice
									   AND B2.partecipante=P1.codicefiscale));
```
Query 3)
```SQL
CREATE VIEW SediSi(Sede,Evento) AS
SELECT E.sede AS Sede, E.codice AS Evento
FROM Evento E
WHERE E.anno=2020
GROUP BY E.sede
HAVING COUNT(*)>10;

CREATE VIEW NumBiglietti(Evento,Numero) AS
SELECT B.evento AS Evento, COUNT(*) AS Numero
FROM Biglietto B, Partecipante P
WHERE P.citta="Cosenza" AND B.costo>40
GROUP BY B.evento;

SELECT SS.Sede
FROM NumBiglietti NB, SediSi SS
WHERE SS.Evento=NB.Evento AND NB.Numero IN (SELECT MAX(NB.Numero)
								    FROM NumBiglietti NB2, SediSi SS2
								    WHERE SS2.Sede=SS.Sede 
									    AND NB2.Evento=SS2.Evento);
```
![[sql040920.jpg]]
Query 1)
```SQL
CREATE VIEW SocSi(Societa) AS
SELECT S.Nome AS Societa
FROM Societa S, Investimento I1, Investimento I2
WHERE I1.Nome!=I2.Nome AND I1.Societa=S.Nome AND I2.Societa=S.Nome;

SELECT C.Nome
FROM Cliente C, Sottoscrizione S1, Sottoscrizione S2 SocSi SS1, SocSi SS2, Societa So1, Societa So2, Investimento I1, Investimento I2
WHERE C.citta="Cosenza" AND S1.cliente=C.codiceFiscale AND SS1.Societa!=SS2.Societa
	AND S1.investimento!=S2.investimento AND S1.investimento=I1.Nome 
	AND I1.Societa=SS1.Societa AND S2.investimento=I2.Nome 
	AND I2.Societa=SS2.Societa AND I1.Nome!=I2.Nome;
```
Query 2)
```SQL
SELECT C.codiceFiscale
FROM Cliente C
WHERE C.codiceFiscale NOT IN (SELECT S.cliente
			   FROM Sottoscrizione S, Investimento I, Societa So
			   WHERE So.citta="Cosenza" AND I.tipoInvestimento!="obbligazione"
				    AND S.Investimento=I.Nome AND I.Societa=So.Nome);
```
Query 3)
```SQL
CREATE View ClientiSi(Citta,Cliente) AS
SELECT C.citta AS Citta, C.codiceFiscale AS Cliente
FROM Cliente C, Investimento I, Sottoscrizione S
WHERE I.tipoInvestimento="fondoAzionario" AND S.cliente=C.codiceFiscale 
	AND S.investimento=I.Nome
GROUP BY C.citta
HAVING COUNT(S.Investimento)>=100;


CREATE VIEW Spesa(Cliente,Investimento,Totale) AS
SELECT C.codiceFiscale AS Cliente, I.Nome AS Investimento, 
	SUM(S.NumeroQuote*ValoreSingolaQuota) AS Totale
FROM Cliente C, Sottoscrizione S, Investimento I
WHERE C.codiceFiscale=S.cliente AND S.investimento=I.Nome;

SELECT CS.citta, CS.Cliente
FROM ClientiSi CS, Spesa S
WHERE CS.Cliente=S.Cliente AND S.Totale IN (SELECT MAX(S2.Totale)
								    FROM Spesa S2);

```

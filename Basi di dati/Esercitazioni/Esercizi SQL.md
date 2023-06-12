---
tag: #basi 
created: 2022-12-13 12:48:25
updated: 2022-12-13 12:48:25
---
#basi 

Fornitori di CS che non forniscono merci di marca $\alpha$
FornitoriNo=$\displaystyle\large\Pi_{\$4}[\sigma_{\$3=\alpha}(Merce)\bowtie_{\$1=\$2}Fornitura)]$
Query algebra: $\displaystyle\large\Pi_{\$1}[\sigma_{\$3='CS'}(Fornitore)]\setminus FornitoriNo$,
in particolare la join la traduco come:
$\displaystyle\large\Pi_{\$5}\{\sigma_{\$1=\$5}[\sigma_{\$3=\alpha}(Merce)\times Fornitura]\}$
```SQL
CREATE VIEW FornitoriNo(PIVA) AS
SELECT X.Fornitore
FROM Merce M, Fornitura X
WHERE M.Marca='α' AND (M.Codice=X.Merce)


SELECT PIVA
FROM Fornitore
WHERE Citta=CS
	EXCEPT
SELECT *
FROM FornitoriNo;
```
![[trattestazauto.jpg]]
![[querystaztrat.jpg]]
![[eser9staz.jpg]]
Query 1)
```SQL
CREATE VIEW TrattaSi(Tratta) AS:
SELECT A1.tratta AS Tratta
FROM Autobus A1, Autobus A2
WHERE A1.codice!=A2.codice AND A1.tipologia=A2.tipologia AND A1.tratta=A2.tratta;

SELECT S.Nome
FROM Stazione S, Tratta T1, Tratta T2, TrattaSi TS1, TrattaSi Ts2
WHERE T1.codice!=T2.codice AND T1.codice=TS1.Tratta AND T2.codice=TS2.Tratta AND T1.stazionePartenza=T2.stazionePartenza AND S.codice=T1.stazionePartenza;
```
Query 2)
```SQL
SELECT A.tipologia
FROM Autobus A
WHERE NOT EXISTS (SELECT *
			  FROM Stazione S, Tratta T
			  WHERE S.citta="Roma" AND S.codice=T.stazionePartenza AND T.distanza<"200" AND T.codice=A.tratta);
```
Query 3)
```SQL
SELECT A.tipologia
FROM Autobus A
WHERE NOT EXISTS (SELECT *
			  FROM Stazione S, Tratta T
			  WHERE S.citta!="Roma" and S.codice=T.stazionePartenza AND T.codice=A.tratta);
```
Query 4)
```SQL
CREATE VIEW TratteSi(Tipologia)
(SELECT A.tipologia AS Tipologia
FROM Stazione S, Tratta T, Autobus A
WHERE S.citta="Roma" and S.codice=T.stazionePartenza AND T.codice=A.tratta);

CREATE VIEW TratteNo(Tipologia) AS
(SELECT A.tipologia AS Tipologia
FROM Stazione S, Tratta T, Autobus A
WHERE S.citta!="Roma" and S.codice=T.stazionePartenza AND T.codice=A.tratta);

SELECT TS.Codice
FROM TratteSi TS
EXCEPT
SELECT TN.codice
FROM TratteNo TN;
```
Query 5)
```SQL
CREATE VIEW AutoNo(Codice,Tipologia) AS
(SELECT A.codice AS Codice, A.tipologia AS Tipologia
FROM Autobus A, Tratta T, Stazione S
WHERE (S.citta="Roma" AND T.distanza>=200) AND S.codice=T.stazionePartenza AND T.codice=A.tratta);

SELECT A.tipologia
FROM Autobus A
WHERE A.tipologia NOT IN (SELECT AN.Tipologia
					 FROM AutoNo AN);
```
Query 6)
```SQL
CREATE VIEW Almeno2 (Tipologia) AS
(SELECT A1.tipologia AS Tipologia
FROM Autobus A1, Autobus A2, Tratta T, Stazione S
WHERE S.citta="Roma" AND T.stazionePartenza=S.codice AND A1.tratta=A2.tratta AND A1.tratta=T.codice AND A1.codice!=A2.codice;)

CREATE VIEW Almeno1 (Tipologia) AS
(SELECT A1.tipologia AS Tipologia
FROM Autobus A, Tratta T, Stazione S
WHERE S.citta="Roma" AND T.stazionePartenza=S.codice AND A.tratta=T.codice;)

SELECT Tipologia
FROM Almeno1
EXCEPT
SELECT Tipologia
FROM Almeno2;
```
Query 7)
```SQL
CREATE VIEW StazioneSi(Tipo,Stazione) AS
(SELECT A.tipologia AS Tipo, T.stazionePartenza AS Stazione
FROM Tratta T, Autobus A
WHERE A.tratta=T.codice;)

CREATE VIEW StazioneNo(Tipo,Stazione) AS
(SELECT A.tipologia AS Tipo, T.stazionePartenza AS Stazione
FROM Autobus A, Tratta T
EXCEPT
SELECT Tipo, Stazione
FROM StazioneSi;)

CREATE VIEW PSSN(SA, SB) AS
(SELECT SS.Stazione AS SA, SN.Stazione AS SB
FROM StazioneSi SS, StazioneNo SN
WHERE SS.Stazione!=SN.Stazione AND SS.Tipo=SN.Tipo;)

CREATE VIEW PNSS(SA, SB) AS
(SELECT SN.Stazione AS SA, SS.Stazione AS SB
FROM StazioneSi SS, StazioneNo SN
WHERE SS.Stazione!=SN.Stazione AND SS.Tipo=SN.Tipo;)

SELECT S1.codice, S2.codice
FROM Stazione S1, Stazione S2
WHERE (S1.codice, S2.codice) NOT IN (SELECT SA,SB
						      FROM PSSN)
	AND (S1.codice, S2.codice) NOT IN (SELECT SA, SB
							     FROM PNSS)
	AND S1.codice!=S2.codice;
```
Query 9)
```SQL
CREATE VIEW CittaStazioni(Citta, nStazioni) AS
(
SELECT S.citta AS Citta, COUNT(S.codice) AS nStazioni
FROM Stazione S
GROUP BY S.citta;
)

CREATE VIEW CittaSi(Citta) AS
(
SELECT CS.citta
FROM CittaStazioni CS
WHERE CS.nStazioni > (SELECT COUNT(S.codice)
				  FROM Stazione S
				  WHERE S.citta="Roma");
)

CREATE VIEW Distanza(Citta, Tipologia, Distanza) AS
(
SELECT S.citta AS Citta, A.tipologia AS Tipologia, SUM(T.distanza) AS Distanza
FROM Stazione S, Autobus A, Tratta T
WHERE A.tratta=T.codice AND T.stazionePartenza=S.codice
GROUP BY S.citta, A.tipologia;
)

SELECT D1.citta AS Citta, D1.tipologia AS Tipologia
FROM CittaSi CS, Distanza D1
WHERE CS.citta=D.citta AND D.distanza IN (SELECT MIN(D2.distanza)
								  FROM Distanza D2
								  WHERE D2.citta=CS.citta
								  GROUP BY D2.citta);

```
---
![[tracciaparruc.jpg]]
Query 1)
```SQL
CREATE VIEW ParrSi(Parrucchiere, Casamadre) AS
(
SELECT P.codice AS Parrucchiere, P.casamadre AS Casamadre
FROM Parrucchiere P
WHERE (P.citta="Roma" OR P.citta="Firenze") 
AND P.codice IN (SELECT S1.parrucchiere
			 FROM Servizio S1, Servizio S2, Cliente C
			 WHERE C.eta>=18 AND C.eta<=25 AND C.codice=S1.Cliente AND S1.parrucchiere=S2.parrucchiere AND C.codice=S2.cliente);
)

SELECT C.codice
FROM ParrSi P1, ParrSi P2, CasaMadre C
WHERE C.annoNascita>=1980 AND C.annoNascita<=2015 AND P1.codice!=P2.codice AND P1.Casamadre=C.codice AND P2.Casamadre=C.codice;
```
Query 2)
```SQL
SELECT P.nome
FROM Parrucchiere P
WHERE P.citta="Roma" AND NOT EXISTS (SELECT *
							  FROM Servizio S, Cliente C
							  WHERE C.genere="Maschile" AND YEAR(S.data)=2018 AND S.tipologia="Colore" AND S.parrucchiere=P.codice AND S.cliente=C.codice);
```
Query 3)
```SQL
SELECT P.nome
FROM Parrucchiere P
WHERE P.codice NOT IN (SELECT S.parrucchiere
				   FROM Servizio S, Cliente C
				   WHERE C.genere="Maschile" AND YEAR(S.data)=2018 AND S.tipologia!="Colore" AND S.cliente=C.cliente)
	AND P.citta="Matera"
```
Query 6)
```SQL
CREATE VIEW ClienteSi(Cliente, Numero) AS
(
SELECT S.cliente AS Cliente, COUNT(S) AS Numero
FROM Servizio S, Parrucchiere P, Casamadre C
WHERE S.tipologia="Taglio" AND YEAR(S.data=2018) AND S.parrucchiere=P.codice AND P.casamadre=C.codice AND C.nome="Jean Luis David"
GROUP BY S.cliente;
)

SELECT C1.citta, C1.Nome
FROM Cliente C1, ClienteSi CS1
WHERE C1.codice=CS1.Cliente AND 
	 CS1.Numero IN (SELECT MAX(CS2.Numero)
				 FROM ClienteSi CS2, Cliente C2
				 WHERE C2.codice=CS2.Cliente AND C1.citta=C2.citta);
GROUP BY C1.citta;
```


---
![[tracciaconc.jpg]]
![[eserconc.jpg]]
```SQL
CREATE VIEW GuidatoriSi(Guidatore, Numero) AS
(
SELECT A.guidatore AS Guidatore, COUNT(A) AS Numero
FROM Acquisto A, Automobile Au
WHERE A.anno>=1998 AND A.anno<=2015 AND Au.marca="FIAT" AND Au.codice=A.automobile
GROUP BY A.Guidatore;
)

SELECT G1.citta AS Citta, GS1.Numero AS Numero
FROM Guidatore G1, GuidatoriSi GS1
WHERE G1.codice=GS1.Guidatore AND GS1.Numero IN (SELECT MAX(GS2.Numero)
									 FROM Guidatore G2, GuidatoriSi GS2
									 WHERE G2.codice=GS2.Guidatore AND G2.citta=G1.citta);
```
---
![[traccpisci.jpg]]
![[querypisci.jpg]]
Query 1)
```SQL
SELECT O1.Matricola, O2.Matricola
FROM Operatore O1, Operatore O2
WHERE O1.citta!=O2.citta AND NOT EXISTS (SELECT *
								 FROM Presenza P
								 WHERE P.operatore=O1.matricola AND 
								 (P.evento,O2.matricola) NOT IN 
								 (SELECT Evento, Operatore
								 FROM Presenza P2))
					AND NOT EXISTS (SELECT *
								 FROM Presenza P
								 WHERE P.operatore=O2.matricola AND 
								 (P.evento,O1.matricola) NOT IN 
								 (SELECT Evento, Operatore
								 FROM Presenza P2))
```
Query 2)
```SQL
CREATE VIEW EventiSi(Evento) AS
SELECT E.nome
FROM Evento E, Presenza P
WHERE E.nome=P.evento AND P.mansione="Sorvegliante"
GROUP BY E.nome
HAVING COUNT(P.operatore)>=30;


SELECT E.Nome AS Nome 
FROM Evento E1, EventiSi ES1, Piscina P1
WHERE ES1.Evento=E1.Nome AND E1.piscina=P1.nome 
	AND P1.area IN (SELECT MIN(P2.area)
				 FROM Piscina P2);
```

---
![[170211.jpg]]
Query 1)
```SQL
SELECT S.citta
FROM Pratica P1, Pratica P2, Ufficio U1, Ufficio U2 Supervisore S, Verifica V1, Verifica V2
WHERE P1.anno=2010 AND P2.anno=P1.anno AND P1.ufficio=U1.Nome AND U1.citta="Cosenza" AND  P2.ufficio=U2.Nome AND U2.citta="Cosenza" AND P1.numero!=P2.numero AND V1.supervisore=S.cf AND V1.pratica=P1.numero AND V2.supervisore=S.cf AND V2.pratica=P2.numero;
```
Query 2)
```SQL
SELECT S.nome
FROM Supervisori S
WHERE NOT EXISTS (SELECT *
			   FROM Pratica P, Verifica V, Ufficio U
			   WHERE P.anno<1999, P.ufficio=U.Nome AND U.citta="Roma" AND V.supervisore=S.cf AND V.pratica=P.numero;
```
Query 3)
```SQL
CREATE VIEW PraticheNO(Pratica) AS
SELECT V.Pratica AS Pratica
FROM Verifica V, Supervisore S
WHERE V.Supervisore=S.cf AND S.citta!="Milano";

SELECT P.Numero
FROM Pratica P
WHERE P.Numero NOT IN (SELECT Pratica
				  FROM PraticheNO);
```
Query 4)
```SQL
CREATE VIEW SuperSi(Supervisore) AS
SELECT V.Supervisore AS
FROM Verifica V
GROUP BY V.Supervisore
HAVING COUNT(*)>10;

CREATE VIEW Pratiche(Pratica,NumeroDoc) AS
SELECT D.Pratica, COUNT(*) AS NumeroDoc
FROM Documento D
GROUP BY D.Pratica;

SELECT S.Supervisore, P.Pratica
FROM SuperSi S, Verifica V, Pratiche P
WHERE S.Supervisore=V.Supervisore AND V.Pratica=P.Pratica 
	AND P.NumeroDoc IN (SELECT MAX(P2.NumeroDoc)
					FROM Pratiche P2, Verifica V2, SuperSi S2
					WHERE S2.Supervisore=V2.Supervisore AND V2.Pratica=P2.Pratica);

```

---
![[sql100311.jpg]]
Query 1)
```SQL
SELECT A.Nome
FROM Esame E1, Esame E2, Materia M1, Materia M2, Docente D1, Docente D2, Aula A
WHERE A.Cubo=41 AND A.Nome=E1.Aula AND E1.Aula=E2.Aula AND YEAR(E1.data)=2010 AND YEAR(E2.data)=2010 AND E1.Materia=M1.Codice AND M1.Docente=D1.Nome AND D1.Dipartimento="DEIS" AND E2.Materia=M2.Codice AND M2.Docente=D2.Nome AND D2.Dipartimento="DEIS" AND (E1.data!=E2.data OR E1.Materia!=E2.Materia); 
```
Query 2)
```SQL
SELECT M.Nome
FROM Docente D, Materia M
WHERE M.Crediti>4 AND M.Docente=D.Codice AND D.Dipartimento="DEIS" 
	AND NOT EXISTS (SELECT *
				 FROM Esame E, Aula A
				 WHERE E.Materia=M.Codice AND E.Aula=A.Nome AND A.Piano="Primo"); 
```
Query 3)
```SQL
SELECT M1.Codice, M2.Codice
FROM Materia M1, Materia M2
WHERE M1.Codice!=M2.Codice AND 
						NOT EXISTS(SELECT *
						FROM Esame E1
						WHERE E1.Materia=M1.Codice AND NOT EXISTS 
							(SELECT *
							 FROM Esame E2
							 WHERE E2.Materia=M2.Codice AND E1.Aula=E2.Aula))
					AND 
						NOT EXISTS(SELECT *
						FROM Esame E1
						WHERE E1.Materia=M2.Codice AND NOT EXISTS 
							(SELECT *
							 FROM Esame E2
							 WHERE E2.Materia=M1.Codice AND E1.Aula=E2.Aula)); 

oppure

CREATE VIEW MateriaAulaNo(Materia,Aula) AS
SELECT M.Codice AS Materia, A.Nome AS Aula
FROM Materia M, Aula A
WHERE (M.Codice,A.Nome) NOT IN (SELECT E.Materia, E.Aula
						  FROM Esame E);

SELECT M1.Codice, M2.Codice
FROM Materia M1, Materia M2
WHERE M1.Codice!=M2.Codice AND 
						NOT EXISTS(SELECT *
								 FROM Esame E, MateriaAulaNo MA
								 WHERE E.Materia=M1.Codice 
								 AND E.Aula=MA.Aula AND MA.Materia=M1.Codice)
					AND 
						NOT EXISTS(SELECT *
								 FROM Esame E, MateriaAulaNo MA
								 WHERE E.Materia=M2.Codice 
								 AND E.Aula=MA.Aula AND MA.Materia=M2.Codice);
```
Query 4)
```SQL
CREATE VIEW DocSi(Docente) AS
SELECT D.Nome AS Docente
FROM Docente D, Materia M
WHERE D.Nome=M.Docente
GROUP BY D.nome
HAVING SUM(M.Crediti)>12;

CREATE VIEW MateriaAule(Materia, NumAule) AS
SELECT E.Materia AS Materia, COUNT(DISTINCT(E.Aula)) AS NumAule
FROM Esame E
GROUP BY E.Materia;

SELECT DS.Docente, MA.Materia
FROM DocSi DS, MateriaAule MA, Materia M
WHERE DS.Docente=M.Docente AND M.Codice=MA.Materia 
	AND MA.NumAule IN (SELECT MAX(MA.NumAule)
				    FROM MateriaAule MA, Materia M, DocSi DS
				    WHERE M.Codice=MA.Materia AND DS.Docente=M.Docente);
```

---
![[sql040220.jpg]]
Query 1)
```SQL
CREATE VIEW CanzoniSi(Canzone) AS
SELECT CA.Codice
FROM CD C1, CD C2, Vendita V1, Vendita V2, Negozio N1, Negozio N2, Canzone CA
WHERE C1.Codice!=C2.Codice AND V1.CD=C1.Codice AND V2.CD=C2.Codice
		AND N1.Codice=V1.Negozio AND N2.Codice=V2.Negozio AND N1.Citta="Torino"
		AND N2.Citta="Torino" AND CA.CD=C1.Codice AND CA.CD=C2.Codice;


SELECT M.Codice
FROM Musicista M, Canzone C1, Canzone C2
WHERE M.Codice=C1.Musicista AND M.Codice=C2.Musicista AND C1.Codice!=C2.Codice 
		AND C1.Codice IN (SELECT CS.Canzone
					   FROM CanzoniSi CS)
		AND C2.Codice IN (SELECT CS.Canzone
					   FROM CanzoniSi CS)
		AND YEAR(M.DataNascita)>=1950 AND YEAR(M.DataNascita)<=1990;
```
Query 2)
```SQL
CREATE VIEW CDNo(CD) AS
SELECT C.Codice AS CD
FROM Musicista M, Canzone CA, CD C
WHERE M.Cognome="Rossi" AND CA.Musicista=M.Codice AND C.Codice=CA.CD;

SELECT N.Nome
FROM Negozio N
WHERE N.Citta="Roma" AND NOT EXISTS (SELECT *
							  FROM Vendita V, CDNo CN
							  WHERE V.Cd=CN.CD AND V.Negozio=N.Codice);
```
Query 3)
```SQL
SELECT M1.Codice, M2.Codice
FROM Musicista M1, Musicista M2
WHERE M1.Codice!=M2.codice
		AND NOT EXISTS(SELECT *
					FROM Canzone C, CD CD, Vendita V
					WHERE C.Musicista=M1.Codice AND C.CD=CD.Codice 
					AND V.CD=CD.Codice 
					AND V.Negozio NOT IN (SELECT V.Negozio
								FROM Canzone C, CD CD, Vendita V
								WHERE M2.codice=C.Musicista AND C.CD=CD.codice
									AND V.CD=CD.Codice))
		AND NOT EXISTS(SELECT *
					FROM Canzone C, CD CD, Vendita V
					WHERE C.Musicista=M2.Codice AND C.CD=CD.Codice 
					AND V.CD=CD.Codice 
					AND V.Negozio NOT IN (SELECT V.Negozio
								FROM Canzone C, CD CD, Vendita V
								WHERE M1.codice=C.Musicista AND C.CD=CD.codice
									AND V.CD=CD.Codice));
```
Query 4)
```SQL
CREATE VIEW CittaSi(Citta) AS
SELECT N.Citta AS Citta
FROM Negozio N
GROUP BY N.citta
HAVING COUNT(N.CodNegozio)>=100;

SELECT N.CodNegozio
FROM CittaSi C, Vendita V, Negozio N
WHERE C.Citta=N.Negozio AND N.CodNegozio=V.Negozio 
	AND YEAR(V.Data)=2018
	AND V.NumeroCopieVenduteIN (SELECT MAX(V2.NumeroCopieVendute)
						    FROM Vendita V2, Negozio N2
						    WHERE N2.Citta=C.Citta AND N2.CodNegozio=V2.Negozio 
							    AND YEAR(V2.Data)=2018);
```
---
![[200123.jpg]]
Query 1)
```SQL
CREATE VIEW StanzeSi(Codice,Sede) AS
SELECT St.codice AS Codice St.Sede AS Sede
FROM Stanza St, Utente U1, Utente U2, Autorizzazione A1, 
	Autorizzazione A2, Sede S
WHERE St.Destinazione="Archivio" AND U1.eta>50 AND U2.eta>50 AND U1.codiceFiscale!=U2.codiceFiscale AND A1.Utente=U1.codiceFiscale 
	AND A2.Utente=U2.codiceFiscale AND St.Sede=S.codice AND A1.Sede=St.Codice 
	AND A2.Sede=St.codice; 

SELECT S.codice 
FROM Sede S, StanzeSi SS1, StanzaSi SS2
WHERE S.citta="Agrigento" AND SS1.Codice!=SS2.Codice AND SS1.Sede=S.codice 
	AND SS2.Sede=S.codice;
```
Query 2)
```SQL
SELECT S.codice
FROM Sede S
WHERE S.citta="Mestre" AND NOT EXISTS (SELECT *
							    FROM Autorizzazione A, Utente U, Stanza St
							    WHERE A.utente=U.codiceFiscale 
								    AND A.sede=St.codice
								    AND St.sede=S.codice 
								    AND U.eta>=40);
```
Query 3)
```SQL
CREATE VIEW SediSi(Sede,Stanza) AS
SELECT S.sede AS Sede, S.codice AS Stanza
FROM Stanza S
GROUP BY S.sede
HAVING COUNT(S.codice)>=20;

CREATE VIEW StanzaDurata(Sede,DurataMedia) AS
SELECT A.sede AS Stanza, AVG(A.Durata) AS DurataMedia
FROM Autorizzazione A
GROUP BY A.sede

SELECT SS.Stanza
FROM SediSi SS, StanzaDurata SD
WHERE SD.Stanza=SS.Stanza AND (SD.Durata) IN(SELECT MAX(SD.Durata))
							  FROM Autorizzazione A, SediDurata SD2, Utente U
							  WHERE U.citta="Bergamo" AND A.utente=U.codice 
								  AND A.sede=SD2.Stanza);
```

---
![[sql181122.jpg]]
Query 1)
```SQL
CREATE VIEW UffSi(Ufficio) AS
SELECT U.codice AS Ufficio
FROM Consulenza C1, Consulenza C2, Ufficio U
WHERE YEAR(C1.Data)=2022 AND YEAR(C2.Data)=2022 AND C1.durataMinuti>=60 
	AND C2.durataMinuti>=60 AND C1.ufficio=U.codice AND C2.ufficio=U.codice; 

SELECT P.cognome
FROM UffSi US1, UffSi US2, Professionista P, Ufficio U1, Ufficio U2
WHERE P.citta="Matera" AND US1.Ufficio=U1.codice AND US2.Ufficio=U2.codice 
	AND US1.Ufficio!=US2.Ufficio AND U1.codice!=U2.codice 
	AND U1.Professionista=P.codiceFiscale AND U2.Professionista=P.codiceFiscale;
```
Query 2)
```SQL
SELECT P1.codiceFiscale, P2.codiceFiscale
FROM Professionista P1, Professionista P2
WHERE P1.codiceFiscale!=P2.codiceFiscale AND P1.citta="Roma" AND P2.citta="Roma" 
		AND NOT EXISTS (SELECT *
					 FROM Consulenza C, Ufficio U
					 WHERE U.professionista=P1.codiceFiscale
						 AND C.ufficio=U.codice AND YEAR(C.data)=2020
						 AND C.cliente 
						 NOT IN (SELECT C2.cliente
							    FROM Consulenza C2, Ufficio U2
							    WHERE C2.ufficio=U2.codice 
								    AND U2.professionista=P2.codiceFiscale
								    AND YEAR(C2.data)=2020))
		AND NOT EXISTS (SELECT *
					 FROM Consulenza C, Ufficio U
					 WHERE U.professionista=P2.codiceFiscale
						 AND C.ufficio=U.codice AND YEAR(C.data)=2020
						 AND C.cliente 
						 NOT IN (SELECT C2.cliente
							    FROM Consulenza C2, Ufficio U2
							    WHERE C2.ufficio=U2.codice 
								    AND U2.professionista=P1.codiceFiscale
								    AND YEAR(C2.data)=2020))
```
Query 3)
```SQL
CREATE VIEW PrSi(CF) AS
SELECT P.codiceFiscale AS CF
FROM Professionista P
GROUP BY P.codiceFiscale
HAVING COUNT(P.ufficio)>=4;


CREATE VIEW ClM(Cliente,Professionista,DurataMedia) AS
SELECT Cl.codiceFiscale, P.CF,AVG(SUM(C.durataMinuti))
FROM Consulenza C, Cliente Cl, PrSi P, Ufficio U
WHERE C.cliente=Cl.codiceFiscale AND U.professionista=P.CF AND C.ufficio=U.codice
GROUP BY Cl.codiceFiscale, P.CF;


SELECT P.CF, CM1.Cliente
FROM PrSi P, ClM CM1
WHERE CM.Professionista=P.CF AND CM1.durataMinuti 
						IN (SELECT MAX(CM2.durataMinuti)
						    FROM ClM CM2
						    WHERE CM2.Professionista=P.Professionista)
GROUP BY P.CF;
```
---
![[sql240322.jpg]]
Query 1)
```SQL
CREATE VIEW AppSi(Condominio,Interno) AS
SELECT AP.condominio AS Condominio, AP.interno AS Interno
FROM Appartamento AP, Affitto A1, Affitto A2, Inquilino I1, Inquilino I2
WHERE YEAR(A1.dataInizio)=2021 AND YEAR(A2.dataInizio)=2021 
	AND I1.codiceFiscale!=I2.codiceFiscale AND A1.inquilino=I1.codiceFiscale
	AND A2.inquilino=I2.codiceFiscale AND A1.appCond=AP.condominio 
	AND A1.appInterno=AP.interno AND A2.appCond=AP.condominio 
	AND A2.appInterno=AP.interno;

SELECT C.nome
FROM Condominio C, AppSi AP1, AppSi AP2
WHERE C.citta="Rende" AND AP1.interno!=AP2.interno 
	AND AP1.condominio=C.nome AND AP2.condominio=C.nome;
```
Query 2)
```SQL
SELECT I1.nome , I2.nome
FROM Inquilino I1, Inquilino I2
WHERE I1.codiceFiscale!=I2.codiceFiscale 
	AND NOT EXISTS (SELECT *
				 FROM Affitto A, Condominio C, Appartamento AP
				 WHERE C.citta="Cosenza" AND AP.condominio=C.nome
					 AND A.appCond=AP.condominio AND A.appInterno=AP.interno
					 AND A.inquilino=I1.codiceFiscale AND (A.appCond,A.appInterno) 
					 NOT IN (SELECT A.appCond, A.appInterno
						    FROM Affitto A, Condominio C, Appartamento AP
						    WHERE C.citta="Cosenza" AND AP.condominio=C.nome
						 AND A.appCond=AP.condominio AND A.appInterno=AP.interno
						 AND A.inquilino=I2.codiceFiscale))
	AND NOT EXISTS (SELECT *
				 FROM Affitto A, Condominio C, Appartamento AP
				 WHERE C.citta="Cosenza" AND AP.condominio=C.nome
					 AND A.appCond=AP.condominio AND A.appInterno=AP.interno
					 AND A.inquilino=I2.codiceFiscale AND (A.appCond,A.appInterno) 
					 NOT IN (SELECT A.appCond, A.appInterno
						    FROM Affitto A, Condominio C, Appartamento AP
						    WHERE C.citta="Cosenza" AND AP.condominio=C.nome
						 AND A.appCond=AP.condominio AND A.appInterno=AP.interno
						 AND A.inquilino=I1.codiceFiscale))
```
Query 3)
```SQL
CREATE VIEW CondSi(Condominio) AS
SELECT C.nome AS Condominio
FROM Condominio C, Affitto A, Appartamento AP
WHERE AP.condominio=C.nome AND A.appCond=AP.condominio AND A.appInterno=AP.interno
	AND YEAR(A.dataInizio)=2022
GROUP BY C.nome
HAVING SUM(A.durataMesi*A.ImportoMensile)>=3000;

SELECT AP.condominio, AP.interno
FROM Affitto A, CondSi CS, Appartamento AP
WHERE AP.condominio=CS.Condominio AND A.appCond=AP.condominio 
	AND A.appInterno=AP.interno AND YEAR(A.dataInizio)=2022
	AND (A.appCond,A.appInterno,A.importoMensile) 
	IN (SELECT A.appCond, A.appInterno, MAX(A.importoMensile)
	    FROM Condominio C, Affitto A, Appartamento AP 
	    WHERE AP.condominio=CS.Condominio AND A.appCond=AP.condominio 
			AND A.appInterno=AP.interno AND YEAR(A.dataInizio)=2022);
```
![[sql6622.jpg]]
Query 1)
```SQL
CREATE VIEW ClSi(CF) AS
SELECT C.codiceFiscale AS CF
FROM Cliente C, Ordine O1, Ordine O2, Articolo A1, Articolo A2
WHERE A1.codice!=A2.codice AND A1.tipologia!=A2.tipologia AND O1.cliente=C.codiceFiscale
	AND O2.cliente=C.codiceFiscale AND YEAR(O1.data)=2021 AND YEAR(O2.data)=2021 
	AND O1.articolo!=O2.articolo AND O1.articolo=A1.codice AND O2.articolo=A2.codice
	AND C.citta="Siena";

SELECT A.codice
FROM ClSi CS1, ClSi CS2, Articolo A, Ordine O1, Ordine O2
WHERE CS1.CF!=CS2.CF AND A.tipologia="Giacca" AND O1.articolo=A.codice AND
	O1.articolo=A.codice AND O2.cliente=CS1.CF AND O1.cliente=CS2.CF;
```
Query 2)
```SQL
SELECT A1.codice, A2.codice
FROM Articolo A1, Articolo A2, Azienda AZ1, Azienda AZ2
WHERE A1.codice!=A2.codice AND A1.azienda=AZ1.nome AND A2.azienda=AZ1.nome AND 
	AZ1.nome!=AZ2.nome AND AZ1.citta=AZ2.citta 
		AND NOT EXISTS (SELECT *
					 FROM Cliente C, Ordine O
					 WHERE C.eta>=18 AND YEAR(O.data)=2022 
						 AND O.cliente=C.codiceFiscale AND O.articolo=A1.codice
						 AND O.cliente NOT IN(SELECT C2.codiceFiscale
										  FROM Cliente C2, Ordine O2
										  WHERE C2.eta>=18 AND
											  YEAR(O2.data)=2022 AND
											  O2.cliente=C2.codiceFiscale
											  AND O2.articolo=A2.codice))
		AND NOT EXISTS (SELECT *
					 FROM Cliente C, Ordine O
					 WHERE C.eta>=18 AND YEAR(O.data)=2022 
						 AND O.cliente=C.codiceFiscale AND O.articolo=A2.codice
						 AND O.cliente NOT IN(SELECT C2.codiceFiscale
										  FROM Cliente C2, Ordine O2
										  WHERE C2.eta>=18 AND
											  YEAR(O2.data)=2022 AND
											  O2.cliente=C2.codiceFiscale
											  AND O2.articolo=A1.codice));
```
Query 3)
```SQL
CREATE VIEW AzSi(Azienda) AS
SELECT A.azienda AS Azienda
FROM Articolo A
GROUP BY A.azienda
HAVING COUNT(A.codice)>=200;

CREATE VIEW ClSi(Cliente) AS
SELECT O.cliente AS Cliente
FROM AzSi AZS, Azienda A, Ordine O, Articolo AR
WHERE A.nome=AZS.Azienda AND A.citta="Agrigento" AND O.articolo=AR.codice 
	AND AR.azienda=A.nome
GROUP BY O.cliente
HAVING COUNT(O.articolo)>=10;

SELECT C.codiceFiscale
FROM AzSi AZS, Cliente C, Ordine O, Articolo A
WHERE A.azienda=AZS.Azienda AND O.articolo=A.codice AND YEAR(O.data)=2020 
	AND O.cliente=C.codiceFiscale 
		AND MAX(importo) IN (SELECT SUM(O.importo)
						 FROM ClSi CS, Ordine O
						 WHERE O.cliente=CS.CF);
```
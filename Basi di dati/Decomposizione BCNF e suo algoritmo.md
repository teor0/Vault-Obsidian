---
tag: #basi 
created: 2023-01-09 10:40:43
updated: 2023-01-09 10:40:43
---
#basi 
[[Grafo delle dipendenze, chiusura, compattezza e regole per la ridondanza]]
# Decomposizione BCNF
Prendiamo lo schema di relazione, Esame(Matricola,Nome,Materia,Docente,Data,Voto) e calcolate le dipendenze funzionali otteniamo:
- Materia$\rightarrow$Docente
- Matricola$\rightarrow$Nome
- Matricola,Materia$\rightarrow$Data,Voto

con possibili chiavi, Keys={Matricola Materia}. Questo schema non è in BCNF, in quanto traspare ridondanza dalle dipendenze funzionali. Per renderlo BCNF lo decomponiamo in:
- Studente(<u>Matricola</u>,Nome) per Materia$\rightarrow$Docente
- Insegnamento(<u>Materia</u>,Docente) per Matricola$\rightarrow$Nome
- Esame2(<u>Matricola,Materia</u>,Data,Voto) per Matricola,Materia$\rightarrow$Data,Voto

Ho decomposto uno schema di relazione in 3, passando ad un nuovo schema di database. Il nuovo schema di database è privo di ridondanza in quanto, ogni schema di relazione è BCNF. Questa decomposizione si chiama <font color=orange> decomposizione BCNF </font>, perché ogni schema è BCNF e le dipendenze riportate da ciascuno schema sono la proiezione delle dipendenze iniziali. Le informazioni in Esame sono le stesse che si otterrebbero facendo una join tra Studente, Insegnamento ed Esame2.

Dato uno schema di relazione, trovare una decomposizione BCNF che soddisfi 2 proprietà: 
1. La lossless Join
2. Preservazione dipendenze funzionali, ovvero che tutti i vincoli d'integrità definiti sullo schema iniziale valgano sugli schemi ricavati.

Non sempre è possibile garantire entrambi i requisiti.
La lossless join garantisce la ricomposizione di un'istanza dello schema relazionale iniziale
> La decomposizione è quindi <font color=red> ragionevole </font>!

Una decomposizione non è una partizione, in quanto un attributo può finire in più relazioni.

Diamo infine una definizione formale:
> Una decomposizione di R in $R_1,...R_n$ è in BCNF se $\forall i\in [1,...n]\ R_i$ è in BCNF. (Per determinare se una $R_i$ è in BCNF occorre riferirsi all'insieme di dipendenze funzionali $F_i$ ottenute proiettando l'insieme di dipendenze funzionali F, definito su R, su $R_i$) 
---
## Esempio Orario
Vediamo un altro esempio per capire come fare e se si può fare sempre la decomposizione BCNF.
Lo schema di relazione è Orario(Aula,Ora,Materia,Docente) con le dipendenze seguenti:
- Materia$\rightarrow$Aula,Docente
- Aula,Ora$\rightarrow$Materia

Le possibili chiavi candidate date dal grafo delle dipendenze sono:
![[esgrap.jpg]]
Keys={Aula ora, Ora Materia}
Proviamo a decomporre in:
R1(Materia,Aula,Docente) per Materia$\rightarrow$Aula,Docente
R2(Aula,Ora,Materia) per Aula,Ora$\rightarrow$Materia e Materia$\rightarrow$Aula.
R2 non è in BCNF in quanto Materia che è presente non è chiave. Proviamo quindi a cambiare R2 in, R2(<u>Ora,Materia</u>). Le dipendenze tra ora e materia non ci sono quindi ho l'insieme vuoto come insieme di dipendenze.

Adesso sia R1 e R2 sono BCNF e la lossless join mi ritorna Orario. Tuttavia ho perso la dipendenza funzionale Aula,Ora$\rightarrow$Materia che non vale ne esplicitamente ne implicitamente. Nell'istanze dei sottoschemi si presentano errori quindi anche se BCNF, non è corretta la decomposizione. Da ciò si capisce che la decomposizione BCNF in alcuni casi fa perdere informazioni o dipendenze funzionali.

>[!regola]
>È sempre possibile calcolare attraverso un algoritmo, che garantisce una decomposizione in BCNF senza perdita di informazioni ma non garantisce il mantenimento delle dipendenze funzionali.
---
# Algoritmo di decomposizione
Presa una relazione R$(A_1,...A_n)$, se prendo X$\subseteq{A_1,...,A_n}$ e Y$\subseteq X^+\setminus X$ (sottoinsieme della chiusura di X tranne X stesso) e con Z = $\{A_1,...,A_n\}\setminus(X\cup Y)$, allora se prendo R1(XY) e R2(XZ) ottengo una decomposizione senza perdita di informazione.

>Applicando questo algoritmo iterativamente prima o poi la relazione sarà BCNF, in quanto alla fine prima o poi si arriva ad una relazione con 2 attributi che è sempre BCNF.

Vediamo un esempio per l'algoritmo:
La relazione è R(ABCDEF) con le dipendenze funzionali seguenti e supponendo che sia una copertura minimale:
- AB$\rightarrow$C
- C$\rightarrow$ED
- ED$\rightarrow$F
- F$\rightarrow$B
- E$\rightarrow$A

![[decomgraf.jpg]]
Le possibili chiavi sono keys={AB,C,ED,EF,BE,AF}. Adesso prendo la relazione R e l'insieme di tutte le dipendenze F e scelgo X,Y e Z.
Come X prendo una parte sinistra che non soddisfa la BCNF. In questo caso E$\rightarrow$A non soddisfa la BCNF quindi X=E, Y=A e Z=BCDF. Cosi facendo ottengo 2 sottorelazioni formate da XY e XZ, R1(AE) e R2(BCDEF) dove su ciascuna di essere metto tutte le proiezioni delle dipendenze funzionali su quei attributi. Quindi per R1: E$\rightarrow$A e per R2: C$\rightarrow$ED, ED$\rightarrow$F, F$\rightarrow$B, EB$\rightarrow$C. La dipendenza EB$\rightarrow$C adesso è rilevante mancando la A quindi la scrivo. Dopo aver finito valuto se le 2 relazioni sono BCNF, in questo caso R1 lo è mentre R2 no in quanto da F$\rightarrow$B si ottiene che la chiusura di F è solo data da B quindi non è BCNF R2. Vado perciò a decomporre R2, ottenendo che X=F, Y=B, Z=CDE, R3(BF) e R4(CDEF) con F$\rightarrow$B dipendenza per R3 e C$\rightarrow$ED, ED$\rightarrow$F, ED$\rightarrow$C. La verifica per R3 e R4 di essere BCNF è positiva perciò ho terminato la decomposizione.

Le foglie dell'albero che ho ottenuto (quindi R1,R3,R4) sono una decomposizione in BCNF senza perdita di informazioni di R, ma dove AB$\rightarrow$C si è persa e non ci sono relazioni dove ABC sono assieme e relazioni da cui è possibile ricongiungere ABC.

---
## Perchè una relazione con 2 attributi è sempre BCNF
Data una relazione R(AB) ho che i possibili casi per l'insieme delle dipendenze funzionali sono:
1. $\oslash$
2. A$\rightarrow$B
3. B$\rightarrow$A
4. A$\rightarrow$B e B$\rightarrow$A

Tutti e 4 i casi sono validi per BCNF.

---

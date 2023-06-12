#fondamenti 
[[Struttura dei primi 3 livelli nel ISO-OSI]]
## Livello 4 - trasporto
Fornisce alle entità di livello sessione le connessioni di livello trasporto e colma le deficienze della qualità di servizio delle connessioni di rete.
Si occupa di frammentare i messaggi in segmenti, consente di fare multiplazione, cioè mandare più segmenti sul medesimo canale logico e consente la suddivisione di connessioni. Funzioni fondamentali sono:
- controllo di flusso
- controllo di errore
- connessione

Il livello trasporto è il primo che vede la rete come un sistema E2E e vuole assicurare che i segmenti arrivino correttamente attraverso il feedback della destinazione.
Il livello trasporto comunica con il livello rete per prendere informazioni dal livello Data Link.

---
## Livello 5 - sessione
È responsabile del dialogo tra 2 programmi applicativi di sistemi diversi, assicura alle entità di presentazione una connessione di sessione, consente di strutturare e sincronizzare lo scambio di dati e maschera le interruzioni del servizio trasporto. Funzioni fondamentali sono:
- gestione del dialogo 
- sincronizzazione tra eventi

---

## Livello 6 - presentazione
Risolve i problemi di compatibilità per quanto riguarda la rappresentazione dei dati da trasferire, risolve i problemi relativi alla trasformazione della sintassi dei dati e può fornire servizi di cifratura.

---

## Livello 7 - applicazione
Fornisce ai processi applicativi i mezzi per accedere all'ambiente OSI. 

---
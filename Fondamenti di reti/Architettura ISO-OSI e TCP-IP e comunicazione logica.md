#fondamenti 
[[Comunicazione e protocolli di comunicazione]]
# ISO/OSI
L'architettura ISO/OSI, ovvero International Standard Organization/ Open System Interconnection, è un modello a strati che separa le funzionalità che i sistemi devono avere per comunicare in dei livelli. Questo favorisce interoperabilità e consente delle progettazioni mirate.
![[isoosi.png]]

3 elementi caratterizzano l'architettura:
1. sistemi: effettuano il trattamento e/o trasferimento di informazione in vista di specifiche applicazioni
2. processi applicativi: sono coinvolti da esigenze di interazione con altri processi
3. mezzi trasmissivi: struttura fisica di interconnessione tra i sistemi

Ogni sistema è logicamente composto da una successione ordinata di sottosistemi ad ognuno dei quali è associato un sottoinsieme funzionale. Uno strato è l'unione di tutti i sottosistemi omologhi appartenenti a sistemi interconnessi. Funzioni simili per logica e per tecnologia realizzativa, sono raggruppati in sottoinsiemi funzionali omogenei. Ad esempio, funzioni orientate al trasferimento dell'informazione quali:
- connessione fisica
- trasmissione
- controllo di errore trasmissivo
- controllo di flusso
- controllo di qualità di servizio
- commutazione

Funzioni orientate all'utilizzazione:
- gestione del dialogo
- adattamento sintattico
- adempimenti semantici

---
#  Architettura TCP/IP
L'IETF è un gruppo che si occupa dell'approvazione dei protocolli che si integrano con l'IP, quindi è un ente di standardizzazione. Il protocollo sta alla base della comunicazione tramite internet.
L'architettura TCP/IP possiede meno strati di quella ISO/OSI in quanto, alcuni strati "condensano" funzioni che appartenevano ad uno strato specifico nel ISO/OSI.
![[tcpip.png]]
Ogni strato:
- è distribuito
- implementa certe funzioni in ogni nodo (modularità)

Strati omologhi su nodi diversi si scambiano messaggi tra loro, quindi la modularità non è dipendente ma indipendente.

---

## Comunicazione logica
Tramite l'incapsulamento dei livelli, l'informazione viene fatta arrivare fino al livello fisico che poi fisicamente trasmette l'informazione. L'informazione come già detto può essere informazione di utente o di controllo.

>[!Utente] Informazione di utente
>Sono l'oggetto principale dello scambio per le finalità del processo di comunicazione

>[!Controllo] Informazione di controllo
>Hanno lo scopo di coordinare le azioni da svolgere in modo cooperativo da parte delle entità di strato

Le informazioni di utente e di controllo costituiscono assieme unità di dati o unità informative. Quando arriva un informazione il TCP/IP la gestisce passando ad ogni livello i dati del livello superiore. Ogni livello aggiunge un header/intestazione, per creare una nuova unità dati e la passa al livello inferiore, avviene quindi l'incapsulamento. Il livello fisico poi passa il messaggio alla destinazione che sa comunicare grazie al protocollo ed essendo parte dello stesso standard. A questo punto ogni livello "smonta" ovvero rimuove i bit di controllo che può interpretare. 
La comunicazione avviene quindi orizzontalmente anche se in realtà, logicamente in verticale perchè il livello fisico ritrasmette l'informazione che viene processata ai livelli superiori.

---



#fondamenti 
[[Meccanismo store e forward e frazionamento dei pacchetti]]
## Definizione comunicazione
Per poter vedere le reti come qualcosa di omogeneo dobbiamo formalizzare le reti con dei modelli di progettazione per semplificare la descrizione e l'analisi delle reti. 
>[!Comunicazione] Il CCITT definisce la comunicazione come:
trasferimento di informazioni secondo convenzioni prestabilite.

La comunicazione richiede cooperazione! Servono quindi degli accordi, ovvero protocolli di rete. I protocolli definiscono il formato, l'ordine di invio e ricezione dei messaggi tra le entità di rete e le azioni intraprese alla trasmissione/ricezione del messaggio.

---

# Protocolli di comunicazione
Un protocollo è un insieme di regole che governano il trasferimento dei dati tra entità che risiedono in diversi sistemi.

>[!Protocollo] Il CCITT definisce protocollo come:
>la descrizione formale delle procedure adottate per assicurare la comunicazione tra 2 o più funzioni dello stesso livello gerarchico

I protocolli definiscono anche:
- sintassi: riguarda la struttura o formato dei dati, più precisamente l'ordine con cui vengono presentati
- semantica: il significato di ogni sequenza di bit
- sincronizzazione: quando e a quale velocità i dati vanno inviati in una comunicazione.

---

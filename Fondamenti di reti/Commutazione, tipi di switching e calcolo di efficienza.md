#fondamenti 
[[Funzioni di rete, controllo e gestione di reti e tipi di segnalazione]]
# Commutazione

La funzione di [[Funzioni di rete, controllo e gestione di reti e tipi di segnalazione#^5dc8cf| commutazione]] o più propriamente switching va distinta dalla funzione di instradamento o routing.

Per instradamento si intende: decidere il percorso che deve essere seguito da un flussso di dati attraverso nodi intermedi per raggiungere la destinazione.

Per routing si intende: procedere all'inoltro del traffico sul percorso calcolato dall'instradamento.

---
## Tipi di switching

Abbiamo 2 tipi di switching:

- <font color=green> circuit switching</font> (commutazione di circuito)
- <font color=green> packet switching</font> (commutazione di pacchetto)

Nel <font color=purple> circuit</font> switching, la rete usa le risorse disponibili per allocare un circuito a ogni richiesta di servizio. Il circuito è di uso esclusivo dei 2 utenti per tutta la durata della comunicazione. Le risorse vengono rilascite alla fine della comunicazione su indicazione degli utenti.

Si hanno quindi 3 fasi:

1. impegno: il circuito viene allocato
2. trasferimento dati: il circuito è in uso esclusivo
3. svincolo: le risorse vengono rilasciate

Vantaggi:

- ritardo di trasferimento costante in quanto si è calcolato a priori il circuito
- trasparenza del circuito, ovvero stessi formati e stessa velocità
- bassi ritardi nell'attraversamento dei nodi

Svantaggi:

- efficienza buona solo in caso di sorgenti non intermittenti
- risorse dedicate ad una comunicazione
- nessuna conversione di formati, velocità e protocolli
- tariffazzione in base al tempo di esistenza del circuito

Nel <font color=cyan> packet</font> switching, non si allocano risorse per l'uso esclusivo di 2 o più utenti. Questo tipo di switching è studiato espressamente per le sorgenti intermittenti. Qui l'informazione da trasferire è organizzata in unità dati che comprendono informazione di utente e di controllo.

Nel packet switching si ha un pacchetto, diviso in 2 sezioni, l'header ed i dati. L'header sostanzialmente contiene le informazioni di controllo del pacchetto, che servono per stabilire il percorso del pacchetto. 
![[pics/infodicontrollo.jpg | PCI= protocol control information  SDU= service data unit]]

--- 
### Calcolo efficienza

Abbiamo parlato di efficienza, quindi vediamo calcolarla:

$\Large\eta={D\over(C+D+R)}$ dove

C= tempo necessario per costruire il circuito. C>0

D= tempo impiegato per trasferire i dati. D>0

R= tempo necessario per il rilascio del canale. R>0

Valore tipico C+R=2s.

Nelle reti ad alta velocità la commutazione di circuito è altamente sconsigliata data la bassa efficienza. Esempio: voglio trasmettere file dati di 1000 byte, su una rete con valore C+R=2s. Per avere un efficienza $\eta=0,98$ si deve avere D=98s cioè una velocità di (1000\*8)/98=81 bit/s bassissima! E più si aumenta la velocità, più si abbassa l'efficienza.

---
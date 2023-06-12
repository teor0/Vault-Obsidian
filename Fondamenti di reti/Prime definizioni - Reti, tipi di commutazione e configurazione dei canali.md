#fondamenti 
# Reti ed il loro obiettivo

La Network Core è l'infrastruttura della rete. I computer (end device) mandano informazioni tramite dispositivi intermedi di vario tipo (router o switch). L'obiettivo primario che viene prefissato è la connettività e la condivisione di informazioni. L'informazione viene inviata attraverso la Network core, ma come trasferire i dati?

Per trasferire i dati si possono usare la commutazione di circuito o di pacchetto. Se per esempio si vuole trasferire la voce, la commutazione di circuito è praticamente un circuito dedicato per chiamata. La voce veniva inizialmente trasferita tramite una rete apposita una volta cattura analogicamente, tuttavia la qualità era sempre soggetta ad un "rumore" dato dalle caratteristiche fisico-chimiche del mondo che ci circonda e degli apparecchi utilizzati.

Nella commutazione di pacchetto i dati sono inviati in rete a "pezzi", qui non si usa la rete telefonica ma Internet.

Nella commutazione di circuito le risore end-to-end (E2E) venivano riservate per la chiamata. La voce doveva avere dei requisiti di qualità un pochino più restrittivi. Le risorse quindi erano riservate ed i nodi intermedi non potevano rilasciare o dedicare le risorse ad altre chiamate, quindi era necessario a priori dedicare risorse per la chiamata.

---
## Come "funziona" un canale

Per risorse si intedeva sia i nodi in campo, sia i canali sul quale viaggiavano le informazioni. Ora, qualunque segnale che viaggia su un mezzo trasmissivo è costituito da un range di frequenze che attraversano il canale che potrebbero non passare nel canale, oppure  un range di frequenze più piccole della banda, che potrei modellarlo per mandare in concorrenza più segnali.

> Per banda si intende risorse di rete.

Supponiamo ora di poter effettuare 10 chiamate quindi di avere un canale diviso in 10 pezzi. Una volta prese le risorse, le teniamo occupate per tutta la durata di una chiamata, anche nei tempi "morti". Abbiamo così un traffico intermittente o traffico a burst che spreca queste risorse. 
Un canale in genere per gestire più chiamate viene diviso in pezzi, tramite 2 modelli:

- <font color=red> frequency division </font>: divisione della frequenza del canale
- <font color=red> time division </font>: divisione del canale in frame temporali dove ad ogni slot di un frame viene associato una chiamata.

---

## Commutazione di pacchetto

Nella commutazione di pacchetto si condividono pacchetti di dati, ogni flusso di dati E2E è diviso quindi in pacchetti. Risulta possibile la condivisone di rete a differenza della commutazione di circuito. Ogni pacchetto usa "tutta" la banda del canale in quanto si possono mandare sottoparti diversi di flussi diversi in istanti di tempo diversi. Le risorse sono quindi usate solo se necessario.

Ovviamente c'è la contesa per le risorse se la domanda di risorse supera l'ammontare disponibile, si crea quindi attesa da parte dei pacchetti che verranno gestiti con politiche di code.

---

## Sharing, reti di accesso e configurazione dei canali

Per fare sharing, ovvero scambiarsi pacchetti i dispositivi intermedi necessitano di:

- <font color=red> storage</font>, per immagazzinare i dati ovvero i pacchetti da mettere in coda
- <font color=red> una logica di forward</font>, ovvero l'attesa non può essere infinita quindi un pacchetto deve essere inviato seguendo delle politiche di gestione

Per accedere alla core network si deve utilizzare una rete d'accesso, tali reti possono essere:

- Reti di accesso <font color=purple> residenziali</font>: legati alla zona geografica
- Reti di accesso <font color=purple> istituzionali</font>: quali aziendali, universitarie ecc
- Reti di accesso <font color=purple> wireless</font>: come un hotspot di smartphone

Nel dettaglio la rete di per se è abbastanza articolata quindi dire rete d'accesso è semplificare il tutto. Vediamo la caratterizzazione di ciascuna rete d'accesso.

L'accesso <font color=green> residenziale </font> può essere punto-punto, che genericamente può venire offerto tramite:

- Modem con velocità fino a 56 Kb/s
- ISDN, integrated services digital network, con velocità fino a 128 Kb/s
- ADSL, asymmetric digital subscriber line fino a 10 Mb/s

L'accesso <font color=green> istituzionale </font> tipicamente LAN offre:

- una local area network (LAN) di una azienda/università che connette end-system all'edge router. Prima con un ordine di grandezza di centinaia di metri adesso di km.
- Ethernet, un cavo che connette l'end-system al router che smista il traffico, che offre velocitò da 10 a 1000 Mb/s

L'accesso <font color=green> wireless </font> offre:

- Una rete d'accesso che connette l'end-system al router che si realizza tramite Wireless LAN o rete cellulare

Per quanto riguarda i canali, essi si possono configurare come detto precedentemente, infatti la comunicazione sui canali può essere di 2 tipi:

1. <font color=red> Punto - punto </font>: solo due nodi collegati agli estremi del canale che viene utilizzato in modo paritetico. La velocità dipende dal canale che introduce un ritardo di propagazione date dalle sue caratteristiche fisco-chimiche. In particolare, anche un'antenna può realizzare una connessione punto-punto.
2. <font color=red> Punto - multi punto </font>: più nodi collegati ad un unico canale, in genere con un nodo master e più nodi slave. ^1bb0c1

C'è anche un altro tipo di canale che è il canale <font color=red> broadcast </font> che è un unico canale di comunicazione condiviso da tutti i nodi. L'informazione inviata da un punto è ricevuta da tutti gli altri, ma se si vuole si può far riceve l'informazione a nodi specifici tramite un indirizzo. È tipicamente usata nelle LAN.

---
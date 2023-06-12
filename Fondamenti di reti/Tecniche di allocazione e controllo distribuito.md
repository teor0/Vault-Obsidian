#fondamenti 
[[Framing e codici controllo e recupero di errori]]
# Allocazione statica
Tra le tecniche di allocazione statica vi sono FDMA, TDMA e CDMA. Nell'allocazione statica si ha una suddivisione che viene percepita da tutte le stazioni che stanno sul canale. Queste tecniche vengono dette tecniche di partizione del canale, dove non si ha contesa di utilizzo e ritardi controllabili.
Nel <font color=red> TDMA (time division multiple access)</font> ad ogni stazione viene assegnato uno slot temporale.

Nel <font color=red> FDMA (frequency division multiple access)</font> ad ogni stazione viene assegnato una banda di frequenza fissa.

Nel <font color=red> CDMA (code division multiple access)</font> ad ogni stazione viene assegnato un codice unico, che viene messo in combinazione con i dati da trasmettere in modo da ricavare un segnale codificato, questo segnale gode di una proprietà di ortogonalità ovvero, se metto in combinazione il segnale con il codice riottengo i dati altrimenti no.
Se finiscono i codici non posso più trasmettere altri dati in contemporanea.

Queste tecniche hanno vantaggi si ma su reti LAN, in quanto riducono gli accessi ma magari chi ha l'accesso non impiega efficientemente le risorse.

# Allocazione dinamica
Nell'allocazione dinamica ci sono 2 metodi di gestione, gestione controllata (centralizzata o distribuito) oppure casuale.
L'accesso controllato non permette collissioni mentre il casuale prima o poi determinerà collisioni. Con questo tipo di gestione i ritardi non sono sempre controllabili, sulla base dell'accesso i protocolli MAC si distinguono in protocolli MAC con collisione e senza collisione.
Nell'allocazione dinamica casuale se il canale è libero allora il pacchetto è inviato con successo altrimenti la stazione dovrà ritrasmettere successivamente. 

> Questo fa capire che traffico elevato porta a collisioni maggiori

Il protocollo deve quindi accorgersi delle collisioni e deve capire come recuperare il frame. L'informazione minima per il protocollo è quelle del riscontro della corretta ricezione.
Nell'allocazione dinamica controllata, se il controllo è centralizzato, una stazione provvede ad abilitare le altre stazioni secondarie. Le stazioni secondarie se non hanno le trame in coda declinano l'opportunità di trasmettere, se hanno trame in coda trasmettono fino ad un numero massimo di trame e dopo il diritto di trasmettere passa alla stazione successiva.
Risulta importante quindi, il tempo di servizio di una stazione, ovvero il tempo in cui una stazione può trasmettere, che può essere:
- "illimitato" cioè finché non finisce di essere trasmesso
- limitato: trasmette fino ad un certo tempo. Tuttavia si perde del tempo nel caso in cui ci sono code vuote e le poche stazioni che devono trasmettere hanno tempi di molti elevati.

In definitiva l'allocazione statica è efficiente su canali a carico alto ed inefficente a basso carico mentre accesso random è efficiente a basso carico ed inefficiente alto carico.

# Controllo distribuito
Qui le stazioni si passano il controllo ordinato tra di loro. Si usa una gestione token ring. Si prende un token che viene modificato dalla stazione, tale token viaggia poi fino al destinatario e quando compie un giro di anello e torna al mittente, si genera un nuovo token per la stazione successiva e ricomincia il tutto.
Criticità del polling (centralizzato):
- latenza
- singolo punto di fallimento
- polling overhead

Criticità token passing (distribuito):
- token overhead
- singolo punto di fallimento
- latenza




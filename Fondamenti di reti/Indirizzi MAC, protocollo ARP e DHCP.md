#fondamenti 
[[Frammentazione, aggregazione, indirizzamento e classi]]
# Utilizzo e tipologie
L'indirizzo MAC è formato da due parti da 3 byte ciascuna, quindi 48 bit ed è mantenuto nella ROM. L'indirizzo MAC è espresso in esadecimale in 6 coppie. Le prime 3 coppie compongono l'OUI (organization unique identifier) e le ultime 3 sono assegnate dal costruttore. Gli indirizzi MAC sono di 3 tipi: 
1. single: per unica scheda
2. multicast: di un gruppo di stazioni
3. broadcast: di tutte le stazioni (ff-ff-ff-ff-ff-ff)

Ogni scheda di rete quando riceve un pacchetto lo passa ai livelli superiori nei seguenti casi:
- Broadcast: sempre
- singoli: se il DSAP è uguale a quello della rete
- multicast: se ne è stata abilitata la ricezione via software

Il protocollo ICMP svolge funzioni accessorie molto utili. Alcune sono:
- ping: utile per verificare la connettività tra 2 host
- traceroute: utile per scoprire il percorso seguito per raggiungere una certa destinazione

2 host possono comunicare direttamente solo se sono collegati alla stessa rete fisica. Se  2 host non utilizzano protocolli proprietari ma utilizzano un protocollo standard tipo IP, non si può consentire una comunicazione se non si conoscono i 2 indirizzi logici. 2 host sulla stessa rete con indirizzi diversi possono comunicare però per conoscere l'indirizzo MAC di un altro host si deve utilizzare l'ARP. Quindi, se non si conosce l'indirizzo fisico ma si conosce l'indirizzo logico di un host si usa il protocollo ARP per ottenerlo.
È importante tenere le informazioni in una ARP table mantenuta in una cache, così da evitare ARP request e ARP reply. 

## Casi ARP request e ARP reply
Ci sono 2 casi possibili:
1. Host della medesima rete
2. Host non della medesima rete

L'ARP attraverso l'ARP request, chiede l'indirizzo fisico al nodo di cui si vuole conoscere che risponde con un ARP reply. Il protocollo RARP è un protocollo che svolge il ruolo opposto del ARP, viene quindi usato per conoscere l'indirizzo logico a partire dall'indirizzo fisico. In genere RARP si usa su dispositivi senza disco e assieme ad un server RARP per conoscere il proprio indirizzo IP. Il default gateway è l'indirizzo IP dell'interfaccia di rete del router che connette il nodo al mondo esterno.

---
## DHCP
Con il tempo RARP è stato sostituido da BOOTP (BOOTstrap Protocol) e DHCP. Il DHCP (Dynamic Host Configuration Protocol) chiede ad un server DHCP l'IP tramite procedure specifiche. Una volta ottenuto l'IP, il router può associarlo ad un'interfaccia di rete ed avendo più interfacce di rete, può avere più indirizzi. ^f6c710

---
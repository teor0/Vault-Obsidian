#fondamenti 
[[Protocollo IP]]
# Perchè frammentare
Le sottoreti possono avere diverse limitazioni circa la lunghezza massima delle loro unità dati. La dimensione massima dell'unità dati di una sottorete è detta MTU (Maximum Transfer Unit) nel TCP/IP. Per questo usiamo la frammentazione per mandare i pacchetti a seconda della MTU. I frammenti non devono essere tutti delle stesse dimensioni, ma almeno l'ultimo deve essere di dimensione minore rispetto agli altri.
Ci sono i seguenti vincoli imposti:
1. I router devono accettare datagrammi pari a quelle delle MTU delle sottoreti connesse
2. Router ed host devono accettare datagrammi di 576 byte
3. I sistemi devono poter inoltrare datagrammi di 68 byte senza ulteriore frammentazione

I datagrammi IP non frammentabili (flag DF=1) comportano la perdita del datagramma se imcompatibile con la capacità di trasporto della rete. Il destinatario usa Identification per ricomporre un pacchetto e poi Fragment offset per l'ordine di ricomponimento. L'informazione presente nell'header viene copiata nell'intestazione di ogni frammento, tranne il campo Total Length che viene modificato.

---
# Indirizzamento

Gli indirizzi IP devono identificare ed indirizzare in modo univoco tutti i sistemi (schede di rete). Abbiamo 2 tipi di indirizzi, il primo è fisico ed è l'indirizzo MAC, il secondo è logico ed è l'indirizzo IP. Questi 2 indirizzi sono essenziali perché MAC servirà a gestire l'informazione a livello di frame, mentre l'indirizzo logico gestito a livello 3, è utile per creare associazioni quando sposto fisicamente il computer. L'indirizzo IP è costituito da una stringa di 32 bit suddiviso in 2 parti: indirizzo della rete e identificato host.

> L'IP address è formato come segue: IP_Address=Net_Id.Host_Id

Net_Id: identifica una porzione di inter-rete, che può coincidere con una sotto-rete fisica. 
Host_Id: identifica il sistema (host o router) nella rete logica.
La divisione tra Net_Id e Host_Id non è sempre fissa. L'indirizzo di 32 bit può essere espresso scrivendo i valori decimali di ciascun byte, separati da un punto ad esempio: 160.97.25.95

---
# Classi di indirizzo

![[classi.png]]
Le classi maggiormente usate sono B e C. Per poter usare indirizzi di classe A, poco sfruttati e quindi per evitare spreco, si sono ideate maschere di rete e sottorete. La classe D è usata per indirizzi multicast (28 bit) con indirizzamento 1 a molti. Questi collegamenti sfruttano alberi che rendono efficiente l'instradamento rispetto a n percorsi separati. Quindi si risparmiano indirizzi IP e sono più efficienti.
>[!Classe A] 
>Il primo ottetto può assumere valore tra 0 e 127. 127.0.0.0 è riservato per l'indirizzo di loopback

>[!Classe B]
>Ottetto compreso tra 128 e 191

>[!Classe C]
>Ottetto compreso tra 192 e 223

>[!Classe D]
>Ottetto compreso tra 224 e 239

>[!Classe E]
>Ottetto compreso tra 240 e 255


Tramite 0.0.0.0 rapprento l'host che origina la richiesta. Tramite 0 e HostId (0.0.0.95) rappresento la rete a cui appartiene l'host. Tramite NetId e restanti 1 rappresento l'indirizzo broadcast dell'host.
Interfacce di rete distinte devono avere indirizzi di rete distinti. Gli indirizzi pubblici sono dati dalla IANA o più specificamente INTER-NIC. Attraverso il subnetting si è introdotta una terza gerarchia, dove l'IP address è dato da: Net_Id+subnet_Id+Host_Id

Il subnetting è la divisione di una singola rete di classe A, B o C in sottoreti di dimensioni minori. La subnet mask identifica il campo subnet_Id, la sottorete consente di suddividere gli indirizzi IP per rendere più efficiente l'uso. Il subnet_Id si prende 3 bit, quindi 5 bit restano alla porzione host cosicché non si sprecano risore. Essendo i primi 3 ottetti bloccati dal Net_Id se gli ultimi 8 bit li blocco per l'host, spreco qualcosa come 200 host.
Per determinare la subnet mask basta effettuare un AND bit a bit tra la netmask con l'indirizzo IP. Se voglio collegare un gruppo di host della stessa rete con un altro gruppo di una rete diversa, uso un router, non uno switch in quanto lo switch lavora fino a livello 2 e non 3. 

Host della stessa rete non necessitano per forza di un indirizzo IP, in quanto se devono comunicare in locale un indirizzo IP non è richieste. Nel caso in cui devono comunicare anche all'esterno della rete locale, serve necessariamente un indirizzo IP. Per estendere una rete da 20 host con 30 host per esempio, si può usare uno switch oppure un hub, ricordando però che:
- se uso un hub i 50 host rappresentano un unico dominio broadcast e quando comunicano contemporaneamente aumenta la loro probabilità di collisione.
- se uso uno switch si ha una separazione degli indirizzi broadcast che porta a meno collisioni ma più risorse impiegate.

---

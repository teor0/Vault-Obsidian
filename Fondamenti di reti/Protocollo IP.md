#fondamenti 
[[Architettura ISO-OSI e TCP-IP e comunicazione logica]]
# Definizione
Il protocollo IP si trova al livello 3 nel ISO/OSI e nel livello 2 nel TCP/IP. Fornisce le seguenti funzionalità:
- <font color=red> definisce lo schema di indirizzamento </font>(indirizzo logico ovvero indirizzo IP associato ad una scheda di rete)
- <font color=red> definisce il percorso di un'unità dati verso la destinazione</font>
- <font color=red> definisce l'unità base per il trasferimento dei dati e ne il suo formato</font>
- <font color=red> definisce la segmentazione e l'aggregazione delle unità dati</font>

Il protocollo fornisce un servizio di trasferimento delle unità con modalità a datagramma, senza connessione ed inaffidabile. Per senza connessione si intende che ciascun unità è trattata indipendentemente dalle altre, ognuna può seguire una strada diversa per arrivare a destinazione. Per inaffidabile indica che non è garantita la consegna di un'unità informativa a destinazione.
L'associazione degli indirizzi è importante per la connettività. 

---
## Formato datagramma IP
Le unità sono caratterizzate da 2 parti, una di controllo ed una di informazioni utili. La parte di controllo va dai 20 ai 60 byte, il datagramma ha lunghezza variabile e massima è di 65536 ottetti.
![[datagrammaip.png| formato dell'unità dati]]
- Version: versione del protocollo IP (4 bit)
- IHL : Internet Header Length (4 bit) esprime la lunghezza del header in parole di 32 bit ovvero 4 byte. Il valore minimo nel caso senza opzioni è 5 perchè 5x4 byte=20 byte. Se tutti e 4 i bit sono a 1 si ha che il valore massimo è 15 quindi 15x4 byte=60 byte. Ecco perchè l'header oscilla tra 20 e 60 byte.
- Type of service (8 bit): specifica parametri della qualità del servizio richiesti dall'utente. Nella versione originale, IP era formato da 2 sottocampi, uno di 3 bit per specificare l'importanza del datagramma ed un subcampo di 3 bit per richiedere particolari prestazioni. I bit erano: D-bit per basso ritardo, T-bit per alta portata e R-bit per alta affidabilità.
- Total length (16 bit): specifica la lunghezza del datagramma misurata in ottetti, includendo l'intestazione ed i dati la lunghezza è sempre multiplo di 4 byte. Tutti gli host devono essere preparati ad accettare datagrammi di lunghezza fino a 576 byte, che permette di trasmettere una quantità ragionevole di dati oltre all'intestazione.
- Identification (16 bit): numero del datagramma, è assegnato dal processo sorgente al datagramma o ai suoi frammenti.
- Fragment offset (13 bit): indica il posizionamento di un frammento all'interno del datagramma originale.

Identification lavora in congiunta con fragment offset. Se il router frammenta, devo usare anche i flag (3 bit) come bit di controllo, dove X non è usato e posto a 0, DF (Don't Fragment) se posto a 0 indica che il datagramma può essere frammentato, altrimenti no. Infine MF (More Fragment) se posto a 0 indica che è l'ultimo frammento altrimenti se posto a 1 indica che seguono altri frammenti.

- Time to live (8 bit): indica quanto tempo il datagramma può rimanere all'interno della rete. Se il time to live è 0 il pacchetto viene scartato.
- Protocol (8 bit): indica a quale processo di livello 4 deve essere inviato il contenuto informativo.
- Header checksum (16 bit): l'intestazione è protetta da un controllo d'integrità.
- Source/Destination Address (32 bit): indirizzo di sorgente/destinazione IP
- Options (multipli di 8 bit): campo opzionale. Con Record Route option, permette al mittente di creare una lista vuota di indirizzi IP, con Source Route option, si consente al mittente di specificare i nodi attraverso i quali vuole che transiti il datagramma e con Timestamp option, si specifica l'istante temporale in cui il datagramma attraversa i diversi nodi.
- Padding (riempitivo): viene usato per completare le righe fino a 32 bit.

---
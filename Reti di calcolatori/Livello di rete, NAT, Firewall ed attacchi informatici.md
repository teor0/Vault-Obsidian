#rdc 
[[Livello di trasporto]]
# Funzioni principali
Il livello di rete si occupa principalmente dell'inoltro e l'instradamento dei pacchetti nella rete. Il protocollo IP si occupa dell'inoltro e dell'indirizzamento attraverso un identificativo univoco, si occupa del formato dei datagrammi e delle convenzioni di manipolazione dei pacchetti quali frammentazione e deframmentazione. Il protocollo <font color=orange>ICMP</font> si occupa di notificare gli errori tramite messaggi appositi. Un datagramma IP è formato dalla seguente struttura:
![[Images/datagrammaip.png]]
importanti sono l'identificatore (id frammento), flag (se segue un frammento) e fragment offset (posizione frammento) per quanto riguarda la frammentazione del datagramma. La frammentazione è dovuta al fatto che essendo internet una rete eterogenea ci sono diverse tecnologie in ballo. L'unità massima di trasmissione detta <font color=red>MTU</font>, rappresenta la quantità massima di dati che un frame a livello di collegamento può trasportare. Differenti tipi di link, portano a differenti MTU.

---
## NAT
Il Network Address Translator si occupa di trasformare gli indirizzi privati di una sottorete in indirizzi pubblici , in particolare tutti i membri di una sottorete avranno come indirizzo pubblico, l'indirizzo IP pubblico del router che si collega con il mondo esterno. 
Quando un router NAT riceve il datagramma, sostituisce l'indirizzo IP d'origine con il proprio e sostituisce il numero di porta origine iniziale con un numero generato da lui. Il protocollo NAT può supportare fino a 60 mila connessioni simultanee con un solo indirizzo IP. Tecnicamente il NAT viola il principio di indipendenza dei livelli, in quanto modifica dettagli di livello 4. Per risolvere propriamente la scarsità di indirizzi si è passati a IPv6. Le funzionalità del NAT permette agli host della rete locale, muniti di IP privato di agire come client verso server che si trovano su internet. Tramite il port forwarding è possibile fare in modo che un host della rete locale agisca da server per client che si trovano all'esterno ^61ed2b

---
# Firewall
Un firewall è una combinazione di hardware e software che isola la rete interna dal resto di internet. Il firewall controlla l'accesso tra le risorse interne ed il mondo esterno, permettendo ad alcuni paccheti di passare e bloccarne di altri. Ci sono 2 tipi di firewall:
1. <font color=blue>Gateway a livello applicazione</font>: sistema di filtraggio e monitoraggio basato sul contenuto del messaggio stesso
2. <font color=red>Filtraggio di pacchetto</font>: lavorano sugli header IP del livello rete e trasporto

![[firewall.png]]
I filtri di pacchetto esaminano le intestazioni IP e TCP/UDP ed applicano delle regole basate su:
- Indirizzi IP sorgente e di destinazione
- Porte sorgente e destinazione TCP o UDP
- Tipo di messaggio ICMP
- Segmenti TCP di inizializzazione della connessione: Il primo segmento di una connessione TCP ha il bit ACK impostato a 0, filtrando i segmenti in arrivo con ACK=0 si bloccano tutte le connessioni originate dall'esterno

L'ordine delle regole descritte è importante in quanto al pacchetto in arrivo viene applicata la prima regola che è compatibile con gli indirizzi sorgente e destinazione del pacchetto. Avere tante regole però può creare problemi perciò è fondamentale avere regole generali che a parità di risultato effettuano un numero di confronti basso.

Un gateway a livello di applicazione può esaminare i dati specifici dell'applicazione. Più gateway possono risiedere sullo stesso host, quindi più regole per più protocolli. 

---
## Attacchi informatici
Un cyberattack è un'operazione compiuta da singole persone o da organizzazioni, che ha l'obiettivo di colpire reti di computer, singoli dispositivi o infrastrutture informatiche di larga scala utilizzando tecniche malevole, provenienti generalmente da terze parti incosapevoli o da anonimi. Tra gli obiettivi dei cyberattack si possono annoverare:
- furto di dati sensibili
- alterazione o distruzione di dati
- alterazione o distruzione di sistemi informatici pubblici e/o privati
- compromissione di infrastrutture informatiche nazionali (cyberterrorismo)

Un attacco <font color=blue>interno</font> è un cyberattack che viene avviato da un'entità interna al perimetro di sicurezza dell'organizzazione (insider) il quale ha accesso alle risorse del sistema, ma fa uso non approvato di tali risorse.
Un attacco <font color=blue>esterno</font> è un cyberattack che viene avviato da un'entità esterna al perimetro di sicurezza dell'organizzazione (outsider).

Un attacco <font color=green>attivo</font> cerca di alterare le risorse di un sistema informatico o di compromettere la sua operatività. 
Un attacco <font color=green>passivo</font> è finalizzato ad apprendere o fare uso di informazioni di sistema, senza tuttavia compromettere la sua operatività.

Gli attacchi di tipo <font color=red>Denial of Service</font> (DoS) tentano di sovraccaricare un server impedendogli di offrire il servizio. Se il traffico in entrata che inonda la vittima proviene da più fonti distribuite si parla di <font color=red>Distributed Denial of Service</font> (DDoS), di norma tale attacco viene effettuato tramite botnet, ovvero più bot. 
L'IP spoofing è una tecnica spesso utilizzata per effettuare attacchi di tipo DoS e DDoS e consiste nel mettere nel pacchetto IP un indirizzo sorgente fasullo.

Gli attacchi di tipo DoS/DDoS sono:
- <font color=purple>SYN Flooding</font>, dove l'attaccante inonda un server di pacchetti SYN aventi pacchetti IP sorgente camuffati. Il server risponde con pacchetti SYNACK che manda agli IP fasulli e va a creare socket che resteranno in attessa consumando risorse
- <font color=purple>UDP flooding</font>, dove un numero alto di pacchetti UDP sono inviati al server per sovraccaricarlo. Se i pacchetti sono indirizzati ad una porta non attiva, il server genera messaggi ICMP d'errore che fanno anch'essi perdere tempo. Un firewall potrebbe proteggere da questo attacco ma potrebbe anche lui venire sovraccaricato nella fase di filtraggio.
- <font color=purple>Smurfing</font>, dove l'attaccante manda un numero ampio di pacchetti ICMP di tipo Echo Request ad un ampio numero di host. L'indirizzo sorgente è camuffato in modo tale da corrispondere all'host che si vuole attaccare. I pacchetti Echo Reply arriveranno tutti a tale host e ne impediranno le funzionalità. L'attacco è ancora più distruttivo se l'indirizzo è multicast.

Per limitare gli attacchi basati su IP spoofing bisogna assicurarsi che i pacchetti in uscita non abbiano indirizzi al di fuori del range compreso nella rete stessa. Allo stesso modo bisogna bloccare i pacchetti in entrata che hanno indirizzi sorgenti appartenenti al range della rete interna, inoltre bisogna bloccare i pacchetti in entrata aventi indirizzi sorgente appartenenti a reti riservate per il NAT.
Per limitare lo smurfing è buona norma rifiutare pacchetti in entrata da indirizzi multicast e impedire l'accesso di segmenti TCP di inizio connessioni in modo da consentire solo le connessioni originata all'interno.

---
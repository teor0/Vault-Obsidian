#rdc 
[[Sicurezza nelle reti - autenticazione]]

# Definizione
Il cloud computing è un modello di elaborazione in cui le risorse sono dinamicamente scalabili e virtualizzate e vengono fornite come servizio su internet. Il cloud è tale quando queste risorse sono accessibili sottoforma di servizi tramite la rete internet. Gli utenti non devono avere conoscenza, esperienza o controllo dell'infrastruttura che li supporta. Il NIST da la seguente definizione:
> Il cloud computing è un modello per abilitare un accesso conveniente e on-demand ad un insieme di risorse computazionali che possono essere forniti con uno sforzo minimo di gestione o interazione con il provider. 

Le caratteristiche del cloud computing sono:
- <font color=green>Scalabile ed elastico</font>: il sistema si adatta al carico di lavoro
- <font color=green>Service based</font>: si può disporrre di memoria, CPU, GPU, app, ecc. sottoforma di servizi
- <font color=green>Internet based</font>: internet è usato come mezzo di erogazione
- <font color=green>Costi a consumo</font>: l'utente paga ciò che usa, per quanto lo usa
- <font color=green>Risorse condivise</font>: i servizi cloud sono multitentant, ovvero sono installati in ambienti condivisi sia a livello hardware che software.

![[cloudestaticcenter.png]]
Si hanno costi e sprechi nel data center statico che nel cloud non ci sono o sono inferiori. Quindi non si rischia overprovisionig/underprovisioning a differenza del data center statico.

I modelli di deployment del cloud sono:
1. Public cloud: è reso disponibile su internet per singoli utenti o aziende ed è tipicamente fornito da grosse aziende. I servizi sono esposti in maniera standardizzata
2. Private cloud: è operato esclusivamente per qualche organizzazione, viene gestito direttamente da tali organizzazioni o da terze parti.
3. Hybrid cloud: è un'infrastruttura ottenuta dalla combinazione di public e private cloud.

Il cloud prevede 3 modelli di servizio, organizzati in una piramide a 3 livelli. Tale piramide è detta di Sheehan dal nome del suo ideatore.
![[sheehanpiramid.png]]

PaaS (Platform as a Service), supporta strumenti di sviluppo, interfacce di controllo, fault tollerance e dynamic provisioning, quindi una piattaforma di sviluppo per gli sviluppatori.
IaaS (Infrastructure as a Service), supporta la scelta di sistema operativo, RAM, CPU e tutto quello presente nel PaaS, in modo da fornire un ambiente virtualizzato liberamente configurabile.
SaaS (Software as a Service),  supporta l'accesso on demand a l'utente finale tramite browser o applicazioni specifiche senza curarsi di installare o fare manutenzione del software. 

IaaS sta alla base di PaaS e SaaS in quanto si tratta sempre di virtualizzazione e cloud computing. Il sistema del cloud computing prevede 3 entità:
- Fornitore di servizi (cloud provider): offre servizi pay per use
- Cliente amministratore: sceglie e configura i servizi offerti
- Cliente finale: usa i servizi opportunamente configurati dall'amministratore

L'architettura informatica del cloud computing prevede uno o più server reali, generalmente in architettura ad alta affidabilità e fisicamente collocati presso uno o più data center del fornitore dei servizi. Il fornitore fornisce interfacce per elencare e gestire i propri servizi ad esempio API. L'amministratore utilizza le interfacce per scegliere i servizi. Il cliente finale usa i servizi configurati senza sapere l'implementazione.

---
##  Virtualizzazione ed interoperabilità dei cloud

La virtualizzazione ha introdotto un notevole incremento dell'efficienza all'interno del data center. L'Hypervisor corrisponde allo strato software e strato fisico che realizza la virtualizzazione. Oggi vengono anche usati i container (ad esempio Docker) che evolvono molto velocemente e che realizzano la virtualizzazione più leggera rispetto al hypervisor.

È molto importante poter spostare le proprie applicazioni su più cloud in modo tale da favorire l'interoperabilità tra i servizi.

---
## Grid computing
Il cloud computing è stato preceduto dal Grid computing, che serviva a risolvere problemi con calcolo parallelo. Il grid computing comprende schemi, strumenti e framework per distribuire il calcolo o i dati, il cloud computing invece virtualizza le risorse hardware e software. Il grid computing fornisce risorse tramite una rete di distribuzione ma non sfrutta la virtualizzazione, inoltre tutti hanno a disposizione tutte le risorse condivise, quindi se io condivido risorse gli posso attingere tranquillamente.

---
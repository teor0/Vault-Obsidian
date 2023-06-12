#fondamenti 

[[Protocollo IP]]
# Cos'è l'instradamento
Per instradamento si intende una funzione logica che consente ai dispositivi della rete di inoltrare pacchetti verso la destinazione desiderata. Ogni pacchetto viene esaminato dal router, perchè un pacchetto potrebbe avere un percorso diverso rispetto al precedente o successivo. Un router ha per ogni interfaccia un indirizzo IP come [[Indirizzi MAC, protocollo ARP e DHCP#^f6c710|abbiamo già visto]], ricordando che indirizzi errati portano a funzionamenti errati. I processi che girano sui router girano a livello 3.
Il router svolge una doppia funzione:
1. decapsulamento frame e verifica informazioni lv 3
2. recapsulamento frame in uscita

Un elemento importante per prendere decisioni in un router, è la conoscenza dell'indirizzo di rete perché conoscere l'indirizzo della destinazione, piuttosto del host, consente ai router di semplificare le informazioni che inseriranno nella tabella d'instradamento. Ci pensa poi la rete finale a mandare il pacchetto alla destinazione specifica.

---
## Tipi di instradamento
Il router effettua 2 tipi di instradamento:
- diretto: il pacchetto che arriva deve essere mandato su una rete collegata ad un'interfaccia del router
- indiretto: il pacchetto che arriva deve essere mandato ad una sottorete per arrivare a destinazione

Per capire quale tipo di instradamento deve effettuare un router esaminiamo due casi.
1. La sottorete logica, ovvero quella individuata dall'indirizzo di rete che esprime la rete che voglio raggiungere, coincide con la sottorete fisica.
2. La sottorete logica è una parte della sottorete fisica, cioè l'indirizzo che esprime la rete di destinazione non coincide con la rete che è associata all'interfaccia del router su cui si vuole mandare il pacchetto. A questo punto per instradare il pacchetto si usa un dispositivo intermedio raggiungibile attraverso il default gateway

Per stabilire in quale dei 2 casi ci si trova, si effettua un bitwise AND tra indirizzo IP dell'interfaccia di rete e la sottomaschera di rete. Ottenuto il risultato si verifica se questo coincide con l'indirizzo di rete del pacchetto IP, se si ci si trova nel caso 1 altrimenti nel 2.

Quando effettuiamo l'instradamento diretto, dobbiamo recapsulare il pacchetto con le informazioni di controllo dell'interfaccia specifica su cui viene mandato il nuovo frame. Gli indirizzi fisici di source e destination devono essere conosciuti dal router, indipendentemente dal tipo di instradamento.
> L'instradamento indiretto, si può considerare come una sequenza di instradementi diretti

---
## Tabella d'instradamento
Il meccanismo operativo usato per l'instradamento IP è basato sulle tabelle di instradamento, che il router mantiene. Una tabella contiene coppie di informazioni quali, l'indirizzo di rete della destinazione e l'indirizzo IP del prossimo router verso la rete di destinazione.
![[tabrouting.png]]
La dimensione della tabella di routing dipende dal numero di reti logiche interconnesse ma non dipende dal numero di host, inoltre il numero di reti logiche sarà inferiore a quello degli host. Grazie a questo approccio gerarchico si riesce a:
- nascondere i dettagli inerenti la sottorete
- mantenere tabelle di dimensione piccole
- semplificare il processo di mantenimento delle tabelle

La tabella inoltre contiene una Metrica, cioè il costo che esprime la distanza da una destinazione secondo vari criteri. La Metrica associata ad ogni hop può essere:
- inversamente proporzionale alla banda del ramo
- proporzionale al carico istantaneo sul ramo
- proporzionale al costo d'uso del ramo
- qualsiasi combinazione tra i precedenti criteri

---
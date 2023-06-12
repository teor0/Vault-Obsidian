#rdc 
[[Sicurezza nelle reti - crittografia]]
# Integrità dei messaggi
Per garantire l'integrità dei messaggi si usano funzioni hash crittografiche, dove si prende un input m e si produce un valore a lunghezza <font color=red>fissa </font>$H(m)$. Per 2 messaggi x e y deve essere impossibile trovare $H(x)=H(y)$ o anche, dato $m=H(x)$ è impossibile determinare x. La checksum di internet ha alcune proprietà di una funzione hash quali:
- è molti a uno
- crea sintesi di messaggi di lunghezza fissa

È relativamente semplice trovare altri dati che utilizzano la stessa checksum del messaggio originale, per questo non è usata la checksum. 

---
## Message Authentication code
MAC (Message Authentication code) usa anche una funzione di hash e garantisce l'integrità ma non la segretezza del messaggio. Il funzionamento è il seguente:

Il messaggio m viene accoppiato al risultato della funzione hash sul messaggio più la chiave. Il destinatario applicherà di nuovo la funzione di hash sul messaggio più la chiave e lo confronterà con quello che ha ricevuto.
![[MAC.png]]
>s è la chiave segreta condivisa tra mittente e destinatario

Le funzioni di hash che vengono impiegate sono:
- MD5: molto usata per l'hash dei messaggi, calcola un hash di 128 bit in 4 fasi.
- SHA-1: più sicuro di MD5 produce una sintesi fissa del messaggio di 160 bit.

---
## Firma digitale
Per firma digitale si intende una tecnica crittografica analoga all'invio di una tradizionale firma scritta. Il mittente firma digitalmente un documento stabilendo che lui è l'unico proprietario/creatore del messaggio attraverso la crittografia. La firma deve essere verificabile, non falsificabile e non ripudiabile. La firma digitale fa uso delle funzioni di hash. Consiste in:
Il mittente, preso il messaggio usa una funzione hash su di esso, ad esempio SHA-1 e preso l'output viene criptato attraverso la chiave privata, infine andrà ad inviare sia il messaggio in chiaro sia il messaggio criptato. 
Il destinatario prenderà il messaggio in chiaro ed applicherà la stessa funzione di hash di prima. Prenderà il messaggio cifrato e dopo averlo decifrato attraverso la chiave pubblica del mittente, andrà a confrontare il risultato con l'output che ha ottenuto applicando la funzione di hash al messaggio. Se il risultato è identico allora la firma è valida. ![[firmadig.jpg]]

Quando si ottiene la chiave pubblica di un utente, chi ne afferma la veridicità? <font color=red>L'autorità di certificazione</font> (CA) si occupa di ciò, collegando una chiave pubblica ad una particolare entità E. L'autorità di certificazione crea un certificato che collega E alla sua chiave pubblica, tale certificato contiene la chiave pubblica di E firmato dalla firma digitale dell'autorità di certificazione. Un certificato è formato da:
- Numero di serie: espresso in esadecimale
- Informazioni sul titolare compreso l'algoritmo ed il valore della chiave
- Informazioni su chi ha emesso il certificato: autorità di certificazione
- Data di validità: scadenza
- Firma digitale di chi lo ha emesso: sempre in esadecimale

Per verificare una firma digitale, posso decifrare il certificato con la chiave pubblica dell'autorità di certificazione ed ottenere la chiave pubblica.

---
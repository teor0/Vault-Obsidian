#rdc 
[[Sicurezza nelle reti - integrità dei messaggi]]

# Protocolli di autenticazione
L'autenticazione è l'insieme di meccanismi e procedure che servono a 2 interlocutori a verificare reciprocamente l'identità. Il più banale protocollo per l'autenticazione, chiamiamolo ap 1.0 consiste nel introdurre se stessi al destinatario. Il protocollo ap 2.0 prevede l'invio dell'indirizzo IP affiancato alla stringa di autenticazione. Anche questo protocollo è facilmente aggirabile tramite l'IP spoofing. Il protocollo ap 3.0 aggiunge una password segreta che è condivisa con il destinatario, ma anche questo protocollo è facilmente aggirabile copiando la password in chiaro. Se criptiamo la password non cambia nulla in quanto anche così basta fare una replica per violare l'autenticazione. 
Passiamo adesso ad una versione più complicata che eviti l'attacco di replica. Questo protocollo ap 4.0 usa un nonce (numero random generato una volta sola), assieme ad una chiave simmetrica condivisa tra mittente e destinatario. A questo punto il funzionamento è il seguente:
- il mittente manda il messaggio 
- il destinatario manda come risposta il nonce 
- Il mittente ricevuto il nonce lo cripta e lo rimanda
- il destinatario per autenticare il mittente decifrerà il nonce criptato e lo confronterà con quello che ha mandato in precedenza. Se risulta uguale allora il mittente è autenticato

Se il nonce non viene utilizzato una volta sola il protocollo può subire facilmente attacchi. Per evitare ciò passiamo al protocollo 5.0 utilizzando il nonce e la crittografia asimmetrica. Il funzionameno sarebbe il seguente:
- il mittente manda il messaggio 
- il destinatario manda come risposta il nonce 
- Il mittente ricevuto il nonce lo cripta con la chiave privata e lo rimanda
- il destinatario richiede la chiave pubblica del mittente
- il mittente da la chiave pubblica al destinatario
- il destinatario decripta il nonce attraverso la chiave pubblica e verifica l'autenticità

---
## Autenticazione tramite KDC
In un sistema distribuito da N host, ogni nodo condivide N-1 chiavi e globalmente sono necessarie $\displaystyle\large N(N-1)\over 2$ chiavi segrete. Si è cercato di trovare quindi una soluzione a questa problematica di gestire molte chiavi, in particolare nacque il Key Distribution Center (KDC), capace di gestire solo N chiavi.
![[kdc.png]]
Per essere più efficiente il KDC può mandare $\displaystyle\large K_{B,KDC}(K_{A,B})$ al mittente cosicché sia lui poi a mandare la chiave al destinatario. $\displaystyle\large K_{B,KDC}(K_{A,B})$ è detto ticket in quanto è usato dal mittente per comunicare con il destinatario. Questo è il meccanismo utilizzato per evitare problemi di perdita e di sincronizzazione tra mittente e destinatario.

---

## E-mail sicure
Mettiamo assiemete tutti i meccanismi visti fino ad ora per creare un sistema di e-mail sicure.
![[mailsicura.png]]
Procedura mittente:
- Crea una chiave simmetrica privata $K_S$
- codifica il messaggio con $K_S$
- codifica $K_S$ con la chiave pubblica del destinatario
- invia $K_S(m)$ e $K_B^+(K_S(m))$ al destinatario

Procedura destinatario:
- usa la chiave privata per ottenere la chiave simmetrica $K_S$
- utilizza $K_S$ per decodificare $K_S(m)$ ed ottiene m

Per garantire l'integrità del messaggio e l'autenticità del mittente si può usare la firma digitale come nel seguente schema:
![[mailintegrity.png]]

Per garantire sicurezza, integrità ed autenticazione, lo schema è il seguente:
![[propersecuremail.png]]

Questo schema fa parte del protocollo <font color=green>PGP (Pretty Good Privacy)</font> divenuto uno standard nel corso degli anni. Usa chiavi simmetriche di crittografia, chiavi pubbliche, funzioni hash e firme digitali, per assicurare integrità del messaggio, sicurezza ed autenticazione del mittente. 

---

## PEC
La PEC, Posta Elettronica Certificata, è un sistema di posta elettronica in grado di superare le debolezze della posta elettronica standard e di poter essere utilizzata in qualsiasi contesto nel quale, sia necessario avere prova dell'invio e della consegna di un documento elettronico. I componenti della PEC sono:
- Mittente: chi invia il documento informatico
- Destinatario: destinatario del mittente
- Gestore del mittente: il soggetto con il quale il mittente mantiene un rapporto finalizzato alla disponibilità del servizio PEC
- Gestore del destinatario: il soggetto con il quale il destinatario mantiene un rapporto finalizzato alla disponibilità del servizio di PEC
- Rete di comunicazione: tipicamente Internet
- Documento informatico: realizzato dal mittente ed oggetto dell'invio verso il destinatario

A differenza della raccomandata non interessa al mittente se il destinatario ha letto o meno la PEC, ma a livello legale è importante la <font color=red>ricezione</font> della PEC. 

>La PEC non sostituisce la firma digitale, occorre sempre apporre la firma digitale al documento e mandarlo tramite PEC.

Predisposto l'oggetto all'invio, il mittente deve farsi riconoscere dal sistema di PEC del proprio gestore secondo le modalità previste da questi. Una modalità molto diffusa è accedere al servizio tramite user-id e password. Una volta riconosciuto, il mittente può inviare un messaggio di posta elettronica. Il sistema di PEC dovrà poi effettuare controlli finalizzati a verificare correttezza formale e l'assenza di virus.


Nel caso in cui i controlli riscontrano criticità, il messaggio non verrebbe inviato ed il mittente riceverebbe una ricevuta firmata elettronicamente dal proprio gestore, contenente l'informazione dell'invio non effettuatato ed il perché. Se i controlli vanno bene, il gestore mittente firma digitalmente il messaggio e lo inoltra attraverso la rete di comunicazione verso il gestore destinatario. Il gestore destinatario deposita il messaggio nella casella del destinatario ed invia la ricevuta di avvenuta consegna al mittente firmata digitalmente. Il sistema PEC non considera la lettura del messaggio come prova dell'effettiva consegna.

Nella situazione in cui il gestore rilevi la presenza di un virus, è tenuto a mantenere la mail in un apposito archivio per 30 mesi, così come previsto dalle norme in modo tale da porre successive verifiche circa l'evento rilevato.

---
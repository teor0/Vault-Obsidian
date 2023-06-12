#rdc 
[[CHORD]]
# Definizione di criptovalute
Le criptovalute impiegano tecniche crittografiche e architetture decentralizzate di pagamento. A differenza dei pagamenti in contanti, l'acquirente invia un dato digitale raffigurante il pagamento. Il pagamento digitale tradizionale si appoggia tramite infrastrutture di pagamento gestiti da terzi, in modo da garantire la correttezza del pagamento. Le caratteristiche comuni di questi metodi di pagamento sono:
- <font color=red>Server certificati</font> (circuiti delle banche o carte di credito)
- <font color=red>Transazioni con commissioni</font>
- <font color=red>0 anonimità</font>

Lo schema può essere ridotto ad una circonferenza dove ogni, attore attua un'azione verso il prossimo.
Nei pagamenti digitali c'è il problema della fiducia. Entrambe le parti (acquirente e venditore) devono accordarsi sul metodo di pagamento, che viene gestito da terzi che si devono fidare in modo da effettuare la transazione una volta sola. Un problema dell'approccio decentralizzato è la possibilità di pagare 2 volte!

---

## Paypal
Paypal è un intermediario tra l'acquirente e il venditore. Paypal si offre come garante nel caso in cui l'acquisto effettuato non dovesse arrivare all'acquirente, restando però un sistema centralizzato.

---

# Bitcoin e blockchain
Nell'ottobre 2008 esce l'articolo riguardante i Bitcoin redatto da Satoshi Nakamoto e  nel 2009 nasce la blockchain. La blockchain si può ridurre ad una linked list di blocchi, dove il primo blocco prende il nome di Genesis block. Il genesis block contiene righe di testo, mentre gli altri contengono degli header e delle serie di transazioni. La blockchain può solo espandersi e non contrarre. La prima vera transazione avvenne nel 2010. Per accedere al proprio portafoglio, l'utente deve utilizzare una chiave privata, che può andare smarrita.

Gli obiettivi del Bitcoin sono:
- Creare un sistema di pagamento senza intermediari
- Creare un sistema Peer to peer puro

>L'ambiente è di default untrusted, ovvero non ci si fida degli altri peer.


I Bitcoin sono gestiti tramite client e garantiscono una pseudoanonimità, in quanto le transazioni sono gestite dalla blockchain e sono rappresentate da stringhe di caratteri. A differenza dei pagamenti digitali centralizzati, le commissioni sono più basse.

Solo il core di Bitcoin è decentralizzato, tutto l'ecosistema attorno ad esso è centralizzato.

---

## Problema del double spendng
Il problema principale del pagamento tramite Bitcoin è il double spending (doppio pagamento). Per evitare quindi di sfruttare ciò in modo malevolo, magari pagando più utenti attraverso gli stessi bitcoin, nasce il concetto di <font color=green>ledger</font>. Il ledger è un database distribuito che memorizza le transazioni tra gli utenti ed evita il double spending. Ci sono però delle difficoltà nell'implementazione del ledger quali:
- aggiornamento del database distribuito in modo uniforme in presenza di ritardo di propagazione
- alcuni nodi potrebbero imbrogliare il sistema

Idealmente si dice che se la maggioranza dei nodi è onesta il sistema funziona.
In Bitcoin il ledger è rappresentato dalla blockchain, che come detto in precedenza si può solo espandare. Esempio di "protocollo":
- A invia Bitcoin verso B e registra la transazione nel suo ledger
- B controlla che i Bitcoin che A manda siano di sua proprietà attraverso il ledger, se si, manda in broadcast la transazione nella rete
- Tutti gli altri peer controllano la validità della transazione, se lecito aggiungono una copia della transazione al loro ledger.

Tuttavia questo "protocollo" permette ad A di mandare la stessa somma di denaro verso C, se la latenza di C è sufficientemente alta tale che il messaggio broadcast di B arrivi dopo la transazione di A. Un ulteriore metodo per aggirare la sicurezza del protocollo sarebbe effettuare un attacco DOS sul canale tra B e C, in modo tale da non far comunicare i due nodi. L'algoritmo di consenso è quello realmente impiegato e segue la logica che: si aggiunge una transazione al ledger di tutti i nodi, <font color=red>se e solo se la maggioranza è d'accordo sulla validità della transazione</font>. L'algoritmo funziona se la maggioranza dei nodi è onesta.

Tuttavia essendo il sistema basato su sistema distribuito con utenti anonimi e non soggetti ad iscrizione, è effettuabile un Sybil Attack, dove attraverso decine e decine di iscrizioni finte, si ottiene la maggioranza disonesta. Bisogna quindi fare in modo che gli utenti legati ad un utente malevolo, valgano 1 voto e non N, per fare ciò, un voto è espresso da potenza di calcolo di un nodo calcolata dalla proof of work. Ovviamente se un utente ha N computer performanti il sistema di voto è aggirato.

---
## Struttura della blockchain
Gli utenti che mantengono il ledger sono i cosidetti <font color=purple>miner</font>, che ottengono come ricompensa una piccola quantità di Bitcoin alla creazione di un nuovo blocco della blockchain. Ogni blocco contiene le transazioni avvenute in 10 minuti, pesa meno di 1MB e contiente circa 7 transazioni per secondo. La blockchain possiamo schematizzarla come segue:
![[blockchain.png]]
Come detto prima, i blocchi sono aggiunti tramite l'attività di mining, che viene effettuata colletivamente dai membri della rete P2P. I miner devono risolvere problemi via via computazionalmente più difficili e chi risolve per primo, crea il nuovo blocco e vince una piccola quantità di bitcoin. I miner non partecipano come singoli, ma come mining pool dove più macchine partecipano come singolo miner che riceveranno una frazione della vincita in base alla potenza di calcolo. Solo i miner posso raccoglie le transazioni avvenute e raggrupparle in un blocco attraverso il proof of work. L'header del blocco contiene una serie di campi quali:
- <font color=green>nVersion</font> (4 Byte): si usa essenzialmente per memorizzare la versione del protocollo, che varia piano piano in soft fork (bug fix) e hard fork (nuova versione)
- <font color=green>hashPrevBlock</font>  (32 Byte): contiene l'hashing del blocco precedente. L'hashing è effettuato 2 volte tramite SHA-256
- <font color=green>hashMerkleRoot</font>  (32 Byte): hash del Merkle Root. Per capire cos'è, introduciamo il Merkle Tree che viene usato per memorizzare in modo sintetico l'hash di un insieme di campi. Nel Merkle Tree, ogni nodo foglia contiene l'hash crittografico di un blocco di dati, ogni nodo superiore contiene l'hash crittografico della concatenazione dei figli. Il Merkle Root contiene l'hash di tutti i nodi sottostanti.
- <font color=green>nTime</font>  (4 Byte): il timestamp di quando il nodo è stato creato
- <font color=green>nBits</font>  (4 Byte): quanto difficile è minare il blocco
- <font color=green>nNonce</font>  (4 Byte): il nonce usato dal miner

La prima transazione di ogni blocco prende il nome di <font color=red>coinbase</font>, e sostanzialmente codifica il trasferimento della ricompensa più le commissioni verso il vincitore. Questa ricompensa di fatto crea nuovi Bitcoin. La proof of work è il meccanismo con cui un'entità dimostra di aver utilizzato della potenza di calcolo. La proof of work, si basa su una sfida crittografica risolvibile con dello sforzo che non può essere "ingannato" che sia però facile da verificare. La proof of work, nasce prima dei Bitcoin per, gli attacchi DOS e lo spam di Mail. La proof of work per evitare attacchi DOS consiste in, mettere a disposizione un servizio solo se l'utente risolve un problema ad alto tasso computazionale. Quindi anche qui, per il richiedente il problema deve essere difficile mentre per il fornitore deve essere facile da verificare. La proof of work per evitare lo spam segue l'approccio di richiedere cicli di CPU, dipendentemente dal numero di mail che bisogna mandare, perciò se mando 10-20 mail spreco poca potenza di calcolo, ma se ne mando 1 milione ne serve molta. La proof of work varia tra client a client di posta.

In Bitcoin per la proof of work, si parte da una stringa challenge C che rappresenta l'intestazione di un blocco. La sfida consiste in trovare un'altra stringa x che assieme a C soddisfi la seguente proprietà:
> C concatenato ad x sottoposto a hashing, ritorni un output con un numero di 0 pari al livello di difficoltà della challenge come prefisso.

L'approccio è naturalmente di brute force. La proof of work è una funzione del tipo:
$\large F_d(c,x)\rightarrow\{true,false\}$ in particolare è $\large F_d(c,x)\rightarrow SHA256(SHA256(c|x))< {2^{224}\over d}$
aumentando d aumentano il numero di bit iniziali pari a 0. Questo numero di bit è il parametro nBits del header del blocco. Essendo la proof of work cosi costosa questo porta a dover far spendere molto denaro a chi vorrebbe imbrogliare rendendo quindi "impossibile" imbrogliare.

Quando un miner trova il nonce x, lo va a scrivere nel parametro nNonce del header del blocco che andrà a creare e che verrà verificato dagli altri peer.  La difficoltà cresce in modo tale che il tempo necessario per creare un nuovo blocco sia pari a 10 minuti. Nel caso in cui due blocchi vengano convalidati nello stesso istante, si viene a creare una biforcazione nella block chain. Questa però dura per poco in quanto la regole è che un blocco nuovo va aggiunto al branch più lungo, quindi a meno che avvengano coppie di nuovi blocchi sempre, uno dei 2 branch smetterà il proseguimento.

---
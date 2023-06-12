#rdc 
[[Applicazioni e architettura P2P]]
# Obiettivi della sicurazze nelle reti
Nell'ambito della sicurezza delle rete ci sono 4 obiettivi:
1. <font color=blue>Riservatezza</font>: i messaggi devono essere cifrati, in modo tale che solo mittente e destinatario possono leggere il contenuto
2. <font color=blue>Autenticazione</font>: mittente e destinatario devono essere certi dell'identità del corrispondente
3. <font color=blue>Integrità del messaggio</font>: il contenuto dei messaggi non deve essere alterato durante la trasmissione
4. <font color=blue>Disponibilità e controllo d'accesso</font>: un servizio deve essere accessibile a chi è legittimamente autorizzato

Per la riservatezza si usa la crittografia la codifica e la decodifica dove:
- Per codifica si intende: testo in chiaro T $\rightarrow$ testo codificato K(T)
- Per decodifica si intende: testo codificato K(T) $\rightarrow$ testo in chiaro T

Si usa un algoritmo pubblico e verificabile per assicurarsi della sua robustezza. 

---

## Crittografia
La crittografia può essere simmetrica o asimettrica. La crittografia impiega un algoritmo e chiavi per garantire sicurezza e segretezza.
Nella crittografia simmetrica, la segretezza, autenticazione ed integrità dipendono segretezza dalla chiave, utilizzata sia per codifica che decodifica. Di solito si usano chiavi di 64-128 bit molto veloci. Le chiavi sono distribuite a coppie e la complessità di distribuzione è $\displaystyle O(n^2)$. Il problema principale è lo scambio delle chiavi nella rete. Esempio:
![[crittsimm.png]]

Il più semplice algoritmo a chiave segreta è il cifrario di Cesare dove ogni lettere è sostituita da quella che segue a distanza k, dove la chiave era k=3 per le lettere dell'alfabeto. L'evoluzione è la sostituzione mono-alfabetica, una generalizzazione del cifrario di Cesare, dove ogni lettera è sostituita da un'altra secondo uno schema "libero". Questa tecnica di cifratura è facilmente attaccabile con metodi statistici.
L'algoritmo di analisi delle frequenze più antico risale al IX secolo e si compone dei seguenti passaggi:
1. Trovare un testo in chiaro nella stessa lingua dell'originale
2. Si calcola la frequenza di ciascuna lettera
3. Si ordinano le lettere in maniera descrescete in base alla frequenza
4. Faccio lo stesso con il testo cifrato
5. Si prova a sostituire la lettura più frequente cifrata con quella più frequente in chiaro, fino a quando non trovo una frase di senso compiuto

Si passa poi ai cifrari poli-alfabetici, che consistono in cifrari composti da 2 o più cifrari mono-alfabetici o di Cesare. Le lettere sono sostituite con l'uno o l'altro cifrario secondo uno schema prederminato. Anche se il tempo aumenta all'aumentare della lunghezza della chiave, il sistema non è sicuro.

Sistemi moderni di cifratura sono:
- Cifrario a traspozione: le lettere trasposte in altre posizioni, secondo una chiave di trasposizione basata su shuffling e trasposizioni. Tuttavia anche questo tipo di cifrario è facile da attaccare statisticamente.
- One-time pad: il testo è codificato con una chiave della stessa lunghezza. Il messaggio può essere al massimo lungo quanto la chiave. La cifratura è randomica ed avviene tramite somma tra il testo in chiaro e la chiave. La tecnica risulta inattaccabile a patto che la chiave sia usata un'unica volta. 

Gli algoritmi moderni usati su internet hanno le seguenti caratteristiche:
- chiavi piccole al massimo poche centinaie di byte
- più operazioni in cascata (trasposizioni, XOR, sostituzioni) secondo logiche complesse, ma non troppe sennò la decodifica è lenta

---

## Algoritmo DES
L'algoritmo DES, codifica il testo in chiaro in blocchi da 64 bit indipendenti dagli altri blocchi. La lunghezza della chiave, detta master key è 56 bit da essa sono estratte 16 chiavi da 48 bit secondo in certo schema. Ogni chiave è usata in iterazioni diverse. Un blocco da 64 bit viene permutato e ritorna una parte left ed una parte right. La parte left assieme alla chiave e la parte right attraverso una funzione formano la parte right successiva. La parte right diverrà poi la parte left successiva. La decodifica è duale alla codifica.
![[algoritmoDES.png]]

---

## Algoritmo AES

L'algoritmo AES, processa i blocchi a 128 ed opera con chiavi a 256 bit. Aumentado i bit della chiave, aumenta esponenzialmente il tempo di codifica e decodifica quindi bisogna "dosare" bene il numero di bit che compongono una chiave.

---

# Crittografia asimmetrica
La crittografia asimmetrica nasce per risolvere la problematica, di comunicare senza aver scambiato a priori chiavi. Nella crittografia asimmetrica, si usa una chiave per la codifica ed una per la decodifica. Ogni utente possiede una coppia di chiavi, una privata ed una pubblica. Entrambe le chiavi sono usabili per codificare e decodificare, in genere sono chiavi a 1024/2048 bit e sono usate per piccole parti di file in quanto le operazioni di codifica e decodifica sono piuttosto lente. Vediamo lo schema generale di codifica e decodifica:
![[crittasimm.png]]
Le chiavi hanno 2 requisiti per essere utilizzate:
1. $\displaystyle K_B^+(*)$ e $\displaystyle K_B^-(*)$ devono garantire che $\displaystyle K_B^-(K_B^+(m))=m$ o $\displaystyle K_B^+(K_B^-(m))=m$
2. Data la chiave pubblica $\displaystyle K_B^+$ deve essere *impossibile* (ovvero computazionalmente molto difficile) calcolare la chiave privata $\displaystyle K_B^-$

## Algoritmo RSA
L'algoritmo a crittografia asimmetrica più famoso è l'algoritmo RSA a chiave pubblica. L'algoritmo garantisce l'impossibilità di ricavare la chiave privata da quella pubblica, sfrutta la proprietà dei numeri primi e la considerazione che è molto difficile fattorizzare numeri molto grandi (aumenta in modo esponenziale in base al numero di bit per rappresentare un numero). Le chiavi possono essere di 512, 1024 o 2048 bit. RSA è molto più lento di algoritmi a chiave segreta ma in genere è applicato a piccole quantità di dati. Il funzionamento è il seguente:
1. Si scelgono 2 numeri primi di valore elevato p e q
2. Si calcola $n=pq$ e <font color=purple>$z=(p-1)(q-1)$</font>
3. Si sceglie <font color=orange>$e<n$</font> tale che non abbia fattori in comune con z
4. Si sceglie <font color=yellow>d</font> tale che $ed-1$ sia esattamente divisibile per z
5. La chiave pubblica è $(n,e)$ quella privata è $(n,d)$

Dati (n,e) e (n,d) per la codifica di un messaggio m si calcola come:
$\displaystyle\large c=m^emod n$
per decifrare il messaggio ricevuto c si calcola:
$\displaystyle\large m=c^dmod n$
Si dimostra che: $\displaystyle\large m=(m^emodn)^dmodn$

RSA permette di applicare sia prima la chiave privata e poi quella pubblica, sia di applicare la chiave pubblica e poi quella privata senza che il risultato cambi. 

---


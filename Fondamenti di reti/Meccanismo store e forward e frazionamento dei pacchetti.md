#fondamenti 
[[Commutazione, tipi di switching e calcolo di efficienza]]
# Store & Forward
È necessario avere un meccanismo intrinseco di bufferizzazione dei pacchetti, ovvero di store & forward per evitare conflitti tra i pacchetti, inoltre si possono avere più code per nodo per utilizzare il meccanismo store & forward. 
Il meccanismo di store consiste nel: memorizzazione del pacchetto, elaborazione del pacchetto e scelta del canale su cui inoltrarlo, infine messa in coda per la trasmissione del canale.
Per lo store & forward occorre disporre dell'intestazione prima di poter effettuare l'instradamento che richiede tempo. Occorre anche qualche forma di protezione da errori sull'intestazione (header) per evitare distorsione da parte del canale quindi servono tecniche di protezione.

Si può perdere un pacchetto perchè ci può essere un errore da parte del canale, oppure avere il buffer pieno ed il pacchetto viene scartato, o il time to live del pacchetto è scaduto, o se il nodo si è spostato.

Si può avere anche un meccanismo di non store & forward dove ogni nodo: memorizza i primi byte del pacchetto, determina il canale su cui inoltrarlo, e inizia immediatamente la ritrasmissione del pacchetto senza attendere la completa ricezione. Tutto ciò comporta vantaggi in velocità e risparmio della memoria. Gli svantaggi sono riguardo la sicurezza, la valutazione del errore e perdita dei pacchetti più frequente.

Questo meccanismo prende il nome di <font color=red> cut-through</font>, ed avviene quando il canale di uscita può essere occupato, perciò il pacchetto viene memorizzato nel nodo. Il cut-throug è simile allo store & forward, ma comporta in perdite di pacchetti a fronte di congestione, necessità di molta memoria nei nodi e riduzione delle latenze solo con basso traffico.
![[pics/strutturapacketsw.png | struttura di un nodo di rete a packet switching]]

---

## Frazionamento dei pacchetti: vantaggi e svantaggi
L'informazione di utente può essere frazionata in molti pacchetti che devo associare ad un informazione di controllo. La lunghezza dei pacchetti è determinata dalla possibilità di parallelizzazione:
- <font color=red> Pacchetti brevi</font>, favoriscono la trasmissione in parallelo su canali diversi e riducono il ritado di pacchettizzazione. 
- <font color=red> Pacchetti lunghi</font>, riducono la percentuale di informazione di controllo che appesantiscono le risorse

 Prendiamo un pacchetto con PCI di dimensione pari a p bit e con SDU di dimensione pari a s bit. Abbiamo che la frazione di informazione di controllo è:
$\displaystyle\Large{p\over{s+p}}$

>La lunghezza dei pacchetti è però eterogenea data l'interoperabilità della rete.

Pacchetti brevi riducono la probabilità d'errore perché, supponiamo sia p la probabilità di errore, n il numero di bit di un pacchetto e di avere un canale con errori indipendenti, la probabilità della correttezza di un pacchetto é data da: $\displaystyle\large{(1-p)}^n$
per $n$→$\infty$ questa probabilità tende a zero qualsiasi sia il valore di p.

Bisogna trovare un compromesso per favorire la parallelizzazione e non sprecare le risorse sull'informazione di controllo.

---


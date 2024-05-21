---
tag: #elettronica 
created: 2023-02-18 19:23:37
updated: 2023-02-18 19:23:37
---
[[Inverter CMOS e regole di applicazione sui circuiti CMOS]]
#elettronica 
# Esercizi sulle regole
Descriviamo il circuito per la funzione: $f=a\land (b+c)\land (d+e)$. Date le parentesi gli OR hanno priorità maggiore quindi andiamo a descriverli per primi e dopo le AND. Se seguo le regole ottengo il circuito seguente:
![[eser1circ.jpg|400x600]]
Da notare che l'ordine degli interruttori in serie nella PDN non influisce, bisogna sempre però seguire le regole per gli operatori AND e OR.

Adesso data la seguente rete:
![[eser2circ.jpg|400x400]]
ricaviamo la PUN e la funzione logica che il circuito rappresenta. La funzione che la PDN rappresenta è $f=a\land (b+c)\land (d+e)$ ma questa è una funzione diretta quindi per la [[Inverter CMOS e regole di applicazione sui circuiti CMOS#^31357b|terza regola]] l'uscita va negata ma come si vede dallo schema, l'uscita è priva di inverter perciò deduciamo che la funzione rappresentata è $f=\overline{a\land (b+c)\land (d+e)}$. Applicando le regole per la PUN abbiamo infine che il circuito è dato da:
![[eser2circfull.jpg|300x600]]

---
# Capacità
Fino ad ora abbiamo visto circuiti i cui interruttori sono ideali, ma nella realtà gli interruttori sono non ideali. Per quanto riguarda l'ordine degli interruttori, anche se la funzione logica descritta rimane la stessa se cambio il loro ordine, il funzionamento può essere influenzato dalla dissipazione di potenza e cambiare il comportamento. Nel corso si rimane ad un livello astratto tale che l'ordine non influisce sul comportamento.
Supponiamo ora di voler analizzare il comportamento di un inverter, per farlo non possiamo considerare un inverter come singolo, ma bisogna considerare il suo comportamento quando la sua uscita è collegata ad altri elementi che costituiscono una rete. Nella situazione reale bisogna considerare che l'uscita di un inverter sia collegata a ciò che nella rete combinatoria reale, rappresenta l'insieme di tutti i carichi, cioè l'insieme di elementi della rete cui l'uscita dell'inverter va in ingresso, il FAN-OUT.
Ad esempio in questa rete
![[forcapac.jpg]]
l'inverter ha come insieme di carichi la AND, la OR e la XOR. L'uscita che produce l'inverter sarà poi utilizzata come segnale di controllo degli interruttori Z1 e U1 della AND, mentre l'ingresso I1 controllera gli interruttori Z2 e U2. Più la rete diventa complessa più interruttori bisognerà gestire, quindi il numero di interruttori da pilotare  equivale al carico. Per modellare un carico si utilizza la capacità, in quanto tiene conto della fisica del dispositivo, ovvero del comportamento del dispositivo elettronico che si utilizza per realizzare il generico interruttore. Il valore della capacità dipenderà da quanti sono gli interruttori che il segnale dovrà pilotare.
La capacità di carico rappresenta il primo effetto di non idealità del circuito e da ora in poi rappresentiamo un inverter come segue:
![[capacita.jpg|500x300]]
Supponiamo adesso di avere un generico interruttore di tipo 1, posizionato tra due punti.
![[extip1.jpg|600x100]]
Sia $V_I$ il segnale di controllo con il quale è definito lo stato dell'interruttore. Considerando l'interrutore come ideale, se $V_I=V{DD}$ abbiamo che lo stato logico è pari a '1' e l'interruttore si chiude. Questa situazione è stata considerata fino ad ora come un cortocircuito, dove il circuito è attraversato da una corrente $I_{ON}$ e tra $P_A$ e $P_B$ si viene a creare una differenza di potenziale pari a $V_{ON}=0$. Di conseguenza se volessimo rappresentare la resistenza equivalente a questa situazione avrei $R_{ON}=0\ohm$.
Se $V_I=0V$ lo stato logico corrispondente è '0' e tra i due punti abbiamo sostituito l'interruttore con un circuito aperto. Il circuito è attraversato da una corrente $I_{OFF}$ e la differenza di potenziale tra $P_A$ e $P_B$ è pari a $V_{OFF}$, la resistenza equivalente che l'interruttore oppone alla corrente è $R_{OFF}=\infty$. 
Questo nella realtà non è possibile, tuttalpiù si distinguono i due casi in: $R_{ON}\approx 0\ohm$ e $R_{OFF}\approx\infty$.
Gli interruttori di tipo 0 hanno resistenze $R^Z_{ON}$ e $R^Z_{OFF}$ mentre gli interruttori di tipo 1 hanno resistenze $R^U_{ON}$ e $R^U_{OFF}$ che assumuno valori diversi.

> Queste due non idealità presenti nella realtà creano dei problemi che occorre considerare.

---


---
created: 2022-10-10 12:07:28
---
#elettronica 
[[Definizioni, logica di rappresentazione, porte logiche e circuiti]]

# Metodo di rappresentazione di un array e rappresentazioni numeriche
All'interno del corso andremo ad utilizzare array di elementi. Essi possono essere rappresentanti nei seguenti modi:
- Rappresentazione a bus: A\[3:0] =A\[3] A\[2] A\[1] A\[0]
- Rappresentazione a bus alternativa A\[3:0] = $a_3, a_2, a_1, a_0$
- Rappresentazione "compatta": A: bit_vector(3 downto 0)

Per quanto riguarda i numeri le rappresentazioni che vengono utilizzate all'interno di circuiti sono le seguenti:
- Rappresentazione in binario - priva di segno
- Rappresentazione modulo e segno - con segno
- Rappresentazione in complemento a 2 - con segno

Le due più utilizzare sono binario e complemento a 2, dove il default all'interno dei circuiti è complemento a 2.

## Recap vantaggi e svantaggi delle rappresentazioni numeriche
Per quanto riguarda la rappresentazione binaria la questione è semplice, si possono esprimere i numeri solo positivi, quindi privi di segno e con $n$ bit si può rappresentare da 0 a $2^n-1$.

Per quanto riguarda la rappresentazione modulo e segno, si usa un bit per rappresentare esplicitamente il segno in particolare, 0 per + e 1 per -. Il bit più significativo esplicita il segno quindi i restanti $n-1$ bit sono utilizzati per rappresentare il numero. Tuttavia, questa rappresentazione risulta ambigua per rappresentare 0 data la natura della rappresentazione. Questo porta a complessità e costi nell'uso di questa rappresentazione che viene quindi di fatto ignorata.

Per quanto riguarda la rappresentazione in complemento a 2, il bit più significativo ha valore $-2^n-1$ anziché $2^n-1$, questo quindi porta a poter rappresentare da -128 a 127 e verificare la proprietà che $x-x=0$ per qualunque numero sia x.

---
# Descrizione circuiti ed importanza della somma binaria
I circuiti possono essere descritti in 3 modi:
1. Tramite tabelle di verità
2. Tramite equazioni logiche
3. Tramite uno schema disegnato

Più circuiti possono avere un funzionamento/risultato uguale ma caratteristiche diverse. Esempio di realizzazione di un half-adder e di un full-hadder.
![[halfAdder.jpg|700x250]]

![[fulladder.jpg]]
Il circuito finale sarà:
![[circuitofull.jpg|400x400]]
dove A e B sono gli operandi, $C_i$ il riporto in ingresso, $C_o$ il riporto in uscita e $S$ la somma.
La somma binaria è alla base di tutti i calcoli più complessi. In qualsiasi microprocessore è presente un'unità logica aritmetica (ALU), quindi implicitamente ottimizzare l'ALU significa ottimizzare tutte le operazioni.

---
# Circuiti sommatori
Esistono diverse reti combinatorie che possono essere utilizzate per realizzare somme con riporto, ma a seconda delle operazioni devo usare un circuito diverso. Vediamo adesso il ripple-carry adder, dove ripple-carry sta per propagazione del riporto. Come base nel circuito ha un full adder e si ottiene collegando in cascata n full-adder.
![[ripplecarry.jpg]]
Da notare che mentre il riporto va propagato, il bit di somma è immediatamente disponibile. Questo circuito sommatore è il più semplice da realizzare ed esegue la somma tra 2 numeri ad n-bit con il metodo "carta-penna". Nel esempio la somma viene svolta su numeri unsigned dove il risultato sarà dato da n+1 bit, in cui il più significativo è il riporto dell'ultimo full adder.
Il ripple-carry fornisce complessità bassa e dissipazione bassa, ma anche velocità d'esecuzione bassa, quindi è quello che costa di meno in assoluto dal punto di vista delle porte logiche. Naturalmente avere prestazioni migliori implica avere più porte logiche e dissipare di più. 
Se prendiamo ad esempio un ripple-carry composto da 8 full adder, avremo che il generico full adder $FA_{i}$ calcola le uscite $C_o$ e $S_i$ in $\large\tau_{FA}$ nel ordine di 500 picosecondi. Sebbene ogni full adder riceva nello stesso istante di tempo $a_i,b_i$, tutti i full adder dopo il primo devono attendere la propagazione del riporto precedente. Quindi per un ripple-carry a $n$ full adder bisogna attendere $\large n\times \tau_{FA}$ per sommare operandi ad n-bit. Un processore a 64 bit impiega a 64$\large\tau_{FA}$ all'incirca 32 nanosecondi. Sapendo che il ritmo di 1GHz impiega un tempo di lavoro di 1 nanosecondo questo fa capire che commercialmente non si usa il ripple-carry adder.
Come miglioramento introduciamo una predizione a metà del circuito, ovvero al quarto full adder. Abbiamo perciò due soluzioni in base al valore di $C_4$ se pari a 0 o 1. Così facendo ho 3 porzioni indipendenti (subadder) che lavorano in parallelo e scelgo il risultato corretto attraverso dei multiplexer. Si passa così da aspettare 8 $\large\tau_{FA}$ ad aspettare 4 $\large\tau_{FA}$+ $\large\tau_{MUX}\simeq5\tau_{FA}$.

Vediamo una tabella che dimostra il miglioramento:

| n bit operandi | Ritardo RCA         | Ritardo RCA + multiplexer       |
| -------------- | ------------------- | ------------------------------- |
| 8              | 8$\large\tau_{FA}$  | 5$\large\tau_{FA}$              |
| 16             | 16$\large\tau_{FA}$ | 9$\large\tau_{FA}$              |
| 32             | 32$\large\tau_{FA}$ | 17$\large\tau_{FA}$             |
| n              | n$\large\tau_{FA}$  | ($n\over 2$+1)$\large\tau_{FA}$ |

Abbiamo incrementato la velocità di calcolo al costo di un incremento di $n\over 2$ full adder e ${n\over 2}+1$ multiplexer e di conseguenza la dissipazione.
La miglioria che abbiamo realizzato è di fatto il carry-select adder.
![[carryselect.jpg]]
Se riuscissimo ad eliminare la propagazione si risolverebbero dei problemi ed avremmo dei vantaggi nelle prestazioni creando così il cosidetto carry look-ahed. Supponiamo di avere un generico full adder di un ripple-carry. La tabella riguardante le sue entrate ed uscite è la seguente:

| $C_i$ | $a_i$ | $b_i$ | $C_{i+1}$ | $S_i$ | $P_i$ | $g_i$ |
| ----- | ----- | ----- | --------- | ----- | ----- | ----- |
| 0     | 0     | 0     | 0         | 0     | 0     | 0     |
| 0     | 0     | 1     | 0         | 1     | 1     | 0     |
| 0     | 1     | 0     | 0         | 1     | 1     | 0     |
| 0     | 1     | 1     | 1         | 0     | 0     | 1     |
| 1     | 0     | 0     | 0         | 1     | 0     | 0     |
| 1     | 0     | 1     | 1         | 0     | 1     | 0     |
| 1     | 1     | 0     | 1         | 0     | 1     | 0     |
| 1     | 1     | 1     | 1         | 1     | 0     | 1     |

Per quanto riguarda il riporto abbiamo 2 tipologie di calcolo:
1. $a_i\neq b_i$: riporto in uscita = riporto in entrata, per indicare ciò utilizziamo un segnale ausiliario propagate $P_i$
2. $a_i=b_i$: se $a_i=b_i=0$ allora riporto in uscita=0 se $a_i=b_i=1$ allora riporto in uscita=1. Per indicare ciò utilizziamo il segnale ausiliario generate $g_i$

I segnali sono rispettivamente dati da: $P_i=a_i\ XOR\ b_i$ e $g_i=a_i\ AND\ b_i$. Abbiamo quindi che $S_i=p_i\ XOR\ c_i$. Supponendo di rimanere nella situazione in cui un carry-select adder ha 4 full adder avremo che:
$C_1=g_0+c_0P_0$
$C_2=g_1+C_1P_1=g_1+P_1g_0+P_1P_0C_0$
$C_3=g_2+C_2P_2=g_2+P_2g_1+P_2P_1g_0+P_2P_1P_0C_0$
$C_4=g_3+C_3P_3=g_3+P_3g_2+P_3P_2g_1+P_3P_2P_1g_0+P_3P_2P_1P_0C_0$

abbiamo cosi eliminato la propagazione del riporto precedente rendendo più semplice il tutto giusto? In realtà no si è complicata la situazione, perciò quando si realizzano circuiti logici è bene tenere a mente due fattori: il FAN-IN ed il FAN-OUT. Quindi il carry look-ahed porta un grande vantaggio nella somma tra bit, ma è difficilmente realizzabile a causa di limitazioni che garantiscono una certa efficienza di circuito.
## FAN-IN e FAN-OUT
Il <font color=blue>FAN-IN</font> corrisponde al numero di ingressi di una porta logica, è limitato a 2. Per risolvere problemi di necessità di più ingressi si utilizza una struttura ad albero o cascata.
![[fanin.jpg|600x500]]
Il <font color=purple>FAN-OUT</font> corrisponde al numero di volte che un segnale viene usato come ingresso, ed anch'esso è limitato. Il FAN-OUT influenza i valori di ritardo di occupazione e dissipazione, tecniche di bufferizzazione diminuiscono il FAN-OUT ma richiedono risorsa aggiuntive.

---
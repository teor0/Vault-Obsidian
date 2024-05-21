---
tag: #elettronica 
created: 2023-02-15 10:35:54
updated: 2023-02-15 10:35:54
---
#elettronica 
[[Rappresentazioni array e numeriche, Adders e circuiti sommatori]]
# Introduzione
VHDL sta per Very high speed Hardware Description Language, un linguaggio ad alto livello d'astrazione per descrivere sistemi ed essere usato per la sintesi e/o la simulazione.
I vantaggi del VHDL sono:
- Indipendente dal sistema di sviluppo
- Indipendenza dall'architettura di implementazione
- Stesso linguaggio per simulazione e sintesi
- Può essere modellato qualunque livello di gerarchia da un chip ad un sistema

La sintesi è il processo di conversione del codice VHDL in elementi fisici specifici per hardware scelto. 

# Elementi strutturali
Il primo elemento è <font color=orange>l'entity</font> che serve a definire cosa riceve in ingresso e cosa produce in uscita la rete logica. È fondamentale quando si crea un'entity, specificare la direzione che assumono le porte che posso essere:
- IN: segnale di sola lettura
- OUT: segnale di sola scrittura
- INOUT: segnale usato si per ingresso che per uscita
- BUFFER: da la possibilità di memorizzare nella porta logica l'output della porta, funzione sostituita ormai da INOUT

Ogni segnale è associato ad un <font color=red>**tipo**</font> dove un tipo definisce un set di valori che l'oggetto può assumere. L'attribuzione del tipo avviene al momento della dichiarazione e quindi all'interno delle specifiche della porta e dell'architettura.
VHDL presenta i seguenti tipi di default:
- Boolean
- Bit 
- Character
- Integer: da $-(2^{31}-1)$ a $2^{31}-1$
- Real: da $-(1.7014e^{38})$ a $1.7014e^{38}$

Vediamo ad esempio come rappresentare un semplice adder con 2 ingressi a 4 bit.
```VHDL
entity ADDER is
	port(
		A,B: in integer range 0 to 3;
		SUM: out integer range 0 to 3;
		CARRY: out bit);
end ADDER;
```
4 bit sono necessari per la rappresentazione in complemento a 2, altrimenti sarebbe serviti 2 bit.

Il secondo elemento è <font color=orange>Architecture</font>. Nell'architettura avviene la descrizione del codice ovvero come viene implementata la porta. Il rapporto tra entity e architecture è necessario esplicitarlo tramite un link nominale attraverso *of*. Esempio:
```VHDL
architecture RTL of ADDER is
	begin
		SUM <= A xor B;
		CARRY <= A and B;
	end RTL;
```
I signal rappresentano connessioni interne all'architecture, non hanno direzioni in quanto rappresentano un collegamento e la direzione è specificata solo per le porte. Hanno sostanzialmente il solo scopo di semplificare la scrittura ma non esistono a livello circuitale.
Esempio attraverso un full adder:
![[fulladderport.jpg]]
``` VHDL
entity FULLADDER is
	port(
		A,B,Cin: in bit;
		S,Cout: out bit);
end FULLADDER;

architecture ex1 of FULLADDER is
	signal g,p: bit;
	begin
		S <= A xor B xor Cin;
		p <= A xor B;
		g <= A and B;
		Cout <= g or (p and Cin);
	end ex1;
```
Sebbene in VHDL le priorità degli operatori logici è rispettata, si possono usare le parentesi comunque. La sintesi avviene quando il codice viene "compilato" dal sintetizzatore.

---
# Esempio ripple-carry
VHDL supporta variabili e segnali. Le variabili aiutano a scrivere codice, i segnali rappresentano collegamenti fisici materiali come già visto. VHDL consente di scrivere architetture gerarchiche, quindi partendo da un full adder posso creare un ripple-carry. Vediamo un esempio di ripple-carry a 4 bit:
Ogni full adder ha internamente  delle porte che si rifanno alla entity. Per scrivere il codice VHTL bisogna identificare ingressi ed uscite del circuito. In VHDL ci sono 2 approcci per descrivere un circuito:
1. Comportamentale: tramite funzioni logiche.
2. Strutturale: al posto di descrivere la funzione logica si descrive quali moduli vengono usati ed in che modo.
```VHDL
entity RCA4 is
	port(
		a3,a2,a1,a0: in bit;
		b3,b2,b1,b0: in bit;
		Cin: in bit;
		Cout: out bit;
		s3,s2,s1,s0: out bit);
end RCA4;

architecture struct of RCA4 is
	signal c1,c2,c3: bit;
	component FULLADDER
		port(
		A,B,Cin: in bit;
		Cout,S: out bit);
	end component;
	begin 
		FA0: FULLADDER port map
			(a0,b0,Cin,s0,c1);
		FA1: FULLADDER port map
			(a1,b1,c1,s1,c2);
		FA2: FULLADDER port map
			(a2,b2,c2,s2,c3);
		FA3: FULLADDER port map
			(a3,b3,c3,s3,Cout);
	end struct;
```
Per questa implementazione si è usato l'approccio strutturale. Attraverso component si crea un collegamento con il modulo del full adder, riportando esattamente gli stessi nomi impiegati nella entity FULLADDER. Si fa poi un mapping tra le informazioni del componente e quelli dell'entity RCA4. Il fatto che $c1$ sia utilizzato come output prima e dopo input fa capire al sintetizzatore che bisogna utilizzare il segnale $c1$, ovvero che $c1$ è un collegamento vero.
Le call vengono dette istanziazioni ed ogni istanza richiede una label.

## Notazione ad array
Supponiamo adesso di voler realizzare un ripple-carry a 16 bit, la mole di codice aumenta di molto e può risultare oneroso e complesso da scrivere. In aiuto ci viene la notazione vettoriale o array. Un array è un insieme di oggetti tutti dello stesso tipo definito tramite *Tipo array*\_Vector quindi esistono:  Boolean_Vector, Bit_Vector, Integer_Vector ecc. Uno degli aspetti fondamentali degli array è l'indicizzazione dei valori al suo interno che può essere crescente o decrescente. Ad esempio prendiamo A=$a_3,a_2,a_1,a_0$ posso implementare un bit_vector più intuitivo quale: `A(3 downto 0)` oppure `A(0 to 3)`.
Supponiamo di dichiarare 2 array:
```VHDL
signal ADDBUS: bit_vector(8 downto 1);
signal DATABUS: bit_vector(7 downto 0);
```
è possibile fare un'assegnazione tra due array, castando uno nell'altro. È importante però che i due abbiano stessa dimensione. Esempio:
```VHDL
DATABUS <= ADDBUS;
-- equivale a 
DATABUS(1) <= ADDBUS(0);
DATABUS(2) <= ADDBUS(1);
...
DATABUS(8) <= ADDBUS(7);
```
Si può anche iniziallizare un array:
```VHDL
DATABUS <= "00101011";
```
È possibile anche utilizzare gli <font color=blue>slice</font>, ovvero partizioni del array, tenendo conto che <font color=red>**non**</font> si può utilizzare un indicizzazione opposta a quella utilizzata nella dichiarazione.
```VHDL 
DATABUS: bit_vector(7 downto 0);
DATABUS(2 to 5) <= "0110" -- è errato
DATABUS(5 downto 2) <= "0110" -- è corretto
```
La concatenazione permette di raggruppare singoli bit e vettori per formare array, attraverso l'operatore &.
```VHDL
signal A,B: bit_vector(3 downto 0);
signal C: bit_vector(7 downto 0);
signal D: bit_vector(4 downto 0);
C <= A&B;
-- oppure
C <= B(3)&A(3)&A&B(1 downto 0);
-- oppure
C <= A&'0'
```
Gli aggregati sono un modo efficiente per assegnare elementi di un vettore. Esempio:
```VHDL
signal A,B,C,D: bit;
signal Z_BUS: bit_vector(3 downto 0);
Z_BUS <= (A,B,C,D);
--  equivale a Z_BUS(3)=A, Z_BUS(2)=B, Z_BUS(1)=C, Z_BUS(0)=D
Z_BUS <= (3 => '1', 1 downto 0 => '1', 2=>B);
-- equivale a Z_BUS(3)=1, Z_BUS(2)=B, Z_BUS(1)=1, Z_BUS(0)=1
Z_BUS <= (3 => '1', others => B);
-- equivale a Z_BUS(3)=1, Z_BUS(2)=B, Z_BUS(1)=B, Z_BUS(0)=B
```

---
# For generate e wait
Anche introducendo i vettori la mole del codice rimane alta, figuriamoci se si cerca di scrivere codice per circuiti a 32/64 bit. Ci viene in aiuto lo statement <font color=orange>for generate</font>. Esempio:
```VHDL
entity FA is:
	port(
	A,B,Cin: in bit;
	S,Cout: out bit
	);
end FA;

entity RCA4_v3 is:
	port(
	A,B: in bit_vector(3 downto 0);
	Cin: in bit;
	Cout: out bit;
	S: out bit_vector(3 downto 0);
	)
end RCA4_v3;

architecture struct of RCA4_v3 is:
	signal C: bit_vector(4 downto 0);
	component FA
		port(
		A,B,Cin: in bit;
		Cout,S: out bit
		);
	end component
	begin 
		myFor: for i in 0 to 3 generate:
			myFA: FA port map 
				(A(i),B(i),C(i),S(i),C(i+1));
			end generate myFor;
		C(0) <= Cin;
		Cout <= C(4);
	end struct;
```
Per utilizzare for generate serve quindi una label, per identificare l'inizio e la fine del for. Lo statement generate serve a generare i componenti circuitali necessari. A livello circuitale $i$ è un elemento astratto utilizzato a supporto della scrittura del codice, non si ha necessità di dichiararla prima del utilizzo in quanto, utilizzarla al livello del for equivale ad una sua dichiarazione ed inoltre il compilatore si aspetta di trovare una variabile intera.

L'attesa all'interno del codice VHDL è possibile attraverso `wait for t ns` con $t>0$. 
 
## Variabili parametriche e If
Un circuito ovviamente è un qualcosa che va generalizzato e non specificato per 4 bit. In VHDL per utilizzare variabili parametriche si usa il costrutto `generic(n:integer:=8)`, dove $n$ è il nome della variabile, integer è il tipo ed 8 è il valore di default. Essendo generic interno al modulo component, all'interno di un test bench occorre riutilizzare il costrutto nell'entity vuota che sfrutta il test bench. Ulteriore passo è quello di utilizzare `generic map(n)` nel momento di mapping del circuito.
In VHDL esiste anche `if condizione generate`, utile a distinguere tra diversi casi una condizione. Anche per l'if come per il for occorre utilizzare una label ad esempio `myIf` e terminarlo tramite `end generate`.

---








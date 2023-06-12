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

---
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

---
# Notazione ad array
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

--- 
# Variabili parametriche e If
Un circuito ovviamente è un qualcosa che va generalizzato e non specificato per 4 bit. In VHDL per utilizzare variabili parametriche si usa il costrutto `generic(n:integer:=8)`, dove $n$ è il nome della variabile, integer è il tipo ed 8 è il valore di default. Essendo generic interno al modulo component, all'interno di un test bench occorre riutilizzare il costrutto nell'entity vuota che sfrutta il test bench. Ulteriore passo è quello di utilizzare `generic map(n)` nel momento di mapping del circuito.
In VHDL esiste anche `if condizione generate`, utile a distinguere tra diversi casi una condizione. Anche per l'if come per il for occorre utilizzare una label ad esempio `myIf` e terminarlo tramite `end generate`.

---
# VHDL per circuiti sequenziali
Nel realizzare circuiti sequenziali in VHDL, si fa riferimento allo statement <font color=purple>process</font>, statement concorrente che incapsula istruzioni sequenziali. La sintassi è la seguente:
``` VHDL
optional_label: process(sensitivity list)
			 begin
				[...]
			end process [optional_label];
```
La sensitibity list, è una lista che contiene i segnali di ingresso o porte di ingresso, che in maniera diretta vanno ad influenzare lo stato di qualche altro segnale o di porte d'uscita. Una sensitivity list vuota corrisponde ad una sensitivity list contenente tutti i segnali e porte d'ingresso.
All'interno del process si può utilizzare lo statement sequenziale <font color=orange>if then else</font>, uguale ad un if di Java, solo che in VHDL l'ordine corretto è importante in quanto influenza la sintesi. È importante coprire tutte le condizioni, per evitare che una condizione non coperta venga interpretata dal sintetizzatore come attivazione di una funzionalità di memoria. Esempio:
``` VHDL
process
begin
	if(a='0')then
		b <= c and d;
	else -- else ricopre tutti gli altri stati possibili STD_LOGIC non solo '1'
	 b <= ((not c) and (not d));
	end if;
end process;
```

## Esempio latch positivo
``` VHDL
library IEEE;
use IEEE.std_logic.1161.all;
entity LP is
	 port(D,Clk: in std_logic);
	 port(Q: out std_logic);
end LP;

architecture behav of LP is
	begin
		process(D,Clk)
		begin
			if(Clk='1')then
				Q <= D;
			else
				Q <= Q; -- modo per attivare la funzione di memoria
			end if;
		end process;
end behav;
```
Come si sa il comportamento del latch è variabile in particolare:
- Il clock influenza direttamente Q.
- D influenza indirettamente Q.

Individuare i segnali responsabili della variazione dell'uscita è importante per capire quali segnali devono essere inseriti nella sensitivity list e nel caso del latch sono sia D che Clk.
Supponiamo di aggiungere al latch un clear asincrono attivo alto (ovvero se $clr='1'\implies Q='0'$),
``` VHDL
library IEEE;
use IEEE.std_logic.1161.all;
entity LP is
	 port(D,Clk,Clr: in std_logic);
	 port(Q: out std_logic);
end LP;

architecture behav of LP is
	begin
		process(D,Clk,Clr)
		begin
			if(Clr='1') then -- prima va verificato il clear!
				Q <= '0';
			else (Clk='1')
				Q <= D; 
			end if;
		end process;
end behav;
```
il clear influenza direttamente Q perciò va nella sensitivity list, inoltre la condizione da verificare sul clear è prioritaria (come già detto) rispetto a quella sul clock, quindi è la prima condizione da verificare.

## Esempio flip flop
Il flip flop ha un comportamento diverso dal latch in quanto, gli eventi che consentono il trasferimento dell'ingresso sull'uscita, sono molto selettivi ovvero i fronti di salita o discesa e non il periodo intero in cui il clock è alto o basso. Considerato ciò possiamo dire che solo il clock influenza direttamente il valore di Q e D non lo influenza affatto.
```VHDL
library IEEE;
use IEEE.std_logic.1161.all;
entity FF is
	port(D,Clk: in std_logic);
	port(Q: out std_logic);
end FF;

architecture behav of FF is
begin
	process(Clk)
	begin
		if(rising_edge(Clk)) then -- istruzione che discrimine un fronte di salita
			Q <= D;
		end if;
	end process;
end behav;
```
È possibile inserire anche per il flip flop un segnale di clear e preset, in particolare si ipotizza di utilizzare il preset attivo alto ed il clear attivo basso asincroni, su un flip flop sensibile a fronti di discesa del clock.
```VHDL
library IEEE;
use IEEE.std_logic.1161.all;
entity FF is
	port(D,Clk: in std_logic);
	port(Q: out std_logic);
end FF;

architecture behav of FF is
begin
	process(Clk,Pr,Clr)
	begin
		if(Pr='1') then 
			Q <= '1';
		elsif(Clr='0') then
			Q <= '0';
		elsif falling_edge(Clk) then 
			Q <= D;
		end if;
	end process;
end behav;
```
L'ordine tra preset e clear è arbitrario, in quanto hanno stessa priorità se sono asincroni mentre sincroni sono errati in partenza.

Esiste anche la versione sincrona con il segnale di clock di preset e clear ovvero reset e set. Se ho un flip flop sensibile a fronti di salita allora anche il reset si attiverà quando il clock è alto. Il process associato al reset sincrono:
```VHDL
process(Clk)
begin 
	if rising_edge(Clk) then
		if(reset='1') then
			Q <='0';
		elsif(reset='0') then
			Q <= D;
		end if;
	end if;
end process;
```
a differenza del preset, nel reset si controlla che il clock sia alto e dopo il valore di reset mentre con il preset si controlla prima il suo valore e poi quello del clock. Per quanto riguarda set:
```VHDL
process(Clk)
begin 
	if rising_edge(Clk) then
		if(set='1') then
			Q <='1';
		elsif(set='0') then
			Q <= D;
		end if;
	end if;
end process;
```
Per quanto riguarda i flip flop non ha molto senso utilizzare la descrizione gerarchica con for generate, ma meglio usare una behavioural come visto nei precedenti esempi.

---
# Test bench per circuiti sequenziali
Supponiamo di voler fare un test bench per un registro a 8 flip flop, per la realizzazione del test bench supponiamo che:
- $T=10ns$ ovvero il periodo tra un fronte di salita ed un altro.
- Duty cicle a 50% (default Vivado), che indica quanto in % sul periodo totale di clock perdura lo stato alto.
- $t_{setup}=2ns$ e $t_{hold}=2ns$

Date queste supposizioni avremo:
![[tbcircseq.jpg|400x500]]
la variazione di D non può coincidere con la variazione del clock altrimenti non si rispetterebbero i tempi di setup e hold. Il codice per il test bench sarà:
```VHDL
library IEEE;
use IEEE.std_logic.1164.all;
entity SimR8 is
end SimR8;   -- vuota in quanto non si usano generic

architecture BenchSim of SimR8 is
	component Reg8
		port(D: in std_logic_vector(7 downto 0);
			Clk: in std_logic;
			Q: out std_logic_vector(7 downto 0));
	end component;
signal ID,OQ: std_logic_vector(7 downto 0);
signal IClk: std_logic:='0'; --inizializzazione clock a 0

begin 
	circ: Reg8 port map(ID,IClk,OQ);
	process
	begin --t=0
		wait for 5ns;
		IClk <= not IClk;
	end process;
	process 
	begin 
		ID <= (others=>'0')
		wait for 7ns;
		ID <= '00001111';
		wait for 10ns;
		ID <= '11111111';
	end process;
end BenchSim;
```
Al clock si dedica un process a parte per il timing, quindi si avranno 2 process concorrenti fra loro uno per il clock ed uno per i segnali che tengono conto dei tempi supposti.

---









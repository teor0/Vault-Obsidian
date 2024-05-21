---
tag: #elettronica 
created: 2023-04-26 11:14:42
updated: 2023-04-26 11:14:42
---
#elettronica 
[[VHDL]]
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
> L'ordine tra preset e clear è arbitrario, in quanto hanno stessa priorità se sono asincroni mentre sincroni sono errati in partenza.

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
Supponiamo di voler fare un test bench per un registro a 8 flip flop, 
```VHDL
library IEEE;
use IEEE.std_logic.1161.all;
entity Reg8 is
	port(D: in std_logic_vector(7 downto 0)
		Clk: in std_logic;
		Q: out std_logic_vector(7 downto 0));
end Reg8;

architecture behav of Reg8 is
begin
	process(Clk)
	begin
		if(rising_edge(Clk)) then 
			Q <= D;
		end if;
	end process;
end behav;
```
per la realizzazione del test bench supponiamo che:
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
Il periodo del clock può essere messo in un package come costante:
```VHDL
library IEEE;
use IEEE.std_logic.1164.all;
package costanti is
	costant nb: integer:=8;
	costant Tclk: Time:=10ns;
end package costanti;
```
Tuttavia essendo una costante di simulazione si dovrebbe più propriamente definire nel test bench. Normalmente un package definisce costanti utilizzate dal circuito

---
# Esempio sommatore a n bit con registri
Si vuole realizzare il seguente circuito in VHDL
![[sumwithreg.jpg|550x500]]
```VHDL
library IEEE;
use IEEE.std_logic.1164.all;
package costanti is
	costant nb: integer:=8;
	costant Tclk: Time:=10ns;
end package costanti;

library IEEE;
use IEEE.std_logic.1164.all;
use IEEE.std_logic_SIGNED; -- contiene operatori per numeri con segno
library word;
use work.costanti.all;

entity RegADD is
	generic (ni: integer:= nb); -- se tolgo il generic perdo la genericità
	port(A,B: in std_logic_vector(ni-1 downto 0);
		Clk: in std_logic;
		Ris: out std_logic_vector(ni downto 0));
end entity;

architecture MyCirc of RegADD is
	signal RA,RB: std_logic_vector(ni-1 downto 0);
	signal ORis: std_logic_vector(ni downto 0);
	begin 
		process begin 
			if rising_edge(Clk) then
				RA <= A; RB <= B; Ris <= ORis;
			end if;
		end process;
	ORis <= (RA(ni-1)&RA)+(RB(ni-1)&RB)); -- estenzione del segno necessaria
end MyCirc;
```
L'istruzione `ORis <= (RA(ni-1)&RA)+(RB(ni-1)&RB));` si può mettere sia prima che dopo il process e va a sostituire, grazia all'uso della libreria `IEEE.std_logic_SIGNED`, l'istanziazione di un component registro semplificando di molto il codice.
Andiamo a fare il test bench:
```VHDL
library IEEE;
use IEEE.std_logic.1164.all;
library word;
use work.costanti.all;

entity SimRADD is
	generic(ni: integer:nb);
end SimRADD;

architecture behav of SimRADD is
	component RegADD 
		port(A,B: in std_logic_vector(ni-1 downto 0)
			Clk: in std_logic;
			Ris: out std_logic_vector(ni downto 0));
	end component;
	signal IA,IB: std_logic_vector(ni-1 downto 0);
	signal IClk: std_logic;
	signal ORis: std_logic_vector(ni downto 0);
	-- costant TClk: Time:=10ns; va messo se non si usa nel package e se c'è nel 
	-- package crea conflitto se messo anche nel test bench.
	begin 
		circ: RegADD port map (IA,IB,IClk,ORis);
		process begin
			wait for TClk/2;
			IClk <= not IClk;
		end process;
		process begin 
		wait for 100ns;
		wait until falling_edge(Clk); --bisogna sincronizzare il clock con il reset
		wait for 2ns;
		IA <= (others =>'0');
		IB <= (others =>'1');
		wait for TClk;
		IA <= (others =>'1');
		end process;
end SimRADD;
```
Il fatto di avere sia nel file di descrizione del circuito e test bench un segnale che si chiama ORis non crea conflitto, in quanto sono 2 segnali utilizzati localmente dai file.
Quando viene eseguita una simulazione post-implementation, Vivado tiene conto del comportamento reale del dispositivo scelto per il progetto, nel momento in cui un dispositivo parte ad eseguire una simulazione, viene eseguito un general reset, che dura 100ns, per cui prima di questo tempo si decide di non effettuare alcuna azione.
Con l’istruzione wait until, tramite un fronte di discesa del clock il circuito si sincronizza con lo stesso, questo è necessario in quanto, non è detto che la fine del reset corrisponda all’inizio di un periodo di clock, ma potrebbero essere sfasati di alcuni ns.

---


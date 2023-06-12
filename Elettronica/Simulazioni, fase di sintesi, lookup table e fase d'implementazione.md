---
tag: #elettronica 
created: 2023-02-17 12:22:05
updated: 2023-02-17 12:22:05
---
#elettronica 
[[Standard logic, process e concurrent statement]]
# Sintesi, lookup table e implementazione
Una simulazione del circuito considera ritardi nulli ma questo nella realtà non è possibile. Per tenere in considerazione le porte logiche realmente in utilizzo in un circuito è necessaria una fase di sintesi del circuito. All'interno di Vivado una volta effettuata la sintesi del circuito, la schematizzazione appare come segue:
![[sintschem.jpg]]
I triangoli sono buffer di tipo IBUF (buffer d'ingresso) o OBUF (buffer d'uscita) e rappresentano i punti di contatto del circuito reale con il mondo esterno. Le equazioni logiche descritte in VHDL non vengono realizzate con porte AND/OR ma tramite <font color=red>lookup table</font>, tabelle di verità che implementano una funzione logica ad $n$ ingressi e $m$ uscite, che sono equiparabili alla RAM in quanto una volta spento il circuito viene cancellata la loro caratterizzazione. Dopo la sintesi è possibile eseguire simulazioni che tengono conto delle componenti reali.
Le board sul quale si svolgono gli esercizi sono dispositivi detti <font color=orange>Field Programmable Gate Aways</font> (FPGAs), che mettono a disposizione dei progettisti una matrice di elementi logici. Il progettista in base a come scrive il codice VHDL utilizza questi elementi collegandoli in maniere opportuna, attraverso il sintetizzatore.
Un chip FPGAs è una matrice di blocchi programmabili, ogni blocco è un elemento di memoria della quale è possibile memorizzare la tabella di verità della funzione da eseguire. All'interno di un chip ci sono decine di migliaia di lookup table interconnesse, dove lungo il perimetro di esse vi sono IBUF o OBUF che servono a far comunicare il dispositivo con altri.

>All'interno della ZedBoard utilizzata nel corso ci sono lookup table con al più 6 ingressi e 1 uscita.

Una volta eseguita la sintesi il numero di bit che compongono il circuito viene fissato, quindi è necessario eliminare i costruitti generic del component e del circuito. Se fatta partire la simulazione adesso tiene conto dei ritardi delle lookup table ma non dei collegamenti tra esse, perciò si è introdotta una non idealità non totale. Per tenere conto dei collegamenti occorre entrare nella fase di implementazione. che mostra all'interno di Vivado come i componenti sono collegati tra loro dai bus. 
A questo punto si può simulare il comportamento del circuito tenendo conto di tutti i comportamenti reali. Si notano adesso dei valori intermedi, per cosi dire errati che sono i <font color=red>valori di assestamento</font>, legati al fatto che ogni bit ha un tempo di calcolo differente e che l'uscita va assestata quando che tutti i bit sono stati calcolati.

---
# Simulazione esaustiva
Per eseguire una simulazione esaustiva considerando quindi tutte le possibili combinazioni degli ingressi, occorre modificare il test bench per introdurre un loop al posto dello statement process. Dati $n$ bit il minimo ed il massimo valore rappresentabile è dato rispettivamente da $-2^{n-1}$ e $2^{n-1}-1$. Attraverso 2 for è possibile generare tutti gli ingressi possibili, ma prima occorre trasformare gli indici in standard logic attraverso il package `IEEE.std_logic_arith.ALL`, che consente di usare il comando `conv_std_logic_vector()`.
Avremo ad esempio il seguente codice:
```VHDL
architecture behav of Simulation is
[...]

signal IA: STD_LOGIC_VECTOR(n-1 downto 0);
signal IB: STD_LOGIC_VECTOR(n-1 downto 0);
signal ICin: STD_LOGIC;
signal OS: STD_LOGIC_VECTOR(n downto 0);
signal TrueRis, Error: integer;

begin 
	circ: Add_nBit port map(IA,IB,ICin,OS);
	process
	begin 
		for va in -(2**(n-1)) to (2**(n-1)-1) loop
			for vb in -(2**(n-1)) to (2**(n-1)-1) loop
				IA<=conv_std_logic_vector(va,n);
				IB<=conv_std_logic_vector(vb,n);
				TrueRis<=va+vb;
				wait for 10ns;
			end loop;
		end loop;
	end process;
	Error<=TrueRis-CONV_INTEGER(SIGNED(OS))
end behav;
```
Una volta fatto ciò non occorre altro che risimulare il comportamento del circuito senza rieseguire la fase di sintesi e di implementazione.

---


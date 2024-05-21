---
tag: #elettronica
created: 2023-02-15 18:25:33
updated: 2023-02-15 18:25:33
---
#elettronica 
[[VHDL]]
# Esempio tramite modulo strutturato
```VHDL
entity RCA4_v2 is
	port(
	A,B: in bit_vector(3 downto 0);
	Cin: in bit;
	Cout: out bit;
	S: out bit_vector(3 downto 0);
	)
end RCA4_v2;

architecture struct of RCA4_v2 is
	signal C: bit_vector(4 downto 0);
	component FA
		port(
		A,B,Cin: in bit;
		Cout,S: out bit
		);
	end component
	begin 
		FA0: FA port map 
			(A(0),B(0),C(0),S(0),C(1));
		C(0) <= Cin;
		FA1: FA port map
			(A(1),B(1),C(1),S(1),C(2));
		FA2: FA port map
			(A(2),B(2),C(2),S(2),C(3));
		FA3: FA port map
			(A(3),B(3),C(3),S(3),C(4));
		Cout <= C(4);
	end struct;
```
L'istruzione `C(0) <= Cin` la posso scrivere dove voglio non ha importanza la sua posizione.

---
# Esempio tramite modulo comportamentale
``` VHDL
entity RCA4_v4 is:
	port(
	A,B: in bit_vector(3 downto 0);
	Cin: in bit;
	Cout: out bit;
	S: out bit_vector(3 downto 0);
	)
end RCA4_v4;

architecture behav of RCA4_v4 is:
	signal C: bit_vector(4 downto 0);
	signal p,g: bit_vector(3 downto 0);
	begin
		C(0) <= Cin;
		p <= A xor B;
		g <= A and B;
		C(4 downto 1) <= ((p and C(3 downto 0)) or g);
		S <= p xor C(3 downto 0);
		Cout <= C(4);
end behav;
```

---
# Esempio ripple-carry per numeri in complemento a 2
Per utilizzare numeri in complemento a 2 cambiamo la configurazione in 5 full adder per il riporto del segno. In generale se faccio una somma con numeri a $n$ bit la somma sarà di $n+1$ bit.
```VHDL
entity RCA4C2 is:
	port(
	A,B: in bit_vector(3 downto 0);
	Cin: in bit;
	S: out bit_vector(4 downto 0);
	)
end RCA4C2;

architecture behav of RCA4C2 is:
	signal C,p,g: bit_vector(4 downto 0);
	begin
		C(0) <= Cin;
		p <= (A(3) xor B(3)) & (A xor B);
		g <= (A(3) and B(3)) & (A and B);
		C(4 downto 1) <= ((p(3 downto 0) and C(3 downto 0)) or g(3 downto 0));
		S <= p xor C;
end behav;
```
Non si ha quindi più bisogno di Cout. p4 e g4 sono sostanzialmente una copia di p3 e g3. Nella definizione di p viene utilizzata la concatenazione, $A xor B$, va infatti a modificare solo i bit 3-0 di p. Sarà quindi necessario specificare il valore di p4, stessa cosa vale per g.
Nella definizione del riporto è necessario fare attenzione agli indici degli array in quanto p4 e g4 non generano riporto utile, inoltre se non venisse specificato l'intervallo degli indici l'operazione sarebbe incompatibile essendo C di 4 bit mentre p e g di 5.
Vediamo adesso come è realizzata l'implementazione strutturale:
```VHDL 
entity FA is:
	port(
	A,B,Cin: in bit;
	S,Cout: out bit
	);
end FA;

entity RCA4C2 is:
	port(
	A,B: in bit_vector(3 downto 0);
	Cin: in bit;
	S: out bit_vector(4 downto 0);
	)
end RCA4C2;

architecture struct of RCA4C2 is:
	signal C: bit_vector(5 downto 0);
	component FA
		port(
		A,B,Cin: in bit;
		Cout,S: out bit
		);
	end component
	signal IA,IB: bit_vector(4 downto 0);
	begin 
		C(0) <= Cin;
		IA <= A(3)&A;
		IB <= B(3)&B;
		myFor: for i in 0 to 4 generate:
			myFA: FA port map 
				(IA(i),IB(i),C(i),S(i),C(i+1));
		end generate myFor;
end struct;
```
Tutti i full adder sono uguali tra loro anche FA4 produce un riporto che non verrà mai utilizzato, quindi sarebbe meglio eliminarlo. In particolare il tool che trasforma il codice VHDL in circuito, capisce che il segnale non è stato utilizzato e lo trimmera, ovvero lo elimina. Considerando che A(4) e B(4), non sono porte del circuito ma interni, si deve in qualche modo indicare che prendono valore da A(3) e B(3), per fare questo si usano dei segnali. Un’idea potrebbe essere quella di introdurre un vettore interno sia per A che per B che abbia un elemento in più rispetto al numero di porte, il loro valore è stato poi specificato nell'architecture.

---



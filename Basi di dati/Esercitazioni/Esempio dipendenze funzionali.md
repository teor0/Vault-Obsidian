---
tag: #basi 
created: 2023-01-06 19:44:33
updated: 2023-01-06 19:44:33
---
#basi 
# Esempio
Dato lo schema R(ABCDE) e l'insiema di dipendenze funzionali:
- AB$\rightarrow$C
- CD$\rightarrow$E
- E$\rightarrow$ABD
- D$\rightarrow$B
- EC$\rightarrow$D

Riduciamo le parti sinistre (RidSX), quando una parte sinistra implica un'altra. Prendiamo AB$\rightarrow$C e vedo se ci sono dipendenze tra A e B. Vado a vedere la chiusura di A, ovvero $A^+=A$ e la chiusura di B, ovvero $B^+=\oslash$.
Vediamo CD$\rightarrow$E: $C^+=C$ e $D^+=DB$. EC$\rightarrow$D: $E^+=EABDC$ quindi posso scrivire in forma compatta E$\rightarrow$D.
Riduciamo le parti destre (RidDX):
AB$\rightarrow$C per ridurre devo calcolare la chiusura di AB considerando solo le altre dipendenze. Quindi, se tolgo AB dalle dipendenze, in cosa coincidono? $(AB)^+=AB$ quindi non posso cancellare la dipendenza.
CD$\rightarrow$E, $(CD)^+=CDB$ anche questa non la posso togliere.
E$\rightarrow$ABD, nel ridurre le parti destre considero il tutto uno per volta quindi, E$\rightarrow$A non porta a nulla, E$\rightarrow$B se calcolo la chiusura ottengo $E^+=EADB$ quindi ho ridondanza. Infine E$\rightarrow$D, $E^+=EAD$ anche in questo caso ho ridondanza.
Alla fine otterroò il seguente grafo:
![[grafdies.jpg]]
Le possibili chiavi sono keys={E,CD,AD} in quanto implicano tutto.

Una volta fatte modifiche si considera l'insieme modificato. L'insieme che si ottiene è diverso in base all'ordine che si fa, non c'è quindi solo una copertura minimale.

---




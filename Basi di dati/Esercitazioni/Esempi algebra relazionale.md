---
tag: #basi 
created: 2022-12-14 11:02:22
updated: 2022-12-14 11:02:22
---
#basi 
# Esempi
Fornitore

| P.IVA | Nome | Città |
| ----- | ---- | ----- |
| F1    | A    | CS    |
| F2    | B    | RC    |
| F3    | C    | CS    | 

Fornitura

| P.IVA | Merce | Prezzo |
| ----- | ----- | ------ |
| F1    | M1    | 10€    |
| F2    | M2    | 5€     |
| F1    | M2    | 6€     | 

Merce

| Codice | Nome | Marca    |
| ------ | ---- | -------- |
| M1     | X    | $\alpha$ |
| M2     | Y    | $\beta$  |
| M3     | Z    | $\alpha$ |

$\displaystyle\large{(Fornitore\bowtie_{\$1=\$1}Fornitura)}$ ritorna 

| P.IVA | Nome | Città | P.IVA | Merce | Prezzo |
| ----- | ---- | ----- | ----- | ----- | ------ |
| F1    | A    | CS    | F1    | M1    | 10€    |
| F1    | A    | CS    | F1    | M2    | 6€     |
| F2    | B    | RC    | F2    | M2    | 5€     |


Query: Elenco dei codici delle merci fornite da A.
$\displaystyle\large{\Pi_{\$5}[\sigma_{\$1=\$4\land \$2='A'}(Fornitore\times Fornitura)]}$ mentre attraverso la join
$\displaystyle\large{\Pi_{\$5}[\sigma_{\$2='A'}(Fornitore\bowtie_{\$1=\$1} Fornitura)]}$

Query: Coppie <Nome fornitore, Nome Merce> tale che il fornitore fornisce la merce.
$\displaystyle\large{\Pi_{\$5,\$8}[(Fornitura\bowtie_{\$1=\$1}Fornitore)\bowtie_{\$2=\$1}Merce]}$

Query: Nomi merci fornite da fornitori di Cosenza
$\displaystyle\large{\Pi_{\$8}\{[\sigma_{\$3='CS'}(Fornitore)\bowtie_{\$1=\$1}Fornitura]\bowtie_{\$5=\$1}Merce\}}$
---

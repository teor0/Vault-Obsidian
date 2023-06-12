#fondamenti
[[Comunicazione e protocolli di comunicazione]]
# Definizione sistema di comunicazione digitale
È un sistema che trasferisce l'informazione digitale, da una sorgente digitale ad un nodo. Un sistema di comunicazione analogico trasferisce l'informazione analogica da una sorgente analogica ad un nodo. Ai fini del livello fisico l'informazione è vista come un'onda.
![[ondaanalogica.png| Forma d'onda analogica]]
Ha dominio e codominio continuo. f(t) periodica forma d'onda armonica. La frequenza f=$\large 1\over T$ dove T è il periodo.
![[ondaanalogica2.png| anche questa è una forma d'onda continua]]
![[ondadigitale.png| Forma d'onda digitale]]
La tensione rappresenta i bit 1 e 0. Il segnale non è continuo nel tempo ed il codominio ha valori discreti, non hanno appartenenza ad un dominio continuo. Questa forma d'onda è chiamata codice unipolare. Un altro tipo di codice è la codifica Manchester
![[manchester.png]]
Lo standard di comunicazione quando definisce lo standard del livello fisico sceglie anche il tipo di codifica con cui i bit 1 e 0 devono essere rappresentati.

---
## Differenza tra sistema elettrico e sistema di comunicazione
Nel sistema elettrico in genere le forme d'onda sono conosciute a priori e la progettazione del sistema mira a ridurre la perdita d'energia. Nel sistema di comunicazione la forma d'onda che arriva al nodo è sconosciuta, altrimenti non ci sarebbe comunicazione e la necessità di un protocollo. Il sistema progettato deve:
- essere robusto
- in grado d'adattarsi alle alterazioni da rumore/disturbo

Vantaggi comunicazione digitale:
- circuiti digitali relativamente poco costosi
- privacy offerta tramite crittografia
- dati provenienti da voce, video e dati tradizionali possono essere unificati e trasmessi sullo stesso sistema digitale, ovverro il multiplexing
- per sistemi di comunicazione a lunga distanza il rumore non si accumula da ripetitore a ripetitore
- gli errori sui dati relativi possono essere resi piccoli in presenza di "grande rumore" sul segnale ricevuto
- gli errori possono essere corretti attraverso l'uso della codifica 

Svantaggi comunicazione digitale:
- in generale è richiesta più banda rispetto i sistemi analogici
- è richiesta la sincronizzazione

---

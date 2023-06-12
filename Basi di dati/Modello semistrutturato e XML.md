---
tag: #basi 
created: 2023-01-13 16:33:04
updated: 2023-01-13 16:33:04
---
#basi 
[[B+-Tree]]
# Modello semistrutturato
Vediamo le differenze tra il modello relazionale ed il modello semistrutturato. Il modello relazionale ha le seguenti caratteristiche:
- È fortemente strutturato
- La struttura dei dati tipicamente non varia
- Schema e dati sono ben distinti
- Schema più piccolo dei dati

Il modello semistrutturato ha le seguenti caratteristiche:
- Struttura lasca, cioè non tutti i dati hanno la stessa forma
- Struttura di ciascun dato può variare nel tempo
- Lo schema può essere codificato nei dati
- Lo schema può avere dimensioni paragonabili ai dati

Un modello destrutturato è il testo libero.
Il linguaggio standard per il modello semistrutturato è XML.

---
# Linguaggio XML
XML sta per eXtensible Markup Language, ovvero linguaggio di delimitatori estendibile. I delimitatori si usano per definire la struttura del dato che sto rappresentando. Esempio di file:
``` xml
<biblioteca>
	<libro>
		<titolo> Divina Commedia </titolo>
		<autore> Dante Alighieri </autore>
	</libro>
	<libro>
		<ISBN> 348-1108 </ISBN>
		<autori>
			<autore> Diterlizzi </autore>
			<autore> Lucentini </autore>
		</autori>
		<titolo> Un caso difficile </titolo>
		<editore> Mondadori </editore>
	</libro>
</biblioteca>
```
Una cosa del genere in una base di dati relazionale non si può rappresentare in maniera semplice.
Perché si chiama extensible? Perchè i delimitatori o tag che dir si voglia, sono "artigianali" ovvero posso scegliere io il nome del tag. Tutto ciò che è tra 2 tag è un elemento. Ogni volta che arriva un dato posso inserirlo come nuovo elemento nella mia collezione. 
Il documento che si ottiene è un documento di testo con codifica UNICODE o UTF-8. Questo modello è pensato per prendere informazioni diverse ed unirle, inoltre il modello è pensato per favorire la condivisione. 
In modo lasco definisco una Biblioteca come una lista di libri, ogni libro ha un titolo, può avere un ISBN, un editore ecc.

Le informazioni possono essere rappresentate anche in termini di attributi e non solo elementi. All'interno di un tag posso scrivere degli attributi in modo da fornire ulteriori informazioni. Esempio:
``` xml
<biblioteca>
	<libro anno="1980" prezzo="29€">
		<titolo> Divina Commedia </titolo>
		<autore> Dante Alighieri </autore>
	</libro>
</biblioteca>
```
Dato che XML favorisce la condivisione, è buona norma scrivere in modo leggibile, sia per la macchina che per l'uomo. Di fatto una struttura comune tuttavia si può trovare, si utilizza una data-guide, un modo per definire ciò che è il documento DTD (Data Type Definition) accoppiato al file XML.
Esempio:
``` xml
<!ELEMENT biblioteca (libro *)>
<!ELEMENT libro (ISBN?,titolo,autori|autore,editore?)>
<!ELEMENT autori (autore +)>
<!ELEMENT ISBN #PCDATA>
<!ELEMENT autore #PCDATA>
<!ELEMENT editore #PCDATA>

<!ATTLIST libro identificatore ID prezzo CDATA curatore IDREF>
```
L'asterisco indica la presenza di 1 o più elementi, il punto interrogativo indica che l'elemento può mancare e la slash verticale sta per OR, il più indica la presenza di almeno un elemento. PCDATA sta per Parsed Character Data ovvero stringhe sottoposte a parsing, utile a visualizzare gli escape character, i caratteri speciali preceduti da una slash. Un elemento può possedere degli attributi, questi hanno un tipo e, se si ha ID l'attributo è identificatore d'oggetto, CDATA indica che il tipo è una stringa infine IDREF si usa come una sorte di chiave esterna, esiste anche la possibilità di usasre IDREFS per impiegare più riferimenti separati da uno spazio. Gli attributi sono CDATA e non PCDATA in quanto non sono sottoposti a parsing.
Esempio:
``` xml
<libro identificatore="L1" prezzo="10€" curatore="C1">
...
</libro>
<curatore identificatore="C1">
...
</curatore>
```
Il meccanismo degli IDREF è molto generico rispetto a quello di una chiave esterna.
Uno schema può essere ricorsivo ad esempio:
``` xml
<!ELEMENT a(a|bc)>
```
Un mixed element ha una struttura del tipo
``` xml
<a> 
string 
<b> ... </b>
string 
<c> ... </c>
</a>
```
Un mixed element perciò contiene sia stringhe che sottoelementi. All'interno del DTD si specifica come:
``` xml
<!ELEMENT a((b|c|d|#PCDATA)*)> 
```
Non esiste una maniera più precisa.

XML è uno standard definito dal [Word Wide Web Consorsium](www.w3c.org).

---
# Interrogazioni in XML
Supponiamo di avere il seguente documento XML:
``` xml
<biblioteca>
	<libro ID="L1" casaEd="CE1">
		<titolo>TL1</titolo>
		<autore>AL1</autore>
	</libro>
	<libro ID="L2" casaEd="CE1">
		<titolo>TL2</titolo>
		<autori>
			<autore>AL2</autore>
			<autore>AL3</autore>
		</autori>
		<annoEd>2000</annoEd>
	</libro>
	<casaEd ID="CE1">nomecasaEd1</casaEd>
</biblioteca>
```
il DTD accoppiato sarà:
``` XML
<!ELEMENT biblioteca (libro+,casaEd+)>
<!ELEMENT libro (titolo, autore|autori,annoEd?)>
<!ELEMENT autori(autore+)>
<!ATTLIST libro ID ID casaEd IDREF>
<!ELEMENT casaEd #PCDATA>
<!ATTLIST casaEd ID ID>
```
Immaginiamo il file XML come un albero:
![[grafdirettxml.jpg]]
Per distinguere un nodo attributo da altri si usa @. Gli attributi sono nodi senza figli, tuttavia i riferimenti tramite IDREF è se fossero archi tratteggiati che cambiano la struttura del albero. 
Questo modello si chiama grafo diretto aciclico, ma continuamo a chiamarlo albero. 

Un primo linguaggio per l'interrogazione di file XML è <font color=red>XPath</font>. XPath consente di specificare comodamente quali cammini da percorrere per raggiungere nodi da cui si vuole estrarre l'informazione. Esempio: `document("mioxml")/child::biblioteca/child::libro/child::titolo`

Il risultato è una sequenza di nodi ordinati o meglio è una porzione di testio ossia: 
``` XML
<titolo>TL1</titolo>
<titolo>TL2</titolo>
```
XPath è una sequenza di assi navigazionali, oltre child si può usare descendant che dato un nodo estrae tutti i discendenti di quel nodo che hanno la proprietà scritta dopo i due punti. Esempio: `document("docxml")/descendant::titolo` 
Si estraggono i titoli discendenti dalla radice, utile il suo utilizzo per trovare tutti gli autori dato che, alcuni libri hanno il tag \<autori> e serve un altro cammino per considerarli.
`document("docxml")/descendant::libro/child::autore`

Gli assi navigazionali di XPath sono:
- child: per scendere al figlio
- descendant: per scendere di un numero qualunque di figli, con la variante descendant-or-self per esprimere la possibilità di specificare i discendenti o se stessi.
- parent: per salire al padre del nodo
- ancestor: per salire alla radice, con la variante ancestor-or-self per esprimere la possibilità di specificare l'ancestor o se stessi.
- sibling: per spostarsi sui fratelli del nodo

Per convenzione se non si scrive nulla è sottointeso child, se si scrive // è sottointeso descendant. Attraverso text() si ottiene come risultato solo il text. Per conoscere gli ID dei libri la query è la seguente:
`document("docxml")//libro/@ID`

Per esprimere una condizione, ovvero un filtro di selezione si utilizzano le parentesi quadre. Ad esempio: `document("docxml")//libro[./annoEd/text()="2000"]/titolo` ritorna libro se l'anno di pubblicazione del libro è 2000. Il titolo dei libri in cui viene specificato l'anno di pubblicazione si ottiene tramite la query: `document("docxml")//libro[./annoEd]/titolo`
La query precedente si può scrivere come `document("docxml")//libro[./annoEd="2000"]/titolo` questo perché quando avviene una comparazione, i due operandi della comparazione vengono tramutati nei loro valori.
XPath serve solo ad estrarre informazioni, per essere ancora user-friendly XPath permette di evitare di scrivere ./ solo quando il primo asse è un figlio.

All'interno di XPath esiste la wildcard * che sta per qualsiasi utile per le condizioni di disgiunzione. Esempio:
``` XML
<!ELEMENT collezione (libro+,rivista+)>
<!ELEMENT libro (titolo,autore)>
<!ELEMENT rivista (titolo,articolo+)>
<!ELEMENT articolo (nome,autore,revisori)>
<!ELEMENT revisori (revisore+)>
<!ELEMENT autore (nome)>
<!ELEMENT revisore (nome)>
```
La query `document()//rivista/autore/nome` può essere riscritta in `document()//rivista/*/nome` in quanto il nome che sta due livelli sotto è solo quello di autore.

Le query sono innestabili quindi `document()//a[b/c="10"][.//d=.//f]/q` è valida.

> XPath non è un vero linguaggio di interrogazione perché non permette di riformulare la struttura del documento ma solo di estrarre informazioni.


---
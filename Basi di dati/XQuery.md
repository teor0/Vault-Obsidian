---
tag: #basi 
created: 2023-01-30 11:37:49
updated: 2023-01-30 11:37:49
---
#basi 
[[Modello semistrutturato e XML]]
# XQuery
XQuery ingloba XPath e consente di riformulare la struttura del documento che viene restituito.
Prendiamo il seguente documento come esempio:
``` xml
<!ELEMENT bib (book*)>
<!ELEMENT book (title, (author+ | editor+), publisher, price )>
<!ATTLIST book year CDATA #REQUIRED >
<!ELEMENT author (last, first)>
<!ELEMENT editor (last, first, affiliation)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT last (#PCDATA)>
<!ELEMENT first (#PCDATA)>
<!ELEMENT affiliation (#PCDATA)>
<!ELEMENT publisher (#PCDATA)>
<!ELEMENT price (#PCDATA)>
```
Con XPath una possibile query, sarebbe quella che estrae i titoli dei libri il cui autore o editore ha last name X e pubblicato nel 2000 ed è data da: 
`document("doc.xml")//book[.//last="X"][@year="2000"]/title`
Il risultato è una sequenza di nodi `<title>...</title>` che non è un documento XML, in quanto manca la radice, tuttavia se il risultato comprende solo un nodo title, allora tecnicamente sarebbe un documento XML ben formato.

XQuery si basa sulle clausole un po' come SQL, ma a differenza sua non è strutturato come SQL che richiede prima SELECT e dopo FROM. L'ordine delle clausole non è quindi imposto a priori. 
La clausola principale di XQuery è <font color=orange>return</font>. La clausola return può avere come argomento un'espressione XPath. Per formare un documento XML a partire da una espressione XPath, posso inglobare tale espressione dentro due tag. Ad esempio:
`return <risultato> document("doc.xml")//book[.//last="X"]/publisher </risultato>`
XQuery è un linguaggio di scripting che può essere innestato in un documento XML, nel farlo bisogna aggiungere le parentesi graffe altrimenti la return interpreta l'espressione XPath come una sequenza di caratteri. Ho due risultati diversi a seconda di cosa scrivo:
```
return <risultato> 
	document("doc.xml")//book[.//last="X"]/publisher 
	</risultato>

Ritorna: <risultato> 
	document("doc.xml")//book[.//last="X"]/publisher 
	</risultato>

return <risultato> 
	{document("doc.xml")//book[.//last="X"]/publisher} 
	</risultato>

Ritorna: <risultato> 
	<publisher> ... </publisher>
	<publisher> ... </publisher>
	<publisher> ... </publisher>
	</risultato>
```
Quando si crea un elemento con dentro un espressione si chiama costruttore di elemento.
Supponiamo adesso di voler ritornare un documento che anziché contenere nodi \<publisher> contenga nodi \<casaEditrice>. Per fare ciò si utilizza la clausola <font color=orange>for</font> che itera all'interno di una espressione XPath. Esempio:
`for $p in document("doc.xml")//book[.//last="X"]/publisher`
questo viene utilizzato assieme a return come segue:
```
for $p in document("doc.xml")//book[.//last="X"]/publisher
return <casaEditrice> 
	{$p/text()} 
	</casaEditrice>
```
Questa query però ritorna:
```
<casaEditrice> ... </casaEditrice>
<casaEditrice> ... </casaEditrice>
<casaEditrice> ... </casaEditrice>
<casaEditrice> ... </casaEditrice>
```
Verrebbe naturale pensare ad una query del tipo:
```
for $p in document("doc.xml")//book[.//last="X"]/publisher
return <risultato> 
		<casaEditrice> 
		{$p/text()} 
		</casaEditrice>
	</risultato>
```
ma anche questa è errata in quanto ritorna:
```
<risultato>
	<casaEditrice> ... </casaEditrice>
</risultato>
<risultato>
	<casaEditrice> ... </casaEditrice>
</risultato>
<risultato>
	<casaEditrice> ... </casaEditrice>
</risultato>
<risultato>
	<casaEditrice> ... </casaEditrice>
</risultato>
```
La soluzione corretta è:
```
<risultato>
{ for $p in document("doc.xml")//book[.//last="X"]/publisher
return <casaEditrice> 
	{$p/text()} 
	</casaEditrice>
}
</risultato>

Ritorna: 
<risultato>
	<casaEditrice> ... </casaEditrice>
	<casaEditrice> ... </casaEditrice>
	<casaEditrice> ... </casaEditrice>
	<casaEditrice> ... </casaEditrice>
</risultato>
```

La clausola <font color=orange>where</font> permette di fare una selezione come quella di SQL. Esempio: restituire i titoli dei libri pubblicati dopo il 2000.
```
<risultato>
{
for $b in document("doc.xml")//book
where $b/@year>"2000"
return <titolo> {$b/title/text()} </titolo>
}
</risultato>
```

>[!regola]
> Si capisce quindi che la clausola return è quella che va messa alla fine!

Esiste anche la clausola <font color=orange>let</font> che permette di assegnare ad una variabile un valore. Esempio:
```
<risultato>
{
for $b in document("doc.xml")//book
let $a:= $b//author
return <libro>
	<titolo> {$b/title/text()} </titolo>
	<autori> 
		{
		for $x in $a
		return <cognomeAutore> {$x/last/text()} </cognomeAutore> 
		} 
	</autori>
	</libro>
}
</risultato>
```
Questa query ritorna una lista di libri all'interno di risultato e ne riporta il titolo e per ogni autore il suo cognome dentro un tag \<cognomeAutore>. 
Le query possono quindi essere innestate e naturalmente hanno regole di visibilità. 
XQuery possiede anche funzioni come ad esempio quella per il conteggio. Esempio:
```
<risultato numTitoli="{count(document("doc.xml")//book)}">
{
for $t in document("doc.xml")//title
return <libro>
	<titolo> {$t/text()} </titolo>
	</libro>
}
</risultato>
```
Count ha come argomento una sequenza, quindi si potrebbe fare a meno di scrivere la let e di mettere come argomento di count `$b//author`.

Esempio, restituire i titoli dei libri scritti solo da Dan Suciu:
```
<risultato>
{
for $b in document("doc.xml")//book[ author[last=Suciu][first=Dan]]
return <titolo> {$b//title/text()} </titolo>
}
</risultato>

oppure 
<risultato>
{
for $b in document("doc.xml")//book
for $a in $b/author
where $a/first="Dan" and $a/last="Suciu"
return <titolo> {$b//title/text()} </titolo>
}
</risultato>
```

Per ogni publisher, la lista di libri che ha pubblicato:
```
<risultato>
{
for $p in document("doc.xml")//publisher
return <publisher>
	<name> {$p/text()} </name>
	<libri> 
	{
	for $t in document("doc.xml")//book[publisher=$p]/title
	return $t
	}
	</libri>
	</publisher>
}
</risultato>
```
La funzione distinct-values applicato ad una sequenza, ne estrae solo i valori diversi in valore testuale.
```
<risultato>
{
for $p in distinct-values (document("doc.xml")//publisher)
return <publisher>
	<name> {$p} </name>
	<libri> 
	{
	document("doc.xml")//book[publisher=$p]/title
	}
	</libri>
	</publisher>
}
</risultato>
```

---
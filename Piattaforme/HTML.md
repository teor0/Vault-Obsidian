Un documento HTML (Hyper Text Markup Language) è testo puro. La struttura è descritta da dei tag che lavorano tipicamente in coppia. Creo cosi una struttura ad albero. Il tag serve a specificare informazioni rispetto al suo contenuto, tali informazioni possono essere di struttura o di formattazione del documento. Il contenuto di un tag può essere un altro tag. Il contenuto vero e proprio del documento è il tag body.

Si hanno poi:
- Il tag head che può mancare
- Header di diverso livello tramite h1, h2, ... fino a h6
- Paragrafi con il tag \<p> 
- Marcatori di formattazione senza testo, ovvero ritorno a capo \<br/>

HTML è stato pensato per poter essere scritto da esseri umani, quindi il browser riesce ad interpretare il documento anche in presenza di errori. 
Un tag di apertura può avere degli attributi esempio:
`<meta name="Author" content ="Pinco Pallino"`
dove name è l'attributo e Author è il valore dell'attributo. I tag meta hanno 2 tipi di uso:
1. Definizione di una coppia nome valore generica
2. Definizione di una coppia nome valore per creare un header della risposta

Il tag font permette di specificare il formato del testo, tuttavia sostituito da CSS. Si ha poi la possibilità di inserire elementi multimediali attraverso gli URI. Ad esempio:
`<img src="pianta.jpg" alt="PIANTA" title="plant" style="width: 100px; height: 100px;">` dove il valore dell'attributo src è un URL, ma nel caso dell'esempio utilizziamo un formato relativo, che parte dalla posizione della pagina corrente.
Il link è un costrutto di base dell'ipertesto. I link vengono implementati con le ancore di origine ovvero il tag \<a> vediamo un esempio:
`<a href="capitolo2.html"> capitolo 2</a>`
Il valore dell'attributo href è un URL relativo o assoluto. Si può avere anche come valore dell'attributo il frammento che parte con #. Per usare i frammenti si sfruttano le ancore di destinazione che a differenza di quelle di origine non hanno l'attributo href, ma name e questo torna utile per le tabelle dei contenuti.

## Liste 
Si hanno le seguenti liste in html:
- Liste non ordinate: 
``` html
<ul type="disc">
    <li> Pippo </li>
    <li> Pluto </li>
    <li> Paperino </li>
</ul>
```
- Liste ordinate: 
``` html
<ol type="I">
    <li> Pippo </li>
    <li> Pluto </li>
    <li> Paperino </li>
</ol>
```
- Liste di definizione: 
``` html 
<dl>
    <dt> Cane </dt>
    <dd> Pluto </dd>
    <dt> Papero </dt>
    <dd> Paperino </dd>
</dl>
```
## Tabelle
Per rappresentare le tabelle si rappresenta il tutto come una sequenza di righe dove ogni riga ha un suo elemento:
``` html
<table border="1">
    <caption align="top"><em> Test tabella </em></caption>
    <tr>
	   <th rowspan="2"></th>
	   <th colspan="2">Medio</th>
	   <th rowspan="2">Occhi<br/>rossi</th>
    </tr>
    <tr><th>Altezza</th><th>Peso</th></tr>
    <tr><th>Maschio</th><td>1.9</td><td>0.03</td><td>40%</td></tr>
    <tr><th>Femmina</th><td>1.7</td><td>0.01</td><td>80%</td></tr>
</table>
```
Il tag table può avere i seguenti attributi:
- align: left,center,right
- width: n oppure n%
- bgcolor: da esprimere in hexadecimal
- border: n
- cellspacing
- cellpadding

## Prendere l'input dall'utente
Per prendere un input dall'utente si usano i form, i form altro non sono che i bottoni, checkbox, menù di selezione, aree di testo, oggetti nascosti ecc. vediamo un esempio: 
``` html
<form name="miaform" action="pagina2.html" method="GET" novalidate="novalidate">
    <input name="Nome" value="Inserisci il cognome" size="20" maxlenght="25" autocomplete="on" type="text"><br>
</form>
```
L'attributo method specifica il modo in cui i dati sono inviati e può essere di 2 tipi:
1. GET: il nome del input viene associato all'input preso e l'url andrà ad essere quello della action seguito da ?/Nome input=input preso
2. POST: stampa il contenuto della richiesta



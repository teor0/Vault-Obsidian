---
tag: #basi 
created: 2022-11-29 11:28:54
updated: 2022-11-29 11:28:54
---
#basi 
[[Modello relazionale]]
# Vincolo di unicità e giusta traduzione dei vincoli di relazione
Se ci sono più chiavi candidate bisogna indicare prima la chiave primaria che è il meccanismo più semplice di ricerca. Se in un modello voglio specificare che una coppia di attributi fa sì che non esistano istanze di un'entità con tale coppia di attributi uguale si utilizza il vincolo di unicità <font color=red>unique</font>. Ad esempio: 
Fornitore(<u>P.IVA</u>, $\overbrace{Nome, Città}^{UNIQUE}$)
> Per consistenza del modello, è buona norma indicare tutti i meccanismi identificativi.

Il vincolo di chiave primaria è definito nello schema e stabilisce che dentro un'instanza non ci possano essere tuple distinte con lo stesso attributo della chiave. Attributi che sono _unique_ non possono far parte di una chiave esterna, quindi solo chiavi primarie possono far parte della chiave esterna.
Prendiamo ora la relazione Fornitore-Fornitura-Merce:
![[vincoli.jpg]]
In quanto la relazione è molti a molti ed una coppia al più c'è una volta, la chiave di fornitura è (Fornitore,Merce). L'attributo fornitore nell'istanza dovrà essere rappresentato con valori presenti nell'istanza di fornitore. Perciò lo schema di tabella sarà: Fornitura(<u>Fornitore,Merce</u>, Prezzo), Fornitura\[Fornitore\]$⊑_{FK}$Fornitore\[P.IVA\], Fornitura\[Merce\]$⊑_{FK}$Merce\[Codice\].

Vediamo un altro esempio per capire meglio:
![[esempioFattura.jpg]]

Fattura(<u>Numero, Anno</u>, Dettagli)
Prodotto(<u>Codice</u>, Nome)
Composizione(<u>Fattura, Prodotto</u>, Quantità, Prezzo)
Composizione\[Fattura\]$⊑_{FK}$Fattura\[Numero, Anno\]
Per com'è la relazione Composizione, ovvero molti a molti la schematizzazione risulta corretta no? Sbagliato, non si può assocciare un attributo a 2! La soluzione corretta sarebbe:
Composizione(<u>Fattura\_Numero, Fattura\_Anno, Prodotto</u>, Quantità, Prezzo)
Composizione\[Fattura\_Numero, Fattura\_Anno\] $⊑_{FK}$ Fattura\[Numero, Anno\].

Riprendiamo la relazione Merce-Marca:
![[utilizzoNull.jpg]]
Schematizzare Produzione(<u>Merce,Marca</u>), Produzione\[Merce\]$⊑_{FK}$Merce\[Codice\], Produzione\[Marca\]$⊑_{FK}$Marca\[Nome\]
Essendo il vincolo 0:1 la chiave <Merce,Marca> non è minimale, perché dentro produzione una merce è presente al più una volta. Il vincolo imposto tramite chiave esterna afferma che non tutti i codici sono dentro produzione ma un sottoinsieme, sarebbe invece corretto aggiungere la proprietà NULL a produzione. 

Come tradurre invece un vincolo 1:n? Se supponiamo che la relazione tra Fornitore e Merce sia con vincolo 1:n allora lo schema

Fornitore(<u>P.IVA</u>, Nome, Città)
Merce(<u>Codice</u>, Nome, $\overset{NULL}{Marca}$)
Fornitore\[Merce\]$⊑_{FK}$Merce\[Codice\]
è errato perchè solo un sottoinsieme di Merce andrà a finire dentro la tabella di fornitore. Per rimendiare si potrebbe utilizzare l'attributo Merce1:
Fornitore(<u>P.IVA</u>, Merce1, Nome, Città), Fornitore\[Merce1\]$⊑_{FK}$Merce\[Codice\] cosi facendo si rispetta il vincolo 1:n ma si crea ancora inconsistenza e riferimenti ciclici, andiamo perciò a rilassare il vincolo portandolo a 0:n.

>Generalmente per vincoli piccoli come 0:1 è bene valutare se è opportuno rilassare mentre per vincoli grandi <font color=red>bisogna</font> rilassare a 0:n. Una volta che si decide di rilassare un vincolo, il perché va scritto a parole e spiegato cosa si perde nel farlo, questo perché il progetto concettuale descrive le informazioni così come sono nelle realtà, indipendentemente da come saranno tradotte nel data base.

Affrontiamo adesso un altro problema, ovvero quello di vincoli specifici del tipo 2:4, 1:2, 0:3. Prendiamo come esempio il seguente modello ER: ![[vincoliSpec.jpg]]
La giusta soluzione per mantenere il vincolo 1:2 sarebbe: Squadra(<u>Nome</u>, Descrizione, Giocatore1,$\overset{NULL}{Giocatore2}$). In alternativa si potrebbe rilassare il vincolo. Ovviamente l'utilizzo di NULL ha senso in questo caso, mentre magari con un vincolo 0:10, non è molto efficiente avere molte colonne vuote.

---

# Generalizzazioni nel modello relazionale
Riprendiamo il modello relazionale che realizza una generalizzazione: ![[generalizzazione.jpg]]
Persona(<u>Codice Fiscale</u>, Nome, Studente/Docente, SSD, Matricola)
Una tupla di persona contiene un booleano che se vero identifica la persona come studente e se falso come docente. Tuttavia se ammetto che SSD sia NULL non ho modo di dire che invece Matricola non lo sia, in più se gli attributi sono molti, c'è il rischio di avere una tabella enorma difficile da gestire.

Vediamo adesso come tradurre il seguente modello ER: ![[tradGen.jpg]]
Per tradurre la generalizzazione, distinguiamo 3 casi:
![[casiGeneral.jpg]]
Il <font color=red>caso A</font> si traduce accorpando tutte sottoentità all'entità madre, Persona(<u>Codice fiscale</u>, Nome, $\overset{NULL}{Matricola}$, $\overset{NULL}{SSD}$) dove a seconda della specificazione tra Studente o Docente un attributo tra matricola e SSD è NULL. Questa soluzione preserva totalità ed esclusività SOLAMENTE se le sottoentità sono isolate altrimenti si perde la distinzione attraverso chiavi esterne di entità in relazioni con una sottoentità, nel modello ER fatto si perderebbe in quanto la relazione titolarità è solo di Docente, mentre per com'è realizzata la tabella Persona anche uno studente potrebbe avere una titolarità, in più se gli attributi delle sottoentità sono tanti si rischia di avere una tabella gigante con tanti NULL.

Il <font color=red>caso B</font> si traduce in materializzare le tabelle: Persona(<u>Codice fiscale</u>, Nome), Studente(<u>Persona</u>, Matricola), Docente(<u>Persona</u>, Nome, SSD), Insegnamento(<u>Codice</u>, Nome, Docente), Studente\[Persona\]$⊑_{FK}$Persona\[Codice fiscale\], Docente\[Persona\]$⊑_{FK}$Persona\[Codice fiscale\] e Insegnamento\[Docente\]$⊑_{FK}$Docente\[Persona\]. Questa soluzione però perde totalità e l'esclusività della generalizzazione, in quanto un tupla di Persona potrebbe non aver nessun corrispondente né in Docente né Studente, inoltre il vincolo di chiave esterna dice che una tupla di Docente o Studente si riferisce ad una in Persona ma non viceversa, quindi si perde la totalità. Infine una tupla di Docente, potrebbe corrispondere ad una in Studente, quindi ho perso l'esclusività.

Il <font color=red>caso C</font> è quello in cui non si materializza l'entità madre, andando a perdere però di esclusività perché, dato un valore della chiave dell'entità madre, si potrebbe mettere una tupla in entrambe le sottoentità. Questo risulta conveniente quando l'entità madre non ha relazioni con altre entità.
Si capisce quindi che non c'è un modo opportuno per tradurre la generalizzazione.
>[!Regola]
>Il caso scelto va espresso a parole all'interno del esame!

Infine per quanto riguarda una generalizzazione IS A in genere si sceglie il caso B oppure A, ma dipende sempre dalle relazioni in ballo tra entità madre e sottoentità ed il numero di attributi di entità madre e sottoentità. 
![[tradISA2.jpg]]

---

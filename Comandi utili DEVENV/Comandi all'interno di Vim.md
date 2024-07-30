# Modalità VIM
Ci sono 3 modalità per VIM:
1. Normal mode, navigare all'interno del file
2. Insert mode, editare il test
3. Visual mode, copiare/eliminare testo

# Come entrare nella insert mode
La insert mode può essere acceduta nelle seguenti maniere:
- i, entra nella insert mode nella posizione attuale del cursore
- I, entra nella insert mode all'inizio della linea
- o, entra nella insert mode nella riga sotta quella attuale
- O, entra nella insert mode nella riga sopra quella attuale
- a, entra nella insert mode nella posizione successiva a quella attuale del cursore
- A, entra nella insert mode a fine linea
- C, cancella dal cursore fino a fine linea ed entra in insert mode

# Come tornare alla normal mode
Per uscire dalla insert mode o visual mode e tornare nella normal mode è sufficiente premere <font color=red> esc</font>.

# Come muoversi all'interno della normal mode
Per muoversi in un documento VIM utilizza i tasti hjkl nel modo seguente:
``` 
       ^
	   k
   < h   l >
       j
	   V
```
ma ci si può muovere anche tra le parole e WORD. Per WORD si intendono stringhe senza contare i caratteri di punteggiatura e le parentesi. Perciò:
- w, vai all'inizio della prossima parola
- W, vai all'inizio della prossima WORD
- b, vai all'inizio della parola precedente
- B, vai all'inizio della WORD precedente
- e, vai alla fine della prossima parola
- E, vai alla fine della prossima WORD

a questi comandi si può aggiungere il numero di volte che si vuole eseguire. Quindi ad esempio se mi trovo in normal mode e scrivo 150B, torno indietro di 150 WORD.

# Cercare e sostituire testo
Per usare la funzione search o replace di VIM bisogna essere in normal mode. Per cercare una parola si usa la slash seguita dalla parola che si vuole cercare. Per muoversi tra un occorrenza e l'altra si usano:
- n per andare avanti
- N per andare indietro

Per ripetere la ricerca precedente è sufficiente fare doppia slash //. 

Si può addirittura utilizzare ? per fare una search all'indietro rispetto a dove si trova il cursore. Ci si muove alla stessa maniera della slash.

\* permette di cercare la prossima occorrenza della parola su cui i trova il cursore, mentre # l'occorrenza precedente.

Per la sostituzione di testo si usa una sintassi simile alla sed, ovvero:
``` :%s/find/replace/options ```
dove le opzioni possono essere:
- g sostituzione globale
- gi sostituzione globale case insensitive
- gc sostituzione con prompt di sicurezza

# Aprire una nuova tab e muoversi tra esse 
Si può aprire una nuova tab, attraverso il comando `` :tabnew `` da eseguire in normale mode. Per muoversi tra le tab si utilizzano:
- ```:tabn ``` tab successiva
- ```:tabp ``` tab precedente
- ```:tabfirst ``` prima tab
- ```:tablast``` ultima tab

Si possono spostare le tab attraverso ```:tabmove 0 ```. In questo caso si mette la tab attuale come prima tab.

# Salvare un file
Per salvare un file, si usa il comando ```:w ``` in normal mode.
Per salvare un file senza nome si usa sempre il comando ```:w nomefile ```
# Aprire un file
Per aprire un file senza avere una GUI si usa ```:e nomefile```. Per conoscere quali file si possono aprire basta preme tab dopo il comando.

Per aprire un file basta scrivere ```:e PATH ASSOLUTO```

# QUITTARE DA VIM
Per uscire da VIM si usa ```:q! ``` (esci senza salvare) oppure ```:wq ``` (salva ed esci)

# Entrare e muoversi in visual mode 
Si può entrare nella visula mode in modi diversi:
- v, visual mode copia il testo che si oltre passa
- V, visual line ovvero seleziona TUTTA la linea dove mi trovo
- ctrl+v, visual block permette di selezionare il testo in modalità blocco. Cioè copi ovunque tu ti muovi.
Per muoversi si usano stessi comandi della normal mode.

# Copiare, incollare, cancellare testo e undo
Per cancellare del testo è sufficiente premere x in normal mode.
Per cancellare una linea basta fare dd.
Per annullare cosa si è appena fatto baste premere u.
Per incollare testo basta premere p.

# Command mode
Per eseguire dei comandi si è visto prima che bisogna utilizzare : ma cosa si può fare altro? 

- :cd ritorna la cartella in cui mi trovo
- :register mostra la "clipboard" di VIM
- :oldfiles lista i file precedentemente aperti da VIM
- :browse oldfiles permette di apri i file aperti prima
- :set number mette i numeri alle linee e permetti jump tra essi
- :explore apre un gestore di file
- :Sexplore apre un gestore di file orizzontalmente
- :Texplore apre un gestore di file in una nuova tab
- :Vexplore apre un gestore di file 
- :! permette di eseguire un comando di shell

# .vimrc
File di configurazione di vim.




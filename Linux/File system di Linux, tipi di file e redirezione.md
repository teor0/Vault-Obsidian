[[Architettura di un sistema GNU-Linux]]
# Caratteristiche
La gestione dei file in Linux è diversa da quella di Windows, in quanto Linux è totalmente gerarchico, ad albero. Linux gestisce il tutto tramite il contenuto dei file, il formato è solo una convenzione. Attraverso il comando `file *` si mostra il contenuto di tutti i file di una tabella. Elenchiamo le cartelle importanti:
- / : la cartella root, ovvero la cartella padre di tutte le cartelle
- /home : la home di ogni utente dove ogni user può lavorare
- /bin : dove si trovano tutti i programmi principali di Linux
- /boot : in boot c'è tutto il necessario al boot del sistema
- /opt : (opzionale) contiene i programmi opzionali degli utenti
- /usr : vengono contenuti i programmi specifici di un user
- /usr/local : vengono contenuti i programmi di questo user e che quindi non vengono condivisi con gli altri
- /root : è la "home" del root
- /etc : contiene file di configurazione ^c31526
- /lib : contiene le librerie di sistema
- /var : contiene file che variano spesso tipo i log di sistema
- /tmp : contiene dei file temporanei che vengono cancellati di frequente. In tmp, tutti gli user sono autorizzati a scrivere
- /var/log : qui sono contenuti i file di log di sistema
- /dev : è una cartella virtuale, dove ci sono dei nomi simbolici per ogni tipo di dispositivo che si può montare. In Linux se inserisco una penna USB, avviene una operazione di mounting che crea una sottocartella in /media dove verranno messi tutti i file che devono essere messi nella USB ^cd8dd1
- /dev/null : questa cartella è il "vuoto", file che ci finisco è come se non fossero mai esistiti. Utile per la redirezione degli errore di comandi
- /mnt : qui vengono montati i file system di dispositivi removibili quali: hard disk, CD, NAS ecc.
- /proc : cartella virtuale contenente i processi e le risorse allocate ad essi

![file system](file-system-tree.png)

# Tipi di file
Come già visto, il comando [[Comandi shell#^17d04f|ls -l ]] mostra un output del tipo:
> -rw-rw-r-- 1 matteo students 15k ott 7 16:27 pollo.txt

Dove vengono indicati: data di ultimo accesso, proprietario del file, gruppo del proprietario e quanto occupa la memoria. Gli altri parametri indicano invece:
- tipo di file : d per directory, - file semplice, s per socket, p per pipe, l per link simbolico (una sorta di collegamento di Windows) che si suddivide in `ln`, hard link e `ln -s` soft link.
- UID (User ID) : dove 0 indica il root ed i restanti numeri indicano gli altri user
- GID (Group ID) : identificativo del gruppo a cui appartiene il proprietario del file
- permessi dei file

## Permessi dei file
I permessi per file e directory sono di 3 tipi:
- r (read) permesso di lettura
- w (write) permesso di scrittura
- x (execute) permesso di esecuzione

> Il permesso di esecuzione è tale per i file mentre per le directory equivale al permesso d'ingresso. Quindi una directory senza permesso di execute non può essere accessa. Il permesso di lettura di una directory permette di utilizzare il comando ls per vedere il contenuto della directory

Vediamo un esempio:
``` shell
	rw- rw- r--
```
In questo caso lo user ha permesso di read e write, idem per il gruppo e others, ovvero gli altri avranno solo il permesso di read. Per cambiare i permessi posso utilizzare il comando <font color=yellow>chmod</font> ad esempio tramite:
```shell
	chmod o+w pippo.txt
```
aggiunge a others il permesso di write su pippo.txt
``` shell
	chmod o-r pippo.txt
```
toglie a others il permesso di read su pippo.txt
Si possono indicare i permessi anche il sistema decimale o ottale.
``` shell
	chmod 777 pippo.txt
```
da a tutti, tutti i permessi sul file pippo.txt

---
## Redirezione
All'interno della shell o in uno scripts che si scrive in un file .sh, si può redirezionare l'input, l'output e l'errore. La sintassi è diversa e si ha rispettivamente:
- 0 indica l'input
- 1 indica l'output
- 2 indica l'errore
- < redirezione input 
- \> redirezione output (overwrite del file)
- \<< uguale a <
- \>> uguale a > (append sul file, quindi non lo elimina)

Vediamo degli esempi:
``` shell
	cat file1 >> fileintero
	cat file2 >> fileintero
	cat file1 file2 >> fileintero
	ls koi 2>/dev/null
```
- la terza versione di cat è la più elegante
- per ls ho redirezionato l'errore nel vuoto

Per redirezionare output ed error assieme si usa &> oppure 2>1

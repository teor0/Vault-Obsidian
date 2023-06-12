eLista dei comandi utili nella BASH (Bourne Again SHell) di Linux:
[[#Comandi di base e variabili speciali]]
[[#Operazioni su file]]
[[#Comandi avanzati]]

### Comandi di base e variabili speciali
>**.** indica la cartella in cui mi trovo al momento
> **\*** carattere jolly per indicare qualunque caratte n volte.
``` shell
	ls *.txt
```
>**?** carattere jolly per indicare un carattere qualunque che appare una volta sola
``` shell
	ls ab?.txt
```
lista tutti i file txt presenti nella cartella
>per scrivere i commenti si usa #
``` shell
	#commento in shell
```
>**history** permette di visualizzare l'elenco completo dei comandi che abbiamo digitato in precedenza
>**;** si può usare per eseguire più file nella stessa riga uno dopo l'altro
``` shell
	mkdir appunti; ls
```
>**ctrl+d** indica la exit nella shell. Quindi se voglio uscire da un comando o da uno script in running basta fare ctrl+d 
>Il file **.bashrc**, contiene delle istruzioni importanti per la shell e si può modificare inserendo dei comandi in modo che ogni qualvolta la shell venga aperta, vengono effettuati tali comandi.
>**/** è la cartella root del file system
>**sudo** rende momentaneamente root e quindi ogni comando che viene fatto è di fatti svolto come root
>**sudo** su rende root
>**su username** cambia utente nel username inserito
---
>**pwd**
``` shell
	pwd
```
>**cd** serve a cambiare cartella e muoversi nel file system di Linux.
``` shell
	cd /home/matteo/Desktop
	cd
	cd ..
```
Le 3 versioni sopra mostrano 3 possibili spostamenti 
1. spostamento in una cartella definita, che può essere espressa tramite path assoluto (come sopra), oppure path locale
2. solamente cd porta alla cartella di home
3. cd .. serve a salire di una cartella, quindi a tornare alla cartella padre
>**touch** serve a crea un file vuoto
``` shell
	touch pippo.txt
```
viene creato il file pippo.txt vuoto.
>**man** che starebbe per manuale, mostra le opzioni di un comando
``` shell
	man ls 
```
viene mostrata la lista di opzioni del comando ls
>**whatis** mostra la descrizione di un comando
``` shell
	whatis bash
```
>**who** mostra gli utenti connessi alla macchina
``` shell
	who
```
>**whoami** dice che tipo di utente si è
``` shell
	whoami
```
>**exit** si utilizza per uscire dalla shell oppure dalla modalità root
``` shell
	exit
```
ritorna Bourne-Again-SHell
>**whereis** cerca file executabili e programmi installati
``` shell
	whereis exif.exe
```
>**clear** pulisce la finestra della shell
``` shell
	clear
```
>**echo** mostra una stringa di testo
``` shell
	echo "Hello World"
```
<font color=red> N.B. </font> le virgolette non sono obbligatorie, ma con caratteri speciali come * si
### Operazioni su file
>**ln** attraverso ln si possono creare link a file
``` shell
	ln -s pippo.txt linkpippo
	ln -s /home/matteo/Downloads Download
```
>**rm** rimuove un file
``` shell
	rm pippo.txt
```
>**mkdir** serve a creare un directory
``` shell
	mkdir esercizi
```
crea la cartella esercizi, nella cartella corrente.
>**rmdir** rimuove la cartella passata come parametro. <font color=red>**ATTENZIONE** </font>rmdir rimuove solo le cartelle vuote
``` shell
	rmdir esercizi
```
per rimuovere una cartella che contiene dei file, bisogna utilizzare `rm -r esercizi`. Da notare che l'opzione -r starebbe per ricorsivo, quindi in sostanza rm -r rimuove ricorsivamente ogni file contenuto in esercizi.
``` shell
	rm -r /
```
questo comando cancella la cartella root del file system, di fatto "distrugge" Linux.
>**mv** serve a spostare un file in una cartella. Necessita del file e della cartella di destinazione
``` shell
	mv file1 file2
	mv olddir newdir
	mv file dir
```
1. rinomina file1 in file2, altrimenti se file2 esiste scrive file1 su file2
2. rinomina olddir in newdir, se newdir esiste sposta olddir in newdir
3. sposta file in dir
il comando sopra sposta il file prova.c++ e cambia l'estensione in cpp.
>**cp** serve a copiare un file in una cartella. La sintassi è identica a quella di mv
``` shell
	cp file1 file2
```
1. se file2 non esiste allora cp lo crea, altrimenti lo sovrascrive
2. se file2 è una directory, cp copia file1 nella directory
>**ls** elenca tutti i file e le cartelle
``` shell
	ls 
	ls Desktop
	ls -l
	ls -a
```

^945c69

1. Solamente ls mostra i file e cartelle contenuti nella cartalla in cui mi trovo
2. ls Desktop mostra file e cartelle contenuti nella cartella Desktop
3. ls -l mostra un elenco più dettagliato dei file e delle cartelle (permessi, peso, data modifica, ecc.) ^17d04f
4. ls -a mostra anche i file nascosti
>**nano** apre la GUI per la edit di un file
``` shell
	nano pippo.txt
```
se pippo.txt non esiste viene creato
>**pico** identico a nano
``` shell
	pico topo.cpp
```
>**cat**  ha 4 possibili usi, vediamo prima la sintassi
``` shell
	cat pippo.txt
	cat file1 file2
	cat file1 file2 > file3
	cat < file1 > file2
```
1. mostra contenuto dei file di testo su standard output
2. copia file di testo
3. concatena file di testo
4. crea nuovi file di testo (effettua una copia di fatti)
>**more** visualizza il contenuto di un file per intero
``` shell
	more listaIngredienti.txt
```
>**less** identico a more
``` shell
	less listaIngredienti.txt
```
sia per more che less, per andare avanti di una linea si usa invio, per andare avanti di una pagina si usa spazio e per uscire si usa q.
>**head** mostra le prime 10 righe di un file di default
``` shell
	head lista.txt
	head -n 30 lista.txt
```
con l'opzione -n si può scegliere il numero di righe da mostrare
>**tail** mostra le ultime 10 righe di un file di default
``` shell
	tail lista.txt
	tail -n 30 lista.txt
	tail -n +2
```
con l'opzione -n si può scegliere il numero di righe da mostrare. tail -n +2 toglie le prime 2 righe
>**grep** fa una ricerca all'interno del file per trovare un pattern oppure il risultato di una regex
``` shell
	grep include helloworld.c
```
1. con l'opzione -r si scansionano ricorsivamente le sottodirectory
2. con l'opzione -n si visualizza il numero di riga
3. con l'opzione -c si mostra il numero di linee in cui il pattern viene trovato
>**wc** fornisce in ordine il numero di linee, parole e caratteri presenti in un file
``` shell
	wc index.txt
```
rispettivamente le opzioni -w, -l e -m forniscono solo il numero di parole, linee e caratteri
>**sort** ordina un flusso di testo o un file in senso crescente o decrescente
``` shell
	sort file
	sort -r file
	sort -u file
```
1. ordina alfanumericamente le linee
2. ordina in ordine inverso
3. elimina dal risultato le linee duplicate

>**nl** numera le linee di un file
``` shell
	nl listaspesa.txt
```
>**find**, utile per cercare file in una directory e ricorsivamente attraverso il path
``` shell
	find -name '*.java'
```
1. cerca tutti i file java a partire dalla directory in cui mi trovo
2. -type d cerca directory
3. -size +1024 file superiori a 1MB

>**uniq** rimuove o reporta i duplicati all'interno di un file
``` shell
	uniq tracce.txt
```
>**tr** sostituisce caratteri all'interno di un file
``` shell
	tr 'c' 'e'
```
>**cut** permette di eliminare gli spazi e di cercare le parole all'interno di quella frase
``` shell
	nome=" ciao Hidetaka Miyazaki"
	echo $nome | cut -d ' ' -f 2
```

### Comandi avanzati
>**|** la pipe manda l'output di un comando come input per un secondo. Più pipe si possono concatenare assieme. 
``` shell
	ls | wc -l
```
restituisce il numero di file che ls conta, dato che l'output viene dato a wc -l che conta le linee.
>**tar** permette di estrarre da una cartella .tar
``` shell 
	tar zxvf source.tar.gz
```

Per eliminare gli orfani tramite pacman, usare il comando:
``` shell
	pacman -Qtdq | sudo pacman -Rns -
```
In passato i software venivano installati tramite sorgente e non tramite i package. Vediamo i passi per installare un sorgente:
1. Scaricare/ottenere un file sorgente con estensione tar.gz
2. Copiare in una directory di installazione il file (/usr/local)
3. Estrarre il file tar con tar zxvf, da notare che .tar sta a significare che la cartella viene compattata, mentre .gz è dato da gzip che zippa le cartelle ed una volta estratte ricrea la loro gerarchia
4. ./configure -prefix=/usr/local (cartella d'installazione del sorgente)
5. Usare il comando <font color=yellow>make</font> che legge un file Makefile ed esegue le sue istruzione per compilare un software.
6. Usare il comando make install per effettuare l'installazione vera e propria

Per conoscere le directory di un particolare package oppure di tutti i package installati tramite pacman o yay basta usare:
``` shell
	pacman -Ql #nomepacchetto
	yay -Ql
```
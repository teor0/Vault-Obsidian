[[File system di Linux, tipi di file e redirezione]]
# Quote utente
All'interno di Linux ogni utente ha una quota predefinita, ad esempio ogni utente ha una quota di spazio sul disco. Le quote possono essere di 2 tipi:
- <font color=blue> Hard limit</font>: un limite che l'utente non può superare mai
- <font color=blue> Soft limit</font>: un limite che può essere superato per un periodo di tempo, detto periodo di grazia.

Attraverso il comando <font color=yellow> quotacheck</font> si creano 2 file di configurazione, uno per il gruppo ed uno per l'user. Per attivare i file si usa il comando <font color=yellow>quotaon</font>. Attraverso <font color=yellow>edquota o setquota</font> si può rispettivamente editare e settare la quota. Infine il comando <font color=yellow>repquota</font> stampa un report sulle quote utente.

# Advanced Packaging Tool
L'Advanced Packaging Tool, permette di installare i [[Terminologia, storia di Linux e caratteristiche di base#^700457|pacchetti]] su sistemi Debian/Ubuntu based, attraverso l'istruzione:
``` shell
	sudo apt-get install
```
Per aggiurnare un'applicazione su una distro Arch based, occorre:
``` shell 
	sudo pacman -S firefox
	# oppure
	yay -S firefox
```
Per eliminare gli orfani tramite pacman, usare il comando:
``` shell
	sudo pacman -Rns $(pacman -Qtdq)
```
In passato i software venivano installati tramite sorgente e non tramite i package. Vediamo i passi per installare un sorgente:
1. Scaricare/ottenere un file sorgente con estensione tar.gz
2. Copiare in una directory di installazione il file (/usr/local)
3. Estrarre il file tar con tar zxvf, da notare che .tar sta a significare che la cartella viene compattata, mentre .gz è dato da gzip che zippa le cartelle ed una volta estratte ricrea la loro gerarchia
4. ./configure -prefix=/usr/local (cartella d'installazione del sorgente)
5. Usare il comando <font color=yellow>make</font> che legge un file Makefile ed esegue le sue istruzione per compilare un software.
6. Usare il comando make install per effettuare l'installazione vera e propria

Nella cartella /etc/apt/sources.list.d sono contenute le repository dei pacchetti. Per ricercare i pacchetti, si può usare il comando apt-cache seach "nomepacchetto", si capisce quindi che Linux mantiene una cache dei package. Il comando `apt-get update` aggiorna la cache dei package, `apt-cache show nomepackage` mostra delle info riguardo un package. Infine apt-get remove rimuove il package.

Per distro arch based, la cache delle repositories si aggiorna tramite `pacman -Syy`
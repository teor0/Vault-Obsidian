[[Comandi shell]]
# Comandi avanzati
Il comando <font color=yellow>find</font> serve a trovare un file in una directory. La sintassi è la seguente:
``` shell
	find libri -name Berserk.cbz
```
L'opzione -exec permette di eseguire un comando su ogni risultato della find. La sintassi è la seguente:
``` shell
	find . -name \*.c -type f -exec cat {} \;
```
Le parentesi graffe stanno ad indicare tutti i file trovati da find, mentre \\; esegue una istruzione per ogni file trovato. \\+ applica lo stesso comando a tutto l'output, come se tutti i file fossero argomenti del comando.
``` shell
	find . -name \*.java -exec cp {} all_java \;
```
Questo comando trova e copia tutti i file .java nella cartella all_java. 
``` shell
	find . -type f -name *.txt -exec rm {} \*
	find . -type f -name *.txt | xargs rm
```
I 2 comandi sono essenzialmente uguali, solo che xargs è più efficiente su grandi moli di file.

# Regex
- . indica qualsiasi carattere
- a? può mancare il carattere a
- a* ripetuto un numero 0-n volte
- a+ ripetuto un numero 1-n volte
- ^a trova solo 'a' all'inizio
- a$ trova solo 'a' alla fine
- \\. serve ad impedire di usare . come metachar

# Sed
È un comando che consente di editare testo presente nei file. 
Opzioni utili sono:
- a\ appende testo
- d cancella testo
- c\ cambia testo 
- s sostituisce una volta per riga. per ogni occorrenza si usa g
- p stampa in output

``` shell
	sed '1,3d' pippo.txt
```
cancella le righe da 1 a 3 nel file pippo.txt
``` shell
	sed '1,$d' pippo.txt
```
cancella le righe da 1 fino all'ultima
``` shell
	sed 's/erori/errori/' testo.txt
```
Per sostituire ogni occorrenza occorre scrivere:
``` shell
	sed 's/erori/errori/g' testo.txt
```
Come cambiare l'estensione di un file:
``` shell
	nomeFile='prova.txt'
	echo $nomeFile | sed 's/\.txt/\.bak/'
```
questa serie di istruzioni cambiano l'estensione da .txt a .bak.
Per trasformare un file che inizia con backup_ ad esempio backup_pippo.txt in copia_pippo.txt
``` shell
	file='backup_pippo.txt'
	nuovo=$(echo $file|sed "s/^backup\_/copia\_/g")
```
<font color=red>Come ottenere il nome di un file senza estensione </font>:
``` shell
 	nome_senza_est=$(echo $miofile|sed 's/\..*$//')
```
Spieghiamo la sintassi: allora /\\. cerca il punto dell'estensione, mentre .* sarebbe una regex del tipo "tutti i caretteri dopo il punto", infine il $ indica che tutto ciò si deve trovare alla fine della stringa. Da notare che questo comando rimuove TUTTE le estensioni. Un file del tipo documento.txt.doc diventerà documento e basta, quando magari si vuole rimuovere solo il .doc Per risolvere ciò si dovrebbe usare un'espressione del tipo:
``` shell
	no_ultima_est=$(echo $miofile|sed 's/\....$//')
```
si hanno 3 punti perchè si assume che l'estensione è lunga 3, per estensioni più lunghe si dovrebbe conoscere la loro lunghezza. Per togliere la prima estensione occorre fare una cosa simile:
``` shell
	no_prima_est=$(echo $miofile|sed 's/\....//')
```
sempre assunto che l'estensione è lunga 3.
Per le espressioni precedute dal $ occorre usare gli apici '' quindi se volessi sostituire l'estensione $est1 con $est2 occorre scrivere:
``` shell 
	sed 's/\.'$est1'$/\.'$est2'/'
```
Ulteriore metodo per rimuovere l'estensione di un file:
``` shell
	no_ext=$(echo $file |sed 's/\.[^.]*$//')
```
<font color=red> Per CONOSCERE le estensioni di un file: </font>
``` shell
	estensione=$(echo $nuovo|sed 's/[^.]*\.//')
```
perciò attraverso questo comando si conoscono tutte le estensioni di un file
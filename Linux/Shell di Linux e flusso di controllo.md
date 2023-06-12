[[Terminologia, storia di Linux e caratteristiche di base]]
[[Comandi shell]]
# Shell
La shell di Linux, è il core del corso e permette di effettuare operazioni avanzante in poche righe. Un programma eseguibile dalla shell è un programma .sh. Per eseguire un programma occorre digitare `programma.sh`.
Nella shell non esistono i tipi, dunque le variabili sono trattate come "pari".
``` shell
	x=10
	echo "$x" #stampa 10
```
Per stampare il valore di una variabile bisogna usare il carattere speciale $, tuttavia è buonanorma utilizzare le virgolette, in quanto alcuni valori contenuti nella variabile potrebbero ostacolare l'output. All'interno della shell vi sono variabili d'ambiente e variabili utente. La variabile PATH è il percorso in cui si trovano tutti i comandi.
> Per aggiungere una cartella a PATH si usa il comando PATH=\$PATH:directory. Risulta utile fare PATH=\$PATH:. per aggiungere la cartella corrente in modo da non dover usare ./comando.sh per eseguire un programma. Tuttavia la PATH viene cambiata solo per quella istanza della shell.

Nella cartella home si trova il file .bashrc che specifica le istruzioni da fare appena si crea un'istanza della shell, quindi risulta efficace scrivere PATH=\$PATH:. nel file .bashrc
Il carattere $ seguito da un comando di Linux mette il risultato del comando nella variabile utilizzata:
``` shell
	n=$(ls -l|wc -l)
	echo $n
	#viene stampato il numero di righe dell'output di ls -l
```
---
# Statement di controllo
All'interno della shell sono presenti: if, for, while e case. Ognuno di essi ha una sintassi precisa che non deve essere violata. Ad esempio:
``` shell
	if [ $x -eq 3 ];then
		echo x=3
	else
		echo x diverso da 3
	fi
```
da notare che then deve essere scritto in un altra linea se non è preceduto da ; le parentesi devono avere gli spazi esattamente come nell'esempio e fi determina la fine del if-else.
Condizioni if per i file:
- -e test esistenza 
- -s esiste e non è vuoto
- -a test esistenza uguale a -e
- -f se è un file
- -d se è una directory
- -L se è un link simbolico
- -r se ha permesso di read
- -w se ha permesso di write
- -x se ha permesso di execute
- ! per negare il la condizione scelta. Ad esempio ! -f equivale a chiedersi se non è un file 

Condizioni per le stringhe:
- "\$stringa1" == "\$stringa2" per uguaglianza
- "\$stringa1" != "\$stringa2" per disuguaglianza
- -n "\$stringa" se non è vuota
- -z "\${stringa// }" se è vuota o contiene solo spazi
- -z "\$stringa" se vuota

Per comparare numeri invece si usano:
- -eq equal
- -ne not equal
- -le less or equal
- -lt less than
- -ge greater or equal
- -gt greater than

La sintassi del for e del while invece è:
``` shell
	for i in $#;do
		let c=$c+1
	done
	while [ $i -le $# ];do
		echo ciao
	done
```
Il while è molto utile per leggere file dove c'è un pattern riccorrente per le righe, ad esempio un file che contiene per ogni riga il nome di una squadra ed il suo punteggio (eg. Inter 40). Per leggere squadra e punteggio posso utilizzare un while del tipo:
``` shell
	while read squadra punt;do
		echo "squadra $squadra ha totalizzato $punt punti!"
	done < $file
```
Molto importante la redirezione dell'input alla fine tramite l'istruzione `done < $file`.
La sintassi del case è:
``` shell
	x=3
	case $x in
	1) echo "1" ;;
	3) echo "3" ;;
	*) echo "def" ;;
	esac
```
\*) è il caso di default e ;; sarebbe il break di C o Java.

Per controllare che dopo un comando sia andato tutto bene si può usare `echo "$?"`. All'interno della shell esistono anche and (&&) e or (||) che permettono di scrivere due comandi sulla stessa riga, solo che vengono eseguiti a patto che:
- per l'and il primo è corretto.
- per l'or uno dei 2 sia corretto. Quindi anche se il primo comando fosse errato, il secondo andrebbe in porto. 
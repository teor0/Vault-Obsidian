[[File system di Linux, tipi di file e redirezione]]
# Processi
I processi non sono altro che programmi in esecuzione. Ogni processo possiede i seguenti identificatori: 
![[proproc.png]]

In Linux, i processi seguono una gerarchia del tipo padre figlio. Il processo padre ed il processo figlio condividono risorse, ad esempio file aperti. In Linux i file sono entità più generiche rispetto a Windows. Una pipe può essere condivisa.
> Il comando `pstree -a` mostra tutti i processi in esecuzione al momento nel pc, sotto forma di albero.

Il padre di tutti i processi è systemd o init per versioni più anziane di Linux, il cui PID è 0. Attraverso il comando `ps` si mostrano i processi attivi, mentre `ps -umatteo` mostra i processi attivi per l'utente matteo.
> Il comando `ps ax` mostra i processi per esteso come se fosse pstree, ma integra i processi del kernel rappresentati tra parentesi quadre.

## Stati dei processi

Un processo può assumere diversi stati:
- R: running
- S: sleeping
- T: il processo è stoppato. In genere con ctrl+z si stoppa un processo e viene messo nella coda dei processi. I processi stoppati sono di tipo <font color=yellow>background</font>, i processi in running o sleep sono di tipo <font color=yellow>foreground</font>. Rispettivamente il comando bg mostra su output i processi stoppati, mentre fg, riporta in esecuzione i processi stoppati.
- Z: il processo si trova nello stato "zombie". Normalmente un processo padre deve aspettare l'esecuzione del figlio, ma quando un processo padre termina prima del figlio, il figlio rimane nello stato di zombie.
- D: il processo è in una uninterruptible sleep. È tipicamento lo stato di processi di I/O.

Attraverso il comando nice, si può alterare la priorità di scheduling dei processi, ricordando che la priorità più alta è associata a numeri piccoli. Un altro comando utile è il comando top, che mostra su output in modo interattivo i processi.

---

# Processi daemon e superdaemon
I processi intuitivamente possono essere "interattivi" e "non interattivi". Ad esempio se sto utilizzando vim il processo sarà interattivo in quanto l'utente è coinvolto nel mentre che il programma esegue. Un processo che invece non è interattivo deve essere attivo anche quando non c'è nessun utente connesso. I daemon sono processi non interattivi.
Un processo daemon, lancia solo un processo alla volta, mentre un superdaemon ne può lanciare più alla volta.
<font color=yellow>xinetd</font> è un superdaemon nella cartella /etc/init.d e sempre in questa cartella troviamo anche dei processi daemon. Un daemon funziona in genere con 3 procedure:
- start
- stop
- restart

<font color=yellow>atd</font> è un daemon che lancia un comando ad una certa ora, per eseguire atd si utilizza il comando <font color=yellow>at</font>.
<font color=yellow>cron</font> esegue un determinato comando in maniera ripetuta fino ad un certo intervallo di tempo, che sia ora, giorno, mese, anno, ecc. cron utilizza un file di configurazione contenuto in /etc/cron.d. Esempio di backup ogni primo del mese alle 6:50:
``` shell
	50 6 1 * * root /bin/esegui_backup.sh>log.txt
```
Nel dettaglio i parametri sono: minuti ora giorno mese giorno_settimana utente comando. \* si usa per i parametri che non si vogliono specificare. Vengono poi in aiuto le cartelle cron.daily, cron.hourly, cron.weekly e cron.monthly che, rispettivamente eseguono comando giornalmente ogni ora ecc.



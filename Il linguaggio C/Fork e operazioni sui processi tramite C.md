Un processo in Linux, quando gira si trova in modalità user. Solo quando effettua una system call entra in modalità kernel. Ogni processo possiede un Task_struct che contiene delle informazioni riguardanti il processo come ad esempio:
- PID: process ID
- PPID: parent process ID
- Stato del processo: z, r, s, i
- UID: user ID
- GID: group ID

Processi padre e figlio hanno aree di memoria separate, tutta via i file aperti dal padre sono condivisi con i figli. La system call fork() permette di creare processi. La fork restituisce un PID di tipo pid_t che altro non è che una typedef int. Vediamo un esempio di nfork:
``` c
	pid=10;
	for(int i=0; i<n; i++){
	   if(pid>0){
		 nfiglio=i; //cosi identifico ogni figlio
		 pid=fork();
	   }
     }
```

Tutte le variabili che esistono prima della fork all'interno dell'heap, verranno duplicate nella memoria del processo figlio. Il figlio esegue lo stesso codice del padre dopo la fork.
Il PID è pari a 0 per il figlio e > 0 per il padre. Se PID è pari a -1 si è verificato un errore. 
>La funzione getpid(), che ritorna un pid_t, si può ottenere il PID di un processo.
>La funzione getppid(), ritorna anch'essa un pid_t, restituisce il PPID di un processo.

---

## Wait e corretta esecuzione dei processi
Un processo padre deve per eseguire correttamente deve svolgere questi passi:
1. Esegue codice preliminare alla creazione del figlio
2. fork del figlio
3. esegue il suo codice
4. aspetta la terminazione del figlio (evita che il figlio passi a zombie)

Un processo figlio invece deve eseguire correttamente altri passi, quali:
1. esegue il suo codice 
2. termina l'esecuzione, con exit opzionale

Per permetter ciò si utilizza la funzione wait(). La wait necessita di una variabile intera per riferimento. La variabile intera ha informazioni al suo interno, tra cui il codice di uscita dell'exit del figlio. Per estrarre questa informazione bisogna fare uno shift sinistro di 8 bit. La wait inoltre restituisce il PID del figlio.
``` c
	int status;
	wait(&status);
```
Attraverso l'istruzione `wait(&status)` il processo entra in wait, perciò attende che <font color=red>un processo figlio specifico</font> termini e poi potrà continuare l'esecuzione che in genere termina dopo la wait(). 

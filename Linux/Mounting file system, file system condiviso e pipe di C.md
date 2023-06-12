[[File system di Linux, tipi di file e redirezione]]
# Mounting file system
Il mounting del file system può essere manuale o automatico. Riferendosi alla cartella [[File system di Linux, tipi di file e redirezione#^cd8dd1|/dev]] per montare il file system, utilizziamo il comando: 
``` shell
	mount -t ext4 /dev/sda5 / 
```
per montare il file system principale. 
Con mount -t si deve indicare il tipo del file system, in questo caso <font color=yellow>ext4</font> indica l'ultima versione del file system di Linux. Altri tipi sono:
- NTFS (attuale file system di Windows)
- vfat/fat32 (vecchio file system di Windows e file system più comune per le pennette USB)

Attraverso `mount -a` si montano tutti i file system. Per ovviare un ipotetico remounting ogni volta che si avvia Linux, nella cartella [[File system di Linux, tipi di file e redirezione#^c31526|/etc]] si trova fstab, file di configurazione con una sintassi simile a quella del comando mount. Ad esempio: `/dev/sda5 / ext4 default 0 0`, dove i bit 0 0 servono al dump del file system ed il check del file system. Ovviamente se messi a 0 non fanno ciò altrimenti se posti ad 1 eseguono le 2 operazioni. Per apprendere il nome di una penna USB si può utilizzare, `dmesg | tail` che stampa le ultime righe di log cosicché posso trovare facilmente il nome. Per rendere il tutto più semplice si utilizza lo UUID (Universal Unique IDentifier) ottenibile attraverso `blkid`, valido sia per il comando mount che per fstab. Si possono aggiungere flag per quanto riguarda il file system, quali:
- user: anche un qualunque user può effettuare la mount
- nouser: solo il root può effettuare la mount
- auto: mount automatica
- noauto: mount non automatica
- exec: permesso di execute
- noexec: non si ha permesso di execute
- ro: permesso read only
- rw: permesso read and write, (default)

## Network File System
Un Network File System, è un file system che permette la condivisione di file attraverso la rete. Il tutto si divide in lato server e lato client. Lato server (192.168.102.11), attraverso /etc/exports si possono condividere cartelle, ad esempio: `/home/drive/film 192.168.102.0/255.255.255.0(rw)`. Lato client (192.168.102.10) bisogna montare il file system attraverso: `mount -t nfs 192.168.102.11:/home/drive/film /media/dump_film`
Il tutto si può fare attraverso fstab come indicato di seguito: `192.168.102.11:/home/drive/film /media/dump_film nfs auto,user,noexec 0 0`

### Samba
Samba implementa il protocollo CIFS (Common Internet File System) usato dai server Windows per condividere file. Per configurare samba su Linux, si può usare il file smb.cfg all'interno di /etc/samba. Samba funziona attraverso il file cfg che contiene variabili globali, e share ovvero cartelle che vengono condivise. Principalmente samba viene utilizzato da lato client, e può essere effettuato il mounting tramite fstab oppure tramite il comando `smbmount`. 

# Pipe e segnali
Le pipe sono file speciali utilizzati per connettere e far comunicare 2 processi con un canale unidirezionale di comunicazione. A differenza dei <font color=blue> socket </font> che permettono di far comunicare processi tra altri computer, la pipe permette la condivisione tra 2 processi di uno stesso computer. Sulla pipe si possono fare 2 operazioni, <font color=red> write </font> e <font color=red> read </font> e la comunicazione viene gestita tramite un <font color=blue>buffer </font>. Se 2 processi leggono e scrivono è sconsigliato utilizzare una sola pipe. Sia write che read sono primitive <font color=red> bloccanti </font>, ovvero se il buffer è pieno la write o la read si interrompono, inoltre se la pipe è all'interno di un processo figlio, la wait da parte del padre non va perforza dopo le operazioni fatte tramite pipe. Esempio di codice che spiega ciò:
``` c
	close(F2C[0]); //chiudo il canale in lettura
    write(F2C[1], &x, sizeof(int));
    close(F2C[1]);
    wait(&status);
    //la wait va bene anche dopo in quanto sono operazioni bloccanti
    close(C2F[1]);
    read(C2F[0], &ret, sizeof(int));
    close(C2F[0]);
```

Esempio: si hanno 2 processi Pa e Pb, Pa effettua 3 write di numeri, Pb effettua una read per trovare il massimo dei 3 numeri e poi scrive il massimo e Pa lo stampa. La stampa del massimo può essere erratta in quanto magari il processo Pa non attende la fine di Pb, quindi si verifica non determinismo. 

La pipe è un canale sincrono, necessità quindi che i 2 processi siano effettivamente in "ascolto". Il paradigma che usa la pipe è del tipo master slave. 

I segnali ovvere le trap (interruzioni software), possono essere ignorati, catturati o causare le interruzioni del processo. Per la cattura si usa il metodo handler, per terminare si può usare sigkill, `kill -9 107` (segnale sigkill inviato al processo con ID 107).

Per usare la pipe allochiamo un vettore di dimensione 2, di tipo int ad esempio: `int pd[2]`. Attraverso la system call pipe(pd) creaiamo la comunicazione. Tramite pd[0] leggiamo e tramite pd[1] scriviamo. Attraverso write e read rispettivamente si scrive e si legge. Per chiudere il canale in lettura o scrittura si usa la funzione close(pd[i]). La pipe deve essere create prima di fare la fork!

Esempio di pipe per mandare un array:
``` c
	int F2C[2];
	if(pipe(F2C)==-1){
    	printf("errore nella creazione della pipe\n");
    	return 1;
  	}
	close(F2C[0]);
	write(F2C[1], v, N*sizeof(int));
```
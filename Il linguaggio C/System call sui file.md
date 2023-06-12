#C 
[[Fork e operazioni sui processi tramite C]]
Gli header da includere per le sys call dedicate ai file sono:
- `#include <fcntl.h>`
- `#include <sys/stat.h>`
- `#include <sys/types.h>`
- `#include <unistd.h>`
Il metodo creat permette di creare un file. Vediamo un esempio:
``` c
	int fd
	fd=creat("ciao.txt", 0644)
```
Tutta via non si usa molto questo metodo in quanto attraverso la open si può usare l'opzione di creazione del file. Ad esempio:
``` c
	int fd
	fd=open("pippo.txt", O_CREAT, 0644)
```
Ci sono altre opzioni che permettono altre operazioni. Le operazioni sono le seguenti:
- O_CREAT se il file non esiste lo crea
- O_WRONLY solo scrittura
- O_APPEND scrive alla fine del file
- O_RDWR letture e scrittura
- O_RDONLY solo lettura

Come in Java un file una volta utilizzato va chiuso tramite close. Le operazioni sono le stesse, ovvero: open, write, read e close. 
``` c
	fd=open("ciao.txt", O_WRONLY|O_CREAT, 0644);
	//uso tipico
	fd=open("ciao.txt", O_WRONLY);
	close(fd);
```
Come standard Linux, scrive file binari. Il vantaggio sta nel non occupare molto spazio, in quanto un numero in un file binario occupa 4 Byte mentre in un file testuale, un numero a 32 bit occupa per ogni cifra un Byte. Per esempio se ho 3 numeri in un file binario avrò complessivamente occupato 12 byte, mentre magari gli stessi numeri in un file testuale occupano 31 byte.
Attraverso SEEK posso muovermi tra i Byte del file in modo simile a Java tramite una "testina". Le operazioni sono:
- SEEK_SET pone la testina ad inizio file
- SEEK_CUR ritorna la posizione della testina
- SEEK_END pone la testina a fine file

Queste operazioni si usano tramite il metodo lseek. Un esempio è:
``` c
	pos=lseek(fd, 16, SEEK_SET);
```
attraverso lseek posso ad esempio leggere un file intero e memorizzarlo 
``` c
	int n=lseek(fd,0,SEEK_END)/sizeof(int);
	int *v;
	v=(int*)malloc(n*sizeof(int));
	read(fd, v, n*sizeof(int))
```
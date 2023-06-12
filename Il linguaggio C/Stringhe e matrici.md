#C
[[Storia e base di C]]
[[Array, puntatori, operatori di indirizzo e dereferenziazione e buffer overflow]]
# Stringhe
Una stringa è una sequenza di caratteri, memorizzati in locazioni contigue di memoria e terminata da un carattere speciale '\0' detto <font color=red> terminatore di stringa </font>aggiunto in automatico.
I metodi relativi alle stringhe si trovano nella libreria <font color=yellow>string.h</font>
``` c
	char nome[80]="Marco";
	char name[]="Boris";
	//nome="Luca"; errore
```
L'array creato alloca lo spazio necessario per memorizzare la stringa in quanto \0 ci fa sapere la fine della stringa. 
Il metodo <font color=yellow> strcpy </font> permette di cambiare il valore di una stringa
``` c
	char nome[]="Luca";
	strcpy(nome, "Paolo");
```
Per conoscere la lunghezza della stringa, si utilizza il metodo <font color=yellow> strlen</font>:  
``` c
	char nome[]="Nicola";
	int n;
	n=strlen(nome);
```
Il metodo <font color=yellow>strcmp</font> compara 2 stringhe e ritorna un intero, se ritorna 0 le stringhe sono uguali altrimenti sono diverse. Il criterio usato è lessicografico alfanumerico.
``` c
	char n[]="Marco";
	char m[]="Mattia";
	int x=strcmp(n,m);
```
Il metodo <font color=yellow>strcat</font> permette di concatenare 2 stringhe fra loro.
``` c
	char n[]="Mi chiamo";
	char m[]=" Lollo ";
	strcat(n,m);
```
Il metodo <font color=yellow>sprintf</font> ha varie funzioni quali: concatenazione, copia e conversione
``` c
	sprintf(str, "%s%s", nome, cognome);
	sprintf(str, "%s", nome);
	sprintf(str, "%d", n);
```
1. concatenazione
2. copia
3. conversione

Il metodo sprintf inoltre può essere utilizzato per scrivere su un file! Vediamo un esempio:
``` c 
	char buffer[100];
	sprintf(buffer, "%d", x);
	write(fd, buffer, strlen(buffer)*sizeof(char));
```
# Matrici
In C una matrice è un concetto un pochino astruso.Le matrici in C, a differenza dei vettori non è assicurata la memorizzazione in celle adiacenti. Per sfruttare la memorizzazione in celle adiacenti posso istanziare una matrice di dimensione nxm, come un vettore:
```c 
	int *mat;
	mat=(int*)malloc(sizeof(int)*n*m);
```
Questo però preclude l'accesso standard ad un elemento della matrice [i][j]. Per accedere un elemento generico devo usare:
```c
	mat[i*m+j]
```
Risulta più semplice utilizzare la definizione proprio di matrice e non usare un vettore per simularla. 
Ad esempio una matrice di 5 colonne e 3 righe che contiene 15 interi, necessita di un array di puntatori di 3 elementi. La figura aiuta a concettualizzare:
![[matrix.jpg]]
int** mat è un puntatore a puntatori di interi. mat[0] è il puntatore alla prima riga. mat[0]\[0\] punta al primo elemento come si è abituati in Java. 

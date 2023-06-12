# Terminal shortcut
- cancella tutto quello che si è scritto
```shell
Ctrl+u
```
- esegui ultimo comando
```shell
!!
# execute da root
sudo !!
```
- esegui ultimo comando che inizia per tale carattere
```shell
!c
```
- esegui un comando cambiando qualche parametro
```shell
^old^new
```
- esegui un comando in background
```shell
comando &
```

---
### Grep
- conta il numero di linee vuote
```shell
grep -c "^$"
```
- trova solo le cifre
```shell
grep -oP "\d*"
```
-trova un numero con un n cifre 
```shell
grep -P "\d{n}"
```

---
### Sed
- rimuovi la prima linea
```shell
sed 1d nomefile
```
- rimuovi le linee con una stringa definita
```shell
	sed -i "/stringa/d" nomefile
```


---
### File 
``` shell 
	tar zxvf source.tar.gz
```

---
### Hardware
- lista di tutti i dispositivi usb
```shell
lsusb
```

---
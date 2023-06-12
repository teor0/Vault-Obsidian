[[File system di Linux, tipi di file e redirezione]]
# Inode
In Linux il virtual file system gestisce il file system (ext4), basandosi sulla struttura fondamentale inode. Tramite `ls -li` posso ottenere l'inode dei file. L'inode nasce dai primi sistemi Unix e tramite esso, posso vedere dove si trova sul disco il file o la cartella, inoltre l'inode contiene informazioni come il tipo, i permessi d'accesso e le dimensioni. L'unica informazione che non contiene l'inode è il nome del file. 
Esiste una tabella degli inode ed ogni file corrisponde ad un inode che contiene info generali e l'indirizzo di memoria dov'è salvato il file. Prima degli inode ci sono:
- boot block: informazioni cruciali sul boot
- super block: informazioni dove si trovano i data block(file) e gli inode.

Supponiamo per semplicità che un blocco di dati sul disco è di 1kbit, quindi per un file di 100kbit ho bisogno di 100 blocchi. Per 100 blocchi dovrei avere 100 inode, quindi una mole di inode enorme. Per risolvere ciò si utilizza l'indirizzamento indiretto. Ogni inode ha degli attributi quali: permessi, dimensioni in Byte, ultimo accesso ecc. successivamente ci sono 10 collegamenti diretti e 3 blocchi indiretti dove:
- il primo è a indirizzamento indiretto che possiede 256 indirizzi
- il secondo è a indirizzamento indiretto doppio che possiede quindi 256\*256 cioè 64k
- il terzo è a indirizzamento indiretto triplo che possiede 256\*256\*256 16GB circa (se non errato)

Nella versione ext2 del file system di Linux si ha una situazione del genere: ![](inode.png) Quindi ci sono più block group dopo il boot block ed ogni gruppo è diviso come mostrato in figura.
I link simbolici sono gestiti tramite inode, infatti un link ed un file possiedono lo stesso inode.
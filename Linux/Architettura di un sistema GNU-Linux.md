[[Terminologia, storia di Linux e caratteristiche di base]]
# Architettura di base 
Il sistema operativo GNU/Linux come tutti i sistemi Unix, nasce come sistema multitasking e multiutente. Questo significa che GNU/Linux ha un'archittetura di sistema pensata fin dall'inizio all'uso in contemporaneo da parte di più utenti. Il concetto base dell'architettura UNIX è quello di una rigida separazione del kernel, che gestisce le risorse hardware ed i processi.
Lo scopo del kernel è quello di essere in grado di eseguire contemporaneamente molti processi in maniera efficiente. Risulta importante la distinzione tra <font color=yellow> user space</font> lo spazio dove sono eseguiti i processi e il <font color=blue>kernel space</font> lo spazio dov'è eseguito il kernel. ![kernel e user space](kernel-user-space.png)

Un altro aspetto importante è la modularità del kernel di Linux. Questo favorisce la manutenzione, lo sviluppo e la flessibilità in aggiungere e togliere capacità, senza appunto dove lavorare ccon un monolite.

---

# Architettura dei file
La gestione dei file in un sistema GNU/Linux, deriva direttamente da uno dei criteri di base della progettazione di tutti i sistemi Unix, cioè <font color=blue>everything is a file</font>, per cui l'accesso ai file ed alle periferiche è gestito attraverso un'interfaccia identica. In un sistema Unix tutti i file di dati sono uguali, non esiste cioè la differenza tra file di testo o binari o pdf ecc come in Windows. Le estensioni sono solo convenzioni anche se in realtà il sistema prevede tipi diversi di file, ma in un altro senso: ad esempio il sistema può accedere alle periferiche, attraverso dei file speciali detti device file o file di dispositivo. Vediamo i tipi di file riconosciuti da Linux: ![file riconosciuti](tipi-file.png)

Quello che contraddistingue Linux è che l’interfaccia per la lettura del contenuto di un file-system è stata completamente virtualizzata, per cui inserendo gli opportuni moduli nel sistema diventa possibile accedere con la stessa interfaccia e, salvo limitazioni della realizzazione, in maniera completamente trasparente all’utente ai più svariati tipi di filesystem, a partire da quelli usati da Windows e dal DOS, dal MacOS, e da tutte le altre versioni di Unix.

---


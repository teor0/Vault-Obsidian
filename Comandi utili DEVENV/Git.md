Git è un sistema di controllo versioni. Attraverso il terminale si possono usare comandi per utilizzare il sistema. 
Per creare una repository ci sono 2 modi:
1. Aggiungere una cartella del pc al version control di Git
2. Clone di una repository che si trova su Gitlab/hub

Elenchiamo alcuni comandi:
- `git config` permette di configurare molti parametri tra cui username ed e-mail
- `git config --list` visioni tutti i parametri di config
- `git help` scontato
- `git add` aggiunge un file untracked, tracked nell'area di stage. Se faccio add su un file già tracked passa direttamente all'area di stage
- `git diff` visualizzo i file modificati ancora non in staging area. Con l'opzione `--staged` posso vedere le differenze tra i file in staging area.
- `git status` visualizza lo stato dei file o della repo intera 
- `git rm` rimozione di un file dal pc e dalla repo remota una volta che effettuo commit e push. `git rm --cached FILE` permette di rimuovere un file dalla repo remota ma di mantenerlo sulla repo locale.
- `git commit` commit di un file. È buona norma scrivere un messaggio ad ogni commit tramite `git commit -m "Messaggio"`
- `git push` effettuo la push sul repo remoto, più precisamente `git push origin master` dove master è dove voglio, ma potrebbe essere un altro branch.
- `git log` mostra il log di tutto quello che è successo nel project

Per inizializzare un repository bisogna da terminale, prima di tutto spostarsi in quella cartella. Poi eseguire i seguenti comandi:
``` bash
git init
git add .
git commit -m 'Initial project version'
```
Per poi salvare la cartella su Github/Gitlab, bisogna creare una repo su Github/lab e successivamente copiare l'URL della repo e usare il comando:
`git remote add origin URL_repo` e poi effettuare la push tramite `git push origin master`.
Per verificare che tutto è andato a buon fine si può usare `git remote -v`. 

Per clonare una repo basta semplicemente usare `git clone URL_repo`. I file di una repo clonata sono file che Git considera unmodified, una volta che effettuo una modifica passeranno a modified. 
Una volta che modifico un file tracked, per aggiungerlo nella staging area, è sufficiente fare `git add NOME_FILE`.

Per fare "ammenda", cioè ho fatto una commit ma mi sono dimenticato di aggiungere un file, posso utilizzare il comando `git commit --ammend` dopo la add del file dimenticato. Se invece voglio fare la commit di un file a parte rispetto ad altri, posso usare il comando `git reset HEAD FILE`

Per tornare alla versione precedente di un file è sufficiente usare il comando `git checkout -- FILE`. Il branching in Git è molto veloce e leggero.


# Come funziona Git
Supponiamo di avere in una cartella in cui ci sono 3 diversi file. Git assoccia ad ogni file o blob come li chiama lui, un checksum. Questi oggetti blob quando viene effettuata la commit vengono puntati da un oggetto tree che ha a sua volta un checksum, che punta ai 3 blob e mantiene le checksum. La commit a sua volta è identificata da un checksum che mantiene, un puntatore al tree, l'autore ed il committer. 
Ad ogni commit corrisponde uno snapshot, ed ogni commit mantiene un puntatore alla commit precedente. Le branch, in realtà sono puntatori che si spostano sulla commit più recente, in particolare si spostano automaticamente tra le commit. La master branch è esattamente uguale al gli altri branch.

Per creare un nuovo branch, basta fare `git branch NOME_BRANCH`. Il branch sarà posizionato sull'ultima commit effettuata. Git mantiene un puntatore speciale HEAD, per mantenere la posizione dell'ultima commit, cosi quando si crea un nuovo branch, sa dove posizionare il puntatore. Per sapere dove si trova HEAD, bisogna usare il comando `git log --decorate`. Per spostare il puntatore HEAD su un'altro branch che non è master, in modo tale da fare commit su quel branch lì è sufficiente usare il comando `git checkout BRANCH`

Per effettuare una merge, si usano i comandi `git checkout BRANCH_WHERE_TO_MERGE` `git merge BRANCH_TO_MERGE`, in particolare prima di effetuare una merge il comando `git checkout BRANCH` sposta il puntatore speciale HEAD sulla merge quindi finchè non si sposta il puntatore HEAD lo "spazio di lavoro" sarà quello di default. Su git si possono fare 2 tipi di merge:
- Fast forward: il puntatore del ramo si sposta in avanti, in quanto i due rami da fondera assieme hanno un antenato comune
- Three way merge: il ramo master ed il ramo figlio, non hanno lo stesso antenato quindi si prendeno le 2 commit puntate rispettivamente dai rami e si prende l'antenato che hanno in comune.

In commit diverse ci potrebbero essere conflitti. Questo va fixato a mano oppure tramite l'auto merging tool.
Per rimuovere un branch è sufficiente usare `git branch -d BRANCH`

Per accedere su git occore effettuare i seguenti comandi:
``` 
git config --global user.name "NOME"
git config --global user.email "MAIL"
```

Utile per ricordare l'access token che viene richiesto al posto della password è il comando:
`git config --global credential.helper cache`
per rimuovere l'access token basta fare
`git config --global --unset credential.helper `

## Recap comandi
- `git help` scontato
- `git add` aggiunge un file untracked, tracked nell'area di stage. Se faccio add su un file già tracked passa direttamente all'area di stage
- `git diff` visualizzo i file modificati ancora non in staging area. Con l'opzione `--staged` posso vedere le differenze tra i file in staging area.
- `git status` visualizza lo stato dei file o della repo intera 
- `git rm` rimozione di un file dal pc e dalla repo remota una volta che effettuo commit e push. `git rm --cached FILE` permette di rimuovere un file dalla repo remota ma di mantenerlo sulla repo locale.
- `git commit` commit di un file. È buona norma scrivere un messaggio ad ogni commit tramite `git commit -m "Messaggio"`
- `git push` effettuo la push sul repo remoto, più precisamente `git push origin master` dove master è il branch dove fare upload. NOTA BENE: se un file non è stato commitato prima, non può essere fatta alcuna push.
- `git log` mostra il log di tutto quello che è successo nel project
# Terminologia e caratteristiche di base
- Kernel: cuore del OS
- Pacchetto: collezione di software che viene installata automaticamente con tutte le dependencies ^700457
- Distribuzione o distro: è un file ISO con dei pacchetti pre-installati per varie necessità. Vedi le [[#Distro|distro storiche e di maggior uso sul mercato]]
- Desktop: a differenza di Windows in Linux per Desktop si intende la GUI o interfaccia grafica del SO. Le due GUI più famose ed usate sono KDE e GNOME
- root o superuser: è l'amministratore di Linux con privilegi sui comandi e molto altro 
- Linux possiede un'interfaccia grafica dopo molto tempo passato ad averne solo una testuale. Tuttavia la shell di Linux è in grado di compiere operazioni molto potenti attraverso sia semplici [[Comandi shell|comandi]], sia attraverso dei programmi scritti su dei file.

---

# Storia di Linux
#### Anni 50'-60'
Nacquero dei computer basati sul sistema batch che potevano essere usati da più utenti per eseguire programmi diversi. Cronologia:
- Nel 1965 il MIT sviluppa MULTICS (MULTIplexed information and Computing Service), che sfruttava la multiprogrammazione in time sharing. 
- Nel 1969 Thompson si stabilisce ai Bell Laboratories e sviluppò per il PDP-7, UNICS (UNIplexed information and Computing Service) scritto totalmente in ASSEMBLER. 
- Nel 1970 Dennis Ritchie e Kernighan scrissero il linguaggio C derivato da B, che implementa le structure a differenza di B. All'interno del PDP-11 Thompson, Ritchie e Kernighan svilupparono UNIX, derivato da UNICS, compilando il codice in C. Si passa quindi da scrivere SO in ASSEMBLER a scriverli in C.
- Nel 1984 i 3 vincono l'ACM Turing award grazie a UNIX
- Il PDP-11 principale computer delle università porta UNIX ad essere il SO principale utilizzato in esse
- A partire dal 1969, Bell Labs and AT&T UNIX: il gruppo di ricerca sviluppa parecchie versioni di UNIX, prima open source e dopo a partire da System V sistemi proprietari,  nacque il concetto di codice proprietario.
- Nel 1980, Thompson abbandona i Bell Labs per stabilirsi alla University of Californa at Berkeley e sviluppa diverse versioni di UNIX tra cui: 4.1, 4.2, 4.3 e 4.4 BSD che presenta innovazioni quali memoria virtuale e paging.
- Nel 1987 Tanenbaum sviluppa Minix con l'obiettivo di renderlo compatto e di sfruttarlo nelle lezione universitarie.
- Nel 1991 Linus Torvald sviluppa Linux che abbraccia la [[#^bcf76f| Free Software]] e nel 1996 rilascia Linux 2.0 con caratteristiche di rete, file system, GUI ecc. Da qui in poi Linux prende piede all'interno del mercato sia per gestire server che computer multi purpose.
- In questi anni anche Sun ed altre aziende decidono di sviluppare versioni personali di UNIX a partire da BSD e non System V.

---
#### Standardizzazione e GNU
Tutta questa varietà però necessitava di una standardizzazione per ottenere un'interfaccia standard per programmare in UNIX. Importante è POSIX	(Portable Operating System), fusione tra System V e BSD che portò compatibilità a livello di codice sorgente. Richard Stallman fondatore della GNU Software Foundation, desiderava distribuire software libero di essere modificato a piacimento. 

Nacque così la filosofia del Free Software(software libero, non gratis) contrapposto al software proprietario. La filosofia Free Software implica che si hanno 4 principi di libertà: ^bcf76f
1. Libertà di eseguire il programma
2. Libertà di studiare e modificare il programma
3. Libertà di ridistribuire copie del programma
4. Libertà di distribuire versioni modificate così che la comunità ne tragga beneficio

Molto altro sulla filosofia Free software si trova su https://www.gnu.org/philosophy/free-sw.html
Inoltre Stallman sviluppò licenze software GPL (GNU General Public License) che deve dare riferimenti open source e LGPL (Lesser General Public License) meno restrittiva per il codice open source che i manufacturer non possono o voglio dare.

La GNU Software Foundation ha realizzato anche il GNU/Compiler per C e C++ in UNIX ovver il gcc.

---

# Distro
- Ubuntu : nata come da una costola di Debian oggi è una distribuzione che ha preso la sua fetta di mercato grazie alla sua accessibilità (anche se...)
- Linux Mint: distro che grazie alla sua intuitività sta girando nel mercato
- Red Hat Linux : distro utilizzata principalmente nel lato enterprise, da qualche tempo a questa parte ha messo a disposizione anche una versione gratis oltre a quella enterprise usate dalle aziende per il supporto e tutti questi vantaggi
- Debian : distro di difficoltà intermedia, predilige la stabilità a versioni pre-release o beta.
- Gentoo: sfrutta a pieno le potenzialità di Linux, ma deve essere compilata al momento del suo utilizzo
- ArchLinux : più instabile delle altre e volta a user più hardcore
- Kali Linux : distro orientata a ethical hacking
- Parrot OS : anche questa distro è orientata a ethical hacking e cybersecurity in generale
- Zorin e Pop OS! : distro Ubuntu based 
- Lubuntu : versione "minimal" di Ubuntu in grado di girare su pc più datati
- Puppy Linux : versione molto piccola e leggera per dispositivi con poca memoria o hardware in generale

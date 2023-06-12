# Firmware, tipi di firmware e differenze
È cura di chi assembla un computer far si che quando viene accesso inizino ad eseguire un programma situato in una specifica locazione di memoria. In genere questo programma viene detto firmware e si trova tra hardware e software. Il firmware quindi altro non fa che iniziare la procedura di bootstrap di un computer. Ci sono 2 tipi di firmware:
- BIOS (Basic Input/Output System): usato tradizionalmente dai computer fino a qualche decennio fa, sviluppato in origine da IBM.
- UEFI (Unified Extensible Firmware Interface):  sostituto del BIOS, sviluppato all'inizio da Intel e successivamente dai principali produttori di processori e sistemi operativi.

Il firmware, UEFI si differenzia dal BIOS in quanto permette di mettere il codice di partenza del bootloader, programma che carica il sistema operativo, in una locazione diversa dal Master Boot Record, ovvero il primo settore del disco scelto per l'avvio. Questo è possibile dato che UEFI richiede una partizione  riservata ESP (EFI System Partition) per installare le EFI application volte ad eseguire il firmware. Inoltre il firmware UEFI permette il cosidetto Secure Boot. Per il resto sia BIOS che UEFI permettono di avviare il bootloader da dispositivi quali HDD, SSD, USB, floppy e CDROM, ma anche dalla rete tramite un server e protocolli opportuni per caricare il kernel ed il bootloader.

Dato che oggi la varietà di dispositivi su cui è possibile installare un sistema è estremamente ampia, nella maggior parte dei casi è previsto di appoggiarsi all’uso di un ramdisk che contenga l’immagine di un filesystem iniziale (creato in RAM) che sarà quello effettivamente montato come radice. Il programma di avvio lanciato dal ramdisk dovrà poi identificare il dispositivo su cui è installato il sistema operativo.

---

## Bootloader di Linux
Il bootloader SYSLINUX viene usato per creare le immagini di avvio usate per CDROM, floppy e USB. Il suo punto di forza, sta nella semplicità con cui consente di creare immagini d'avvio e che tali immagini sono mantenute in un filesystem FAT che permette sia l'uso in modalità live-USB sia una facilità nel modificare l'immagine d'avvio.
Uno dei bootloader più sofisticati è GRUB, (GRand Unified Bootloader), il quale ha raggiunto la versione GRUB2. La caratteristica principale è la divisione in stadi, i quali servono a lanciare progressivamente il successivo. In realtà gli stadi sono 2, il primo stadio è installato nel MBR e ha il compito di trovare il secondo stadio e lanciarlo. Questo porta al grande vantaggio che essendo il secondo stadio a fare tutto il lavoro, si perdono tutte le restrizioni riguardo al MBR.

Sia GRUB che SYSLINUX offrono tramite riga di comando, comandi e funzionalità per il boot.

---
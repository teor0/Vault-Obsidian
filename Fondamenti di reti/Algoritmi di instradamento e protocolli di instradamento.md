#fondamenti 

[[Instradamento]]
# Algoritmi e protocolli
Il router sceglie il percorso che minimizza il costo in base ad algoritmi di instradamento. Per determinare il percorso a costo minimo, il router deve avere informazioni sui costi dei percorsi alternativi, per acquisire tali costi si usano protocollo di instradamento.
Algoritmi e protocolli possono non funzionare bene in coppia, in genere i router usano una coppia di metriche in quanto possono girare più algoritmi e protocolli diversi su di essi. In particolare la coppia di metriche è metrica effettiva e metrica amministrativa. Il router valuta prima la metrica amministrativa e poi sceglie la metrica minima tra effettiva ed amministrativa.

Le tabelle di instradamento possono essere costruite in 2 modi:
1. Tabella <font color=red> statica</font>: le tabelle sono definite manualmente dal gestore della rete, il vantaggio sta nel mantenimento dei percorsi snellendo l'invio di informazioni però si perde in flessibilità
2. Tabella <font color=red> dinamica</font>: le tabelle sono calcolate dal protocollo e l'algoritmo dinamicamente in funzione della tipologia di rete. Questo porta a migliori prestazioni e controllo della congestione, ma carico elevato e cambi di percorso continuo

All'accensione dei router, viene inizializzata la tabella usando le informazioni contenute in memorie di massa, successivamente gli aggiornamenti della tabella avvengono in seguito a cambiamenti reputati importanti oppure in modo periodico. Questo implica che i router debbano scambiarsi parte di tabella per accrescere la proprio conoscenza.

---
## Sistema autonomo
Si definisce <font color=green> sistema autonomo</font> una porzione di rete amministrata da un unico gestore. Su sistemi autonomi diversi è possibile avere protocolli di routing diversi. I nodi che instradano messaggi all'interno del sistema sono detti <font color=red> interior router</font>, mentre quelli che instradano messaggi tra sistemi autonomi diversi, sono detti <font color=red>exterior router</font>.
I sistemi autonomi sono discriminati tramite dei numeri speciali univoci assegnati da RIPE/interNIC.

Tutti gli interior router possono essere raggiunti con percorsi interni, se si vuole raggiungere un nodo al di fuori del dominio amministrativo, bisogna passare dai <font color=red>border router </font>, in cui sono implementate politiche di instradamento uguali o differenti. I border router di un sistema possono comunicare con altri border router di altri sistemi e questa comunicazione serve a costruire la topologia dei border router. Alcuni router, detti <font color=red>core router </font> consentono di instradare informazioni verso altre reti quindi costituiscono l'infrastruttura che consente di comunicare fra reti diverse. 

---
## Categorie di protocolli
Abbiamo 2 macrocategorie di protocolli di instradamento:
1. IGP, interior gateway protocol: protocolli per comunicare all'interno dello stesso sistema autonomo 
2. EGP, exterior gateway protocol: protocolli per comunicare tra sistemi autonomi

Bisogna distinguere 2 tipi di logiche per i protocolli:
- centralizzata: il protocollo deve raccogliere informazioni dai vari router per conoscere la tipologia affinché poi ogni router l'apprenda per far girare l'algoritmo
- decentralizzata: i router conoscono solo le reti connesse a loro e pian piano successivamente i nodi a 2 hop e poi a 3 ecc. Questo avviene perché i nodi scambiano informazioni secono una periodicità, tuttavia questo può portare a problematiche come il conteggio infinito

La maggior parte dei IGP si basano su 2 macrocategorie:
1. Distance Vector: si usa l'algoritmo di Bellman-Ford, più semplice da implementare, impegna meno risorse sul router ed è adatto a reti piccole al costo di una efficienza più bassa.
2. Link state: si usa l'algoritmo di Dijkstra, molto complesso e molto efficiente, impegna molte risorse ed è adatto a reti di grandi dimensioni

---

---
tag: #basi 
created: 2022-11-30 18:52:06
updated: 2022-11-30 18:52:06
---
#basi 
# Esercizio 1
Dopo aver ottenuto il modello ER seguente: ![[EsercizioLaserX.jpg]] andiamo a fare il modello relazionale con le tabelle. In particolare, ogni qualvolta che si deve creare un modello relazione:
- È consigliato partire dall'entità più "semplice"
- Per rappresentare una relazione 0:1 0:n si concretizza mettendo come attributi un riferimento all'entità opposta al lato 0:1 e scrivendo la relazione di chiave esterna.

Il modello dell'esercizio è:
Sala(<u>Piano,Numero</u>, Capacità Massima)
Incontro(<u>Data, Orario, Sala\_Piano, Sala\_Numero</u>, Sq\_GiallaN, Sq\_GiallaD, Sq\_RossaN, Sq\_RossaD, Organizzatore)
Squadra(<u>Nome, Data Fondazione</u>, $\overset{NULL}{Capitano}$)
Giocatore(<u>Codice Fiscale</u>, Nome, Data di nascita, Data Sottoscrizione, Abbonamento)
Organizzatore(<u>Codice Fiscale</u>, Nome, Data di nascita, Disponibilità)
Componenti(<u>Giocatore, Sq\_N, Sq\_D</u>, Nickname)
Abbonamento(<u>Codice</u>, Nome, Descrizione)
Colpo(<u>Data, Ora, Gioc\_S</u>, Zone, Gioc\_C, Inc\_D, Inc\_O, Inc\_SP, Inc\_SN)

Incontro\[Sala\_Piano,Sala\_Numero\]$⊑_{FK}$Sala\[Piano,Numero\]
Incontro\[ Sq\_GiallaN, Sq\_GiallaD\]$⊑_{FK}$Squadra\[Nome, Data Fondazione\]
Incontro\[ Sq\_RossaN, Sq\_RossaD\]$⊑_{FK}$Squadra\[Nome, Data Fondazione\]
Incontro\[Organizzatore\]$⊑_{FK}$Organizzatore\[Codice Fiscale\]
Squadra\[Capitano\]$⊑_{FK}$Giocatore\[Codice Fiscale\]
Giocatore\[Abbonamento\]$⊑_{FK}$Abbonamento\[Codice\]
Componenti\[Giocatore\]$⊑_{FK}$Giocatore\[Codice Fiscale\]
Componenti\[Sq\_N, Sq\_D\]$⊑_{FK}$Squadra\[Nome, Data Fondazione\]
Colpo\[Inc\_D, Inc\_O, Inc\_SP, Inc\_SN\]$⊑_{FK}$Incontro\[Data, Orario, Sala\_Piano, Sala\_Numero\]
Colpo\[Gioc\_S\]$⊑_{FK}$Giocatore\[Codice Fiscale\]
Colpo\[Gio\_C\]$⊑_{FK}$Giocatore\[Codice Fiscale\]


La relazione capitano 0:1 ha NULL sopra. La relazione Membro la rilasso a 0:n, quindi serve una tabella d'appoggio che chiamo Componenti. Nel modello ho perso l'esclusività.

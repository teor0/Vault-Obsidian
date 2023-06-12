#rdc 
[[Cookie, FTP e posta elettronica]]

# DNS
Il DNS (Domain Name System) è un protocollo a livello applicazione, che permette agli host, ai router ed ai server DNS di assocciare ad un nome simbolico ad un indirizzo IP di un host. Questa associazione permette 2 risoluzioni:
1. Risoluzione <font color=red>diretta</font>: dato un hostname (nome simbolico) trovare l'indirizzo IP
2. Risoluzione <font color=red>indirette</font>: dato un indirizzo IP trovare l'hostname

Il protocollo si basa su un database distribuito implementato in una gerarchia di server DNS. 

I servizi offerti dal DNS sono:
- Traduzione degli hostname in indirizzi IP
- Host aliasing: un host può avere più nomi simbolici per facilitare la memorizzazione del nome
- Distribuzione locale: server web replicati cioè, si ha un insieme di indirizzi IP per un nome canonico distribuiendo il lavoro tra più macchine
- Mail server aliasing

Avere un DNS centralizzato porterebbe a:
- singolo punto di guasto
- volume di traffico elevato
- database centralizzato distante
- manutenzione costosa

Un database centralizzato su un singolo server DNS non è scalabile!

Il DNS ha una struttura gerarchica del tipo:
![[dnsgerarchia.png]]
Approssimazione della richiesta da parte del client dell'indirizzo IP di www.amazon.com:
1. Il client interroga il server DNS radice per trovare il server DNS com
2. Il client interroga il server DNS com per ottenere il server DNS di amazon.com
3. Il client interroga il server DNS di amazon.com per ottenere l'indirizzo IP di www.amazon.com

In totale ci sono 13 DNS radice per resilienza e connettività. Se il DNS locale non riesce a tradurre il nome si rivolge al DNS radice, se il DNS radice non conosce la mappatura, contatta un DNS autorizzato ottiene la mappatura e restituisce la mappatura al DNS locale. 
Il DNS locale si occupa di fare richieste alla gerarchia di server DNS, quindi funge da client ai server DNS. Il DNS locale può fare caching che è utile per tradurre gli hostname rapidamente. Ogni provider ha un DNS locale.
Una volta che un server DNS importa la mappatura la mette nella cache e, tali informazioni dopo un tot di tempo vengono invalidate. Di solito un DNS locale memorizza nella cache gli IP del server TLD( Top Level Domain), quindi i DNS radice non sono visitati spesso. Quando un host effettua una richiesta DNS, la query viene inviata al suo server DNS locale, che opera da intermediario ed inoltra la query in una gerarchia di server DNS.

---
## Server TLD e server di competenza
Per server TLD (Top Level Domain): si intende un server che si occupa di domini org, com, edu ecc. e di tutti i domini di alto livello quali it, uk, fr, jp ecc.

Per server di competenza (authoritative server): ogni organizzazione dotata di host Internet pubblicamente accessibili deve fornire i record DNS di pubblico dominio che mappano i nomi di tali host in indirizzi IP. Tali server possono essere mantenuti dall'organizzazione o dal service provider.

---
## Risoluzione iterativa e ricorsiva
Per quanto riguarda la query iterativa i passi illustrati in figura sono:
![[dnsiterativo.png]]
1. Host richiede l'indirizzo IP di gaia.cs.umass.edu
2. Il DNS locale che si trova a dns.poly.edu, non trova l'indirizzo IP nella cache e contatta il server DNS radice
3. Il server DNS radice non conosce nemmeno l'indirizzo IP e reindirizza il DNS locale al server DNS TLD
4. Il DNS locale effettua la richiesta al server DNS TLD 
5. Il server DNS TLD risponde con il responsabile di umass.edu
6. Il DNS locale contatta il server DNS di competenza e richiede l'indirizzo IP
7. Il server DNS di competenza risponde con l'indirizzo IP
8. Il DNS locale ritorna l'indirizzo IP al host cis.poly.edu

Questo schema si chiama iterativo perchè vengono fatte più iterazioni di avvicinamento alla risposta.

Per quanto riguarda la query ricorsiva i passi illustrati in figura sono:
![[dnsricorsivo.png]]

1. Host richiede l'indirizzo IP di gaia.cs.umass.edu
2. Il DNS locale che si trova a dns.poly.edu, non trova l'indirizzo IP nella cache e contatta il server DNS radice
3. Il server DNS radice non conosce nemmeno l'indirizzo IP e lo richiede al server DNS TLD
4. Il server DNS TLD richiede alresponsabile di umass.edu l'indirizzo IP
5. Il server DNS di competenza risponde al server DNS TLD con l'indirizzo IP
6. Il server DNS TLD riporta l'indrizzo IP al server DNS radice
7. Il server DNS radice risponde al DNS locale con l'indirizzo IP
8. Il DNS locale ritorna l'indirizzo IP al host cis.poly.edu

La soluzione iterativa è più centralizzata sul DNS locale rispetto a quella ricorsiva e le distanza tra il DNS locale e gli altri server DNS si fanno sentire di più. Inoltre la soluzione ricorsiva impiega meglio il caching in quanto le richieste passano tra i server e non direttamente al DNS locale.

---

## Record DNS

Il database distribuito di un DNS è costituito da un insieme di record detti record di risorsa (RR). Ogni RR è costituito da 4 campi:
- ttl: time to live, ovvero la scandeza del record
- name: descritto da type
- value: descritto da type
- type: esistono 4 type che determinano il significato di name e value.
  1.  Type=A: name rappresenta il nome dell'host, value l'indirizzo IP. Record usato per traduzione diretta degli host name in indirizzi IP
  2. Type=NS: name indica il nome di un dominio, value indica il nome dell'host del server di competenza di questo dominio. Usato per trovare il responsabile di un dominio
  3. Type=CNAME: name indica il nome alias di un nome vero, value è nome canonico. Usato quindi per gestire l'aliasing
  4. Type=MX: value è il nome del server di posta associato a name. Usato per gestire la posta   

---
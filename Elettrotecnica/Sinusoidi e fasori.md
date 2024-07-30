---
tags: elettrotecnica, 
created: 2024-05-14 11:58:22
updated: 2024-05-14 11:58:22
---
[[Metodi di analisi]]
# Regime sinusoidale
Una sinusoide è un segnale che ha la forma della funzione seno o coseno. Una corrente o tensione sinusoidale è anche detta corrente o tensione alternata. I segnali sinusoidali essendo variabili sono soggetti a relazioni differenziali, e ogni segnale di questo tipo può essere scomposto in una somma di funzioni sinusoidali più semplici grazie all’analisi di Fourier.
La tensione come sinusoide è $v(t)=V_mcos(\omega t+\phi)$ ![[tensin.jpg]] dove:
- $V_m$ ampiezza della sinusoide
- $\omega$ frequenza angolare o pulsazione
- $\phi$ fase della sinusoide
- il periodo $T={2\pi\over\omega}$ è il tempo impiegato per compiere un ciclo
- la frequenze $f={1\over T}$ è il numero di cicli per secondo

Dati due segnali sinusoidali: $v_1(t)=V_msen(\omega t+\phi_1)$ e $v_2(t)=V_msen(\omega t+\phi_2)$ sono "in fase" se $\phi_1=\phi_2$ altrimenti si dicono sfasati. $v_1$ è in anticipo rispetto a $v_2$ se $\phi_1<\phi_2$ invece $v_2$ è in ritardo rispetto a $v_1$

Un <font color=orange>fasore</font> è un numero complesso che rappresenta l'ampiezza e la fase della sinusoide. Data l'identità di Eulero $e^{\pm j\phi}=cos\phi\pm sen\phi$ si ha:
$\displaystyle v(t)=V_mcos(\omega t+\phi)=V_mRe\{e^{j(\omega t+\phi)}\}=Re\{V_me^{j\omega t}e^{j\phi}\}=Re\{Ve^{j\omega t}\}$
Il numero complesso $V=Ve^{j\omega t}$ rappresenta il fasore che corrisponde alla funzione $v(t)$ alla pulsazione $\omega$ ed è indipendente dal tempo $t$. In particolare:
- $v(t)=V_mcos(\omega t+\phi)$ è la funzione
- $V=Ve^{j\omega t}$
- $|V|=V_m$
- $arg\{V\}=\phi$

La trasformazione da segnale in fasore è la seguente: $V_mcos(\omega t+\phi)=V_m\angle\phi$.
Non essendo dipendenti dal tempo i fasori fanno perdere l'informazione nel tempo del segnale originale. Ma siccome lavoriamo con circuiti tempo invarianti e tutti i segnali condividono la stessa pulsazione, dal momento in cui il sistema è a regime, il tempo non ci interessa dato che i segnali di ogni componente differiranno al più di ampiezza e/o fase. Un circuito può essere analizzato nel dominio dei fasori quando tutti i segnali sono sinusoidi alla stessa pulsazione $\omega$, dunque i generatori lavorano tutti alla stessa pulsazione ed il circuito ha solo elementi lineari.

## Proprietà dei fasori
<font color=orange>Linearità</font>: 
$v_1(t)=V_{m1}cos(\omega t+\phi_1)\implies \overline{V_1}=V_{m1}e^{j\phi_1}$
$v_2(t)=V_{m2}cos(\omega t+\phi_2)\implies \overline{V_2}=V_{m2}e^{j\phi_2}$
$v(t)=a_1v_1(t)+a_2v_2(t)$
Dimostrazione:
$v(t)=a_1v_1(t)+a_2v_2(t)=a_1V_{m1}cos(\omega t+\phi_1)+a_2V_{m2}cos(\omega t+\phi_2)=Re\{a_1V_{m1}e^{j\phi_1}e^{j\omega t}\}+Re\{a_2V_{m2}e^{j\phi_2}e^{j\omega t}\}$
$=Re\{(a_1V_{m1}e^{j\phi_1}+a_2V_{m2}e^{j\phi_2})e^{j\omega t}\}=Re\{(a_1V_1+a_2V_2)e^{j\omega t}\}$
<font color=orange>Derivazione</font>:
$v_1(t)=V_{m1}cos(\omega t+\phi_1)$ $v(t)=\displaystyle{dv_1(t)\over dt}$ 
$v_1=V_{m1}e^{j\phi_1}$ $V=j\omega V_1$
Dimostrazione: 
$v(t)=\displaystyle{dv_1(t)\over dt}={d\over dt}(V_{m1}cos(\omega t+\phi_1))={d\over dt}Re\{V_{m1}e^{j\phi_1}e^{j\omega t}\}=Re\{{d\over dt}(V_{m1}e^{j\phi_1}e^{j\omega t})\}=$
$=\displaystyle Re\{j\omega V_{m1}e^{j\phi_1}e^{j\omega t}\}=Re\{j\omega V_{1}e^{j\omega t}\}$
<font color=orange>Integrale</font>:
$v_1(t)=V_{m1}cos(\omega t+\phi_1)$ $v(t)=\int v_1(t)dt$
$V_1=V_{m1}e^{j\phi_1}$ $V=\displaystyle{V_1\over j\omega}$
Dimostrazione:
$\displaystyle v(t)=\int v_1(t)dt=\int V_{m1}cos(\omega t+\phi_1)dt=\int Re\{V_{m1}e^{j\phi_1}e^{j\omega t}dt=Re\{\int V_{m1}e^{j\phi_1}e^{j\omega t}dt\}=$
$\displaystyle=Re\{{V_{m1}e^{j\phi_1}e^{j\omega t}\over j\omega}\}=Re\{{V_1\over j\omega}e^{j\omega t}\}$

---
# Impedenza ed ammettenza
L'impedenza $Z$ di un circuito è il rapporto tra il fasore della tensione V e il fasore della corrente I, misurata in Ohm. $\displaystyle Z={V\over I}=R+jX$ dove $R=Re\{Z\}$ $X=Im\{Z\}$
$|Z|=\sqrt{R^2+X^2}$ $\theta_Z=arctan({X\over R})$
L'ammettenza $Y$ è il reciproco dell'impedenza e si misura in Siemens. $\displaystyle Y={1\over Z}={I\over Z}=G+jB$ 
$\displaystyle|Y|=\sqrt{G^2+B^2}={1\over |Z|}$
$\theta_Y=arctan({B\over G})=-\theta_Z$
Parallelo delle impedenze:
$\displaystyle{1\over Z_{eq}}={1\over Z_1}+{1\over Z_2}+{1\over Z_n}\implies Z_{eq}={Z_1Z_2Z_n\over Z_1+Z_2+Z_n}$
Serie delle impedenze:
$Z_{eq}=Z_1+Z_2+Z_n$
Per gli elementi passivi le ammette e le impedenza sono:

| Elemento | Impedenza              | Ammettenza             |
| -------- | ---------------------- | ---------------------- |
| $R$      | $Z=R$                  | $Y={1\over R}$         |
| $L$      | $Z=j\omega L$          | $Y={1\over j\omega L}$ |
| $C$      | $Z={1\over j\omega C}$ | $Y=j\omega C$                       |

---
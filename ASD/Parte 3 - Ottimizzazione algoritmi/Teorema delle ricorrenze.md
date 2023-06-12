[[Divide et impera]]
#asd 
# Teorema delle ricorrenze

Abbiamo visto in precedenza l'esempio che ci ha portato ad utilizzare un'equazione di ricorrenza a seconda del tipo di algoritmi dividi et impera. Adesso le vedremo entrambe nel dettaglio. Ma prima ricapitoliamo il teorema master:

- $a$: numero di sottoistanze
- c: costante che regola la dimensione delle sottoistanze
- d: complessità dei metodi dividi e combina

Vediamo come utilizzare l'equazione di ricorrenza per il tipo 1.

---
## Equazione ricorrenza per tipo 1

L'equazione di ricorrenza per il tipo 1 è la seguente:

$T(n)=b$ se $n≤1$ 
$T(n)=\displaystyle\large aT({n \over c})+bn^d$ se $n>1$ sia $\displaystyle n={n \over c}$ allora:

$\displaystyle\large T({n \over c})=aT({n \over c^2})+b({n \over c})^d$ che sostituito in T(n) porta ad avere

$\large T(n)=a(aT({n \over c^2})+b({n \over c})^d)+bn^d$ che porta a

$\large T(n)=a^2T({n \over c^2})+ab({n \over c})^d+bn^d$ dove $\large bn^d$ posso renderlo $\large a^0b({n \over c^0})^d$

$\large T(n)=a^2T({n \over c^2})+ab({n \over c})^d+a^0b({n \over c^0})^d$ ovvero

$\large T(n)=a^2T({n \over c^2})+ \displaystyle\sum_{j=0}^1a^jb({n \over c^j})^d$

perciò  $\displaystyle\large T(n)=aT({n \over c})+bn^d$ è il caso in cui

$\large T(n)=a^1T({n \over c^1})+ \displaystyle\sum_{j=0}^0a^jb({n \over c^j})^d$

mettondo a confronto le 2 equazioni si capisce che dopo k passi si dovrebbe ottenere la formula seguente:

$\displaystyle\large T({n\over c})=a^kT({n \over c^k})+ \sum_{j=0}^{k-1}a^jb({n \over c^j})^d$ valida per k=1. Sfruttando il principio di induzione se l'equazione è valida per k+1 allora $\displaystyle\large T({n \over c^k})$ sarà valida per ogni k finché $\displaystyle\large {n \over c^k}>1$.

Sostituendo $\displaystyle\large T({n \over c^k})$ in T(n) come fatto prima per $\displaystyle\large n={n\over c}$ si ha:

$\displaystyle\large T(n)= a^k(aT({n \over c^{k+1}})+b({n \over c^k})^d)+\sum_{j=0}^{k-1}a^jb({n \over c^j})^d$=

$\displaystyle\large a^{k+1}T({n \over c^{k+1}})+a^kb({n\over c^k})^d+\sum_{j=0}^{k-1}a^jb({n \over c^j})^d$=

$\displaystyle\large a^{k+1}T({n \over c^{k+1}})+\sum_{j=0}^{k}a^jb({n \over c^j})^d$ come volevasi dimostrare.

Quindi $\large\displaystyle T(n)=a^kT({n \over c^k})+ \sum_{j=0}^{k-1}a^jb({n \over c^j})^d$ è valida dopo k sostituzioni. 

Prima o poi però $\large\displaystyle {n \over c^k}\le 1$ quindi $\large\displaystyle T({n \over c^k})=b$ ottenuto per il più piccolo valore di k tale che $\displaystyle\large {n \over c^k}\le 1$. 
Sostituendo $\displaystyle\large T({n \over c^k})=b$ in $T(n)$ si ottiene $\large T(n)=a^kb+\displaystyle\sum_{j=0}^{k-1}a^jb({n\over c^j})^d$ ma b si può scrivere come $\displaystyle\large b({n\over c^k})^d$ assumendo $\displaystyle\large {n \over c^k}= 1$ quindi

$\large T(n)=a^kb({n\over c^k})^d+\displaystyle\sum_{j=0}^{k-1}a^jb({n\over c^j})^d=\displaystyle\sum_{j=0}^ka^jb({n\over c^j})^d$.

Poiché il più piccolo valore di k tale che $\large {n \over c^k}\le 1$ vuol dire

$\large n\le c^k$ $\large \Rightarrow k=\lceil{log_cn}\rceil$. Si ottiene dunque:

$\large T(n)=\displaystyle\sum_{j=0}^{\lceil {log_cn} \rceil} a^jb({n \over c^j})^d=\displaystyle\sum_{j=0}^{\lceil {log_cn} \rceil} bn^d{a^j\over {c^j}^d}=\displaystyle\sum_{j=0}^{\lceil {log_cn} \rceil} bn^d({a\over c^d})^j=bn^d\displaystyle\sum_{j=0}^{\lceil {log_cn} \rceil} ({a\over c^d})^j$

Ragionando per casi in particolare sul valore $\displaystyle\large {a\over c^d}$ che sono tutti i valori definiti dall'algoritmo:

1. se <font color=red>$\displaystyle\large {a\over c^d}$=1</font> allora la sommatoria degenera in una sommatoria da 0 a $\large \lceil {log_cn}\rceil$ di $1^j$ cioè $\large\lceil {log_cn}\rceil$+1 si ha che $\large T(n)=bn^d(\lceil {log_cn}\rceil+1)$  che asintoticamente è pari a <font color=red> $\large\theta(n^d{log_cn})$ </font>.
2. se <font color=red> $\displaystyle\large {a\over c^d}$<1 </font> allora poiché $\displaystyle\sum_{j=0}^{+\infty} \alpha^j$ per $\alpha$<1 converge allora esiste un valore M tale che $\displaystyle\sum_{j=0}^{+\infty} ({a\over c^d})^j\le M$ quindi $T(n)=bn^dM$ ovvero <font color=red> $\large T(n)\in \theta(n^d)$ </font>
3. se <font color=red> $\displaystyle\large{a\over c^d}$>1</font> poiché $\displaystyle\sum_{j=0}^k \alpha^j={{\alpha^{k+1}-1}\over{\alpha -1}}$ per $\alpha$>1 se moltiplico per $\alpha$ la sommatoria ottengo $\displaystyle\sum_{j=1}^{k+1} \alpha^j$. Sottraendogli $\displaystyle\sum_{j=0}^k \alpha^j$ si ottiene la seguente equazione, $(\alpha -1)\displaystyle\sum_{j=0}^k\alpha^j=\alpha\displaystyle\sum_{j=0}^k \alpha^j-\displaystyle\sum_{j=0}^k \alpha^j=\alpha^{k+1}-1$. In sostanza $\large(\alpha-1)\displaystyle\sum_{j=0}^k \alpha^j=\alpha^{k+1}-1$ se divido entrambi i membri per $(\alpha-1)$ ottengo $\displaystyle\sum_{j=0}^k \alpha^j={{\alpha^{k+1}-1}\over{\alpha -1}}$ come volevasi dimostrare. Perciò $\large T(n)=bn^d\displaystyle\sum_{j=0}^{\lceil {log_cn} \rceil} \large({a\over c^d})^j=bn^d{{({a\over c^d})^{\lceil log_cn \rceil +1}-1}\over {a\over c^d}}$ quindi $\large T(n)\in \theta(bn^d({a\over c^d})^{log_cn})$ perché $\large ({a\over c^d})$-1 non dipende da n. Si può semplificare il tutto ANCORA elevando $log_cn$ $\displaystyle\large {a\over c^d}$ quindi,$\displaystyle T(n)=bn^d*\large{{a^{log_cn}}\over {c^d}^{log_cn}}$=$bn^d*\displaystyle\large{{a^{log_cn}}\over {c^{log_cn}}^d}$=$\displaystyle\large bn^d{{a^{log_cn}}\over n^d}$=$\large ba^{log_cn}$. Applicando $\displaystyle\large log_cn=log_ca*log_an$ si ottiene: $\displaystyle\large ba^{log_cn}=ba^{log_ca*log_an}=bn^{log_ca}$. IN CONCLUSIONE $T(n)\in \displaystyle\large\theta(bn^{log_ca})$.


Perciò per i tipo 1:

- se $\displaystyle\large {a\over c^d}=1 \Rightarrow \theta(n^d{log_cn})$
- se $\displaystyle\large {a\over c^d}<1\Rightarrow \theta(n^d)$
- se $\displaystyle\large {a\over c^d}>1 \Rightarrow \displaystyle\large\theta(bn^{log_ca})$

> d=1 se praticamente ho che costo di dividi e combina è $\theta(n)$

Per il tipo 2 l'unico modo per risolvere è srotolare l'equazione di ricorrenza.
Vediamo degli esempi [[Esempi algoritmi tipo 1 e 2|esempi]]

---



#fondamenti 
[[Framing e codici controllo e recupero di errori]]
[[Diagramma di timing, protocollo stop n wait e calcolo efficienza]]
# Distanza di Hamming
La distanza di Hamming rappresenta il numero di bit per cui una determinata sequenza a seguito di alterazioni può differire dalla sequenza in uscita dal canale. Sulla base della distanza si decide come rilevare e correggere l'errore.

> Se due parole di codice hanno una distanza di Hammign d, vuol dire che saranno necessari d errori di singoli bit per convertire l'una all'altra.

Per rilevare d errori è necessario un codice con distanza d+1, poiché con questo codice non c'è modo che d errori di bit singolo mutino una codeword valida in un'altra codeword valida. Per correggere d errori è necessario un codice con distanza 2d+1 poiché le sue parole valide sono così distanti che anche con d mutazioni, la parola originale è ancora la più vicina valida e può quindi essere individuata.

Immaginiamo di voler progettare un codice con m bit di messaggio e r bit di controllo che garantisca la correzione di tutti gli errori singoli.
Ognuno dei $\large2^m$ messaggi legali ha n parole di codice illegali a distanza 1. Ognuno dei $\large2^m$ legali necessita n+1 combinazioni di bit dedicate. Poiché il numero totale di combinazioni è $\large2^n$ si devono avere: $\large(n+1)2^m\le 2^n$. Usando n=m+r si ottiene:
$\large (m+r+1)\le 2^r$

>Dato m, questo definisce un limite inferiore al numero di bit di controllo necessari per correggere un errore singolo.

---

## Codici a ridondanza ciclica
I bit di una stringa M di m bit da proteggere sono visti come i coefficienti di un polinomio M(x), dove l'i-esimo bit è il coefficiente di $x_i-1$. Ad una stringa di k bit corrisponde un polinomio di grado k-1. Quando si usano i codici a ridondanza ciclica (CRC), sorgente e destinazione si devono accordare su un polinomio generatore G(x) in anticipo. 
Sia il primo che l'ultimo bit del pattern generato devono essere uguali a 1. Per calcolare la checksum per un frame di m bit, corrispondente al polinomio M(x), il frame dev'essere più lungo del polinomio generatore. L'idea è di appendere la checksum alla fine del frame in modo tale che il polinomio rappresentato dal frame e dalla checksum sia divisibile da G(x). Quindi quando al destinazione riceve il frame cerca di dividerlo per G(x) e se trova resto allora significa che c'è stato un errore. ^0e219e

Il CRC rivela tutti gli errori a burst con lunghezza minore di r+1 bit.

---

## Piggybacking
Per essere più efficiente sia il Go back n che selective repeat sfrutta il piggybacking: quando il flusso è full duplex (bidirezionale) è possibile includere alle informazioni utili i riscontri che devono essere mandati in direzione opposta.

---
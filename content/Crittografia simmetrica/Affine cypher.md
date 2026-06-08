Il **Cifrario Affine** è un classico sistema di crittografia a sostituzione **monoalfabetica**. Per usare il cifrario affine, dobbiamo prima mappare ogni lettera dell'alfabeto a un numero intero. Usando l'alfabeto internazionale di 26 lettere:

- A = 0, B = 1, ..., Z = 25.
- Il modulo ($m$) è 26.

> [!NOTE] Problema per la sicurezza
> Essendo un cifrario monoalfabetico (una lettera viene sempre sostituita dalla stessa lettera cifrata), mantiene le caratteristiche statistiche della lingua.

## Processo di Cifratura

La chiave del cifrario è costituita da due numeri interi, $a$ e $b$. La funzione di cifratura per una lettera $x$ è definita dall'equazione lineare:

$$
E(x) = (ax + b) \pmod m
$$

Dove:

- **$x$**: è il numero corrispondente alla lettera in chiaro.
- **$a$**: è il coefficiente moltiplicativo (parte della chiave).
- **$b$**: è il coefficiente additivo (traslazione, parte della chiave).
- **$m$**: è la dimensione dell'alfabeto (solitamente 26).


> [!NOTE] Una regola fondamentale per "$a$"
> Per poter decifrare il messaggio, la funzione deve essere invertibile. Questo accade solo se **$a$ e $m$ sono coprimi** (cioè il loro massimo comun divisore è 1). Se $m = 26$, i possibili valori di $a$ sono: 1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25.

## Processo di Decifratura

Per decifrare, dobbiamo invertire la funzione. La formula di decifratura è:

$$
D(x) = a^{-1}(x - b) \pmod m
$$

> [!NOTE] Attenzione all'inverso di a
> Qui **$a^{-1}$** non è $1/a$ in senso classico, ma è l'**inverso moltiplicativo modulare** di $a$. È quel numero che, moltiplicato per $a$, dà 1 modulo 26.

## Considerazioni sul numero di chiavi disponibili

Essendo $a^{-1}$ invertibile se e solo se $gcd(a,26)=1$ la $a$ può assumere solo il numero di valori invertibili in $\mathbb{Z_{26}}$. Questo numero di valori invertibili possiamo calcolarlo tramite la $\phi$ di Eulero che nel nostro caso è 13. La variabile $b$ può assumere valori da $\{0,\dots,25\}$ quindi in tutto 26 valori. Quindi il numero di chiavi disponibili per questo crittosistema è $13*26=338$.
L'**Affine Hill Cypher** è, in sostanza, la versione "potenziata" dell'[[Affine cypher]] che abbiamo visto. Se il Cifrario Affine combina moltiplicazione e addizione su _singoli numeri_, e il Cifrario di Hill usa la moltiplicazione su _matrici_. 

> [!NOTE] Più sicuro rispetto al classico Affine cypher
> L'Affine Hill cypher ha proprietà **polialfabetiche**, quindi la cifratura di una lettera dipende dalla **combinazione lineare** con le altre lettere del suo blocco.

# Processo di Cifratura

L'Affine Hill cypher è un **cifrario a blocchi** quindi rispetto all'Affine cypher cambia radicalmente il modo in cui prepariamo il testo prima di cifrarlo, perché in questo caso non analizziamo più lettere per lettera ma blocchi che possono essere composti da due o più lettere. La dimensione del blocco è determinata dalla dimensione della matrice chiave $X$. Se ad esempio usassimo una matrice **$2 \times 2$**, dovremmo dividere il testo in **bigrammi** (coppie di 2 lettere). Una volta diviso il testo in blocchi possiamo procedere con la seguente formula per effettuare la cifratura :

$$C = (X \cdot \vec{a} + \vec{b}) \pmod m$$

Dove:

- **$C$**: è il vettore del testo cifrato (il blocco risultante).
- **$\vec{a}$**: è il vettore del testo in chiaro (il blocco di lettere convertite in numeri).
- **$X$**: è la **Matrice Chiave** (come nel Hill standard, deve essere invertibile).
- **$\vec{b}$**: è un **Vettore di Traslazione** (una chiave aggiuntiva che viene sommata al risultato).
- **$m$**: è il modulo (26 per l'alfabeto standard).

> [!NOTE] Attenzione alla matrice X
> Non possiamo scegliere una matrice di numeri a caso come chiave $X$. Affinché il messaggio possa essere decifrato, la matrice deve essere **invertibile modulo 26**. Il **determinante** della matrice $X$, indicato come $\det(X)$, non deve essere zero, e ancora più importante: il determinante deve essere **coprimo** con il modulo $m$ (26) quindi deve avere $\gcd(\det(X), 26) = 1$.

# Processo di Decifratura

Per tornare indietro, bisogna invertire l'operazione. La matematica richiede prima di sottrarre il vettore di spostamento e poi moltiplicare per l'inversa della matrice.

La formula di decifratura è:

$$P = X^{-1} \cdot (\vec{C} - \vec{b}) \pmod m$$


# Considerazioni sul numero delle chiavi disponibili

Il termine $\underline{b} \in \mathbb{Z}_{26}^s$, questo significa che $\underline{b}$ è un vettore colonna di lunghezza $s$ (dove $s$ è la dimensione del blocco, es. digrammi o trigrammi). Ogni elemento del vettore può essere uno dei 26 numeri (da 0 a 25). Quindi ci sono $26^s$ possibili scelte per il vettore $\underline{b}$. Il termine $A \in M_s(\mathbb{Z}_{26}), \det(A) \in Inv(\mathbb{Z}_{26})$, questo significa che $A$ è una matrice quadrata $s \times s$ e, per poter decifrare il messaggio, il suo determinante deve essere invertibile modulo 26 (cioè coprimo con 26). Questa espressione $$(\ell(26)^s - 1)(\ell(26)^s - \ell(26))\dots(\ell(26)^s - \ell(26)^{s-1})$$ serve a contare quante matrici $A$ esistono. Quindi la formula finale è:
$$|K| = \underbrace{26^s}_{\text{Opzioni per } b} \cdot \underbrace{|GL(s, \mathbb{Z}_{26})|}_{\text{Opzioni per } A}$$


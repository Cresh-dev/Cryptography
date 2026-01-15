La sicurezza di ElGamal risiede nella difficoltà computazionale del **Problema del Logaritmo Discreto (DLP)** in campi finiti, cioè è facile calcolare l'esponenziale: $y = g^x \pmod p$ ma è estremamente difficile (computazionalmente impossibile) fare l'inverso: dato $y$, $g$ e $p$, trovare l'esponente $x$. 

# Generazione delle Chiavi

Questo è un crittosistema molto similare a [[Diffie-Hellman|D-H]]. Alice e Bob concordano pubblicamente su due numeri:

1. Un numero primo molto grande, $p$.  
2. Un generatore $g$ sul gruppo moltiplicativo $\mathbb{Z_p} \setminus \{0\}$.
3. Alice sceglie una chiave privata $e_1 \in \mathbb{Z}$ e invia la chiave pubblica $g^{e_1} \pmod p$ a Bob.
4. Bob sceglie una chiave privata $e_2 \in \mathbb{Z}$ e invia la chiave pubblica $g^{e_2} \pmod p$ a Alice.

# Cifratura

Prima di cifrare dobbiamo dividere il messaggio in blocchi tale che $m_i < p$. Ogni blocco viene cifrato con questa formula:

$$m_i \cdot {(g^{e_B})}^{e_A} \pmod{p}$$

# Decifratura

Ogni blocco viene decifrato con questa formula:

$$m_i \cdot {(g^{e_B})}^{e_A} \cdot {(g^{e_A})}^{-e_B} \pmod{p} \equiv m_i \pmod{p}$$

# Firma digitale

La **firma digitale di ElGamal** è uno schema crittografico che serve a **garantire autenticità, integrità e non ripudio** di un messaggio. È basata sul **problema del logaritmo discreto**, lo stesso su cui si fonda l’algoritmo di cifratura ElGamal. Per firmare un messaggio $m$ l'utente A sceglie un grande intero chiamato $k \in \mathbb{Z_{p-1}}$, con $gcd(k, p-1) = 1$. L'utente A calcola $S_1$ e $S_2$ che hanno le seguenti formule:

$$S_1 = g^{k} \pmod p$$
$$S_2 = k^{-1}(f(m)-S_1e_A) \pmod{p-1}$$

L'utente A invia a B non solo il messaggio cifrato $f(m)$ ma anche la firma digitale $(S_1,S_2)$. L'utente B per accettare la firma deve porre l' uguaglianza $V=W$ e verificare se è vera.

$$V = g^{f(m)} \pmod p$$
$$W = (g^{e_A})^{S_1} \cdot S_1^{S_2} \pmod{p}$$

# El-Gamal con Curve Ellittiche

**EC-ElGamal** è la versione di ElGamal che lavora non su $\mathbb{Z}_p​^*$, ma sul **gruppo dei punti di una curva ellittica** su un campo finito. La sicurezza non si basa più sul logaritmo discreto classico, ma sul **problema del logaritmo discreto su curve ellittiche (ECDLP)**, molto più difficile a parità di dimensioni. Tutti conoscono:

- la curva ellittica $E$
- un campo finito $\mathbb{F}_p$
- un punto generatore $G$ di ordine grande $n$

Per fare la cifratura utilizziamo:

$$P_{m_i} \oplus e_A(e_BG)$$

Nella formula utilizziamo
- $e_AG$ e $e_BG$ chiavi pubbliche di A e di B
- $e_A$ e $e_B$ chiavi private di A e di B

Per fare la decifratura utilizziamo:

$$P_{m_i} \oplus e_A(e_BG) \oplus -e_B(e_AG) = P_{m_i}$$

## Firma digitale con Curve Ellittiche

Si fissano i parametri pubblici del sistema:

- **$p$**: un numero primo.
- **$E_{a,b}$**: una curva ellittica definita sul campo $\mathbb{Z}_p$.
- **$G$**: un punto generatore della curva.
- **$n$**: l'ordine del gruppo generato da $G$, tale che $|E_{a,b}| = |\langle G \rangle| = n$.

Ogni utente (A e B) genera le proprie coppie di chiavi:

- **Chiave Privata ($e$):** scelta casualmente.
- **Chiave Pubblica:** calcolata come $eG$ (moltiplicazione scalare del punto $G$).

Nel caso specifico:

- Utente A: privata $e_A$, pubblica $e_A G$.
- Utente B: privata $e_B$, pubblica $e_B G$.

Per firmare un messaggio $m$, l'utente **A** esegue i seguenti passaggi:

1. **Scelta di $k$:** Sceglie un intero casuale $k$ tale che sia invertibile modulo $n$.
    - Condizione: $k \in Inv(\mathbb{Z}_n)$ ovvero $\gcd(k, n) = 1$.
2. Calcolo di $S_1$: Calcola il punto sulla curva:
    $$S_1 = kG = (x_{S1}, y_{S1})$$
3. Calcolo di $S_2$: Calcola lo scalare utilizzando l'hash del messaggio e la coordinata x di $S_1$:  $$S_2 = k^{-1} (h(m) + x_{S1} \cdot e_A) \pmod n$$

Dove $h: m \to \mathbb{Z}_n$ è una funzione di hash sicura.

**La firma generata è la coppia: $(S_1, S_2)$.** L'utente **B** riceve il messaggio $m$ e la firma $(S_1, S_2)$ e calcola due valori per verificare la validità:

1. Calcolo di $V$: $$V = S_2 S_1$$
2. Calcolo di $W$: $$W = h(m)G \oplus (x_{S1} e_A) G$$

La firma è accettata se e solo se **$V = W$**.
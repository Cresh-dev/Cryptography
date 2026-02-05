Il crittosistema D-H permette a due persone di generare insieme una chiave segreta attraverso un canale di comunicazione non sicuro (come internet), senza che nessuno che stia ascoltando possa capire quale sia quella chiave. Alice e Bob concordano pubblicamente su due numeri:

1. Un numero primo molto grande, $p$.  
2. Un generatore $g$ sul gruppo moltiplicativo $\mathbb{Z_p} \textbackslash \{0\}$.
3. Alice sceglie una chiave privata $K_1 \in \mathbb{Z}$ e invia la chiave pubblica $g^{K_1} \pmod p$ a Bob.
4. Bob sceglie una chiave privata $K_2 \in \mathbb{Z}$ e invia la chiave pubblica $g^{K_2} \pmod p$ a Alice.
5. Bob può computare ${(g^{K_1})}^{K_2} \pmod p$ e Alice può fare lo stesso ${(g^{K_2})}^{K_1} \pmod p$.
6. Entrambi ottengono la stessa chiave ${g^{K_1 \cdot K_2}} \pmod p$.


> [!NOTE] Perché è sicuro il crittosistema D-H
> La sicurezza di D-H risiede nella difficoltà computazionale del **Problema del Logaritmo Discreto (DLP)**. Dato un elemento $c \in G$ è computazionalmente impossibile per grandi $p$ trovare $K \in \mathbb{Z}$ tale che $c=g^{k}$

# D-H con Curve Ellittiche

**ECDH (Elliptic Curve Diffie–Hellman)** è il protocollo che permette a due parti di **stabilire una chiave segreta condivisa** su un canale insicuro usando le **curve ellittiche**.

È l’equivalente di Diffie–Hellman classico, ma:

- più **sicuro**
- con **chiavi più piccole**
- più **efficiente**

La sicurezza si basa sul **problema del logaritmo discreto su curve ellittiche (ECDLP)**.

Tutti conoscono:

- una curva ellittica $E$ su $\mathbb{F}_p$
- un punto generatore $G$ di grande ordine $n$

L'utente A ha come chiave privata $K_1$ e chiave pubblica $K_1G$
L'utente B ha come chiave privata $K_2$ e chiave pubblica $K_2G$

L'utente A computa $K_1(K_2G)$ e l'utente B fa lo stesso con $K_2(K_1G)$. Alla fine della computazione, entrambi gli utenti hanno la stessa chiave:

$$
K_1(K_2G) = K_2(K_1G)
$$


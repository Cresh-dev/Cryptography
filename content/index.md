---
title: Panoramica sulla Crittografia
---

La **crittografia** è la scienza che permette di rendere un messaggio incomprensibile a chiunque non sia autorizzato a leggerlo. È l'arte di proteggere le informazioni trasformandole in un formato illeggibile.

# I due tipi principali di crittografia

Esistono due modi principali per proteggere i dati, ognuno con uno scopo diverso. Innanzitutto iniziamo con il definire il crittosistema che è una quintupla di elementi $(P,C,K,E,D)$ con:
- $P$: plaintexts (testo in chiaro)
- $C$: cyphertexts (testo cifrato)
- $K$: insieme delle chiavi
- $E$: encryption
- $D$: decryption

## Crittografia Simmetrica (La stessa chiave)

È il metodo più antico e veloce. Mittente e destinatario usano la **stessa identica chiave** sia per chiudere che per aprire il messaggio. Possiamo analizzare questi crittosistemi:

- [[Affine cypher]]
- [[Affine Hill cypher]]

## Crittografia Asimmetrica (Chiave pubblica e privata)

Questo sistema risolve il problema dello scambio della chiave simmetrica. L'idea che sta alla base di ciò è la **_trapdoor function_** che è una funziona a senso unico con tre caratteristiche principali:
- Semplice da calcolare
- Difficile da invertire 
- Se è conosciuta una determinata informazione allora è semplice da invertire.

> [!NOTE] Esempio della _trapdoor function_ in RSA
> L'algoritmo RSA si basa su una **asimmetria computazionale**: mentre la cifratura del messaggio è un'operazione semplice, la decifrazione senza conoscere la chiave privata è un problema intrattabile. La sicurezza del sistema risiede nella difficoltà di fattorizzare numeri interi molto grandi: senza conoscere i fattori primi $p$ e $q$ che compongono il modulo $n = p \cdot q$, è computazionalmente infattibile calcolare la funzione $\phi$ di Eulero, parametro indispensabile per derivare la chiave privata.

In questa tipologia di crittografia si usano due chiavi diverse ma matematicamente collegate:

- **Chiave Pubblica:** La condividiamo con tutti. Chiunque può usarla per criptare un messaggio per noi (chiuderlo).
- **Chiave Privata:** La teniamo solo per noi. È l'unica che può decifrare (aprire) i messaggi criptati con la nostra chiave pubblica.

> [!NOTE] Curva ellittica (richiamo minimo)
> Una curva ellittica su un campo finito $\mathbb{F}_p$​ ha forma: $y^2 = x^3 + ax + b \pmod p$ con una legge di gruppo definita sui **punti della curva** + il punto all’infinito $\mathcal{O}$.

Possiamo analizzare questi crittosistemi:

- [[RSA]]
- [[Diffie-Hellman]]
- [[El-Gamal]]
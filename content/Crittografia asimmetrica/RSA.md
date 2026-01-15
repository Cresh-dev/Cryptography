La sicurezza di RSA si basa sulla teoria dei numeri, in particolare sulla difficoltà di scomporre numeri molto grandi nei loro fattori primi.

# Processo di Cifratura

Prima di cifrare il testo dobbiamo dividerlo in blocchi tramite questa regola: 

"Dobbiamo dividere la sequenza in blocchi lunghi $2N$ cifre, dove $N$ è il numero più grande possibile tale che il blocco risultante sia sempre minore di $n_B$". 

Una volta diviso il testo in blocchi si scelgono due numeri primi molto grandi, $p$ e $q$ e si calcola il loro prodotto: $n = p \cdot q$ (questo $n$ è parte della chiave pubblica ed è chiamato _modulo_). Insieme al modulo $n$ abbiamo un esponente pubblico $e$. Quindi la chiave pubblica è composta in questo modo:

$$(n, e)$$

La cifratura fatta dall'utente A usa la chiave pubblica dell'utente B ($n_{B}, e_{B}$) per calcolare il messaggio cifrato $C$:

$$C = M^{e_{B}} \pmod{n_{B}}$$

# Processo di Decifratura

Prima di effettuare la decifratura dobbiamo calcolare la chiave privata ($d_{B}$) dell'utente B. Per farlo dobbiamo eseguire questo calcolo:

$$d_{B} \cdot e_{B} \equiv 1 \pmod{\phi(n_{B})}$$

La decifratura fatta da B usa la sua chiave privata ($d_{B}$) per recuperare il messaggio originale $M$:

$$M = C^{d_{b}} \pmod{n_{B}}$$

# Perché RSA è sicuro

La sicurezza di RSA risiede nel problema della **fattorizzazione degli interi**. È facilissimo per un computer moltiplicare due numeri primi giganti ($p \cdot q$) per ottenere $n$, ma è estremamente difficile (computazionalmente intrattabile), dato solo $n$, risalire ai due numeri originali $p$ e $q$.

# Autenticazione della firma digitale

La **Firma Digitale** è l'applicazione "speculare" dell'RSA rispetto alla cifratura. Se nella cifratura l'obiettivo è la _segretezza_ (nascondere il messaggio), nella firma digitale l'obiettivo è l'**autenticità** (provare chi l'ha scritto) e l'**integrità** (provare che non è stato modificato). Quando l'utente A invia a B il messaggio cifrato insieme ad esso viene inviata anche la firma $F$ (che nel nostro caso corrisponde all'ultima parte del messaggio) cifrata con la seguente formula:

$$F^{d_{A}} \pmod{n_{A}}$$

L'utente B decifra il messaggio (nella maniera classica vista sopra) e anche la firma tramite questa operazione:

$$(F^{d_{A}})^{e_{A}} \pmod{n_{A}} \equiv F \pmod{n_{A}}$$

Il messaggio è autenticato se l'ultima parte del messaggio decifrato coincide con la decifratura della firma $F$ che l'utente B ha svolto.
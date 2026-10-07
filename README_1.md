# Sito Campolux (statico)

Sito di una pagina, senza framework e senza build: solo HTML + CSS.
Nessun cookie, nessun tracciamento, nessun servizio esterno → non serve il banner cookie.

## Struttura

```
index.html     la pagina
style.css      lo stile
favicon.svg    icona
img/           (da creare) qui vanno le foto
```

## Da completare prima di pubblicare

Nel sito ho usato solo dati trovati in rete (storia dal 1961, indirizzo, telefono 010 921028). Mancano:

- [ ] **Orari di apertura** (in `index.html`, sezione "Dove siamo", c'è un commento TODO)
- [ ] **Email di contatto** (stesso punto)
- [ ] **P.IVA / C.F. / REA** nel footer (obbligatori per i siti di attività commerciali in Italia)
- [ ] **Foto**: negozio, lampadari di produzione, ristrutturazioni, chiese. Il codice della galleria è già pronto, commentato in `index.html`
- [ ] **Controllo dei testi** con i titolari: ho riscritto con parole mie quello che era sul vecchio sito, vanno verificati
- [ ] Eventuali **marchi trattati** e un link a Facebook/Instagram, se esistono

## Provare il sito in locale

Basta aprire `index.html` con un doppio clic. In alternativa, con un mini server:

```
python3 -m http.server 8000
```
poi vai su http://localhost:8000

## Pubblicazione (deploy)

Prima cosa da chiarire con i titolari: **chi possiede il dominio `campolux.it`** (quale registrar: Aruba, Register, GoDaddy, Register.it...) e **dove puntano ora i DNS**. Il vecchio gestore potrebbe avere ancora le credenziali: serve il codice di accesso al pannello, oppure farsi intestare/delegare il dominio.

### Opzione A – Cloudflare Pages (consigliata, gratuita)

1. Crea un account su https://dash.cloudflare.com
2. *Workers & Pages* → *Create* → *Pages* → **Upload assets**
3. Trascina la cartella del sito (quella con `index.html`) e premi *Deploy*
4. Ottieni subito un indirizzo `nome.pages.dev` per fare le prove
5. *Custom domains* → aggiungi `campolux.it` e `www.campolux.it` e segui le istruzioni DNS
6. Il certificato HTTPS è automatico

### Opzione B – Netlify (gratuita, ancora più semplice)

1. Vai su https://app.netlify.com/drop
2. Trascina la cartella del sito nella pagina: è online in pochi secondi
3. *Domain management* → *Add a domain* → `campolux.it`
4. HTTPS automatico

### Opzione C – GitHub Pages (gratuita, utile per tenere lo storico delle modifiche)

1. Crea un repository su GitHub e carica i file
2. *Settings* → *Pages* → Source: branch `main`, cartella `/ (root)`
3. In *Custom domain* inserisci `campolux.it`

### Opzione D – Hosting tradizionale (se il dominio ha già un hosting con FTP)

Carica `index.html`, `style.css`, `favicon.svg` (e `img/`) nella cartella `public_html` (o `www`) via FTP, ad esempio con FileZilla. Verifica che il certificato HTTPS sia attivo dal pannello.

### Collegare il dominio (DNS)

Dal pannello del registrar, in base alla scelta:

| Servizio | Cosa configurare |
|---|---|
| Cloudflare Pages | Più semplice spostare i nameserver su Cloudflare (te li indica lui), oppure `CNAME www` → `nome.pages.dev` |
| Netlify | `A @` → indirizzo indicato da Netlify, `CNAME www` → `nome.netlify.app` |
| GitHub Pages | 4 record `A @` verso gli IP indicati dalla documentazione GitHub, `CNAME www` → `utente.github.io` |

I valori esatti cambiano nel tempo: usa quelli che mostra il servizio nella schermata del dominio. La propagazione DNS può richiedere da pochi minuti a 24 ore.

### Se il vecchio sito è ancora online

Prima di cambiare i DNS controlla cosa risponde oggi `campolux.it` e, se ci sono caselle email sul dominio (`@campolux.it`), **non toccare i record MX**: spostare i DNS senza copiarli farebbe smettere di funzionare la posta.

## Modificare il sito in futuro

- Testi: apri `index.html` con un editor (VS Code, Blocco Note) e cambia il testo tra i tag
- Colori e font: variabili all'inizio di `style.css` (`:root`)
- Nuove foto: mettile in `img/`, poi attiva la galleria in `index.html`
- Dopo ogni modifica, ricarica la cartella su Cloudflare/Netlify (o fai il commit su GitHub)

## Font

Per evitare caricamenti da Google (privacy/GDPR) il sito usa solo font di sistema. Se vorrai un font personalizzato, scaricalo e servilo dalla stessa cartella con `@font-face`.

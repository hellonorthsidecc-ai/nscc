# NSCC — Sito Northside Cycling Club

Memoria di progetto. Leggere all'inizio di ogni sessione. (L'utente parla italiano.)

## Cos'è
Sito **statico** (HTML/CSS/JS puro, niente framework, niente build step) del **Northside Cycling Club** — club di ciclismo su strada della Valtellina (nord Italia). Est. 2026. Tono: "No fees, no hierarchy".

- **Pubblicato su:** GitHub Pages → dominio **northsidecc.com** (file `CNAME`)
- **Repo:** https://github.com/hellonorthsidecc-ai/nscc — branch **main** (il push su main aggiorna il sito live)
- **Pagina principale:** `index.html` (è un singolo file grande con CSS e JS inline). Altre pagine: join, merch, tee, socks, kit, links, privacy, cookies, ecc.

## Flusso di lavoro (IMPORTANTE)
1. **Modifico i file**
2. L'utente vede le modifiche in locale su **http://localhost:8000** (avviare con `python3 -m http.server 8000` in background dalla cartella del sito) e ricarica con Cmd+R
3. Solo quando l'utente è soddisfatto → **push** (lo faccio io)
4. Il push richiede `dangerouslyDisableSandbox: true` perché serve l'accesso al portachiavi macOS

> L'utente NON usa git da riga di comando. Pubblico io: commit + `git push origin main`. Le credenziali (token GitHub fine-grained, solo questo repo, Contents R/W) sono salvate nel portachiavi osxkeychain.

> Online GitHub Pages ci mette 1-2 minuti ad aggiornarsi. Localhost è istantaneo.

## Strumenti ambiente
- **ImageMagick non installato**; usare **Pillow** (Python, installato) per le immagini. `poppler` installato per i PDF.
- **Impeccable** (skill design di pbakaus) installata globalmente in `~/.claude/skills/impeccable` (v3.5.0). Usarla per audit/critique/polish del sito e togliere il "look AI". Il comando `/plugin` NON è disponibile in questo ambiente, perciò è stata installata copiando la skill a mano. Comandi tipo: craft, shape, audit, critique, polish, typeset, layout, colorize, quieter, bolder.
- Verde brand: **`#4B5F49`** (var `--green-1`, "Forest Night"). Sfondo off-white: **`#F0EDE8`** (`--bg`).

## Decisioni di design prese
- **Font titoli: Barlow Condensed** (confermato giu 2026). Architettura via variabile CSS `--font-display` (cambiare lì per swap globale).
  - Alternative valutate e scartate per ora (documentate in commento nell'`<head>`): **Syne** (wght 800), **Space Grotesk** (700), **Russo One** (400). Variante "schiacciata" provata: `transform: scaleX(1.14) scaleY(0.80)` sui titoli display.
- **Logo:** versione completa col nome esteso ("northside cycling club"). Asset: `img/logo-full.png` (verde su trasparente, generato da `img/7 box wg2.png`) usato in header e footer. Solo simbolo NSCC (`img/logo.png`) nello sfondo della sez"MORE THAN".
- **Anteprima link social (Open Graph):** `img/og.png` (1200×630) = logo su verde brand. Meta con `?v=2` per cache-bust. Nota: WhatsApp/Telegram cachano le anteprime; per forzare il refresh usare un parametro nuovo nell'URL (es. `northsidecc.com/?x`) o @WebpageBot (solo Telegram).
- **Sfondo scorrevole:** la grana (`body::before`) e le macchie (`.bg-blobs`) sono `position:absolute` (non più `fixed`) così scorrono con la pagina. Il colore di sfondo è su `html`. (L'utente non voleva lo sfondo "fermo" mentre il testo scorre.)

## Feedback del grafico (amico "Enni"/Enri) — punti da affrontare
Da un PDF ("Feedback Sito"). Stato:
- [x] Logo completo col nome esteso
- [x] Font (valutato; tenuto Barlow)
- [ ] **Testi "troppo AI style"** da riscrivere più asciutti: hero "Born in Valtellina" e sezione "More than"
- [~] **Sezione "Behind" a tutto schermo** con testo in `mix-blend-mode: difference` — IN CORSO (foto `img/matenri.jpeg` = Enri e Matti, i fondatori). Da rifinire leggibilità/inquadratura.
- [ ] Sezione "More than": valutare se ridurre a parole singole (FAMILY/COMMUNITY/CYCLING); il payoff forse non serve.

## Note di stile comunicazione
Rispondere in **italiano**, tono pratico e chiaro. L'utente non è tecnico: spiegare i passaggi senza dare per scontato git/CSS. Procedere una modifica alla volta e far verificare su localhost prima di pubblicare.

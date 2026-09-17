# Facet — sito vetrina per un brand di gioielleria fittizio (Milano)

Progetto realizzato per mostrare le mie competenze di sviluppo front-end: "Facet" è un brand di gioielleria immaginario con sede a Milano, non un cliente reale.

Live at https://k0m1d3v.github.io/Facet-JeweleryWebsite/sites/facet/

## Struttura

```
Luxury/
├── assets/
│   └── video/          # asset video condivisi o specifici dei siti
│       └── diamond_hero.mp4
├── shared/
│   └── tokens.css       # @import font Google, variabili colore (:root), reset di base
├── sites/
│   └── facet/            # una cartella per cliente/demo
│       └── index.html
├── package.json
└── README.md
```

- **`shared/tokens.css`** contiene solo ciò che è davvero comune a tutte le demo: caricamento font (Fraunces/Work Sans), variabili colore (`--ink`, `--ivory`, `--platinum`, `--ice`, ecc.) e un reset minimo (`box-sizing`, margini body, font-family di base su `h1`/`h2`). Ogni pagina lo importa con:
  ```html
  <link rel="stylesheet" href="../../shared/tokens.css">
  ```
- **`sites/<nome-cliente>/`** contiene l'HTML e lo stile/script specifici di quella demo (layout, componenti, animazioni). Lo scroll-jacking del video hero, ad esempio, resta interamente dentro `sites/facet/index.html` — non è stato toccato.
- **`assets/video/`** raccoglie i video usati dalle demo, referenziati con path relativi (es. `../../assets/video/diamond_hero.mp4`).

## Avviare il dev server in locale

Richiede solo Node.js/npx (nessuna dipendenza installata nel repo):

```bash
npm run dev
```

Questo lancia `serve` sulla porta 3000 (via `npx`, senza bisogno di `npm install`). Apri poi, ad esempio:

```
http://localhost:3000/sites/facet/
```

In alternativa, qualunque static server va bene (es. `python -m http.server` dentro la cartella del progetto, o l'estensione "Live Server" di VS Code).

## Aggiungere un nuovo progetto/cliente

1. Crea una cartella sotto `sites/<nome-cliente>/` (es. `sites/hotel-aurora/`) con il suo `index.html`.
2. Nel `<head>`, importa i token condivisi:
   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   <link rel="stylesheet" href="../../shared/tokens.css">
   ```
3. Se la palette del cliente differisce da quella base, sovrascrivi le variabili in un `<style>` locale dopo l'import di `tokens.css` (es. ridefinisci `--ink`/`--ivory` per quel progetto), invece di duplicare tutto il blocco `:root`.
4. Metti eventuali asset (video, immagini) in `assets/` (sottocartella dedicata se voluminosi o specifici del cliente, es. `assets/video/hotel-aurora/`).
5. Se una nuova regola CSS/JS risulta utile a più di una demo, valuta di spostarla in `shared/` — altrimenti tienila locale al progetto.

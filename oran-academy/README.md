# O-RAN Academy — Platform v1.0

Piattaforma didattica modulare O-RAN. HTML statico, zero dipendenze backend.

## Struttura file

```
oran-academy/
├── index.html        ← Dashboard principale
├── p1.html           ← P1 Foundations & Architecture
├── p2.html           ← P2 Near-RT RIC & E2
├── p3.html           ← P3 Non-RT RIC & A1
├── p4.html           ← P4 Open Fronthaul
├── p5.html           ← P5 Cloud, OAM & Security
├── p6.html           ← P6 HW & Stack Reference
├── security.html     ← Tema trasversale Security
├── automation.html   ← Tema trasversale Automation
├── percorso.html     ← Percorso personalizzato MD/CTO
├── css/
│   └── academy.css   ← Design system condiviso
└── README.md
```

## Deploy su GitHub Pages

### Passo 1 — Crea repository
1. Vai su [github.com](https://github.com) e accedi
2. Clicca **New repository**
3. Nome: `oran-academy`
4. Visibilità: **Public** (richiesto per GitHub Pages gratuito)
5. Clicca **Create repository**

### Passo 2 — Carica i file
**Opzione A — Upload diretto (più semplice):**
1. Nel repository appena creato clicca **Add file → Upload files**
2. Trascina tutta la cartella `oran-academy/`
3. Scrivi un messaggio di commit: `Initial deploy O-RAN Academy v1.0`
4. Clicca **Commit changes**

**Opzione B — Git da terminale:**
```bash
cd oran-academy/
git init
git add .
git commit -m "Initial deploy O-RAN Academy v1.0"
git branch -M main
git remote add origin https://github.com/tuonome/oran-academy.git
git push -u origin main
```

### Passo 3 — Attiva GitHub Pages
1. Nel repository vai su **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** → cartella **/ (root)**
4. Clicca **Save**
5. Attendi 2-3 minuti

### Passo 4 — Accedi alla piattaforma
URL: `https://tuonome.github.io/oran-academy`

La dashboard è `index.html` — GitHub Pages la serve automaticamente come homepage.

## Aggiornare i contenuti

Per aggiornare un file dopo il deploy:
1. Modifica il file HTML localmente
2. Su GitHub: **Add file → Upload files** → carica solo il file modificato
3. Commit — le modifiche sono live in 1-2 minuti

## Note tecniche

- Tutto il CSS è in `css/academy.css` — modificare lì per cambiare stile globale
- I profili utente vengono salvati in `localStorage` del browser
- Font caricati da Google Fonts (richiede connessione internet)
- Icone Tabler Icons via CDN jsdelivr
- Zero JavaScript framework — vanilla JS puro
- Compatible con tutti i browser moderni (Chrome, Firefox, Safari, Edge)

## Versione e stato

- Versione: 1.0
- Data: Maggio 2026
- Lingua: Italiano
- Stato: Fase 0 — validazione
- Multilingua: pianificata dopo validazione contenuti

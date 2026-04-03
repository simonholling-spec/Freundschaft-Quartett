# Freundschaft. Kartengenerator

Sammelkarten-Generator für die Freundschaft. Personalfeier am 27.04.2026.

## Setup

```bash
# 1. Repository klonen / Dateien in einen Ordner legen

# 2. Dependencies installieren
npm install

# 3. Lokal starten (Entwicklung)
npm run dev

# 4. Für GitHub Pages bauen
npm run build
```

## Auf GitHub Pages deployen

### Option A: Automatisch mit gh-pages

```bash
npm run deploy
```

Das baut die App und pusht den `dist`-Ordner automatisch auf den `gh-pages`-Branch.

### Option B: Manuell

1. Erstelle ein GitHub-Repository (z.B. `freundschaft-cards`)
2. Push den Code:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/DEIN-USERNAME/freundschaft-cards.git
   git push -u origin main
   ```
3. Baue die App: `npm run build`
4. Deploye den `dist`-Ordner:
   ```bash
   npx gh-pages -d dist
   ```
5. Gehe in den GitHub Repo Settings → Pages → Source: "Deploy from a branch" → Branch: `gh-pages` → Save
6. Die Seite ist dann erreichbar unter: `https://DEIN-USERNAME.github.io/freundschaft-cards/`

### Option C: GitHub Actions (automatisch bei jedem Push)

Erstelle `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist
      - uses: actions/deploy-pages@v4
```

Dann unter Settings → Pages → Source: "GitHub Actions" auswählen.

## Wichtig

- Der `base`-Pfad in `vite.config.js` muss zum Repository-Namen passen
- Falls dein Repo anders heißt, ändere `base: '/freundschaft-cards/'` entsprechend
- Das Logo liegt als `public/logo.png` — wird automatisch mit deployed

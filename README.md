# CUBE

## Installations

### Création d'un projet vite

```bash

npm create vite@latest

```

### Aframe

```bash

npm install aframe

```

### Première page

```html
<!-- index.html -->
<a-scene>
  <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
  <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
  <a-cylinder
    position="1 0.75 -3"
    radius="0.5"
    height="1.5"
    color="#FFC65D"
  ></a-cylinder>
  <a-plane
    position="0 0 -4"
    rotation="-90 0 0"
    width="4"
    height="4"
    color="#7BC8A4"
  ></a-plane>
  <a-sky color="#ECECEC"></a-sky>
</a-scene>
```

```js
// File main.js
import AFRAME from "aframe";
```

### GitHub Pages

#### Initialisation git

```bash
git init
git remote add origin https://github.com/<nom-repo>.git
git branch -M main
git push -u origin main
```

#### Update Vite Config

Créer un fichier `vite.config.js` à la racine du projet.

```js
import { defineConfig } from "vite";

export default defineConfig({
  base: "/<nom-repo>/",
});
```

#### Create a Workflow

Créer un nouveau fichier dans votre repository à
`.github/workflows/deploy.yml`.

Copie le code suivant :

```bash

# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ['main']

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets the GITHUB_TOKEN permissions to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
      - name: Set up Node
        uses: actions/setup-node@v6
        with:
          node-version: lts/*
          cache: 'npm'
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
        with:
          # Upload dist folder
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

#### Enable GitHub Pages

Dans `settings → pages → source (Build and deployment)`, sélectionnez **github actions**.

`Push` votre projet sur github.

## Links des projets

https://denis-springinsfeld.github.io/S6_25/

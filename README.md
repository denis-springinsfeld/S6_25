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
import AFRAME from "aframe";
```

### GitHub Pages

```bash
git init
git remote add origin https://github.com/denis-springinsfeld/S6_25.git
git branch -M main
git push -u origin main
```

Update Vite Config

Set the correct base in vite.config.js.

If you are deploying to https://<USERNAME>.github.io/, or to a custom domain through GitHub Pages (eg. www.example.com), set base to '/'. Alternatively, you can remove base from the configuration, as it defaults to '/'.

If you are deploying to https://<USERNAME>.github.io/<REPO>/ (eg. your repository is at https://github.com/<USERNAME>/<REPO>), then set base to '/<REPO>/'.

Enable GitHub Pages

In your repository, go to Settings → Pages. Under Build and deployment, open the Source dropdown, and select GitHub Actions.

GitHub will now deploy your site using a GitHub Actions workflow, which is necessary since Vite requires a build step for deployment.

Create a Workflow

Create a new file in your repository at .github/workflows/deploy.yml. You can also click on “create your own” from the previous step, which will generate a starter workflow file for you.

Here’s a sample workflow that installs dependencies with npm, builds the site, and deploys it whenever you push changes to the main branch:

`.github/workflows/deploy.yml`

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

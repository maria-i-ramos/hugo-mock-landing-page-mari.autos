# hugo-mock-landing-page

# hugo-mock-landing-page-autodeployed

This repository hosts a Hugo static site that is automatically built and deployed to GitHub Pages using GitHub Actions.

## 📦 Overview

This project demonstrates a fully automated CI/CD workflow to:

- Build a Hugo site using a custom theme
- Deploy the generated static files to the `gh-pages` branch
- Host the site using GitHub Pages

## ⚙️ GitHub Actions Workflow

We use a `.github/workflows/gh-pages-deployment.yaml` file to define our deployment process. The workflow is triggered on every push to the `main` branch and performs the following:

1. Checks out the repository
2. Initializes and updates Git submodules (for the Hugo theme)
3. Sets up Hugo
4. Builds the site into the `public/` directory
5. Deploys the output to the `gh-pages` branch using [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages)

### ✅ Key Steps from the Workflow

```yaml
- name: Initialize and update submodules
  run: |
    git submodule sync
    git submodule update --init --recursive

- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v3
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
    publish_dir: ./public
    publish_branch: gh-pages

## 🧠 Troubleshooting & Fixes

Initially, the deployment failed due to a corrupted Git submodule reference to hugo-bootstrap-theme. Here's how we fixed it:

1. Removed the broken submodule:
git submodule deinit -f themes/hugo-bootstrap-theme
rm -rf .git/modules/themes/hugo-bootstrap-theme
git rm -f themes/hugo-bootstrap-theme
2. Re-added the submodule with the correct URL:
git submodule add https://github.com/filipecarneiro/hugo-bootstrap-theme themes/hugo-bootstrap-theme
Committed all changes and verified the .gitmodules file was restored.
💬 If you get stuck, don’t hesitate to ask ChatGPT or Claude for help! Both were instrumental in debugging this process.

## 🌐 Live Site

Once deployed, the site is live at:

https://maria-i-ramos.github.io/hugo-mock-landing-page-autodeployed/

(Replace with the actual deployed URL if it’s customized.)

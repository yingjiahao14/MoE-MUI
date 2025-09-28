# MoE Mechanisms via MUI — One‑Page GitHub Pages Site

A clean, OpenAI‑style single page (Jekyll) to introduce your MoE paper.

## Quick Start

1. **Create a new GitHub repository** (e.g., `username.github.io` for a user site or any repo for a project site).
2. Upload all files in this zip to the repo root.
3. In **Settings → Pages**, select the `main` branch and `/ (root)` as the Pages source.
4. Wait 1–2 minutes and open the URL shown under Pages.

### If this is a *project* site
Set `baseurl: /your-repo-name` in `_config.yml`.

### Replace links
- In `index.md`, update the "Paper (PDF)" and "Code" links and the author list.
- Optionally update `favicon.svg` in `assets/`.

## Local Preview (optional)
```bash
gem install bundler
bundle install
bundle exec jekyll serve
```
Open http://localhost:4000

## License
MIT

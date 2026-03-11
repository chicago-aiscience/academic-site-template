# Academic Site Template — Jupyter Book Website

A template for building a personal academic website using [MyST Markdown](https://mystmd.org/) and [Jupyter Book](https://jupyterbook.org/), deployed automatically to GitHub Pages.

## Quick Start

### 1. Fork this repository

Click **Fork** at the top of this page to create your own copy under your GitHub account.

### 2. Rename your fork

Go to **Settings → General → Repository name** and rename the repo to `yourusername.github.io`. This makes your site available at `https://yourusername.github.io`.

### 3. Enable GitHub Pages

Go to **Settings → Pages** under **Build and deployment** and set **Source** to **GitHub Actions**. Every push to `main` will automatically build and deploy your site.

> If you enable Pages after your first push, the initial workflow run will fail. Just re-run the failed job from the **Actions** tab once Pages is enabled.

### 4. Customize your content

All site content lives in the `docs/` directory. Edit these files with your own information:

| File | Purpose |
|------|---------|
| `docs/myst.yml` | Site title, description, keywords, GitHub URL, table of contents |
| `docs/index.md` | Homepage — introduction and navigation cards |
| `docs/cv.md` | Education, positions, awards, teaching, service |
| `docs/publications.md` | Journal articles, proceedings, preprints, theses |
| `docs/outreach.md` | Talks, seminars, workshops, media |

#### Update `docs/myst.yml`

```yaml
version: 1
project:
  title: Your Name
  description: Academic website of Your Name
  keywords: [your, research, keywords]
  authors: [Your Name]
  github: https://github.com/yourusername/yourusername.github.io
  toc:
    - file: index.md
    - file: cv.md
    - file: publications.md
    - file: outreach.md

site:
  template: book-theme
  options:
    style: styles/custom.css
```

#### Add a profile image

Drop a photo into `docs/images/` and reference it in `docs/index.md`.

#### Custom styles

Edit `docs/styles/custom.css` to adjust colors, fonts, or layout.

---

## Project Structure

```
.
├── docs/                    # Source content directory
│   ├── index.md             # Homepage
│   ├── cv.md                # Curriculum Vitae
│   ├── publications.md      # Publications list
│   ├── outreach.md          # Talks & outreach
│   ├── myst.yml             # MyST site configuration
│   ├── images/              # Image assets
│   └── styles/              # Custom CSS
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Actions deployment
├── pyproject.toml           # Python dependencies
├── Makefile                 # Development commands
└── README.md
```

---

## Local Development

### Prerequisites

- **Python 3.11+**
- **uv** (optional, recommended) — [installation](https://github.com/astral-sh/uv#installation)
- **Node.js 18.x+** — used by GitHub Actions for deployment

### Install dependencies

```bash
# With uv (recommended)
uv sync

# Or with pip
pip install "jupyter-book>=2.1.0" "nbconvert>=7.17.0"
```

### Build and serve locally

```bash
make serve    # Build and serve at http://localhost:3000
```

Or manually:

```bash
cd docs
jupyter book start
```

> **Note:** Do not open `_build/html/index.html` directly in a browser. MyST static output loads assets via absolute paths and requires a web server. `make serve` starts one automatically.

### Other Makefile commands

```bash
make install   # Install dependencies only
make build     # Build static HTML (output in docs/_build/html/)
make clean     # Remove build artifacts
make rebuild   # Clean then build
make check     # Verify environment setup
```

---

## GitHub Pages Deployment

Deployment is fully automated via `.github/workflows/deploy.yml`. Every push to `main` builds the site and publishes it to GitHub Pages — no extra configuration needed beyond enabling Pages in your repo settings (see Step 3 above).

---

## Custom Domain -- DRAFT, not tested

You can serve your site from a personal domain (e.g., `yourname.com`) instead of `yourusername.github.io`.

### 1. Configure GitHub Pages

Go to **Settings → Pages → Custom domain**, enter your domain, and save. GitHub will verify it and automatically enable HTTPS via Let's Encrypt. Check **Enforce HTTPS** once verification completes.

### 2. Add a CNAME file to your build

To prevent GitHub from losing your custom domain setting on each deploy, add a step to `deploy.yml` that writes a `CNAME` file into the build output:

```yaml
- name: Add custom domain
  run: echo 'yourdomain.com' > ./docs/_build/html/CNAME
```

Place this step between **Build HTML Assets** and **Upload artifact**.

### 3. Update your DNS

At your domain registrar, add the following records:

| Type | Host | Value |
|------|------|-------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `yourusername.github.io` |

### Recommended DNS providers

For a personal academic site, any standard domain registrar works — DNS configuration is a one-time manual step. Good options:

| Provider | Notes |
|----------|-------|
| [**Namecheap**](https://namecheap.com) | Most popular in the academic/developer community. Free WHOIS privacy, clean DNS editor, ~$10–12/year for `.com`. |
| [**Porkbun**](https://porkbun.com) | Lowest prices on most TLDs (`.com`, `.io`, `.me`). Free WHOIS privacy, simple interface. |
| [**Hover**](https://hover.com) | No upsells, privacy included, very clean UI. Good if you want a hassle-free experience. |
| [**Gandi**](https://gandi.net) | European registrar with strong privacy defaults, includes email forwarding. |

---

## Resources

- [Jupyter Book](https://jupyterbook.org/)
- [MyST Markdown Guide](https://mystmd.org/guide)
- [GitHub Pages custom domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

# Academic Site Template — Jupyter Book Website

A template for building a personal academic website using [MyST Markdown](https://mystmd.org/) and [Jupyter Book](https://jupyterbook.org/), deployed automatically to GitHub Pages.

## Quick Start

### 1. Fork this repository

Click **Fork** at the top of this page to create your own copy under your GitHub account.

### 2. Rename your fork (optional but recommended)

If you want a user/org site at `yourusername.github.io`, rename the repo to `yourusername.github.io` under **Settings → General → Repository name**.

If you want a project site at `yourusername.github.io/academic-site`, keep any name you like and update `BASE_URL` in `.github/workflows/deploy.yml`:

```yaml
BASE_URL: '/your-repo-name'
```

### 3. Enable GitHub Pages

Go to **Settings → Pages** and set **Source** to **GitHub Actions**. Pushes to `main` will trigger a build and deploy automatically.

### 4. Customize your content

All site content lives in the `docs/` directory. Edit these files with your own information:

| File | Purpose |
|------|---------|
| `docs/myst.yml` | Site title, description, keywords, GitHub URL |
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
  github: https://github.com/yourusername/your-repo-name
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
make serve    # Build and serve at http://localhost:8000
```

Or manually:

```bash
cd docs
jupyter book start
```

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

## Resources

- [Jupyter Book](https://jupyterbook.org/)
- [MyST Markdown Guide](https://mystmd.org/guide)
- [GitHub Pages](https://docs.github.com/en/pages)

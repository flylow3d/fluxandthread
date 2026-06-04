# Flux & Thread

Source for the **Flux & Thread** stained glass studio website — classes, patterns, and shop.
Static HTML; can be hosted on GitHub Pages (or any static host).

## Local preview

Open `index.html` directly in a browser. No build step.

## Image generation (optional)

Some figures can be generated with Google's Gemini image API via `tools/gen_figure.py`:

```powershell
python -m venv tools\.venv
.\tools\.venv\Scripts\Activate.ps1
pip install -r tools\requirements.txt
copy .env.example .env
# then paste your Gemini API key into .env
```

See `tools/README.md` for usage. Prefer real studio photos where possible.

## Roadmap

Landing page is live as a mockup. Next: real photos & copy, class signup, pattern downloads,
shop + payments. See `CLAUDE.md` for the full plan.

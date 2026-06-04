# Flux & Thread — Session Log

### Session 1 (2026-06-04)
- Kicked off the project for Sarah's stained glass studio website.
- Scaffolded from the sibling `MrGreenlee` static-site project: copied the Gemini figure
  tool (`tools/`), `.env.example`, and the whitelist `.gitignore` / `/log-session` patterns.
- Attempted to pull Instagram content from [@fluxandthread](https://www.instagram.com/fluxandthread/)
  — blocked by Instagram's login wall; only the handle was retrievable. Real photos/captions
  to come from Sarah.
- Chose the brand name **Flux & Thread** and a stained-glass visual language: warm light
  background, jewel-tone accents (teal/amber/ruby/cobalt/plum), near-black "lead came" lines,
  Cormorant Garamond + Lora type.
- Built a single-page landing mockup (`index.html` + `styles.css`): sticky nav, hero, "what we
  offer", upcoming-classes cards, patterns/shop teaser, about Sarah, newsletter signup band,
  footer. Image slots have graceful text fallbacks until real photos are added.
- Wrote `CLAUDE.md` capturing the full vision (classes, class material, patterns, CRM, shop,
  payments), status, image slots, and decisions-for-later (interactive stack, domain/hosting).

### Session 2 (2026-06-04)
- Sarah provided 4 real images: `logo.png`, `gnome.png`, `inprocess-diamonds.png`, and
  `flyer.jpg` (the workshop flyer she's sending out).
- Corrected the brand from the flyer/logo: it's **Flux + THREAD** (plus sign, not ampersand),
  tagline **"Handmade with love."** Re-themed the whole site from my guessed jewel-tone palette
  to her real brand: lavender + charcoal on ivory.
- Cropped the logo's black circle out of its blurry background into `logo-badge.png` (black-pixel
  density scan per row/column), used in header/about/footer with a CSS circular clip.
- Rebuilt `index.html` around real flyer content: featured "first workshop" block with the real
  curriculum (intro / cutting & grinding / foiling & soldering / finishing) and perks (no
  experience, all materials, 4 spots, take home a piece). Removed the fabricated dates/prices —
  the flyer is gathering interest, so the section asks weekday-afternoon vs weekend preference and
  drives to the email signup. Added a studio gallery (gnome, diamonds, flyer) and used the gnome
  as the hero image.
- Updated `CLAUDE.md` (brand, status, real workshop facts, images-in-use table).

### Session 3 (2026-06-04)
- Mobile-tuned the layout and verified at a true 390px CSS width with headless Edge: fixed a
  horizontal-overflow bug (decorative hero offset panel) that was clipping the hero title, made
  the header non-sticky on phones, centered hero/about, single-column perks, full-width signup,
  and made the gallery flyer a tappable link cropped from the top so its headline shows.
- Published: `git init`, committed, created public repo **flylow3d/fluxandthread**, pushed, and
  enabled GitHub Pages (main/root). Verified live: page + all images + CSS return 200 at
  **https://flylow3d.github.io/fluxandthread/**.
- To deploy future edits: `git add` + `git commit` + `git push` → Pages rebuilds in ~30–60s.

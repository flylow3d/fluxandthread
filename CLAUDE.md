# Flux & Thread — Project Context

## What We're Building

A website for **Flux + Thread**, Sarah's stained glass studio. It manages the studio's
public presence and, over time, its operations. Today the site is a **single-page landing
mockup** (`index.html` + `styles.css`); the roadmap below grows it into a real business site.

**Brand (confirmed from Sarah's logo + flyer):** the name is **Flux + Thread** (a PLUS sign,
not an ampersand — match this everywhere). Tagline: **"Handmade with love."** The name nods to
**flux**, the soldering agent in stained glass work. Visual identity: lavender (flyer headline)
+ charcoal/black (logo) on warm ivory. Instagram: [@fluxandthread](https://www.instagram.com/fluxandthread/).

## Vision / Scope

In rough priority order — this is what the site should eventually do:

1. **Classes** — list upcoming stained glass classes; let students sign up / reserve seats.
2. **Class material** — teaching handouts, quick-start guides, books, supply lists for students.
3. **Templates / patterns** — browse and (later) download original stained glass patterns.
4. **Customer relations (CRM)** — capture leads, manage students & inquiries, email list.
5. **Shop** — sell patterns (digital download), finished pieces, commissions, and supplies/kits.
6. **Payments** — take payment online (class deposits + shop checkout).

The current mockup stubs sections for all of these so the shape is visible; only the landing
content is real so far.

## Status

**LIVE** at https://flylow3d.github.io/fluxandthread/ — repo `flylow3d/fluxandthread` (public),
GitHub Pages from `main` / root. To update: edit locally, `git add` + `git commit` + `git push`;
Pages rebuilds in ~30–60s. Mobile-verified at 390px (headless Edge).

**Landing page rebuilt with real content** (2026-06-04). Single static page: sticky nav with
the real logo, hero (gnome suncatcher photo), "what we offer", **featured first workshop** (real
flyer copy — curriculum + perks + "dates being planned, weekday vs weekend?" interest CTA),
studio gallery, shop/patterns teaser, about, email signup band, footer. Palette is now Sarah's
real brand: lavender + charcoal on ivory. All four images she provided are wired in.

**Real workshop facts (from the flyer):** beginner copper-foil; curriculum = intro / cutting &
grinding / foiling & soldering / finishing; perks = no experience needed, all materials provided,
**4 spots**, take home a finished piece. **Dates are NOT set yet** — the flyer (and the site) is
gathering interest + asking weekday-afternoon vs weekend preference. Do not invent dates/prices.

**Open items / next steps:**
- Get real workshop dates + price from Sarah once decided; replace the "dates being planned" note
  with a real schedule and a Reserve flow.
- **Email signup: built, awaiting activation.** Real Web3Forms form is live (name + email +
  timing-preference pills) but needs a free access key pasted into the `access_key` hidden field
  in `index.html`. Get key at web3forms.com (emailed instantly). Until then it shows a graceful
  "goes live shortly" message. After pasting: commit, push, test a real submission.
- More studio photos welcome (gallery currently reuses the 2 work photos + the flyer).
- Interactive stack (booking/shop/payments): **deferred** — keep iterating on the brochure
  mockup for now; revisit when content is in place.
- Decide the stack for the interactive parts (class signup, shop, payments) — see "Decisions
  for later". A static GitHub Pages site can host the brochure; bookings/commerce need a hosted
  service or a no-code embed.
- Register a domain and wire up hosting (the MrGreenlee project this was scaffolded from used
  IONOS DNS → GitHub Pages; the same pattern works here).
- Build out per-section pages (`classes.html`, `patterns.html`, `shop.html`, `about.html`) once
  content exists; the landing page currently uses in-page `#anchors`.

See `SESSION_LOG.md` for full session history.

## Images in use

All provided by Sarah (2026-06-04) and live in `Images/`:

| File | Used for |
|---|---|
| `logo.png`                | Original logo (black "FLUX + THREAD / HANDMADE WITH LOVE" badge on a blurry bg) |
| `logo-badge.png`          | Auto-cropped square of the logo circle; used in header, about, footer (CSS clips to a circle so the leftover gray corners are hidden) |
| `gnome.png`               | Gnome suncatcher (portrait) — hero image + gallery |
| `inprocess-diamonds.png`  | Copper-foiled hexagons in process — workshop section + gallery |
| `flyer.jpg`               | The actual workshop flyer — linked from the workshop CTA + shown in gallery |

No portrait photo of Sarah was provided; the About section uses the logo badge as a brand mark
instead. Swap in a portrait if she wants one.

To regenerate `logo-badge.png` from `logo.png`, crop the black circle (detect by black-pixel
density per row/column; see session 2 in `SESSION_LOG.md`).

## File Structure

```
Sarah_Stained Glass/
├── index.html              ← the landing page (real content)
├── styles.css              ← stained-glass aesthetic
├── Images/                 ← photos & generated figures (add real ones here)
├── tools/                  ← Gemini image-generation helper (copied from MrGreenlee)
│   ├── gen_figure.py
│   ├── requirements.txt
│   └── README.md
├── .env.example            ← Gemini API key template (copy to .env, fill in)
├── README.md
├── SESSION_LOG.md          ← rolling work log; updated via /log-session
└── .claude/commands/
    └── log-session.md      ← project-scope /log-session command
```

## Origin

Scaffolded **2026-06-04** by reusing the pattern from the sibling project at
`C:\Users\smitjj09\Documents\MrGreenlee` (a static GitHub-Pages site). Copied verbatim:
the Gemini figure tool (`tools/gen_figure.py`, `requirements.txt`, `tools/README.md`),
`.env.example`, and the whitelist `.gitignore` / `/log-session` patterns. The HTML, CSS,
and all copy here are original to Flux & Thread. Instagram content could not be scraped
(login wall) — only the handle was retrievable; real captions/photos to come from Sarah.

## Decisions for later

1. **Interactive stack.** The brochure site is fine as static HTML on GitHub Pages. Bookings,
   a real shop, and payments are not — options to weigh:
   - **No-code embeds on the static site:** e.g. a scheduling tool for class signups, a
     storefront/checkout widget for the shop, and an email-list embed. Cheapest, fastest, keeps
     GitHub Pages.
   - **All-in-one platform** (site + booking + store + payments in one): less to wire together,
     monthly fee, less control over design.
   - **Custom app** (framework + database + payment API): most flexible, most work; only worth it
     if the no-code tools become limiting.
   Recommended start: static landing page + no-code embeds, migrate later only if needed.
2. **Domain & hosting.** Pick a domain (e.g. `fluxandthread.com`) and decide host. GitHub Pages
   + custom DNS mirrors the MrGreenlee setup and is free for the static parts.
3. **Brand assets.** A logo/wordmark, real color values pulled from Sarah's actual glass work,
   and a consistent photo style would tighten the design.

## Image generation workflow (optional helper)

`tools/gen_figure.py` calls Google's Gemini image API to generate figures/decorative art.
Needs a key in `.env` (`GEMINI_API_KEY`). Usage:

```powershell
python tools\gen_figure.py "<prompt>" --out Images\<name>.png
```

Add `--pro` for images with precise text. See `tools/README.md`. Useful for placeholder hero
art or pattern thumbnails before real photos exist — but real studio photos should win wherever
possible.

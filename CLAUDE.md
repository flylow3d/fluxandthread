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

**LIVE** at **https://fluxandthread.com** (custom domain, HTTPS enforced). Repo
`flylow3d/fluxandthread` (public), GitHub Pages from `main` / root; `CNAME` file holds the
domain. The old `flylow3d.github.io/fluxandthread` URL now redirects here. To update: edit
locally, `git add` + `git commit` + `git push`; Pages rebuilds in ~30–60s. Mobile-verified at
390px (headless Edge).

**Domain/DNS:** `fluxandthread.com` registered at **Porkbun** (Cloudflare-backed DNS). Records:
four apex `A` records → GitHub Pages IPs (185.199.108–111.153), `www` `CNAME` → flylow3d.github.io.
Porkbun's default email records (MX → fwd1/fwd2.porkbun.com, SPF TXT) were kept, so
`hello@fluxandthread.com`-style email forwarding can be set up later.

**Landing page rebuilt with real content** (2026-06-04). Single static page: sticky nav with
the real logo, hero (gnome suncatcher photo), "what we offer", **featured first workshop** (real
flyer copy — curriculum + perks + "dates being planned, weekday vs weekend?" interest CTA),
studio gallery, shop/patterns teaser, about, email signup band, footer. Palette is now Sarah's
real brand: lavender + charcoal on ivory. All four images she provided are wired in.

**Real workshop facts (from the flyer):** beginner copper-foil; curriculum = intro / cutting &
grinding / foiling & soldering / finishing; perks = no experience needed, all materials provided,
**4 spots**, take home a finished piece. **Dates are NOT set yet** — the flyer (and the site) is
gathering interest + asking weekday-afternoon vs weekend preference. Do not invent dates/prices.

**Workshops pages added** (2026-06-04). The nav "Workshop" link, the featured-workshop CTA, and
the offerings "Workshops" card now open a dedicated **`workshops.html`** listing page, which links
to a per-workshop detail page (date/time/location/deposit + special notes + a "Sign Up Now"
reservation form). **Workshops are organized by design, not technique** (Sarah's choice, 2026-06-07):
the design name is the title/hook (e.g. **Simple Suncatcher**, later Blooming Flowers, Sweet Like
Honeycomb) and the technique is a small `.smallcaps` sub-tag ("Beginner · Copper Foil"). The first
workshop is **`workshop-simple-suncatcher.html`** (formerly `workshop-copper-foil-beginner.html`).
Future workshops follow the `workshop-<design-slug>.html` scheme (copy the detail page, edit content
+ the hidden `workshop`/`subject` form fields, add a card to `workshops.html`). New pages duplicate the header/footer inline (no
partials — GitHub Pages has no build step) and are whitelisted in `.gitignore` via `!/workshops.html`
+ `!/workshop-*.html`. **Every workshop page includes the waitlist toggle by default** (Sarah's
choice, 2026-06-09): a `var SPOTS_LEFT = N` at the top of the page script is the single source of
truth — lower it as seats book; at `0` the page auto-flips to **waitlist mode** (badge → "This class
is full", buttons → "Join the Waitlist", form subject → "Waitlist — <design>", confirmation → "You're
on the waitlist!", reserve-only deposit/choose-glass actions hidden via `body.class-full` +
`.reserve-only`/`.waitlist-only` CSS). Copying the detail page carries this over automatically — just
update the `SPOTS_LEFT` count and the "Waitlist — <design>" subject string. **Booking model = "start simple, manual deposits"** (Sarah's choice): the
reservation form emails her via Web3Forms (same access key), then she sends a **Square** deposit
link and confirms personally. An optional "Pay Your Deposit" Square button is built into the
confirmation but **gated** — it stays hidden until the placeholder `square.link/REPLACE-…` href is
swapped for a real Square link. All workshop specifics are clearly-marked amber `[… TBD]`
placeholders (`.placeholder` class) until Sarah provides real values.

**About page added** (2026-06-05). **`about.html`** — two-column framed portrait (`Images/sarah.jpg`)
+ Sarah's real first-person bio (church-youth-group start → inherited her husband's grandmother's
supplies → community + new-mom closing). Nav "About" on every page now points here; the homepage
`#about` section is intentionally left unchanged. The homepage **glass bar** was recolored to
lavender→deep-purple→lavender (brand-only, was multi-color).

**"Choose Your Glass" page added** (2026-06-06; refactored data-driven 2026-06-07).
**`choose-glass.html`** lets a guest pick the exact glass **sheet for each piece** of their project
before class. Wired to the **real Simple Suncatcher pattern** (2026-06-07): the page shows the labeled
pattern diagram (`Images/simple-suncatcher-pattern.png`, a 5-piece pinwheel) and has one `<fieldset>`
per numbered piece — `data-part="1".."5"` → `name="glass_for_1".."glass_for_5"`, legends "Piece 1 ·
Top bar" … "Piece 5 · Center square". Each glass
sheet is a **native radio styled as a photo swatch** — single-select per piece, "Reserved for you"
state is pure CSS, no selection JS. Picks email Sarah via Web3Forms (one `glass_for_<part>: <name>`
line each); a ~12-line submit nudge blocks partial picks. A **"Surprise me"** button lets a guest opt
out (hides the grids, emails `glass_selection: ✨ SURPRISE ME …`, skips the nudge — Sarah hand-picks).
**Swatches are generated from a `GLASS = [...]` array in the page's inline `<script>`** (each entry
`{name, file, ooak?}`) — defined ONCE, rendered under all parts. **To add/edit a sheet: drop the
photo in `Images/glass/` and add/edit one line in `GLASS`** (`ooak: true` for one-of-a-kind → badge +
"(one of a kind)" in the email). Now showing **23 real sheets** (all placeholders replaced; 12
flagged one-of-a-kind). Sheets are **name-only** (no numbers; `.sw-no` is `display:none`) and
default to **restockable** unless flagged (see [[glass-restockable-default]]). Linked from the workshop booking box + reservation confirmation; not
in nav. Whitelisted via `!/choose-glass*.html`; future workshops copy → `choose-glass-<slug>.html`.

**Open items / next steps:**
- **Fill in the workshop placeholders** in `workshop-simple-suncatcher.html` (+ the listing card
  in `workshops.html`): real **price, deposit amount, session date(s), spots-left count, time,
  location, special notes / age minimum**, real **workshop photos** (gallery thumbs currently reuse
  inprocess-diamonds + gnome), and the **Square deposit link** (replace the `REPLACE-…` href
  to un-gate the Pay button). Search for `[` / `.placeholder` / `REPLACE` to find every spot. The
  detail page now has a **Lucent-inspired layout** (2026-06-05): photo gallery + thumbnails, a
  right-column **booking box** (price, a "Choose your date" `<select>` that is the single source of
  truth for sessions — add/remove `<option>`s; keep the form's hidden `#session-field` default equal
  to the first option — spots badge, Reserve button), and a structured What-you'll-learn / What's-
  included / What-to-bring / Good-to-know description.
- Get real workshop dates + price from Sarah once decided; replace the "dates being planned" note
  with a real schedule (the Reserve flow now exists).
- **Email signup: ACTIVATED.** Web3Forms access key (tied to `fluxandthread.com`) is pasted into
  the `access_key` field in `index.html`, committed + pushed — the form now emails real signups to
  Sarah's inbox. **Pending Sarah's confirmation** that a real browser submission lands (server-side
  tests are blocked by Cloudflare's bot challenge, which is expected). Note: Web3Forms usually
  sends a one-time **verification email** that must be clicked before submissions deliver.
- **Form error fallback** still references `hello@fluxandthread.com`, which isn't an active mailbox
  yet — repoint to a real address or set up the Porkbun forwarding.
- **Publishing workflow:** Claude handles all git (Sarah just says "publish"). git + stored GitHub
  creds are already set up on this laptop — nothing to install.
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
├── workshops.html          ← Workshops listing page (nav "Workshop" → here)
├── workshop-simple-suncatcher.html  ← per-workshop detail + reservation form (design-named; first workshop)
├── choose-glass.html       ← "Choose Your Glass": pick a sheet per pattern part (per workshop)
├── about.html              ← About page (nav "About" → here); Sarah's portrait + bio
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

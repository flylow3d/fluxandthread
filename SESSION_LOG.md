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

### Session 4 (2026-06-04)
- Built the real email signup form (was a mockup `alert()`). Uses **Web3Forms** (free, no
  backend, emails submissions). Captures name + email + a **timing-preference** field (Weekday
  afternoons / Weekends / Either works) as lavender pill radios — turning the flyer's
  weekday-vs-weekend question into structured data for Sarah.
- AJAX submit with inline success/error status; **graceful fallback** so it shows a friendly
  "goes live shortly" message (never an error) until the access key is pasted in. Mobile-tuned.
- Committed + pushed (live). **PENDING:** user to get a free Web3Forms access key from
  web3forms.com and paste it into the `access_key` hidden field in `index.html` to activate;
  then test a real submission end-to-end.

### Session 5 (2026-06-04)
- Registered **fluxandthread.com** at Porkbun (user's choice; dislikes IONOS). Walked the user
  through the Porkbun (Cloudflare-backed) DNS editor from a screenshot: deleted the two default
  parking records (ALIAS + wildcard CNAME → uixie.porkbun.com), kept the MX/SPF email records,
  added four apex `A` records → GitHub Pages IPs and a `www` `CNAME` → flylow3d.github.io.
- Verified DNS propagation from here, then attached the domain on GitHub: committed a `CNAME`
  file (`fluxandthread.com`) and whitelisted it in `.gitignore`. GitHub provisioned the
  Let's Encrypt cert (authorization_pending → approved) and we enabled `https_enforced=true`
  (note: gh api needs `-F` for the boolean, not `-f`).
- Verified end-to-end: https apex 200 + real content + images, www→apex 301 redirect, cert
  approved. **Site is live at https://fluxandthread.com.**
- Still pending from session 4: Web3Forms access key to activate the signup form.

### Session 6 (2026-06-04)
- **Confirmed the publish toolchain** for handing the laptop to Sarah: git 2.52 already
  installed, repo wired to `flylow3d/fluxandthread` over HTTPS, GitHub creds already stored in
  Windows Credential Manager, GCM bundled — verified a dry-run push authenticates. Nothing to
  install. Established workflow: **Sarah just says "publish" and Claude does git add/commit/push**
  (saved to project memory; she won't touch the terminal or a git GUI).
- **Activated the email signup form** (the session-4/5 pending item). Sarah created a free
  **Web3Forms** access key tied to `fluxandthread.com` and provided it; pasted it into the
  `access_key` hidden field in `index.html`, committed, and pushed — form now sends real
  submissions instead of the "goes live shortly" placeholder.
- Tried to smoke-test via a server-side POST but Web3Forms sits behind a **Cloudflare bot
  challenge** that blocks non-browser requests — expected, not a key problem. Directed Sarah to
  do the authentic end-to-end test from the live site (browser submit → "🎉 You're on the list!"
  → check inbox), and flagged that Web3Forms typically sends a **first-time verification email**
  that must be clicked before submissions deliver. **PENDING:** Sarah's confirmation that a real
  signup landed in her inbox.
- Noted (not yet changed) that the form's error-path fallback points at `hello@fluxandthread.com`,
  which isn't an active mailbox yet — offered to repoint it to her personal email or leave it for
  when the Porkbun forwarding is set up.
